# Hero Background Image Setup

## Required Image
Place your hero background image in this folder as: **`hero-bg.jpg`**

## Image Specifications

### Recommended Sizes
- **Desktop**: 1920×1000px (primary)
- **Tablet**: 1200×800px (optional, for optimization)
- **Mobile**: 800×600px (optional, for optimization)

### File Format & Optimization
- **Format**: JPG or WebP
- **Quality**: 80-85% (balance quality vs. file size)
- **Target file size**: Under 200KB
- **Tools**: Use TinyPNG.com or Squoosh.app to compress

### Current Image Details
The provided automotive tools image is perfect:
- ✅ Dark/moody tones (matches site theme)
- ✅ Cool blue color palette (aligns with accent colors)
- ✅ Tools in focus with car blurred (depth of field)
- ✅ Horizontal composition (works across screen sizes)

## CSS Implementation

The hero section uses:
- **`background-size: cover`** - Automatically scales to fill container
- **`background-position: center`** - Keeps tools centered on desktop
- **`background-position: 60% center`** - Shifts focus on mobile (768px and below)
- **Subtle zoom animation** - 20s scale(1) to scale(1.05) for dynamic feel
- **Dark overlay** - 70-85% opacity gradient ensures text readability

## Responsive Behavior

| Device | Background Position | Notes |
|--------|---------------------|-------|
| Desktop (1024px+) | center center | Full image visible, tools prominent |
| Tablet (768-1023px) | center center | Maintained composition |
| Mobile (<768px) | 60% center | Shifts to focus on tools (left side) |

## Optional: Multiple Image Sizes (Future Enhancement)

For production, consider serving different sizes:

```html
<picture>
  <source media="(min-width: 1024px)" srcset="images/hero-bg-desktop.webp">
  <source media="(min-width: 768px)" srcset="images/hero-bg-tablet.webp">
  <img src="images/hero-bg-mobile.webp" alt="Automotive tools">
</picture>
```

Or use Hugo's image processing in the full build phase.

## Placeholder Products Images

Other images needed for listicle cards (800×600px):
- `product-1.jpg` through `product-5.jpg`

Currently using placehold.co placeholders - replace with actual product photos when available.
