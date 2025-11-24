# Quick Start Guide

## 🚀 Get Running in 5 Minutes

### 1. Install Hugo Extended

**Mac (Homebrew):**
```bash
brew install hugo
```

**Windows (Chocolatey):**
```bash
choco install hugo-extended
```

**Linux:**
```bash
snap install hugo
```

**Verify installation:**
```bash
hugo version
# Should show v0.121.0 or later with "extended"
```

### 2. Clone and Run

```bash
# Navigate to the project folder (you're probably already here)
cd cartoolhq_hugo_website

# Run local server
hugo server -D

# Open your browser to http://localhost:1313
```

### 3. Replace Hero Image

Copy your automotive tools image to:
```
static/images/hero-bg.jpg
```

Recommended: 1920×1000px, JPG format, < 200KB

### 4. Create Your First Listicle

```bash
hugo new listicles/best-socket-sets-2025.md
```

Edit the file at `content/listicles/best-socket-sets-2025.md`:

```yaml
---
title: "Best 7 Socket Sets for Home Mechanics (2025)"
date: 2025-11-20
draft: false
featured_image: "/images/socket-sets.jpg"
excerpt: "We tested 20 socket sets to find the best for DIY car maintenance."
categories: ["Hand Tools"]
tags: ["sockets", "mechanics"]

products:
  - rank: 1
    name: "Craftsman 450-Piece Set"
    specs: "1/4, 3/8, 1/2-inch Drives • Chrome Vanadium"
    affiliate_link: "https://amazon.com/..."
    pros:
      - "Comprehensive coverage"
      - "Lifetime warranty"
    cons:
      - "Heavy case"
---

Your introduction goes here...
```

### 5. Preview Your Content

Visit http://localhost:1313 - changes auto-reload!

### 6. Build for Production

```bash
hugo --minify

# Output is in /public/ folder
```

---

## 📝 Quick Content Tips

### Affiliate Link Format
Use your Amazon Associates tracking ID:
```
https://amazon.com/dp/PRODUCT_ID?tag=YOUR_TRACKING_ID
```

### Image Sizes
- **Hero**: 1920×1000px
- **Featured (listicle cards)**: 800×600px
- **Product images**: 400×400px

### SEO Best Practices
- Title: 50-60 characters
- Excerpt: 150-160 characters
- Use keywords in title (e.g., "Best X for Y")
- Update `lastmod` date when refreshing content

---

## 🔧 Common Commands

```bash
# Start server with drafts
hugo server -D

# Start server (production mode, no drafts)
hugo server

# Build for production
hugo --minify

# Create new listicle
hugo new listicles/my-new-post.md

# Create new page
hugo new pages/contact.md

# Check for broken links (requires htmltest)
hugo && htmltest
```

---

## 📁 Key Files to Edit

| File | Purpose |
|------|---------|
| `config.toml` | Site settings, menus, social links |
| `content/listicles/*.md` | Your blog posts |
| `static/images/` | All images |
| `assets/css/main.css` | Styling (if needed) |
| `static/admin/config.yml` | CMS configuration |

---

## 🎨 Customization

### Change Site Title
Edit `config.toml`:
```toml
title = "Your New Name"
```

### Update Social Links
Edit `config.toml`:
```toml
[params]
  youtube = "https://youtube.com/@yourhandle"
  instagram = "https://instagram.com/yourhandle"
```

### Modify Colors
Edit `assets/css/main.css` CSS variables:
```css
:root {
  --accent-primary: #3b82f6;  /* Change blue */
  --accent-secondary: #8b5cf6; /* Change purple */
}
```

---

## ❓ Need Help?

1. **Check README.md** - Full documentation
2. **Check DEPLOYMENT.md** - Deployment guide
3. **Hugo Docs** - https://gohugo.io/documentation/
4. **Open an Issue** - GitHub issues tab

---

**Happy building! 🔧**
