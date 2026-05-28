# Deployment Guide: SudokuAI on Netlify

Deploy your sudoku solver to a live URL in **under 5 minutes**.

## Prerequisites

- [GitHub](https://github.com) account (free)
- [Netlify](https://netlify.com) account (free)
- Your SudokuAI code pushed to GitHub

## Step 1: Push to GitHub

### First time setup:

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# First commit
git commit -m "Initial commit: SudokuAI v1.0"

# Create a new repository on GitHub (https://github.com/new)
# Name it: sudokuai

# Add remote
git remote add origin https://github.com/YOUR_USERNAME/sudokuai.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Subsequent pushes:

```bash
git add .
git commit -m "Your message here"
git push
```

---

## Step 2: Deploy to Netlify

### Option A: Connect GitHub (Recommended)

1. Go to [netlify.com](https://netlify.com)
2. Click **Sign up** → Choose **GitHub**
3. Authorize Netlify to access your GitHub
4. Click **New site from Git**
5. Select your **sudokuai** repository
6. Leave all build settings default (no build command needed for static HTML)
7. Click **Deploy site**

**Done!** 🎉 Your site is live. Netlify gives you a URL like:
```
https://sudokuai-xyz123.netlify.app
```

### Option B: Manual (Drag & Drop)

1. Go to [netlify.com/drop](https://netlify.com/drop)
2. Drag your `index.html` file into the box
3. Instant live URL in seconds

---

## Step 3: Add Environment Variables (Production Security)

⚠️ **Important:** Your API key is currently hardcoded in `index.html`. For production:

### On Netlify:

1. Go to your site dashboard
2. **Site settings** → **Build & Deploy** → **Environment**
3. Click **Edit variables**
4. Add:
   ```
   VITE_GEMINI_API_KEY = your_api_key_here
   ```
5. Save

### Update your HTML (Optional, for advanced setup with build tools)

If using a build tool like Vite:
```javascript
const GEMINI_API_KEY = import.meta.env.VITE_GEMINI_API_KEY;
```

---

## Step 4: Custom Domain (Optional)

1. In Netlify dashboard → **Site settings** → **Domain management**
2. Click **Add custom domain**
3. Enter your domain (e.g., `sudokuai.com`)
4. Follow DNS instructions

Cost varies ($0-15/year depending on registrar).

---

## Step 5: Enable HTTPS (Automatic)

Netlify automatically provides **free SSL/TLS certificate**. Your site is secure by default.

---

## Continuous Deployment

Every time you push to GitHub:
```bash
git push
```

Netlify automatically rebuilds and deploys your changes. ✅

---

## Troubleshooting Deployment

### Site shows blank page
- Check **Deploys** tab in Netlify
- Make sure `index.html` exists in root
- Clear browser cache (Cmd+Shift+Delete)

### API returns 403/401
- Your API key is invalid
- Regenerate at [Google AI Studio](https://makersuite.google.com/app/apikey)
- Update in Netlify environment variables

### CORS errors (if using backend)
- Add `Access-Control-Allow-Origin: *` headers
- Netlify can set this in `netlify.toml`:
  ```toml
  [[headers]]
    for = "/*"
    [headers.values]
      Access-Control-Allow-Origin = "*"
  ```

---

## Monitoring

### Check build logs:
1. Netlify dashboard → **Deploys**
2. Click latest deploy
3. View **Deploy log**

### Monitor API usage:
1. [Google Cloud Console](https://console.cloud.google.com)
2. Search "Generative Language API"
3. View quota & usage

---

## Performance Tips for Production

- ⚡ Enable Netlify's image optimization (automatic)
- 🔍 Add meta tags for SEO (`description`, `og:image`)
- 📊 Set up Netlify Analytics (optional, paid)
- 🛡️ Restrict API key to HTTP referrer (Google Cloud Console)

---

## Rollback (Undo deployment)

If something breaks:

1. Netlify dashboard → **Deploys**
2. Click a previous deployment
3. Click **Restore**

Takes 30 seconds. ✅

---

## Next Steps

- ✅ Domain name: [namecheap.com](https://namecheap.com), [godaddy.com](https://godaddy.com)
- ✅ Analytics: [Netlify Analytics](https://www.netlify.com/products/analytics/) or [Google Analytics](https://analytics.google.com)
- ✅ Email: Add contact form with [Netlify Forms](https://docs.netlify.com/forms/overview/)

---

**Your sudoku solver is now live for the world! 🌍**

Share the link with friends: `https://your-site-name.netlify.app`
