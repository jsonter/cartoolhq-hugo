# Hero Image Setup Instructions

## The Problem
The hero-bg.jpg file is currently a placeholder. You need to copy your actual image file.

## Solution: Copy Your Hero Image

### Step 1: Save the image you provided
Save the automotive tools image (the one with the car and socket wrenches) to your computer.

### Step 2: Copy to the correct location
Copy that image file to:
```
prototype/images/hero-bg.jpg
```

**Important**: Make sure it's named exactly `hero-bg.jpg` (lowercase, with .jpg extension)

### Step 3: Refresh your browser
Open `prototype/index.html` in your browser and do a hard refresh:
- **Mac**: Cmd + Shift + R
- **Windows**: Ctrl + Shift + R

---

## Alternative: Use Absolute Path (Testing)

If the relative path isn't working, temporarily update `styles.css` line for `.hero-background`:

**Change from:**
```css
background-image: url('images/hero-bg.jpg');
```

**To (use full path on your machine):**
```css
background-image: url('file:///FULL/PATH/TO/prototype/images/hero-bg.jpg');
```

Replace `FULL/PATH/TO` with your actual file system path.

---

## Verify It's Working

You should see:
- Dark moody automotive tools in foreground
- Car blurred in background
- Blue/gray tones
- Text clearly visible over the image

If you see a plain dark gradient instead, the image isn't loading.

## File Size Check
Your hero image should be:
- **Format**: .jpg or .jpeg
- **Size**: Under 500KB (ideally under 200KB for web)
- **Dimensions**: At least 1920×1000px recommended
