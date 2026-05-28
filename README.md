# SudokuAI

A fast, elegant web application that solves sudoku puzzles from photos using **Google Gemini Vision API** in seconds.

![Status](https://img.shields.io/badge/status-active-success)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

✨ **Drop & Solve** — Upload a sudoku image, get the solution in seconds  
🎨 **Beautiful UI** — Dark theme with gold accents, smooth animations  
👁️ **Vision AI** — Google Gemini extracts the grid automatically  
📱 **Responsive** — Works on desktop and mobile devices  
⚡ **Fast** — Optimized prompts for quick API responses  

## Live Demo

🔗 [Live on Netlify](https://sudokuai-demo.netlify.app) *(deploy in Step 4)*

## How It Works

1. **Upload** → Drop or browse a sudoku puzzle image (PNG, JPG, WebP)
2. **AI Reads** → Gemini Vision extracts all 81 cells from the grid
3. **Solve** → The puzzle is solved and displayed with filled cells highlighted
4. **Download** → *(Optional in future versions)*

## Tech Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Vision API:** Google Gemini 1.5 Flash (or 2.0 Flash)
- **Deployment:** Netlify (recommended)
- **No backend** — Everything runs client-side

## Quick Start

### Prerequisites

- A free Google API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
- Modern web browser (Chrome, Safari, Firefox, Edge)

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/sudokuai.git
cd sudokuai

# No dependencies! Just open in browser
open index.html
```

Or serve locally with:
```bash
# Using Python 3
python -m http.server 8000

# Using Node.js http-server
npx http-server
```

Then visit: `http://localhost:8000`

### Setup API Key

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey) and generate a **free API key**
2. Open `index.html`
3. Find this line (around line 772):
   ```javascript
   const GEMINI_API_KEY = 'YOUR_GEMINI_API_KEY_HERE';
   ```
4. Replace `YOUR_GEMINI_API_KEY_HERE` with your actual key
5. Save and reload the page

⚠️ **Security Note:** For production, use environment variables or backend authentication. See [Security](#security) section.

## API Configuration

The app uses **Google's Generative AI API**:

- **Endpoint:** `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent`
- **Model:** `gemini-1.5-flash` (fast, recommended) or `gemini-2.0-flash` (more accurate)
- **Request Type:** Vision + Text (multi-modal)
- **Timeout:** 30 seconds

### Customize Model

To use a different model, edit line 773:

```javascript
// For better accuracy (slightly slower):
const GEMINI_API_URL = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent';
```

## Project Structure

```
sudokuai/
├── index.html              # Main UI + JavaScript (all-in-one)
├── README.md              # This file
├── .gitignore             # Git ignore rules
├── .env.example           # Environment variables template
└── docs/
    ├── SETUP.md           # Detailed setup guide
    ├── DEPLOYMENT.md      # Netlify deployment steps
    └── TROUBLESHOOTING.md # Common issues & fixes
```

## Development Roadmap

**✅ Step 1** — Build UI shell  
**✅ Step 2** — Wire Gemini API  
**✅ Step 3** — Parse & display solution  
⏳ **Step 4** — Error handling & graceful failures  
⏳ **Step 5** — Deploy to Netlify  

## Troubleshooting

### API Error 404
- ❌ Wrong model name
- ✅ Use `gemini-1.5-flash` or `gemini-2.0-flash`

### API Error 503
- ❌ Google servers overloaded
- ✅ Retry after 30-60 seconds

### Slow responses (20+ seconds)
- ❌ Network delay or complex image
- ✅ Try a clearer photo, closer angle
- ✅ Switch to `gemini-1.5-flash` for speed

### Grid not rendering
- ❌ API returned invalid JSON
- ✅ Check browser Console (Cmd+Option+I) for parse errors
- ✅ Try a clearer, well-lit sudoku image

For more help, see [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)

## Security

⚠️ **Current Implementation:**
Your API key is embedded in `index.html`. This works for demos but is **not secure for production** because:
- Anyone can see your key in the browser
- Your key is exposed in git history
- Malicious users can abuse your quota

**For Production:**
1. Create a backend (Node.js, Python, etc.) that handles API calls
2. Store the API key in environment variables on the server
3. Frontend sends requests to your backend (not directly to Google)

Example backend pseudocode:
```javascript
// backend/routes/solve.js
app.post('/api/solve', async (req, res) => {
  const { imageBase64 } = req.body;
  const response = await fetch(GEMINI_API_URL, {
    body: { contents: [{ parts: [{ inlineData: { data: imageBase64 } }] }] },
    headers: { Authorization: `Bearer ${process.env.GEMINI_API_KEY}` }
  });
  res.json(response);
});
```

## Performance Tips

- 📸 **Image Quality:** Clear, well-lit, straight-on photos solve faster
- 🚀 **Model Choice:** Use `gemini-1.5-flash` for speed, `gemini-2.0-flash` for accuracy
- ⏱️ **Timeout:** Currently 30 seconds — adjust in code if needed

## Known Limitations

- 🔴 Handwritten sudoku may have lower accuracy (Gemini prefers printed grids)
- 🔴 Requires internet connection (API calls are online)
- 🔴 Google API has rate limits on free tier (~60 requests/minute)
- 🔴 Very blurry or rotated images may fail

## Contributing

Found a bug? Have a suggestion?

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/your-idea`)
3. Make changes and test
4. Commit with clear messages (`git commit -m "Fix: grid parsing for rotated images"`)
5. Push and create a Pull Request

## License

MIT License — see [LICENSE](LICENSE) file for details.

## Credits

- **Vision AI:** [Google Gemini](https://gemini.google.com)
- **Design:** Custom dark theme with gold accents
- **Fonts:** [Google Fonts](https://fonts.google.com) (DM Mono, Syne)

## Roadmap & Future

- 🔄 Batch processing (multiple puzzles)
- 💾 Save/export solutions as PDF
- 🎨 Theme customization (light mode)
- 📊 Solve time analytics
- 🌍 Multi-language support

---

**Made with ❤️ for sudoku lovers.**

Have questions? Open an [Issue](https://github.com/yourusername/sudokuai/issues) on GitHub.
