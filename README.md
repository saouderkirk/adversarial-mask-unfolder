# Mask Unfolder - Accordion Fold Pattern Generator

Convert any folded mask design into print-ready unfolded patterns for manufacturers.

**Live App**: [https://maskfolder.app](https://maskfolder.app)

## 🚀 Quick Start

Simply open [https://maskfolder.app](https://maskfolder.app) in your browser and start uploading images. No installation required!

### Running Locally

Since this is a pure HTML/CSS/JavaScript app, you can:

1. **Open directly in browser**
   ```bash
   open index.html
   ```

2. **Or use a local server** (optional)
   ```bash
   # Python 3
   python -m http.server 8000

   # Node.js
   npx serve
   ```

   Then visit `http://localhost:8000`

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
- Canvas API for client-side image processing
- Responsive design with cyberpunk aesthetic
- Hosted on GitHub Pages

## 🌐 Deployment

This app is deployed on GitHub Pages and accessible at [https://maskfolder.app](https://maskfolder.app).

### Deploy Your Own Copy

1. **Fork this repository** on GitHub

2. **Enable GitHub Pages**
   - Go to Settings → Pages
   - Select `main` branch and `/` (root) folder
   - Click Save

3. **Your site will be live** at `https://yourusername.github.io/adversarial-mask-unfolder`

### Custom Domain (Optional)

To use your own domain:

1. Add a `CNAME` file with your domain name
2. Configure DNS A records to point to GitHub Pages:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
3. Enable HTTPS in GitHub Pages settings
