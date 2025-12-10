# eBook Maker

> Generate professional McKinsey-style eBooks with AI-generated covers in minutes.

![Sample Cover](sample/cover_image.png)

Transform your content into polished, professional eBooks with stunning AI-generated covers. No design skills required.

## What You'll Create

- **Professional Cover Pages** — Full-bleed AI-generated abstract imagery
- **Clean Typography** — McKinsey-inspired corporate aesthetic
- **Complete Documents** — Table of contents, styled sections, headers/footers
- **Print-Ready PDFs** — Export to PDF with one command

[See sample output →](sample/State_of_AI_2026.pdf)

---

## Quick Start (5 Minutes)

### Prerequisites

- **Node.js** (v16+) — [Download](https://nodejs.org/)
- **Python 3.8+** — [Download](https://python.org/)
- **LibreOffice** (for PDF export) — [Download](https://libreoffice.org/)

### Step 1: Clone the Repository

```bash
git clone https://github.com/promptadvisers/ebook-maker.git
cd ebook-maker
```

### Step 2: Get Your API Key

You'll need a **Google Gemini API key** (free tier available):

1. Go to [Google AI Studio](https://aistudio.google.com/apikey)
2. Click **"Create API Key"**
3. Copy your key

### Step 3: Configure

Create a `.env` file in the root directory:

```bash
echo "GEMINI_API_KEY=your_api_key_here" > .env
```

### Step 4: Install Dependencies

```bash
# Python dependencies (for cover image generation)
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Node.js dependencies (for document generation)
cd ai_report_package && npm install && cd ..
```

### Step 5: Generate Your First eBook

```bash
# Create output directory
mkdir -p output

# Generate cover image
source venv/bin/activate && python generate_image.py

# Generate document
cd ai_report_package && node create_report.js && cd ..

# Convert to PDF (macOS)
/Applications/LibreOffice.app/Contents/MacOS/soffice --headless --convert-to pdf output/State_of_AI_2026.docx

# Convert to PDF (Linux)
libreoffice --headless --convert-to pdf output/State_of_AI_2026.docx
```

Your eBook is ready in `output/`!

---

## Customization Guide

### Change the Cover Image

Edit `generate_image.py` and modify the `prompt` variable:

```python
prompt = "Abstract visualization of YOUR_TOPIC, swirling blue and teal patterns, professional corporate style, soft gradients, ethereal atmosphere"
```

**Tips for great prompts:**
- Be specific about colors (match your brand)
- Use "abstract" or "visualization" for professional looks
- Add "corporate", "professional", "clean" for business aesthetic
- Avoid: photos, clipart, busy patterns

### Change Title & Branding

Edit `ai_report_package/create_report.js`:

**1. Find the cover section** (search for `McKINSEY-STYLE COVER PAGE`)

**2. Update these values:**
```javascript
// Company name
new TextRun({ text: "Your Company", ... })

// Main title
new TextRun({ text: "YOUR TITLE", ... })

// Subtitle
new TextRun({ text: "Your subtitle here", ... })
```

### Change Colors

At the top of `create_report.js`, modify:

```javascript
const BLUE = "1E5FAA";        // Primary blue
const DARK_BLUE = "0A2744";   // Headers, footer bar
const ACCENT_BLUE = "2B7DE9"; // Accent color (highlighted words)
```

Use any hex color (without the `#`).

---

## Project Structure

```
ebook-maker/
├── .claude/
│   └── skills/
│       └── ebook-creator.md    # Claude Code skill (optional)
├── ai_report_package/
│   ├── create_report.js        # Main document generator
│   ├── logo.png                # Your company logo
│   └── package.json
├── output/                     # Generated files (gitignored)
├── sample/                     # Example output
│   ├── cover_image.png
│   └── State_of_AI_2026.pdf
├── generate_image.py           # AI cover generator
├── requirements.txt            # Python dependencies
├── CLAUDE.md                   # Claude Code instructions
└── README.md                   # You are here
```

---

## Using with Claude Code

This repo includes a skill for [Claude Code](https://claude.ai/code). Just say:

> "Create an ebook about [your topic]"

Claude will:
1. Ask for your title, subtitle, and company name
2. Generate a custom cover image
3. Build the document
4. Export to PDF

---

## API Keys Explained

### Google Gemini API (Required)

**What it's for:** Generating the AI cover images

**Cost:** Free tier includes 60 requests/minute

**Get it:**
1. Visit [Google AI Studio](https://aistudio.google.com/apikey)
2. Sign in with Google
3. Click "Create API Key"
4. Add to `.env` file

---

## Troubleshooting

### "Module not found" errors

```bash
# Make sure you're in the virtual environment
source venv/bin/activate
pip install -r requirements.txt
```

### Cover image not generating

1. Check your API key in `.env`
2. Ensure you have internet connection
3. Try a simpler prompt first

### PDF conversion fails

**macOS:** Make sure LibreOffice is installed in `/Applications/`

**Linux:** Install with `sudo apt install libreoffice`

**Windows:** Use LibreOffice GUI or install via [chocolatey](https://chocolatey.org/): `choco install libreoffice`

### Document looks wrong

- Check that `output/cover_image.png` exists before running `create_report.js`
- Ensure Node.js dependencies are installed: `cd ai_report_package && npm install`

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Cover Generation | Google Gemini 3 Pro Image |
| Document Creation | Node.js + [docx](https://www.npmjs.com/package/docx) library |
| PDF Export | LibreOffice (headless) |
| AI Assistant | Claude Code (optional) |

---

## Examples

### Business Report
```python
prompt = "Abstract visualization of business growth and data analytics, ascending geometric shapes in navy blue and gold, professional corporate style"
```

### Tech Whitepaper
```python
prompt = "Abstract neural network and cloud computing visualization, glowing blue nodes connected by light streams, futuristic tech aesthetic"
```

### Healthcare Guide
```python
prompt = "Abstract visualization of medical innovation, soft teal and white flowing patterns, clean and calming healthcare aesthetic"
```

---

## Contributing

PRs welcome! Ideas for improvement:
- [ ] More document templates
- [ ] Web interface
- [ ] Multiple cover style presets
- [ ] Batch generation

---

## License

MIT — use it however you want.

---

<p align="center">
  <b>Built with Claude Code</b><br>
  <a href="https://claude.ai/code">claude.ai/code</a>
</p>
