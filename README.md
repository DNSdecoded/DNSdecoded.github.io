# Portfolio Website - Deployment Guide

## 🚀 Production Deployment

This portfolio is production-ready and can be deployed to any static hosting platform.

---

## Quick Deploy Options

### 1. **GitHub Pages** (Recommended - Free)
```bash
# 1. Create a GitHub repository
# 2. Push your code
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/portfolio.git
git push -u origin main

# 3. Enable GitHub Pages
# Go to: Settings → Pages → Source: main branch → Save
# Your site will be live at: https://yourusername.github.io/portfolio/
```

### 2. **Netlify** (Free)
1. Drag and drop the `portfolio` folder to [netlify.com/drop](https://app.netlify.com/drop)
2. Or connect your GitHub repo for automatic deployments
3. Custom domain support included

### 3. **Vercel** (Free)
```bash
npm i -g vercel
cd portfolio
vercel
```

### 4. **Cloudflare Pages** (Free)
1. Connect your GitHub repository
2. Build settings: None (static site)
3. Deploy

---

## 📝 Before Deploying

### 1. Update Meta Tags
Edit `index.html` and replace placeholder URLs:

```html
<!-- Line ~17: Update your domain -->
<meta property="og:url" content="https://YOUR-DOMAIN.com/">
<meta property="og:image" content="https://YOUR-DOMAIN.com/photo.png">

<!-- Line ~23: Update Twitter meta -->
<meta property="twitter:url" content="https://YOUR-DOMAIN.com/">
<meta property="twitter:image" content="https://YOUR-DOMAIN.com/photo.png">

<!-- Line ~35: Update canonical URL -->
<link rel="canonical" href="https://YOUR-DOMAIN.com/">

<!-- Line ~42: Update JSON-LD structured data -->
"url": "https://YOUR-DOMAIN.com",
"image": "https://YOUR-DOMAIN.com/photo.png"
```

### 2. Add Favicon
Create a favicon for your site:
- **Easy way**: Use [favicon.io](https://favicon.io/) to generate from your photo
- Place `favicon.ico` in the root directory
- Optional: Add `apple-touch-icon.png` (180x180) for iOS

### 3. Test Contact Form
- The form uses Formspree endpoint: `https://formspree.io/f/xangqlnw`
- Test it after deployment to ensure emails are received
- To change endpoint: Edit `index.html` line ~498

### 4. Add Analytics (Optional)
Add Google Analytics before `</head>`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

---

## 📂 File Structure

```
portfolio/
├── index.html              # Main HTML file
├── style.css               # Styles
├── script.js               # JavaScript
├── photo.png               # Profile image
├── SanjayBhargav_AI_ML_Engineer.pdf  # Resume
├── favicon.ico             # (Add this)
├── apple-touch-icon.png    # (Add this - optional)
├── robots.txt              # SEO (provided)
├── sitemap.xml             # (Optional)
├── README.md               # This file
└── TECHNICAL_NOTES.md      # Development notes
```

---

## 🔍 SEO Checklist

- ✅ Meta tags with description and keywords
- ✅ Open Graph tags for social sharing
- ✅ Twitter Card tags
- ✅ Structured data (JSON-LD)
- ✅ Semantic HTML with `<main>` element
- ✅ Proper heading hierarchy (H1 → H2 → H3)
- ✅ Alt text on images
- ✅ Canonical URL
- ✅ robots.txt included
- ⏳ Add sitemap.xml (optional)
- ⏳ Submit to Google Search Console after deployment

---

## 🎨 Customization

### Update Colors
Edit CSS variables in `style.css` (lines 18-28):
```css
:root {
    --primary-dark: #2C3E50;
    --primary-medium: #34495E;
    --accent: #3498DB;
    /* ... */
}
```

### Update Content
- **Personal info**: Edit `index.html` sections
- **Projects**: Update project cards (lines ~206-301)
- **Experience**: Update timeline items (lines ~311-363)
- **Resume**: Replace `SanjayBhargav_AI_ML_Engineer.pdf`

---

## ⚡ Performance

Current optimizations:
- ✅ Minified Google Fonts load
- ✅ Preconnect to font CDN
- ✅ Image dimensions specified (prevents layout shift)
- ✅ Efficient CSS with no unused styles
- ✅ Minimal JavaScript footprint
- ✅ No external dependencies

**Optional improvements:**
- Compress images (use [TinyPNG](https://tinypng.com/))
- Enable CDN caching
- Add service worker for offline support

---

## 🔒 Security Headers

If using Apache, create `.htaccess`:
```apache
<IfModule mod_headers.c>
    Header set X-Content-Type-Options "nosniff"
    Header set X-Frame-Options "SAMEORIGIN"
    Header set X-XSS-Protection "1; mode=block"
    Header set Referrer-Policy "strict-origin-when-cross-origin"
</IfModule>
```

If using Netlify, create `netlify.toml`:
```toml
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "SAMEORIGIN"
    X-Content-Type-Options = "nosniff"
    X-XSS-Protection = "1; mode=block"
    Referrer-Policy = "strict-origin-when-cross-origin"
```

---

## 📊 Post-Deployment

1. **Test on multiple devices**
   - Desktop (Chrome, Firefox, Safari, Edge)
   - Mobile (iOS Safari, Chrome Mobile)
   - Tablet

2. **Run Lighthouse audit**
   - Open Chrome DevTools → Lighthouse
   - Run Performance, Accessibility, Best Practices, SEO audits
   - Target: 90+ scores in all categories

3. **Test contact form**
   - Submit a test message
   - Verify email receipt

4. **Check social sharing**
   - Use [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)
   - Use [Twitter Card Validator](https://cards-dev.twitter.com/validator)

5. **Submit to search engines**
   - [Google Search Console](https://search.google.com/search-console)
   - [Bing Webmaster Tools](https://www.bing.com/webmasters)

---

## 🆘 Troubleshooting

**Form not working?**
- Check Formspree endpoint in `index.html` line 498
- Verify network requests in browser DevTools

**Images not loading?**
- Check file paths are relative (no leading `/`)
- Verify file names match exactly (case-sensitive)

**Animations not working?**
- Check browser console for JavaScript errors
- Verify `script.js` is loading

**Mobile menu not opening?**
- Check JavaScript console for errors
- Verify ARIA attributes are present

---

## 📞 Support

For bug fixes reference or technical questions, see:
- `TECHNICAL_NOTES.md` - Implementation details
- `walkthrough.md` - Completed fixes and improvements

---

## 📄 License

This portfolio is for personal use by Sakhinala Sanjay Bhargav.

---

**Last Updated**: November 27, 2025
**Version**: 1.0.0 (Production Ready)
