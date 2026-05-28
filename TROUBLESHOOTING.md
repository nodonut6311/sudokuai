# Troubleshooting Guide

Common issues and how to fix them.

---

## API Errors

### Error 404 — Not Found
**Problem:** API endpoint doesn't exist

**Causes:**
- ❌ Wrong model name
- ❌ Typo in API URL

**Fix:**
```javascript
// Line 773 - Make sure model name is correct:
// ✅ Correct:
const GEMINI_API_URL = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent';

// ❌ Wrong:
// const GEMINI_API_URL = 'https://generativelanguage.googleapis.com/v1/models/gemini-1.5-flash:generateContent';
```

---

### Error 401 — Unauthorized
**Problem:** API key is invalid or expired

**Causes:**
- ❌ Wrong API key
- ❌ API key doesn't have Generative Language API enabled

**Fix:**
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Regenerate a new API key
3. Replace in code: `const GEMINI_API_KEY = 'YOUR_NEW_KEY';`
4. Reload page

---

### Error 403 — Forbidden
**Problem:** API key exists but doesn't have permission

**Causes:**
- ❌ Generative Language API not enabled in Google Cloud Console
- ❌ Billing not set up

**Fix:**
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Search for "Generative Language API"
3. Click **Enable**
4. Set up billing (free tier available)

---

### Error 500 — Internal Server Error
**Problem:** Google's servers crashed

**Causes:**
- ❌ Temporary Google outage
- ❌ Bug in Gemini API

**Fix:**
- Wait 5-10 minutes and retry
- Check [Google Cloud Status](https://status.cloud.google.com)

---

### Error 503 — Service Unavailable
**Problem:** Google's API is overloaded

**Causes:**
- ❌ Too many requests globally
- ❌ Maintenance window

**Fix:**
- Wait 30-60 seconds
- Retry the request
- Code already has retry logic, just be patient

---

## Performance Issues

### "Analyzing puzzle..." takes 20-30+ seconds

**Causes:**
- 🌐 Slow internet connection
- 📊 Complex image with unclear numbers
- 🤖 Gemini model is slower today

**Fixes:**

1. **Try a clearer image:**
   - Use good lighting
   - Straight-on angle (not tilted)
   - Avoid shadows
   - Print quality (not handwritten)

2. **Use faster model:**
   ```javascript
   // Line 773 - Confirm you're using flash:
   const GEMINI_API_URL = '...models/gemini-1.5-flash:generateContent';
   // ✅ Flash is fastest
   // ❌ Avoid gemini-pro (too slow)
   ```

3. **Simplify the prompt:**
   ```javascript
   // Line 915 - Shorter prompt = faster response
   text: `Extract sudoku grid: {"given": [81 nums], "solution": [81 nums]}`
   ```

4. **Increase timeout:**
   ```javascript
   // Around line 901 - Change from 30000 to 60000
   const timeoutId = setTimeout(() => controller.abort(), 60000); // 60 seconds
   ```

---

## Grid Display Issues

### Grid doesn't render (blank on right side)

**Causes:**
- ❌ API response parsing failed
- ❌ Invalid JSON from Gemini
- ❌ Browser console errors

**Debug:**
1. Open **DevTools**: Cmd+Option+I
2. Click **Console** tab
3. Look for red error messages
4. Common error: `Cannot read property 'given' of null`

**Fix:**
- API likely returned malformed JSON
- Try a different, clearer sudoku image
- Check console logs for exact error

---

### Grid shows all zeros (all empty)

**Causes:**
- ❌ Gemini couldn't read the image
- ❌ Image too blurry or dark

**Fix:**
1. Take a clearer photo:
   - Good lighting (natural light best)
   - Straight angle, not tilted
   - Printed grid (not handwritten)
   - Close-up of the puzzle
2. Retry solving

---

### Numbers in grid are wrong

**Causes:**
- ❌ Image quality/contrast
- ❌ Gemini misread some digits (5→S, 8→0, etc.)

**Fix:**
1. Try `gemini-2.0-flash` for better accuracy:
   ```javascript
   const GEMINI_API_URL = '...models/gemini-2.0-flash:generateContent';
   ```
   (Slower but more accurate)

2. Take a clearer photo
3. Increase contrast in image editor before uploading

---

## File & Upload Issues

### File won't upload

**Causes:**
- ❌ Wrong file format
- ❌ File too large
- ❌ Browser doesn't support FileReader

**Fix:**
1. Use supported formats: **PNG, JPG, WebP**
2. File should be under 20MB (most are <5MB)
3. Use modern browser: Chrome, Safari, Firefox, Edge

---

### Preview shows but can't solve

**Causes:**
- ❌ currentBase64 is null
- ❌ FileReader didn't finish loading

**Fix:**
- Wait for image preview to fully load
- Try uploading a different image
- Refresh page and try again

---

## Browser Issues

### DevTools won't open
**Problem:** Can't debug

**Fix:**
- Mac: **Cmd + Option + I**
- Windows: **F12** or **Ctrl + Shift + I**
- Right-click page → **Inspect**

---

### "Blocked by CORS"
**Problem:** Browser blocked API request

**Causes:**
- ❌ Using `file://` protocol (wrong)
- ❌ Running locally without http server

**Fix:**
```bash
# Don't use file:// - run a server:
python -m http.server 8000
# Then visit: http://localhost:8000
```

---

### API key visible in Network tab
**Problem:** Security risk

**Fix:**
- This is normal for client-side apps
- Restrict key in [Google Cloud Console](https://console.cloud.google.com):
  1. APIs & Services → Credentials
  2. Click your API key
  3. Add **HTTP referrer** restriction
  4. Only allow your domain
- Better: Move API key to backend (see README)

---

## Image Quality

### How to take the best sudoku photo

✅ **Good:**
- Printed sudoku (clearest)
- Close-up, entire grid in frame
- Straight angle (not tilted)
- Good lighting, no shadows
- High contrast (dark grid, light background)

❌ **Bad:**
- Handwritten sudoku (harder to read)
- Distant photo (grid too small)
- Tilted/rotated
- Dim lighting or shadows
- Low contrast or faded paper

---

## Still Stuck?

1. **Check Console Logs:**
   ```
   Cmd + Option + I → Console tab → Look for errors
   ```

2. **Check Network Request:**
   ```
   Cmd + Option + I → Network tab → Look for API call response
   ```

3. **Open an Issue:**
   - Go to [GitHub Issues](https://github.com/yourusername/sudokuai/issues)
   - Include:
     - Error message (from Console)
     - Steps to reproduce
     - Screenshot of issue
     - Browser/OS info

---

## Common Solutions Checklist

- [ ] API key is correct and valid
- [ ] Using HTTPS or localhost (not file://)
- [ ] Image is clear and well-lit
- [ ] Grid is straight (not rotated)
- [ ] Browser is up to date
- [ ] Console shows no red errors
- [ ] Network tab shows successful API response
- [ ] Cache cleared (Cmd+Shift+Delete)

---

**Most issues are solved by:** Better image quality + clearing cache + refreshing page.
