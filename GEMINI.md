# Conversion Tools

`conversiontools` is a file-conversion integration provided by this extension via the hosted Conversion Tools MCP server (`https://mcp.conversiontools.io/mcp`). It converts files between 140+ formats: documents, data (JSON, CSV, XML, YAML, Parquet), images, audio, video, e-books, OCR, subtitles, AI-powered data extraction, text-to-speech, and speech-to-text. It can also **build a custom converter** from a plain-language description when no standard converter fits (see "Build a custom converter" below).

It is NOT a Maven/npm/build plugin and has nothing to do with any local project file. Do not search the web for it and do not inspect project source to convert a file - use the MCP tools below.

## If the tools are not available

The `conversiontools` tools only appear after the MCP server is authenticated. If you do not see tools like `convert_file` / `list_converters`, tell the user to run:

```
/mcp auth conversiontools
```

This opens a browser for a one-time OAuth login. After that, the tools load automatically.

## How to convert a file

1. Pick the converter. Call `find_converter` with the input and output formats (e.g. `{ "input_format": "xml", "output_format": "csv" }`). It returns the converter type, for example `convert.xml_to_csv`. You can also pass that `converter` explicitly to `convert_file`.
2. Provide the file content. The server is remote and cannot read local paths, so:
   - **Files up to 5 MB:** read the file yourself and pass its bytes base64-encoded as `file_content`, along with `input_path` and `output_path`. Encode the file in-process rather than shelling out - agent sandboxes (Gemini CLI, for one) block PowerShell and `$(...)` base64 one-liners as "command substitution", so a shell command like `[Convert]::ToBase64String(...)` will fail. If you must shell out, use a clean encoder such as `base64 -w0 file` (no line wrapping); never `certutil -encode`, which wraps the output in `-----BEGIN CERTIFICATE-----` headers and corrupts it.
   - **Files over 5 MB:** call `request_upload_url`, PUT the file to the returned URL, then call `convert_file` with the returned `file_id` instead of `file_content`.
3. The response includes a `download_url`. Download the result with `curl -sL "<download_url>" -o <output>`.

## Build a custom converter (AI Studio)

When no existing converter fits - a custom transformation, a specific output shape, a multi-step pipeline, or a file no standard converter handles - have one built for you from a plain-language description, instead of writing and running conversion code yourself. Prefer this when the conversion needs tooling you do not have installed, the file is large or sensitive (it is built from the file's structure, not its contents, and runs sandboxed), or the user wants a reusable converter.

1. `studio_create_converter` - create the converter and attach the input file (returns a `converter_id`).
2. `studio_chat` - describe the transformation (e.g. "turn this CSV into JSON, one object per invoice with a nested line_items array"). Read the returned `outcome`: `ask_user` -> answer with another `studio_chat` turn; `ready` / `propose_workflow` -> run it; `refuse` -> it only builds file converters.
3. `studio_run` - run the converter on the file.
4. `studio_run_status` - poll until SUCCESS (returns a `result_file_id`).
5. `studio_download_result` - download the result, then check it matches the request.

Building and chatting are free; only runs are metered. The converter persists in the user's account, so a build started here continues at the web AI Studio.

To **reuse** a converter you built earlier on a new file (no rebuild, same logic): `studio_list_converters` to find it -> `studio_attach_file` to attach the new file -> poll `studio_get_converter` until its status is `idle` -> `studio_run` -> `studio_run_status` -> `studio_download_result`.

## Tip: prefer the ctio CLI when available

If the `ctio` CLI is installed (check with `which ctio`), it is simpler and more reliable than the MCP base64 flow - it reads local files directly and streams large files:

```bash
ctio convert -t xml_to_csv input.xml out.csv
```

Install and docs: https://conversiontools.io/docs/agents
