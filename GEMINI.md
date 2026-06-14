# Conversion Tools

`conversiontools` is a file-conversion integration provided by this extension via the hosted Conversion Tools MCP server (`https://mcp.conversiontools.io/mcp`). It converts files between 140+ formats: documents, data (JSON, CSV, XML, YAML, Parquet), images, audio, video, e-books, OCR, subtitles, AI-powered data extraction, text-to-speech, and speech-to-text.

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
   - **Files up to 5 MB:** base64-encode the file and pass it as `file_content`, along with `input_path` and `output_path`. Use a clean base64 (no PEM headers, no line wrapping). On Linux/macOS: `base64 -w0 file`. On Windows PowerShell: `[Convert]::ToBase64String([IO.File]::ReadAllBytes('file'))`. Do NOT use `certutil -encode` (it adds `-----BEGIN CERTIFICATE-----` headers that corrupt the content).
   - **Files over 5 MB:** call `request_upload_url`, PUT the file to the returned URL, then call `convert_file` with the returned `file_id` instead of `file_content`.
3. The response includes a `download_url`. Download the result with `curl -sL "<download_url>" -o <output>`.

## Tip: prefer the ctio CLI when available

If the `ctio` CLI is installed (check with `which ctio`), it is simpler and more reliable than the MCP base64 flow - it reads local files directly and streams large files:

```bash
ctio convert -t xml_to_csv input.xml out.csv
```

Install and docs: https://conversiontools.io/docs/agents
