# eBook Creator Skill

Create professional McKinsey-style eBooks with AI-generated cover images.

## When to Use

Invoke this skill when the user asks to:
- Create an ebook, report, or whitepaper
- Generate a professional document with a cover page
- Make a PDF report or downloadable content

## Design Philosophy

Default style is **McKinsey Consulting** aesthetic:
- Full-bleed abstract cover image (AI-generated)
- Clean white text on dark backdrop overlay
- Company branding at top-left
- Bold sans-serif titles (Arial)
- Accent color for key words (cyan/teal)
- Dark accent bar at bottom

## Workflow

### Step 1: Gather Requirements

Before generating, ask the user:

1. **Title**: What is the ebook called?
2. **Subtitle**: One-liner describing the content
3. **Company/Author**: Who is publishing this?
4. **Cover Style** (optional): Default is abstract AI visualization

If user doesn't specify design preferences, use our default McKinsey style. Push back on:
- Clipart or stock photos → suggest abstract AI imagery
- Multiple fonts → stick to Arial
- Bright/neon colors → suggest corporate blues, teals
- Comic Sans → professional sans-serif only

### Step 2: Generate Cover Image

Edit `generate_image.py` prompt for their topic:

```python
prompt = "Abstract visualization of [TOPIC], swirling [BRAND_COLORS] patterns emanating from a luminous center, professional corporate style, soft gradients, ethereal atmosphere, suitable as ebook cover"
```

Run:
```bash
source venv/bin/activate && python generate_image.py
```

Output: `output/cover_image.png`

### Step 3: Update Document

Edit `ai_report_package/create_report.js`:

**Colors** (top of file):
```javascript
const BLUE = '1E5FAA';
const DARK_BLUE = '0A2744';
const ACCENT_BLUE = '2B7DE9';
```

**Cover text** (search for "McKINSEY-STYLE COVER PAGE"):
- Update "Prompt Advisers" → their company
- Update "THE STATE OF AI 2026" → their title
- Update subtitle text

### Step 4: Generate Output

```bash
cd ai_report_package && node create_report.js
```

Output: `output/State_of_AI_2026.docx`

### Step 5: Convert to PDF

macOS:
```bash
/Applications/LibreOffice.app/Contents/MacOS/soffice --headless --convert-to pdf output/State_of_AI_2026.docx
```

Linux:
```bash
libreoffice --headless --convert-to pdf output/State_of_AI_2026.docx
```

## File Structure

```
eBook Maker/
├── .claude/skills/
│   └── ebook-creator.md    # This file
├── ai_report_package/
│   ├── create_report.js    # Document generator
│   └── logo.png            # Company logo
├── output/                 # All generated files
│   ├── cover_image.png
│   └── *.docx, *.pdf
├── sample/                 # Example output
├── generate_image.py       # Cover generator
├── requirements.txt
└── .env                    # GEMINI_API_KEY
```

## Sample

See `sample/` folder for example output demonstrating the default style.
