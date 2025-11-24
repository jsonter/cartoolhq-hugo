# Spec Provenance

**Date**: 2025-11-18  
**Mode**: Plan  
**Previous Phase**: Static prototype (approved)  
**Current Phase**: Hugo custom theme build + CMS + deployment

**Key Decisions**:
- Custom Hugo theme (not Blowfish) - converts approved prototype
- Netlify CMS for content management
- Cloudflare Pages for hosting (GitHub integration)
- Listicle-focused content structure
- Schema.org markup for SEO

---

# Spec Header

**Name**: CarToolHQ - Hugo Custom Theme Build

**Smallest Acceptable Scope**:
A fully functional Hugo site with:
- Custom theme matching approved dark modern professional prototype
- Homepage with listicle preview grid
- Single listicle template (ranked product layout)
- Netlify CMS configured for easy content editing
- GitHub repo ready for Cloudflare Pages deployment
- 1-2 sample listicle posts to demonstrate
- Schema.org structured data (Product + ItemList)
- SEO meta tags & Open Graph

**Non-Goals** (can add later):
- Multi-author support
- Comment system
- Search functionality
- Multiple layout variations
- Advanced analytics integration
- Email newsletter integration
- A/B testing for CTAs

---

# Paths to Supplementary Guidelines

**Design System**:  
https://raw.githubusercontent.com/memextech/templates/refs/heads/main/design/dark-modern-professional.md

**Reference Materials**:
- Approved prototype: `./prototype/` (HTML, CSS, images)
- Hugo documentation: https://gohugo.io/documentation/

---

# Decision Snapshot

| Decision | Chosen Path | Rationale |
|----------|-------------|-----------|
| **Theme approach** | Custom (not Blowfish) | Prototype already approved; no design rework; leaner codebase |
| **Content structure** | Listicle archetypes | Matches affiliate business model; structured product data |
| **CMS** | Netlify CMS | GitHub-based; free tier sufficient; works with Cloudflare Pages |
| **Hosting** | Cloudflare Pages | User requested; excellent CDN; auto-deploy from GitHub |
| **SEO strategy** | Schema.org + Hugo built-ins | Google-friendly product markup; Hugo handles sitemaps/RSS |
| **Asset management** | Hugo Pipes | Built-in SCSS processing, minification, fingerprinting |

---

# Architecture at a Glance

## Hugo Directory Structure

```
cartoolhq-hugo/
├── archetypes/
│   └── listicle.md              # Template for new listicle posts
├── assets/
│   ├── css/
│   │   └── main.css             # Prototype CSS (converted)
│   └── images/
│       └── hero-bg.jpg
├── content/
│   ├── _index.md                # Homepage content
│   ├── listicles/               # Blog posts
│   │   ├── top-5-jump-starters-diesel.md
│   │   └── best-7-torque-wrenches-under-100.md
│   └── pages/
│       ├── about.md
│       └── privacy.md
├── layouts/
│   ├── _default/
│   │   ├── baseof.html          # Base template
│   │   ├── list.html            # Listicle listing page
│   │   └── single.html          # Single listicle page
│   ├── partials/
│   │   ├── head.html            # Meta tags, fonts, CSS
│   │   ├── header.html          # Site header/nav
│   │   ├── footer.html          # Footer + disclosure
│   │   ├── listicle-card.html   # Preview card component
│   │   ├── ranked-product.html  # Product card in listicle
│   │   └── schema-listicle.html # Schema.org markup
│   ├── index.html               # Homepage template
│   └── shortcodes/
│       └── product-card.md      # Shortcode for easy product authoring
├── static/
│   ├── admin/
│   │   ├── config.yml           # Netlify CMS configuration
│   │   └── index.html           # CMS entry point
│   └── favicon.ico
├── config.toml                  # Hugo site configuration
├── netlify.toml                 # Build config (optional)
└── README.md
```

---

## Content Model: Listicle Posts

**Front Matter Structure** (`archetypes/listicle.md`):

```yaml
---
title: "Top 5 Jump Starters for Diesel Engines (2025)"
date: 2025-11-15
publishDate: 2025-11-15
lastmod: 2025-11-15
draft: false
featured_image: "/images/jump-starters-hero.jpg"
excerpt: "We tested 15 heavy-duty jump starters to find the best options for diesel trucks and large engines."
categories: ["Jump Starters", "Emergency Tools"]
tags: ["diesel", "trucks", "emergency", "battery"]
seo_title: "Best Jump Starters for Diesel Engines 2025 - Tested & Reviewed"
seo_description: "Expert comparison of the top 5 jump starters for diesel engines. Real-world tests, pros/cons, and buying guide."

# Listicle-specific fields
products:
  - rank: 1
    name: "NOCO Boost Plus GB70"
    image: "/images/products/noco-gb70.jpg"
    specs: "2000A Peak • 8.0L Gas / 6.0L Diesel • UltraSafe Technology"
    affiliate_link: "https://amzn.to/example1"
    pros:
      - "Powerful 2000A peak current"
      - "Can jump start up to 40 times per charge"
      - "Spark-proof and reverse polarity protection"
      - "Built-in LED flashlight"
    cons:
      - "Higher price point than competitors"
      - "Heavier than pocket-sized models"
  - rank: 2
    name: "HULKMAN Alpha85"
    # ... etc
---

# Top 5 Jump Starters for Diesel Engines (2025)

Intro paragraph with context...

<!-- Products render automatically from front matter -->
```

---

# Implementation Plan

## Phase 1: Hugo Site Scaffold (30 mins)

**1.1 Initialize Hugo site**
```bash
hugo new site cartoolhq-hugo
cd cartoolhq-hugo
git init
```

**1.2 Create directory structure**
- Set up folders: `archetypes/`, `layouts/`, `assets/`, `static/`
- Copy prototype CSS → `assets/css/main.css`
- Copy hero image → `assets/images/hero-bg.jpg`

**1.3 Configure `config.toml`**
```toml
baseURL = "https://cartoolhq.com"
languageCode = "en-us"
title = "CarToolHQ"
theme = ""  # Custom theme (no external theme)

[params]
  description = "Stop Guessing. Start Wrenching."
  author = "CarToolHQ Team"

[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true  # Allow HTML in markdown

[outputs]
  home = ["HTML", "RSS", "JSON"]
  section = ["HTML", "RSS"]
```

---

## Phase 2: Base Templates (45 mins)

**2.1 Create `layouts/_default/baseof.html`**
- HTML5 doctype, head, body structure
- Include partials: head, header, main block, footer
- Google Fonts preconnect for Inter

**2.2 Create `layouts/partials/head.html`**
- Meta charset, viewport
- SEO meta tags (title, description, OG tags)
- Favicon link
- CSS pipeline: `{{ $css := resources.Get "css/main.css" | minify | fingerprint }}`
- Schema.org JSON-LD placeholder

**2.3 Create `layouts/partials/header.html`**
- Convert prototype header HTML
- Use Hugo menu system for nav links
- Site title links to homepage

**2.4 Create `layouts/partials/footer.html`**
- Convert prototype footer HTML
- Dynamic copyright year: `{{ now.Year }}`
- Affiliate disclosure text

---

## Phase 3: Homepage Template (30 mins)

**3.1 Create `layouts/index.html`**
- Hero section with background image
- "Stop Guessing. Start Wrenching." title
- Listicle grid pulling from `content/listicles/`
- Range over recent posts: `{{ range first 5 (where .Site.RegularPages "Section" "listicles") }}`

**3.2 Create `layouts/partials/listicle-card.html`**
- Convert prototype listicle card HTML
- Accept `.` context (page object)
- Use `.Params.featured_image`, `.Title`, `.Params.excerpt`
- Link to `.Permalink`

**3.3 Create `content/_index.md`**
- Empty front matter (homepage uses template logic)

---

## Phase 4: Listicle Template (60 mins)

**4.1 Create `layouts/_default/single.html`**
- Listicle header: breadcrumb, title, meta (author, date, last updated)
- Affiliate disclosure notice
- Range over `.Params.products` to render ranked cards
- Include Schema.org partial

**4.2 Create `layouts/partials/ranked-product.html`**
- Convert prototype ranked product card
- Accept product data as context
- Rank badge with conditional styling (gold/silver/bronze/blue)
- Pros/cons lists from arrays
- Affiliate button with link

**4.3 Create `layouts/partials/schema-listicle.html`**
```json
{
  "@context": "https://schema.org",
  "@type": "ItemList",
  "name": "{{ .Title }}",
  "description": "{{ .Params.excerpt }}",
  "itemListElement": [
    {{ range $index, $product := .Params.products }}
    {
      "@type": "ListItem",
      "position": {{ add $index 1 }},
      "item": {
        "@type": "Product",
        "name": "{{ $product.name }}",
        "description": "{{ $product.specs }}",
        "url": "{{ $product.affiliate_link }}"
      }
    }{{ if ne $index (sub (len $.Params.products) 1) }},{{ end }}
    {{ end }}
  ]
}
```

**4.4 Create `archetypes/listicle.md`**
- Template with all front matter fields
- Sample product entries
- Helpful comments for content authors

---

## Phase 5: Sample Content (30 mins)

**5.1 Create sample listicles**
- `content/listicles/top-5-jump-starters-diesel.md`
- `content/listicles/best-7-torque-wrenches-under-100.md`
- Fill with realistic data from prototype

**5.2 Create static pages**
- `content/pages/about.md`
- `content/pages/privacy.md`

**5.3 Add product images**
- `static/images/products/` folder
- Placeholder images or actual product photos

---

## Phase 6: Netlify CMS Integration (45 mins)

**6.1 Create `static/admin/config.yml`**
```yaml
backend:
  name: git-gateway
  branch: main

media_folder: "static/images/uploads"
public_folder: "/images/uploads"

collections:
  - name: "listicles"
    label: "Listicles"
    folder: "content/listicles"
    create: true
    slug: "{{slug}}"
    fields:
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Publish Date", name: "date", widget: "datetime"}
      - {label: "Featured Image", name: "featured_image", widget: "image"}
      - {label: "Excerpt", name: "excerpt", widget: "text"}
      - {label: "Categories", name: "categories", widget: "list"}
      - {label: "Tags", name: "tags", widget: "list"}
      - label: "Products"
        name: "products"
        widget: "list"
        fields:
          - {label: "Rank", name: "rank", widget: "number"}
          - {label: "Product Name", name: "name", widget: "string"}
          - {label: "Image", name: "image", widget: "image"}
          - {label: "Specs", name: "specs", widget: "string"}
          - {label: "Affiliate Link", name: "affiliate_link", widget: "string"}
          - {label: "Pros", name: "pros", widget: "list"}
          - {label: "Cons", name: "cons", widget: "list"}
      - {label: "Body", name: "body", widget: "markdown"}
  
  - name: "pages"
    label: "Pages"
    folder: "content/pages"
    create: true
    slug: "{{slug}}"
    fields:
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Body", name: "body", widget: "markdown"}
```

**6.2 Create `static/admin/index.html`**
```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Content Manager</title>
  <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
</head>
<body>
  <script src="https://unpkg.com/netlify-cms@^2.0.0/dist/netlify-cms.js"></script>
</body>
</html>
```

**6.3 Add identity widget to baseof.html**
- Include Netlify Identity script in head
- Add redirect logic for CMS login

---

## Phase 7: GitHub & Cloudflare Setup (30 mins)

**7.1 Create `.gitignore`**
```
/public/
/resources/_gen/
.DS_Store
.hugo_build.lock
```

**7.2 Initialize GitHub repo**
```bash
git add .
git commit -m "Initial CarToolHQ Hugo site"
gh repo create cartoolhq-hugo --public --source=. --remote=origin
git push -u origin main
```

**7.3 Cloudflare Pages configuration**
- Build command: `hugo --minify`
- Build output directory: `public`
- Environment variables: `HUGO_VERSION=0.121.0` (or latest)
- Node version: `18` (for Hugo extended features)

**7.4 Create README.md**
- Local development instructions
- Content authoring workflow
- Deployment info

---

## Phase 8: SEO & Performance (30 mins)

**8.1 Meta tags & Open Graph**
In `layouts/partials/head.html`:
```html
<meta name="description" content="{{ .Description | default .Site.Params.description }}">
<meta property="og:title" content="{{ .Title }}">
<meta property="og:description" content="{{ .Description }}">
<meta property="og:image" content="{{ .Params.featured_image | absURL }}">
<meta property="og:type" content="article">
<meta name="twitter:card" content="summary_large_image">
```

**8.2 RSS feed**
- Hugo generates automatically
- Customize `layouts/_default/rss.xml` if needed

**8.3 Sitemap**
- Hugo generates automatically at `/sitemap.xml`
- Configure update frequency in config.toml

**8.4 Asset optimization**
- CSS minification via Hugo Pipes
- Image processing for responsive images (future enhancement)

---

# Verification & Demo Script

**Local Development Test**:
```bash
hugo server -D
# Open http://localhost:1313
```

**Checklist**:
1. ✅ Homepage loads with hero background image
2. ✅ "Stop Guessing. Start Wrenching." title visible
3. ✅ 5 listicle preview cards display in grid
4. ✅ Click card → navigates to full listicle page
5. ✅ Listicle shows ranked products #1-5 with badges
6. ✅ Pros/cons lists render correctly
7. ✅ Affiliate buttons link properly
8. ✅ Footer disclosure visible
9. ✅ Responsive: resize to mobile → single column, vertical product cards
10. ✅ View source → Schema.org JSON-LD present

**Netlify CMS Test**:
1. Navigate to `/admin/`
2. Authenticate via GitHub (after Git Gateway enabled)
3. Create new listicle post
4. Fill in products array
5. Save → commit to GitHub
6. Verify content appears on site

**Production Deploy Test**:
1. Push to GitHub main branch
2. Cloudflare Pages auto-builds
3. Site live at `cartoolhq.pages.dev`
4. Test CDN speed (should be <1s TTFB globally)

---

# Deploy

## Step 1: GitHub Repository
```bash
# Already initialized in Phase 7
git push origin main
```

## Step 2: Cloudflare Pages Setup

1. **Connect Repository**:
   - Go to Cloudflare Dashboard → Pages
   - Click "Create a project"
   - Connect GitHub account
   - Select `cartoolhq-hugo` repo
   - Branch: `main`

2. **Build Configuration**:
   - Framework preset: Hugo
   - Build command: `hugo --minify`
   - Build output directory: `public`
   - Environment variables:
     - `HUGO_VERSION`: `0.121.0`
     - `NODE_VERSION`: `18`

3. **Deploy**:
   - Click "Save and Deploy"
   - Initial build takes 1-2 minutes
   - Site live at `https://cartoolhq.pages.dev`

## Step 3: Custom Domain (Optional)

1. Add custom domain in Cloudflare Pages settings
2. Update DNS records (CNAME to `cartoolhq.pages.dev`)
3. SSL automatically provisioned

## Step 4: Netlify CMS Git Gateway

1. Enable Netlify Identity (free tier)
2. Configure Git Gateway in Netlify site settings
3. Invite users to CMS
4. Access CMS at `https://cartoolhq.com/admin/`

---

## Notes for Future Enhancements

### Phase 2+ Ideas:
- **Category pages**: Taxonomy templates for product categories
- **Search**: Algolia or Fuse.js client-side search
- **Related posts**: Hugo's `.Site.RegularPages.Related` feature
- **Image optimization**: Hugo image processing for responsive images
- **Analytics**: Cloudflare Web Analytics or Plausible (privacy-friendly)
- **Newsletter**: ConvertKit or Mailchimp embed
- **Table of contents**: Auto-generated for long listicles
- **Affiliate link cloaking**: Hugo shortcode for link management
- **Last updated badges**: Show freshness for SEO

### Content Strategy:
- Target 20-30 listicles for critical mass
- Update top posts quarterly (change "2025" to "2026" in titles)
- Use `lastmod` front matter to signal freshness to Google
- Create category landing pages for major tool types
- Build internal linking strategy between related listicles

### Performance Optimization:
- Lazy-load images below fold
- Preload hero background image
- Use WebP with JPG fallback
- Implement critical CSS inline in head
- Defer non-critical JavaScript

---

**Estimated Total Build Time**: 4-5 hours

**Post-Launch Checklist**:
- [ ] Submit sitemap to Google Search Console
- [ ] Set up Cloudflare Web Analytics
- [ ] Configure Amazon Associates tracking IDs
- [ ] Add FTC disclosure to all affiliate posts
- [ ] Test affiliate links work correctly
- [ ] Set up uptime monitoring (UptimeRobot free tier)
- [ ] Create content calendar for first 10 listicles
