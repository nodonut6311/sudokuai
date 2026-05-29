# Setup Guide

Complete step-by-step guide to get SudokuAI running locally.

## Prerequisites  

- Mac, Windows, or Linux
- Web browser (Chrome, Safari, Firefox recommended)
- Text editor (VS Code, Sublime, etc.)
- Git installed (for version control)

---

## 1. Get Your Google API Key (Free)

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Click **Create API Key**
3. Choose **Create API key in new project**
4. Copy the key (looks like: `AIzaSy...`)
5. Keep this safe!

---

## 2. Clone or Download the Project

### Option A: Clone from GitHub (Recommended)

```bash
git clone https://github.com/yourusername/sudokuai.git
cd sudokuai
```

### Option B: Download ZIP

1. Go to GitHub → Click **Code** → **Download ZIP**
2. Unzip the folder
3. Open terminal in that folder

---

## 3. Add Your API Key

1. Open `index.html` in your text editor
2. Find this line (around line 772):
   ```javascript
   const GEMINI_API_KEY = 'YOUR_GEMINI_API_KEY_HERE';
   ```
3. Replace `YOUR_GEMINI_API_KEY_HERE` with your actual API key
4. Save the file

Example:
```javascript
const GEMINI_API_KEY = 'AIzaSyDxsK_example_key_12345';
```

---

## 4. Run Locally

### Option A: Python (Built-in on Mac/Linux)

```bash
# If you have Python 3
python -m http.server 8000

# If you have Python 2 (older systems)
python -m SimpleHTTPServer 8000
```

### Option B: Node.js (if installed)

```bash
npx http-server
```

### Option C: Open directly

Double-click `index.html` in Finder (Mac) or Explorer (Windows)

⚠️ **Note:** This may not work with some browsers due to CORS. Use a local server instead.

---

## 5. Visit Your Site

Open your browser and go to:

```
http://localhost:8000
```

You should see the SudokuAI interface with:
- Upload area
- "How it works" section
- Logo with gold accents

---

## 6. Test It

1. **Upload a sudoku image:**
   - Print a sudoku puzzle or find one online
   - Take a clear photo or use a digital image
   - Upload using the UI

2. **Click "Solve Puzzle"**
   - Should show "Analyzing puzzle..." spinner
   - After 10-30 seconds, solution appears on right

3. **Verify:**
   - Grid shows 81 cells
   - Filled cells (from AI) are highlighted in gold
   - Original numbers are shown without highlight

✅ If you see this, everything is working!

---

## 7. Development Tips

### Using VS Code

1. Open folder in VS Code
2. Use Live Server extension for easier testing:
   - Install extension
   - Right-click `index.html` → **Open with Live Server**
   - Automatically refreshes on save

### Editing Code

All code is in `index.html`. Key sections:

- **Lines 1-400:** CSS styling
- **Lines 754-770:** HTML structure
- **Lines 771-950:** JavaScript (logic & API calls)

Make changes and refresh browser (Cmd+R or Ctrl+R).

### Debugging

Use DevTools to debug:

```
Cmd + Option + I (Mac)
F12 (Windows)
```

Check:
- **Console tab:** Error messages
- **Network tab:** API requests/responses
- **Sources tab:** Step through code

---

## 8. Project Structure

```
sudokuai/
├── index.html                 # Main file (HTML + CSS + JS)
├── README.md                  # Project overview
├── LICENSE                    # MIT License
├── .gitignore                 # Files to ignore in git
├── .env.example               # Environment variable template
└── docs/
    ├── SETUP.md              # This file
    ├── DEPLOYMENT.md         # How to deploy to Netlify
    └── TROUBLESHOOTING.md    # Common issues & fixes
```

---

## 9. Git Setup (Version Control)

### First time:

```bash
# Initialize git repo
git init

# Configure git with your info
git config user.name "Your Name"
git config user.email "your.email@gmail.com"

# Add all files
git add .

# Create first commit
git commit -m "Initial commit: SudokuAI v1.0"
```

### Connect to GitHub:

1. Go to [GitHub.com](https://github.com) → **New repository**
2. Name it: `sudokuai`
3. Copy the commands shown (looks like):
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/sudokuai.git
   git branch -M main
   git push -u origin main
   ```
4. Run those in your terminal

### Regular updates:

```bash
# Make changes to code
# Then:

git add .
git commit -m "Fix: faster API responses"
git push
```

---

## 10. Next Steps

Once running locally:

1. **Test with different images** — try various sudoku puzzles
2. **Optimize for speed** — see TROUBLESHOOTING.md
3. **Deploy to Netlify** — see DEPLOYMENT.md
4. **Share with friends** — give them your live URL

---

## Common Setup Issues

### "Module not found" errors
- You don't need any modules! It's vanilla JavaScript.
- Just open in browser.

### "CORS error"
- Don't open `index.html` directly (file://)
- Use a local server: `python -m http.server 8000`

### API key still showing "YOUR_GEMINI_API_KEY_HERE"
- You didn't save the file
- Or you edited the wrong line
- Check line 772 in `index.html`

### Nothing happens when I click "Solve"
- Check browser Console for errors
- Make sure API key is valid
- Make sure image is clear

---

## API Key Security Notes

⚠️ **For Development:** Hardcoding is fine  
⚠️ **For Production:** Use environment variables or backend

If you push to GitHub with an API key:

1. **Revoke the key immediately:**
   - Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
   - Delete the exposed key
   - Generate a new one

2. **Remove from git history:**
   ```bash
   git rm --cached index.html
   git commit -m "Remove API key"
   git push
   ```

3. **Use .env file for future:**
   - Copy `.env.example` to `.env`
   - Add your key to `.env`
   - Add `.env` to `.gitignore`

---

## Updating Code

To pull latest changes from GitHub:

```bash
git pull origin main
```

To push your changes:

```bash
git add .
git commit -m "Your message"
git push origin main
```

---

## Getting Help

1. Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
2. Check browser Console for errors
3. Check Network tab for API responses
4. Open an issue on GitHub with details

---

**Everything ready? Time to deploy!** 🚀

See [DEPLOYMENT.md](DEPLOYMENT.md) to go live on Netlify.
