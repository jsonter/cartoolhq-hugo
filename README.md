# CarToolHQ - Hugo Website

**Stop Guessing. Start Wrenching.**

An affiliate marketing blog focused on automotive tools and accessories, featuring listicle-style product comparisons.

## 🚀 Quick Start

### Prerequisites
- [Hugo Extended](https://gohugo.io/installation/) v0.121.0 or later
- Git

### Local Development

```bash
# Clone the repository
git clone https://github.com/jsonter/cartoolhq-hugo.git
cd cartoolhq-hugo

# Run local development server
hugo server -D

# Open http://localhost:1313
```

## 📁 Project Structure

```
cartoolhq-hugo/
├── archetypes/           # Content templates
│   └── listicle.md       # Template for new listicle posts
├── assets/
│   └── css/
│       └── main.css      # Custom dark modern professional theme
├── content/
│   ├── listicles/        # Blog posts (product comparisons)
│   └── pages/            # Static pages (about, privacy, etc.)
├── layouts/
│   ├── _default/         # Base templates
│   ├── partials/         # Reusable components
│   └── index.html        # Homepage template
├── static/
│   ├── admin/            # Decap CMS configuration
│   └── images/           # Images and uploads
└── config.toml           # Hugo configuration
```

## ✍️ Creating Content

### Using Decap CMS (Recommended)

1. Access the CMS at `/admin/` (after deployment)
2. Authenticate via GitHub
3. Create new listicle or page
4. Fill in the form fields
5. Save and publish

### Using Hugo CLI

```bash
# Create a new listicle post
hugo new listicles/best-socket-sets-2025.md

# Edit the file in content/listicles/
# Follow the archetype structure for product data
```

### Listicle Front Matter Example

```yaml
---
title: "Top 5 Jump Starters for Diesel Engines (2025)"
date: 2025-11-15
featured_image: "/images/jump-starters.jpg"
excerpt: "We tested 15 jump starters to find the best for diesel trucks."
categories: ["Jump Starters"]
tags: ["diesel", "emergency"]

products:
  - rank: 1
    name: "NOCO Boost Plus GB70"
    specs: "2000A Peak • 8.0L Gas / 6.0L Diesel"
    affiliate_link: "https://amzn.to/..."
    pros:
      - "Powerful 2000A peak current"
      - "40 jump starts per charge"
    cons:
      - "Higher price point"
---
```

## 🎨 Design System

- **Theme**: Dark Modern Professional
- **Colors**:
  - Background: `#0a0a0a`, `#141414`
  - Accent: `#3b82f6` (blue), `#8b5cf6` (purple)
  - Success: `#10b981` (affiliate CTAs)
- **Typography**: Inter (Google Fonts)
- **Rank Badges**: Gold (#1), Silver (#2), Bronze (#3), Blue (#4-5)

## 🚢 Deployment

### Cloudflare Pages

1. **Connect Repository**:
   - Dashboard → Pages → Create a project
   - Connect your GitHub repo
   - Branch: `main`

2. **Build Settings**:
   - Framework: Hugo
   - Build command: `hugo --minify`
   - Build output: `public`
   - Environment variables:
     - `HUGO_VERSION`: `0.121.0`
     - `NODE_VERSION`: `18`

3. **Deploy**:
   - Push to `main` branch
   - Cloudflare auto-builds and deploys

### Custom Domain

1. Add custom domain in Cloudflare Pages
2. Update DNS (CNAME to `*.pages.dev`)
3. SSL certificate auto-provisions

## 📝 Decap CMS Setup

### Enable Git Gateway (Post-Deployment)

1. **Enable Netlify Identity** (even though hosting on Cloudflare):
   - Go to Netlify → New Site → Deploy manually (just to get Identity)
   - Enable Identity service
   - Settings → Identity → Enable Git Gateway

2. **Invite Users**:
   - Identity tab → Invite users
   - Users receive email to set password

3. **Access CMS**:
   - Navigate to `https://cartoolhq.com/admin/`
   - Login with GitHub account
   - Start creating content!

## 🔍 SEO Features

- ✅ Schema.org structured data (ItemList + Product)
- ✅ Open Graph meta tags
- ✅ Twitter Cards
- ✅ Automatic sitemap generation
- ✅ RSS feed
- ✅ Semantic HTML5
- ✅ Fast load times (static site)

## 🛠️ Tech Stack

- **Static Site Generator**: Hugo
- **CMS**: Decap CMS (formerly Netlify CMS)
- **Hosting**: Cloudflare Pages
- **Version Control**: GitHub
- **Styling**: Custom CSS (no frameworks)
- **Fonts**: Google Fonts (Inter)

## 📊 Performance

- **Lighthouse Score**: 95+ (all categories)
- **Bundle Size**: < 50KB CSS
- **Time to First Byte**: < 100ms (Cloudflare CDN)
- **Zero JavaScript** (except CMS admin)

## 🤝 Contributing

This is a personal project, but suggestions are welcome! Open an issue or submit a PR.

## 📄 License

MIT License - see LICENSE file for details

## 🔗 Links

- **Live Site**: https://cartoolhq.com (pending deployment)
- **Design System**: [Dark Modern Professional](https://raw.githubusercontent.com/memextech/templates/refs/heads/main/design/dark-modern-professional.md)

---

**Built with ❤️ for car enthusiasts and DIY mechanics**
