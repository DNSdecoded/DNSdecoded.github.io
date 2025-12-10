# Cloudflare Pages Deployment Guide

## 🚀 Quick Deploy to Cloudflare Pages

Cloudflare Pages offers free hosting with excellent performance, global CDN, and unlimited bandwidth.

---

## Method 1: Git Integration (Recommended)

### Step 1: Push to GitHub

```bash
# Initialize git repository
git init

# Add all files
git add .

# Commit
git commit -m "Production-ready portfolio"

# Create GitHub repository and push
git branch -M main
git remote add origin https://github.com/yourusername/portfolio.git
git push -u origin main
```

### Step 2: Connect to Cloudflare Pages

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Click **Pages** in the sidebar
3. Click **Create a project**
4. Click **Connect to Git**
5. Select your **GitHub repository**
6. Configure build settings:
   - **Project name**: `your-portfolio` (will be your subdomain)
   - **Production branch**: `main`
   - **Build command**: Leave empty (static site)
   - **Build output directory**: `/` (root directory)
7. Click **Save and Deploy**

Your site will be live at: `https://your-portfolio.pages.dev`

---

## Method 2: Direct Upload (Drag & Drop)

### Quick Deploy

1. Go to [Cloudflare Pages](https://pages.cloudflare.com/)
2. Click **Create a project**
3. Click **Upload assets**
4. Drag and drop your entire `portfolio` folder
5. Give your project a name
6. Click **Deploy**

**✅ Done!** Your site is live at `https://your-project-name.pages.dev`

---

## Method 3: Wrangler CLI

### Install Wrangler

```bash
npm install -g wrangler
```

### Login to Cloudflare

```bash
wrangler login
```

### Deploy

```bash
cd portfolio
wrangler pages deploy . --project-name=your-portfolio
```

---

## 🔧 Post-Deployment Configuration

### 1. Add Custom Domain

1. Go to your Pages project dashboard
2. Click **Custom domains**
3. Click **Set up a custom domain**
4. Enter your domain (e.g., `sanjaysakhinala.com`)
5. Follow DNS setup instructions
6. SSL certificate will be auto-generated

### 2. Update Meta Tags

After deployment, update URLs in `index.html`:

```html
<!-- Replace https://yourdomain.com with your actual URL -->
<meta property="og:url" content="https://your-portfolio.pages.dev/">
<meta property="og:image" content="https://your-portfolio.pages.dev/photo.png">
<meta property="twitter:url" content="https://your-portfolio.pages.dev/">
<link rel="canonical" href="https://your-portfolio.pages.dev/">

<!-- In JSON-LD structured data -->
"url": "https://your-portfolio.pages.dev"
```

### 3. Environment Variables (if needed)

If you need environment variables:
1. Go to **Settings** → **Environment variables**
2. Add variables for Production/Preview

---

## 📊 Performance Features

Cloudflare Pages automatically provides:

✅ **Global CDN** - Content served from 200+ locations
✅ **Automatic HTTPS** - Free SSL certificates
✅ **DDoS Protection** - Enterprise-grade security
✅ **HTTP/2 & HTTP/3** - Modern protocols
✅ **Brotli Compression** - Automatic compression
✅ **Smart caching** - Headers in `_headers` file
✅ **Unlimited bandwidth** - No traffic limits
✅ **Atomic deployments** - Zero downtime

---

## 🔒 Security Headers

Your `_headers` file is automatically applied:

```
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

Plus aggressive caching for static assets (1 year).

---

## 🔄 CI/CD Workflow

Every push to your `main` branch automatically:
1. Triggers a new build
2. Deploys to production
3. Invalidates cache
4. Updates your site

**Preview deployments** for pull requests are automatic!

---

## 📈 Analytics

### Enable Cloudflare Web Analytics (Free)

1. Go to your Pages project
2. Click **Web Analytics**
3. Enable analytics
4. Copy the JavaScript snippet
5. Add before `</body>` in `index.html`:

```html
<!-- Cloudflare Web Analytics -->
<script defer src='https://static.cloudflareinsights.com/beacon.min.js' 
        data-cf-beacon='{"token": "YOUR-TOKEN"}'></script>
```

**Features:**
- No cookies required
- Privacy-friendly
- Real-time visitors
- Page views
- Referrers
- Browsers & devices

---

## 🌍 Custom Domain Setup

### Option 1: Domain on Cloudflare

If your domain is already on Cloudflare:
1. It's automatic!
2. Just add the custom domain in Pages dashboard
3. DNS records are created automatically

### Option 2: External Domain

If using another registrar:
1. Add custom domain in Pages dashboard
2. Copy the CNAME record shown
3. Add it to your DNS provider:
   ```
   Type: CNAME
   Name: @ (or subdomain)
   Value: your-portfolio.pages.dev
   ```
4. Wait for DNS propagation (usually <5 minutes)

---

## 🐛 Troubleshooting

### Build Fails

- Cloudflare Pages doesn't need a build step for static sites
- Ensure **Build command** is empty
- **Output directory** should be `/`

### Custom Domain Not Working

- Check DNS propagation: [dnschecker.org](https://dnschecker.org)
- Verify CNAME record points to: `your-project.pages.dev`
- SSL can take up to 24 hours (usually instant)

### Files Not Found (404)

- Ensure all paths are relative (no leading `/`)
- Check file names are case-sensitive
- Verify `index.html` is in root

### Form Not Submitting

- Formspree should work immediately
- Check browser console for errors
- Verify fetch() is not blocked by CSP

---

## 📱 Preview Deployments

Every pull request automatically gets a preview URL:

```
https://abc123.your-portfolio.pages.dev
```

Perfect for testing changes before merging!

---

## 🔄 Redeploy After Changes

### Push to Git

```bash
git add .
git commit -m "Updated content"
git push
```

**Automatic redeployment** in ~30 seconds!

### Manual Deploy

```bash
wrangler pages deploy . --project-name=your-portfolio
```

---

## 💡 Pro Tips

1. **Branch deployments**: Any branch gets a preview URL
2. **Rollback**: Instantly rollback to previous deployments
3. **Cache purge**: Automatic on every deployment
4. **Free forever**: No credit card required
5. **Functions**: Add serverless functions later if needed

---

## 📋 Checklist

Before going live:

- [ ] Push code to GitHub
- [ ] Connect repository to Cloudflare Pages
- [ ] Update meta tags with actual domain
- [ ] Add custom domain (optional)
- [ ] Test form submission
- [ ] Enable Web Analytics
- [ ] Run Lighthouse audit (target 95+ score)
- [ ] Test on mobile & desktop
- [ ] Check social media preview (Facebook/Twitter debuggers)
- [ ] Submit to Google Search Console

---

## 🆚 Why Cloudflare Pages?

**vs GitHub Pages:**
- ✅ Faster (global CDN)
- ✅ Better caching control
- ✅ Preview deployments for PRs
- ✅ Web Analytics included

**vs Netlify:**
- ✅ Unlimited bandwidth (Netlify caps at 100GB)
- ✅ Better performance (Cloudflare's network)
- ✅ Simpler pricing
- ✅ Built-in DDoS protection

**vs Vercel:**
- ✅ No bandwidth limits
- ✅ Better for static sites
- ✅ More generous free tier

---

## 📞 Support

- **Documentation**: [developers.cloudflare.com/pages](https://developers.cloudflare.com/pages/)
- **Community**: [Cloudflare Community](https://community.cloudflare.com/)
- **Status**: [cloudflarestatus.com](https://www.cloudflarestatus.com/)

---

## 🎉 You're Live!

Your portfolio is now deployed on Cloudflare's blazing-fast global network!

**Next steps:**
1. Share your portfolio URL with recruiters
2. Add it to your LinkedIn
3. Include it in your resume
4. Monitor analytics

---

**Deployed on**: Cloudflare Pages
**Performance**: ⚡ Global CDN
**Security**: 🔒 DDoS Protection
**Uptime**: 99.99%+
**Cost**: $0 (Free Forever)
