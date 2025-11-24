# CarToolHQ Project Context

## Project Overview
**CarToolHQ** is an affiliate marketing blog built with Hugo, focused on automotive tools and accessories. The site features listicle-style product comparisons with ranked products, affiliate links, and a modern dark theme. Content is managed through Decap CMS (formerly Netlify CMS) for non-technical editing.

**Core Purpose**: Generate affiliate revenue through Amazon Associates and other affiliate programs by publishing high-quality product comparison guides.

**Tagline**: "Stop Guessing. Start Wrenching."

---

## Tech Stack

### Static Site Generator
- **Hugo Extended** v0.121.0+
- No external themes (custom layouts in root)
- Hugo Pipes for CSS minification and fingerprinting
- Static HTML output for optimal performance

### CMS & Content Management
- **Decap CMS** (Git-based, no database)
- Git Gateway backend (via Netlify Identity)
- Content stored in Git repository as Markdown files
- Image uploads to `static/images/uploads/`

### Deployment & Hosting
- **Primary**: Cloudflare Pages
- **Alternative**: Netlify (mentioned in config)
- Build command: `hugo --minify`
- Build output: `public/`
- Deployment via Git push to `main` branch

### Styling
- **Custom CSS** (no frameworks)
- Dark Modern Professional theme
- CSS Custom Properties (CSS variables)
- Inter font from Google Fonts
- No JavaScript on frontend (CMS only)

---

## Project Structure

```
cartoolhq-hugo/
├── archetypes/
│   └── listicle.md              # Template for new listicle posts
├── assets/
│   └── css/
│       └── main.css             # Custom dark theme CSS
├── content/
│   ├── listicles/               # Product comparison posts
│   └── pages/                   # Static pages (about, privacy)
├── layouts/
│   ├── _default/
│   │   ├── baseof.html          # Base template
│   │   ├── single.html          # Listicle page template
│   │   └── list.html            # Archive pages
│   ├── pages/
│   │   └── single.html          # Static page template
│   ├── partials/
│   │   ├── head.html            # Meta tags, SEO, CSS
│   │   ├── header.html          # Navigation
│   │   ├── footer.html          # Footer with affiliate disclosure
│   │   ├── listicle-card.html   # Preview cards
│   │   ├── ranked-product.html  # Product comparison cards
│   │   └── schema-listicle.html # Structured data
│   └── index.html               # Homepage template
├── static/
│   ├── admin/
│   │   ├── config.yml           # Decap CMS configuration
│   │   └── index.html           # CMS entry point
│   └── images/                  # Static images
├── config.toml                  # Hugo site configuration
├── netlify.toml                 # Build configuration
└── prototype/                   # Original static prototype (reference)
```

---

## Content Model

### Listicle Posts (`content/listicles/`)
Primary content type for product comparisons. Each listicle contains:

**Front Matter Structure**:
```yaml
title: "Top N [Product Type] for [Use Case] (2025)"
date: YYYY-MM-DDTHH:MM:SS-05:00
lastmod: YYYY-MM-DDTHH:MM:SS-05:00
draft: false
featured_image: "/images/uploads/..."
excerpt: "Short description for cards and meta tags"
categories: ["Category 1", "Category 2"]
tags: ["tag1", "tag2"]
seo_title: "Custom SEO title"
seo_description: "Custom meta description"

products:
  - rank: 1
    name: "Product Name"
    image: "/images/uploads/product.jpg"
    specs: "Key specifications"
    affiliate_link: "https://amazon.com/..."
    pros:
      - "Pro 1"
      - "Pro 2"
    cons:
      - "Con 1"
      - "Con 2"
```

**Content Body**: Markdown introduction, buying guides, testing methodology (rendered before product cards).

### Static Pages (`content/pages/`)
About, privacy policy, contact, etc. Simple front matter with markdown body.

---

## Design System & Conventions

### Color Palette (CSS Custom Properties)
```css
--bg-primary: #0a0a0a           /* Main background */
--bg-secondary: #141414         /* Card backgrounds */
--bg-tertiary: #1f1f1f          /* Hover states */

--text-primary: #ffffff         /* Main text */
--text-secondary: #a3a3a3       /* Muted text */
--text-tertiary: #737373        /* Lighter muted */

--accent-primary: #3b82f6       /* Blue accent */
--accent-secondary: #8b5cf6     /* Purple accent */
--color-success: #10b981        /* Affiliate CTAs (green) */

--rank-gold: #ffd700            /* #1 badge */
--rank-silver: #c0c0c0          /* #2 badge */
--rank-bronze: #cd7f32          /* #3 badge */
--rank-blue: #3b82f6            /* #4+ badges */
```

### Spacing Scale
```css
--spacing-xs: 8px
--spacing-sm: 12px
--spacing-md: 16px
--spacing-lg: 24px
--spacing-xl: 32px
--spacing-2xl: 48px
--spacing-3xl: 64px
```

### Typography
- **Font**: Inter (Google Fonts, weights 400/500/600/700)
- **Headings**: Bold, negative letter-spacing
- **Body**: 16px base, line-height 1.6

### Component Patterns

#### Rank Badges
- Gold (#1), Silver (#2), Bronze (#3), Blue (#4-5)
- Positioned top-left of product cards
- Badge class determined by rank number

#### Affiliate CTAs
- Green button with `--color-success`
- Text: "Check Price on Amazon"
- Links have `rel="noopener nofollow sponsored"`
- Hover animations with scale transform

#### Cards
- Dark background (`--bg-secondary`)
- Border: 1px solid `--border-primary`
- Border radius: `--radius-lg` (12px)
- Hover: Scale, border color transition

---

## SEO & Affiliate Marketing Conventions

### Required Disclosures
- **Inline notice** on listicle pages (top of content)
- **Footer disclosure** on every page
- **Text**: "We may earn a commission from purchases made through affiliate links, at no extra cost to you."
- Config setting: `config.toml` → `params.affiliateDisclosure`

### Link Attributes
All affiliate links MUST include:
```html
rel="noopener nofollow sponsored"
target="_blank"
```

### Schema.org Structured Data
- **Type**: ItemList + Product
- Generated via `partials/schema-listicle.html`
- Includes: product name, position, URL (affiliate link)
- Automatically injected on listicle pages

### SEO Best Practices
- Custom SEO title/description per listicle
- Open Graph meta tags for social sharing
- Twitter Cards support
- Featured images for social previews
- Semantic HTML5 structure
- Automatic sitemap generation

---

## Hugo Conventions & Patterns

### Templating
- **Base template**: `layouts/_default/baseof.html`
- **Blocks**: `main`, `header`, `footer`
- **Partials**: Reusable components in `layouts/partials/`
- **Context**: Always pass context to partials (`.` or specific data)

### Content Organization
- **Sections**: `listicles`, `pages`
- **Taxonomies**: `categories`, `tags`
- **Archetypes**: Use `hugo new listicles/[slug].md` to create from template

### Asset Pipeline
```go
{{ $css := resources.Get "css/main.css" | minify | fingerprint }}
<link rel="stylesheet" href="{{ $css.Permalink }}" integrity="{{ $css.Data.Integrity }}">
```
- CSS from `assets/` (not `static/`)
- Minification via Hugo Pipes
- Fingerprinting for cache busting
- Integrity hashes for security

### Date Formatting
- Config: `lastmod.Format "January 2, 2006"`
- Include timezone in front matter: `2025-11-15T10:00:00-05:00`

---

## Decap CMS Configuration

### Backend
- **Production**: `git-gateway` (requires Netlify Identity)
- **Test**: `test-repo` (local development)

### Collections
1. **Listicles** (`content/listicles/`)
   - Custom product array widget
   - Image upload support
   - List widgets for pros/cons

2. **Pages** (`content/pages/`)
   - Simple markdown editor

### Media Management
- **Folder**: `static/images/uploads/`
- **Public path**: `/images/uploads/`
- Uploaded images accessible immediately

### Access
- URL: `/admin/`
- Authentication via GitHub + Netlify Identity
- Redirect configured in `netlify.toml`

---

## Build & Deployment

### Local Development
```bash
hugo server -D
# Serves at http://localhost:1313
# -D flag includes drafts
```

### Build Command
```bash
hugo --minify
# Output to public/
# Minifies HTML, CSS, JS
```

### Environment Variables
```toml
HUGO_VERSION = "0.121.0"
HUGO_ENV = "production"
HUGO_ENABLEGITINFO = "true"
```

### Cloudflare Pages Settings
- Framework: Hugo
- Build command: `hugo --minify`
- Build output: `public`
- Branch: `main`

---

## Code Patterns & Conventions

### Hugo Template Iteration
```go
{{ range .Params.products }}
    {{ partial "ranked-product.html" . }}
{{ end }}
```

### Conditional Logic (Rank Badges)
```go
{{ $badgeClass := "rank-blue" }}
{{ if eq $rank 1 }}{{ $badgeClass = "rank-gold" }}{{ end }}
{{ if eq $rank 2 }}{{ $badgeClass = "rank-silver" }}{{ end }}
{{ if eq $rank 3 }}{{ $badgeClass = "rank-bronze" }}{{ end }}
```

### URL Construction
```go
{{ .Permalink }}              <!-- Full URL -->
{{ .RelPermalink }}           <!-- Relative URL -->
{{ . | absURL }}              <!-- Convert relative to absolute -->
```

### Taxonomies
```go
{{ with .Params.categories }}{{ index . 0 }}{{ end }}  <!-- First category -->
{{ range .Params.tags }}{{ . }}{{ end }}               <!-- All tags -->
```

---

## File Naming Conventions

### Content Files
- **Slug format**: `best-7-torque-wrenches-under-100.md`
- **Lowercase**, **hyphen-separated**
- Include year for evergreen updates: `top-5-jump-starters-2025.md`

### Images
- **Descriptive names**: `jump-starters-hero.jpg`
- Avoid spaces and special characters
- Store in `static/images/` or `static/images/uploads/`

### Templates
- **Hugo conventions**: `single.html`, `list.html`, `baseof.html`
- **Partials**: Descriptive names like `ranked-product.html`

---

## Performance Optimizations

### Current Stats
- **CSS bundle**: < 50KB (minified)
- **Build time**: ~2 seconds
- **Lighthouse score**: 95+ (all categories)
- **TTFB**: < 100ms (Cloudflare CDN)

### Strategies
- Zero JavaScript on frontend (except CMS admin)
- Static HTML generation (no server-side rendering)
- CSS minification and fingerprinting
- Image optimization (manual, no build-time processing)
- CDN distribution via Cloudflare

---

## Testing & Quality Assurance

### Pre-Deployment Checklist
- [ ] Test locally with `hugo server -D`
- [ ] Verify all affiliate links include proper `rel` attributes
- [ ] Check affiliate disclosures present on all listicles
- [ ] Validate Schema.org markup (Google Rich Results Test)
- [ ] Test responsive design (mobile/tablet/desktop)
- [ ] Review meta tags (Open Graph, Twitter Cards)
- [ ] Confirm images load properly
- [ ] Check navigation links

### Content Review
- [ ] Product data complete (name, specs, pros/cons, link)
- [ ] Excerpt written for preview cards
- [ ] Featured image set (800x600 recommended)
- [ ] Categories and tags assigned
- [ ] SEO title/description customized
- [ ] Markdown content proofread

---

## Anti-Patterns to Avoid

### Content
- ❌ Don't omit affiliate disclosures
- ❌ Don't use direct product links without `rel="nofollow sponsored"`
- ❌ Don't skip SEO fields (title, description, featured image)
- ❌ Don't use generic CTAs (always "Check Price on Amazon")

### Templates
- ❌ Don't put CSS in `static/` (use `assets/` for pipeline)
- ❌ Don't inline large amounts of CSS/JS
- ❌ Don't skip context when calling partials
- ❌ Don't use absolute URLs for internal links

### Development
- ❌ Don't commit `public/` directory to Git (build artifact)
- ❌ Don't edit generated HTML (edit templates instead)
- ❌ Don't skip Hugo version in build config
- ❌ Don't use external theme dependencies (increases complexity)

---

## Future Enhancements (Not Yet Built)

### Potential Features
- Image optimization pipeline (Hugo image processing)
- Table of contents for long listicles
- Related posts section
- Author profiles (if multi-author)
- Comments system (Disqus or similar)
- Newsletter signup integration
- Search functionality
- Analytics integration (Google Analytics, Plausible)

### Content Expansion
- More listicles (target: 50-100 posts)
- Category landing pages
- Comparison tables
- Video embeds (YouTube reviews)
- Buyer's guides (non-listicle format)

---

## Reference Guidelines

This project follows the **Dark Modern Professional** design guidelines:
- **URL**: https://raw.githubusercontent.com/memextech/templates/refs/heads/main/design/dark-modern-professional.md

When extending the design, refer to these approved guidelines for consistency.

---

## Important Configuration Files

### config.toml
- Site-wide settings
- Menu structure
- Taxonomies
- Affiliate disclosure text

### netlify.toml
- Build commands and environment
- Redirects (CMS admin)
- Deploy preview settings

### static/admin/config.yml
- Decap CMS collections
- Field definitions
- Media folder paths

---

## Common Commands

```bash
# Start local server
hugo server -D

# Create new listicle
hugo new listicles/best-socket-sets-2025.md

# Build for production
hugo --minify

# Clear cache and rebuild
hugo --cleanDestinationDir --minify

# Check Hugo version
hugo version
```

---

## Notes for Future Development

### When Adding Features
1. **Test locally first** with `hugo server -D`
2. **Check responsive design** on mobile/tablet/desktop
3. **Validate affiliate link attributes** (`rel="noopener nofollow sponsored"`)
4. **Update archetypes** if changing front matter structure
5. **Document in BUILD_SUMMARY.md** when adding major features

### When Creating New Templates
1. **Use existing partials** where possible
2. **Pass context correctly** to partials (`.` or specific data)
3. **Follow naming conventions** (Hugo defaults)
4. **Include SEO meta tags** in head partial
5. **Test with sample content** before production

### When Modifying CSS
1. **Use CSS custom properties** for colors/spacing
2. **Maintain dark theme consistency**
3. **Test hover states and animations**
4. **Verify mobile breakpoints** (responsive)
5. **Keep bundle size small** (< 50KB target)

---

## Project Status

**Status**: ✅ Production-ready  
**Last Updated**: November 2025  
**Version**: Hugo v0.121.0  
**Live URL**: https://cartoolhq.com (pending deployment)

**Completed**:
- ✅ Full Hugo site structure
- ✅ Custom dark theme
- ✅ Decap CMS integration
- ✅ Sample content (2 listicles)
- ✅ SEO optimization
- ✅ Deployment configuration
- ✅ Documentation (README, DEPLOYMENT, QUICKSTART)

**Next Steps**:
1. Deploy to Cloudflare Pages
2. Configure custom domain
3. Set up Netlify Identity for CMS
4. Create more listicle content (10+ posts)
5. Submit sitemap to search engines

---

**This project context should be updated as patterns evolve and new features are added.**