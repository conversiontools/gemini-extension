# Conversion Tools - Gemini CLI Extension

[Conversion Tools](https://conversiontools.io) extension for Gemini CLI. Convert 140+ file formats directly in your terminal - no browser tabs, no copy-pasting. Or build a custom converter from a plain-language description when no standard one fits.

Part of the [Conversion Tools agent integrations](https://conversiontools.io/docs/agents) (Claude Code, Cursor, Codex, Grok, Gemini, plus the `ctio` CLI).

## Install

```bash
gemini extensions install https://github.com/conversiontools/gemini-extension
```

## Update

Pull the latest version (recommended periodically - new converters and fixes ship regularly):

```bash
gemini extensions update conversiontools
```

Or update every installed extension:

```bash
gemini extensions update --all
```

## Usage

Once installed, just ask Gemini to convert files:

```
Convert data.json to Excel
```

```
Transform this XML file to CSV
```

```
Convert report.pdf to a Word document
```

## Available Tools

| Tool | Description |
|------|-------------|
| `convert_file` | Convert a file from one format to another |
| `list_converters` | List available converters by category |
| `find_converter` | Find the best converter for specific formats |
| `get_converter_info` | Get detailed info about a converter |
| `request_upload_url` | Get upload URL for large files (over 5MB) |
| `auth_status` | Check authentication status |
| `auth_login` | Login via OAuth |
| `auth_logout` | Logout and clear credentials |
| `studio_create_converter` | Build a custom converter: create it + attach the input file |
| `studio_chat` | Describe the transformation in plain language; the converter is built |
| `studio_run` | Run the built converter on the file |
| `studio_run_status` | Poll the run until it finishes |
| `studio_download_result` | Download the result |
| `studio_list_converters` | List your previously built converters (to reuse one instead of rebuilding) |
| `studio_get_converter` | Inspect a converter's details and check it's ready to run |
| `studio_attach_file` | Attach a new file to an existing converter and re-run its built logic |

## Supported Conversions

**140+ conversion types** including:

- **Documents**: Word, PowerPoint, Excel, Markdown, ODS to/from PDF, HTML, Text, LaTeX
- **Data**: JSON, CSV, XML, YAML, Parquet, JSONL, BSON, Excel - with validators and formatters
- **Images**: PNG, JPG, WebP, AVIF, HEIC, JXL (JPEG XL), SVG, BMP, TIFF, GIF
- **PDF**: Extract to Word, Excel, CSV, Text, HTML, Images (JPG, PNG, SVG, TIFF), EPUB
- **Audio**: MP3, WAV, FLAC - plus AI text-to-speech and speech-to-text
- **Video**: MP4, MOV, MKV, AVI - plus audio extraction
- **E-books**: EPUB, MOBI, AZW, AZW3, FB2, FBZ, PDF
- **OCR**: Extract text from images and scanned PDFs - output as Text or searchable PDF
- **AI-powered**: Smart extraction from complex documents, subtitle translation, TTS, STT
- **Subtitles**: SRT, VTT, ASS - bidirectional conversions
- **Web**: Website screenshots (URL to PDF, JPG, PNG)
- **Custom (AI Studio)**: describe a transformation in plain language and have a reusable converter built, run, and returned - for when no standard converter fits

## Authentication

On first use, you will be prompted to authenticate via OAuth. This opens a browser window to log in to your Conversion Tools account.

Free accounts get 100 conversions per month (10 per day). Paid plans available at [conversiontools.io/pricing](https://conversiontools.io/pricing).

## Examples

### Convert JSON to Excel

```
I have a data.json file with an array of objects. Convert it to Excel.
```

### Extract data from PDF

```
Extract the table from invoice.pdf to CSV
```

## Links

- [All agent integrations](https://conversiontools.io/docs/agents)
- [Pricing](https://conversiontools.io/pricing)
- [Support](https://conversiontools.io/contact)

## License

MIT
