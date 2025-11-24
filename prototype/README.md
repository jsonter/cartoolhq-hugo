# CarToolHQ - Static Prototype

## Overview
This is a single-page static HTML/CSS prototype for CarToolHQ, an affiliate marketing blog focused on automotive accessories and car tools. The site specializes in **listicle-style comparisons** targeting micro-niches (e.g., "Top 5 Jump Starters for Diesel Engines").

## Design System

### Color Palette
- **Backgrounds**: `#0a0a0a` (primary), `#141414` (secondary), `#1f1f1f` (tertiary)
- **Text**: `#ffffff` (primary), `#a3a3a3` (secondary), `#737373` (tertiary)
- **Accents**: `#3b82f6` (primary blue), `#8b5cf6` (secondary purple)
- **Status**: `#10b981` (success/affiliate), `#f59e0b` (warning), `#ef4444` (error)
- **Rank Badges**: Gold (#1), Silver (#2), Bronze (#3), Blue (#4-5)

### Typography
- **Font Family**: Inter (Google Fonts)
- **Headings**: 
  - H1: 48px / Bold
  - H2: 36px / SemiBold
  - H3: 24px / Medium
  - H4: 20px / Medium
- **Body**: 16px / Regular, 1.6 line-height

### Spacing System
- Grid: 24px base unit (responsive: 16px mobile)
- Card padding: 24px → 16px tablet → 12px mobile

## Key Features

### 1. Homepage Structure
- **Hero Section**: Value proposition + CTA to latest comparisons
- **Listicle Grid**: 3 columns (desktop) → 2 (tablet) → 1 (mobile)
- Each card shows: featured image, publish date, title, excerpt, CTA button

### 2. Sample Listicle Layout
Demonstrates a full "Top N" ranking post:
- **Ranked Product Cards**: #1-5 with colored rank badges
- **Product Details**: Image, name, key specs
- **Pros/Cons Lists**: Two-column layout (desktop), stacked (mobile)
- **Affiliate CTAs**: Green "Check Price on Amazon" buttons
- **Inline Disclosure**: Warning banner at top of post

### 3. Responsive Behavior
- **Desktop (1024px+)**: 3-column grid, horizontal product cards
- **Tablet (768-1023px)**: 2-column grid, maintained horizontal layout
- **Mobile (<768px)**: 
  - Single column grid
  - Product cards stack vertically (image above details)
  - Pros/cons in single column
  - Typography scales down 30%

### 4. Micro-Interactions
- **Button hovers**: Color shift + 2px lift + shadow
- **Card hovers**: 4px lift + border color change + image zoom
- **Smooth transitions**: 150-200ms ease-in-out

## File Structure
```
prototype/
├── index.html          # Single-page prototype
├── styles.css          # Dark modern professional theme
└── README.md           # This file
```

## Design Decisions

### Why Listicles?
- **SEO-friendly**: "Best X for Y" queries have high search volume
- **Affiliate-optimized**: Multiple product CTAs per post = more conversion opportunities
- **Scannable**: Ranked format makes quick comparisons easy
- **Shareable**: Definitive "Top N" lists perform well socially

### Why Rank Badges?
- **Visual hierarchy**: Gold/silver/bronze immediately communicate winners
- **Trust signals**: Appears editorial and unbiased
- **Mobile-friendly**: Color-coded badges work on small screens

### Why Dark Theme?
- **Reduced eye strain**: Better for research/comparison sessions
- **Product focus**: Makes images and CTAs pop against dark background
- **Professional tone**: Conveys technical competence for automotive tools

## Next Steps (Post-Approval)

### Phase 2: Hugo Conversion
1. Convert prototype to Hugo theme structure
2. Create partials: `header.html`, `listicle-card.html`, `ranked-product.html`, `footer.html`
3. Set up archetypes for listicle posts with structured front matter
4. Add shortcode for ranked product cards (easier content authoring)

### Phase 3: CMS Integration
1. Configure Netlify CMS with `admin/config.yml`
2. Set up editorial workflow (draft → review → publish)
3. Create collections for listicles, pages, site settings
4. Configure GitHub OAuth for CMS authentication

### Phase 4: Cloudflare Deployment
1. Create GitHub repo and push Hugo site
2. Connect Cloudflare Pages to repo
3. Configure build: `hugo --minify` → `public/`
4. Set up custom domain and SSL

## Content Strategy Notes

### Micro-Niche Targeting
Instead of broad topics, focus on ultra-specific queries:
- ✅ "Best torque wrenches for motorcycles"
- ✅ "Top jump starters for diesel trucks"
- ✅ "Car vacuums with HEPA filters"
- ❌ "Best car tools" (too broad, high competition)

### Schema Markup (Future)
Add structured data for SEO:
- `Schema.org/ItemList` for ranked lists
- `Schema.org/Product` for each item
- `aggregateRating` if adding user reviews

### Affiliate Compliance
- Disclosure at top of every listicle (done)
- Footer disclosure on every page (done)
- Consider "as an Amazon Associate..." language
- Include last updated dates for freshness

## Testing Checklist

- [x] Visual check: dark background loads correctly
- [x] Typography: Inter font rendering properly
- [x] Grid layout: 3 columns on desktop
- [x] Rank badges: gold/silver/bronze visible
- [x] Hover states: buttons and cards respond
- [x] Responsive: single column on mobile (<768px)
- [x] Mobile product cards: vertical stack
- [x] Pros/cons: green checkmarks and red X icons
- [x] Footer disclosure: visible and readable

## Browser Support
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile Safari (iOS 13+)
- Chrome Mobile (Android)

## Performance Notes
- Static HTML/CSS = instant load
- Google Fonts preconnect for faster typography
- Placeholder images via placehold.co (replace with optimized product photos)
- No JavaScript required for core functionality

---

**Design System Reference**: https://raw.githubusercontent.com/memextech/templates/refs/heads/main/design/dark-modern-professional.md
