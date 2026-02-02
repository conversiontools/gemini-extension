# Conversion Tools - Gemini CLI Extension

[Conversion Tools](https://conversiontools.io) extension for Gemini CLI. Convert 140+ file formats directly in your terminal — no browser tabs, no copy-pasting.

## Installation

```bash
gemini extensions install https://github.com/conversiontools/gemini-extension
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
Convert report.pdf to Word document
```

## Available Tools

| Tool | Description |
|------|-------------|
| `convert_file` | Convert a file from one format to another |
| `list_converters` | List available converters by category |
| `find_converter` | Find the best converter for specific formats |
| `get_converter_info` | Get detailed info about a converter |
| `request_upload_url` | Get upload URL for large files (>5MB) |
| `auth_status` | Check authentication status |
| `auth_login` | Login via OAuth |
| `auth_logout` | Logout and clear credentials |

## Supported Conversions

**140+ conversion types** including:

- **Documents**: Word, PowerPoint, Excel ↔ PDF
- **Data**: JSON, CSV, XML, YAML, Excel conversions
- **Images**: PNG, JPG, WebP, AVIF, HEIC, SVG
- **PDF**: Extract to Word, Excel, CSV, Text, Images
- **Audio/Video**: MP3, WAV, MP4, MOV
- **E-books**: EPUB, MOBI, PDF
- **OCR**: Extract text from images and scanned PDFs
- **AI-powered**: Smart extraction from complex documents

## Authentication

On first use, you'll be prompted to authenticate via OAuth. This opens a browser window to log in to your Conversion Tools account.

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

### Convert image format

```
Convert screenshot.png to WebP format
```

### Batch conversion

```
Convert all JSON files in the data/ folder to CSV
```

## Links

- [Documentation](https://conversiontools.io/docs/mcp)
- [Pricing](https://conversiontools.io/pricing)
- [Support](https://conversiontools.io/contact)

## License

MIT
