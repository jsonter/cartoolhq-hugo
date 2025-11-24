# Spec Provenance

**Date**: 2025-11-18  
**Mode**: Plan  
**User Request**: Build an affiliate marketing blog about automotive accessories and car tools using Hugo, custom theme, Cloudflare Pages deployment, and Netlify CMS. Start with a single-page static prototype to validate design and layout.

**Key Decisions**:
- Start with static HTML/CSS prototype (fastest validation)
- Dark modern professional design direction
- Defer Hugo build, CMS integration, and deployment until prototype approved

---

# Spec Header

**Name**: CarToolHQ – Static Prototype

**Smallest Acceptable Scope**:
A single-page static HTML prototype that demonstrates:
- Hero section with CarToolHQ branding
- 3-5 listicle blog post preview cards (e.g., "Top 5 Jump Starters for Cold Weather", "Best 7 Torque Wrenches Under $100")
- Sample expanded listicle layout showing how a ranked product comparison looks (Top N format with product cards)
- Navigation header structure (logo + menu items, non-functional links OK)
- Footer with affiliate disclosure
- Fully responsive (mobile/tablet/desktop)
- Dark modern professional aesthetic applied

**Non-Goals** (deferred to later phases):
- Hugo static site generator setup
- Custom Hugo theme development
- Netlify CMS integration
- Cloudflare Pages deployment pipeline
- Multiple pages or blog post templates
- Working affiliate tracking links
- Search functionality
- Category/tag filtering

---

# Paths to Supplementary Guidelines

**Design System**:  
https://raw.githubusercontent.com/memextech/templates/refs/heads/main/design/dark-modern-professional.md

**Future Build Reference** (for Hugo + deployment phase):  
- None applicable yet (static site guidelines not in index; will use vanilla HTML/CSS)

---

# Decision Snapshot

| Decision | Chosen Path | Rationale |
|----------|-------------|-----------|
| **First version** | Single-page static prototype | Fastest feedback loop; validates design/layout before committing to Hugo build |
| **Design direction** | Dark modern professional | High-contrast works well for product photography; conveys trust for affiliate content |
| **Tech for prototype** | Plain HTML + CSS (no frameworks) | Zero build step; instant preview; easy handoff to Hugo theme later |
| **Product showcasing** | Card-based layout | Scannable, image-forward; standard pattern for affiliate/review sites |
| **Deployment** | Local file only (this phase) | No hosting needed until design approved |

**Deferred Decisions** (for next phase):
- Hugo theme structure (layouts, partials, archetypes)
- Cloudflare Pages vs. Netlify (user requested Cloudflare)
- Netlify CMS config and editorial workflow
- Affiliate link management strategy

---

# Architecture at a Glance

**Prototype Structure**:
```
prototype/
├── index.html          # Single-page prototype
├── styles.css          # Dark modern professional styles
├── images/             # Placeholder product images
│   ├── hero-bg.jpg
│   ├── product-1.jpg
│   ├── product-2.jpg
│   └── ...
└── README.md           # Notes on design decisions
```

**Page Sections**:
1. **Navigation Header**: "CarToolHQ" logo (left) + menu items (Home, Reviews, Categories, About) + search icon
2. **Hero Section**: Large headline ("Expert Comparisons for Car Enthusiasts"), subheading, CTA to latest listicles
3. **Featured Listicles Grid**: 3-5 blog post cards showing listicle titles, featured image, excerpt, "Read Comparison" CTA
4. **Sample Listicle Section**: Inline example of a "Top 5" post showing ranked product cards (#1-5) with images, pros/cons, affiliate buttons
5. **Footer**: Affiliate disclosure (Amazon Associates, etc.), copyright, social links

**Design Token Application**:
- Background: `#0a0a0a` (primary), `#141414` (cards)
- Text: `#ffffff` (headings), `#a3a3a3` (descriptions)
- Accent: `#3b82f6` (CTAs, links)
- Typography: Inter (body), Inter Bold (headings)
- Spacing: 24px grid system, responsive scaling

---

# Implementation Plan

## Phase 1: HTML Structure (30 mins)

**1.1 Create base HTML**
- Semantic HTML5 structure (`<header>`, `<main>`, `<section>`, `<footer>`)
- Navigation with logo placeholder + menu items
- Hero section with headline, subheading, CTA button
- Product grid container with 3-5 article cards
- Footer with disclosure text

**1.2 Content placeholders**
- Hero: "Expert Comparisons for Car Enthusiasts" + subheading "In-depth reviews and rankings of the best automotive tools and accessories"
- Listicle blog post examples:
  - "Top 5 Jump Starters for Diesel Engines (2025)"
  - "Best 7 Torque Wrenches Under $100"
  - "Top 6 Tire Pressure Gauges for Precise Readings"
  - "Best 8 Car Vacuum Cleaners for Detailing"
  - "Top 4 OBD-II Scanners for DIY Mechanics"
- Each listicle card: featured image, title, publish date, excerpt (1-2 sentences), "Read Comparison" button
- Sample expanded listicle: "Top 5 Jump Starters..." with ranked product cards (#1-5), each showing:
  - Rank badge, product image, name, key specs, pros/cons list, affiliate "Check Price" button

---

## Phase 2: CSS Styling (45 mins)

**2.1 Apply design system**
- CSS custom properties for color palette (backgrounds, text, accents)
- Inter font from Google Fonts
- Typography scale (H1 48px, H2 36px, body 16px)
- Spacing utilities (24px grid)

**2.2 Layout implementation**
- Flexbox navigation (space-between alignment, CarToolHQ logo left-aligned)
- Hero section: centered text, max-width 800px, vertical padding 120px
- Listicle preview grid: CSS Grid, 3 columns desktop → 2 tablet → 1 mobile
- Listicle card styling: secondary background, 8px border radius, hover lift effect
- Sample listicle section: single column, ranked product cards stacked vertically
- Ranked product cards: Flexbox layout, rank badge (gold #1, silver #2, bronze #3, accent blue #4-5), product image left, details right, pros/cons in two columns, affiliate button bottom-right

**2.3 Responsive behavior**
- Mobile-first approach
- Breakpoints: 768px (tablet), 1024px (desktop)
- Hamburger menu icon (visible <768px, non-functional in prototype)
- Typography scaling (reduce headings by 30% on mobile)
- Card padding reduction (24px → 16px → 12px)

---

## Phase 3: Polish & Interactivity (15 mins)

**3.1 Micro-interactions**
- Button hover states (color shift + subtle scale)
- Card hover effect (lift 4px, shadow increase)
- Smooth transitions (150-200ms ease-in-out)

**3.2 Placeholder images**
- Use https://placehold.co or similar for product images (800x600px)
- Add alt text for each image
- Hero background: subtle gradient overlay

**3.3 Documentation**
- README.md: design decisions, color codes, next steps for Hugo conversion

---

# Verification & Demo Script

**Visual Checks**:
1. Open `index.html` in browser
2. Verify dark background (`#0a0a0a`) loads correctly, CarToolHQ logo visible in header
3. Confirm Inter font rendering (check headings vs. body weight)
4. Check listicle preview cards display in grid (3 columns on desktop)
5. Scroll to sample listicle section → verify ranked product cards (#1-5) stack vertically with rank badges visible
6. Hover over "Read Comparison" buttons → color changes to `#2563eb`, slight scale increase
7. Hover over listicle preview cards → subtle lift animation
8. Check pros/cons list formatting (green checkmarks for pros, red X for cons)

**Responsive Tests**:
1. Resize browser to 375px width (mobile)
   - Listicle preview grid collapses to single column
   - Ranked product cards in sample listicle: image stacks above details (vertical layout)
   - Pros/cons list: single column instead of two
   - Headings scale down proportionally
   - Navigation condenses (hamburger icon visible)
2. Resize to 768px (tablet)
   - Listicle preview grid shows 2 columns
   - Ranked product cards: image left, details right (horizontal maintained)
   - Typography 20% smaller than desktop
3. Resize to 1200px (desktop)
   - Full 3-column listicle grid
   - Ranked product cards: full horizontal layout with two-column pros/cons
   - Navigation horizontal, all items visible

**Accessibility Spot-Check**:
- Tab through navigation and buttons (focus states visible with blue outline)
- Check color contrast (white text on `#0a0a0a` = 21:1 ratio, AAA compliant)
- Alt text present on all images

**Demo Flow**:
> "This is CarToolHQ—an affiliate blog focused on micro-niche comparisons of car tools and accessories. The hero section positions us as experts who do the comparison work for readers. Below, we have listicle blog post previews like 'Top 5 Jump Starters for Diesel Engines'—these are the main traffic drivers. Scroll down to see what an actual listicle looks like: a ranked list of products with clear winner (#1 gold badge), runner-ups, and detailed pros/cons for each. Every product has a prominent affiliate CTA. On mobile, everything reflows into a single column—ranked products stack vertically, making it easy to scroll through comparisons. The dark professional design reduces eye strain during research and makes product photos stand out."

---

# Deploy

**This Phase**: No deployment—prototype lives as local HTML file for approval.

**Next Phase** (after design approval):
1. Convert approved prototype to Hugo theme structure
2. Set up GitHub repo with Hugo site
3. Configure Cloudflare Pages:
   - Connect GitHub repo
   - Build command: `hugo --minify`
   - Output directory: `public/`
4. Integrate Netlify CMS:
   - Add `admin/` folder with `config.yml`
   - Configure editorial workflow
   - Set up GitHub OAuth for CMS login
5. Create content templates for product reviews, categories

**Estimated Next Phase Effort**: 3-4 hours (Hugo theme conversion + CMS setup + deployment config)

---

## Notes for Future Build

**Hugo Theme Considerations**:
- Use approved prototype CSS as theme stylesheet
- Create partials: `header.html`, `hero.html`, `listicle-card.html`, `ranked-product.html`, `footer.html`
- Set up archetypes for listicle posts (front matter: title, featured_image, publish_date, excerpt, products array with rank, name, image, specs, pros, cons, affiliate_link)
- Consider shortcode for ranked product cards to simplify content authoring

**Content Strategy**:
- Listicle template with structured data (Schema.org ItemList + Product markup for each ranked item)
- Micro-niche targeting examples: "best X for Y" (e.g., "torque wrenches for motorcycles", "jump starters for diesel trucks")
- Category pages (Hand Tools, Power Tools, Maintenance, Detailing, Electronics, Safety)
- Affiliate disclosure on every page (footer partial) + inline disclosure at top of listicles
- Consider "last updated" dates to signal freshness (important for "Best of 2025" style posts)

**Performance**:
- Lazy-load product images below fold
- Optimize images with Hugo's image processing
- Cloudflare CDN + minification handles static asset delivery
