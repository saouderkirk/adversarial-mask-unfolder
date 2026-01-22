# Mask Unfolder - Accordion Fold Pattern Generator

Convert any folded mask design into print-ready unfolded patterns for manufacturers.

## 🚀 Deploy to Railway

### Quick Deploy

1. **Push to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin your-repo-url
   git push -u origin main
   ```

2. **Connect to Railway**
   - Go to [railway.app](https://railway.app)
   - Click "New Project" → "Deploy from GitHub repo"
   - Select this repository
   - Railway auto-detects Node.js and deploys!

3. **Get your domain**
   - Railway gives you a free domain: `your-app.up.railway.app`
   - Or add a custom domain in settings

### Local Development

```bash
npm install
npm start
```

Visit `http://localhost:3000`

## 📦 What It Does

- Upload folded mask image (500×250px recommended)
- Generates unfolded pattern with accordion geometry
  - 7 rows total
  - Rows 1, 2, 4, 6, 7 visible when folded
  - Rows 3, 5 hidden (mirrored and tucked under)
- Downloads print-ready 300 DPI file (2066×2244px for 175mm×190mm)

## 🎯 For Manufacturers

The output file is ready to print on flat mask material. When accordion-folded with pleats between rows 2-3 and 4-5, the original design appears perfectly on the folded mask.

## 🛠️ Tech Stack

- Pure HTML/CSS/JavaScript (no build step!)
- Express.js server for Railway deployment
- Canvas API for image processing
- Responsive design

## 💡 Alternative Hosting

If you don't need a custom domain immediately, consider:
- **Netlify**: Drag & drop HTML file → instant deployment
- **Vercel**: Great for static sites
- **GitHub Pages**: Free with GitHub repo

Railway is excellent if you plan to add backend features later!
