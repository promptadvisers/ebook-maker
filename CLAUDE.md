# eBook Maker

Generate professional McKinsey-style eBooks with AI-generated covers.

## Quick Start

Just say:
> "Create an ebook about [your topic]"

Claude will invoke the `ebook-creator` skill and guide you through the process.

## What You Get

See `sample/` folder for example output:
- Professional full-bleed cover with AI-generated abstract imagery
- Clean typography and corporate color scheme
- Multi-section document with table of contents
- PDF ready for distribution

## Setup

### 1. API Key

Add your Gemini API key to `.env`:
```
GEMINI_API_KEY=your_key_here
```

### 2. Install Dependencies

```bash
# Python (for cover image generation)
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Node.js (for document generation)
cd ai_report_package && npm install
```

### 3. PDF Conversion (Optional)

Requires LibreOffice for .docx to .pdf conversion.

## Project Structure

```
eBook Maker/
├── .claude/skills/
│   └── ebook-creator.md    # Skill with full workflow
├── ai_report_package/
│   ├── create_report.js    # Document generator (edit for content)
│   └── logo.png            # Company logo
├── output/                 # Generated files go here
│   ├── cover_image.png
│   └── State_of_AI_2026.docx/.pdf
├── sample/                 # Example output for reference
├── generate_image.py       # Cover image generator (edit prompt)
├── requirements.txt
└── .env                    # API key (not committed)
```

## Customization

| What | Where |
|------|-------|
| Cover image style | `generate_image.py` → edit `prompt` variable |
| Brand colors | `ai_report_package/create_report.js` → top of file |
| Title & subtitle | `ai_report_package/create_report.js` → cover section |
| Report content | `ai_report_package/create_report.js` → content sections |

## Commands Reference

```bash
# Generate cover image
source venv/bin/activate && python generate_image.py

# Generate document
cd ai_report_package && node create_report.js

# Convert to PDF (macOS)
/Applications/LibreOffice.app/Contents/MacOS/soffice --headless --convert-to pdf output/State_of_AI_2026.docx
```

## Default Design

McKinsey-inspired consulting aesthetic:
- Full-bleed AI-generated abstract cover
- White text on dark semi-transparent backdrop
- Arial typography throughout
- Corporate blue/teal palette
- Bottom accent bar with tagline

## Notes

- Always run scripts directly — never ask user to run them
- Cover uses Gemini 3 Pro Image (`gemini-3-pro-image-preview`)
- Document uses docx library v8.x
- All measurements in DXA units (1440 DXA = 1 inch)
