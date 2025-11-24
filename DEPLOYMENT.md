# Deployment Guide - CarToolHQ

## Prerequisites

- [x] GitHub account
- [x] Cloudflare account
- [x] Hugo site built and tested locally
- [x] Hero background image added to `static/images/hero-bg.jpg`

---

## Step 1: Prepare for Deployment

### 1.1 Copy Hero Image

Replace the placeholder at `static/images/hero-bg.jpg` with your actual automotive tools hero image.

**Recommended specs:**
- Size: 1920×1000px
- Format: JPG (optimized)
- File size: < 200KB

### 1.2 Test Locally

```bash
hugo server -D

# Visit http://localhost:1313
# Verify:
# - Homepage loads correctly
# - Hero image displays
# - Listicle pages work
# - All styles applied
```

### 1.3 Build Static Site

```bash
hugo --minify

# This creates the /public/ folder with your built site
```

---

## Step 2: Create GitHub Repository

### 2.1 Initialize Git (if not already done)

```bash
git init
git add .
git commit -m "Initial CarToolHQ Hugo site"
```

### 2.2 Create GitHub Repo

**Option A: Using GitHub CLI**
```bash
gh repo create cartoolhq-hugo --public --source=. --remote=origin
git push -u origin main
```

**Option B: Via GitHub Website**
1. Go to https://github.com/new
2. Repository name: `cartoolhq-hugo`
3. Public repository
4. Don't initialize with README (we have one)
5. Create repository
6. Follow the "push an existing repository" instructions

```bash
git remote add origin https://github.com/YOUR_USERNAME/cartoolhq-hugo.git
git branch -M main
git push -u origin main
```

---

## Step 3: Deploy to Cloudflare Pages

### 3.1 Connect GitHub to Cloudflare

1. **Login to Cloudflare Dashboard**
   - Go to https://dash.cloudflare.com
   - Navigate to "Pages" in the left sidebar

2. **Create a New Project**
   - Click "Create a project"
   - Select "Connect to Git"
   - Choose "GitHub"
   - Authorize Cloudflare to access your GitHub account

3. **Select Repository**
   - Find `cartoolhq-hugo` in the list
   - Click "Begin setup"

### 3.2 Configure Build Settings

**Framework preset:** Hugo

**Build configuration:**
- Build command: `hugo --minify`
- Build output directory: `public`
- Root directory: `/` (leave empty)

**Environment variables** (click "Add variable"):

| Variable Name | Value |
|--------------|-------|
| `HUGO_VERSION` | `0.121.0` |
| `NODE_VERSION` | `18` |

### 3.3 Deploy

1. Click "Save and Deploy"
2. Wait 1-2 minutes for build to complete
3. Your site will be live at `https://cartoolhq-hugo.pages.dev`

---

## Step 4: Set Up Custom Domain (Optional)

### 4.1 Add Custom Domain

1. In Cloudflare Pages → Your Project → Custom domains
2. Click "Set up a custom domain"
3. Enter your domain (e.g., `cartoolhq.com`)

### 4.2 Configure DNS

Cloudflare will provide DNS instructions. Typically:

**For root domain (cartoolhq.com):**
- Type: CNAME
- Name: `@`
- Target: `cartoolhq-hugo.pages.dev`

**For www subdomain:**
- Type: CNAME
- Name: `www`
- Target: `cartoolhq-hugo.pages.dev`

### 4.3 SSL Certificate

- Cloudflare automatically provisions SSL
- Takes 5-10 minutes
- Your site will be accessible via HTTPS

---

## Step 5: Enable Decap CMS

Decap CMS needs Git Gateway for authentication. Even though you're hosting on Cloudflare, you'll use Netlify Identity for CMS auth (it's free and separate from hosting).

### 5.1 Create a Netlify Site (for Identity only)

1. Go to https://app.netlify.com
2. Create account (if you don't have one)
3. Click "Add new site" → "Deploy manually"
4. Drag any folder (we're just using this for Identity, not hosting)
5. Name it `cartoolhq-identity`

### 5.2 Enable Identity

1. In Netlify site → Settings → Identity
2. Click "Enable Identity"
3. Registration preferences: "Invite only"

### 5.3 Enable Git Gateway

1. Same Settings → Identity page
2. Scroll to "Services" → "Git Gateway"
3. Click "Enable Git Gateway"
4. Connect to GitHub (authorize Netlify)

### 5.4 Invite Yourself

1. Identity tab → "Invite users"
2. Enter your email address
3. Check your email and accept invitation
4. Set a password

### 5.5 Update Netlify Identity Script

In your Hugo site, update the Netlify Identity widget URL in `layouts/partials/head.html`:

The script is already included:
```html
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
```

This should work automatically, but if CMS login fails, you may need to add:
```html
<script>
  if (window.netlifyIdentity) {
    window.netlifyIdentity.on("init", user => {
      if (!user) {
        window.netlifyIdentity.on("login", () => {
          document.location.href = "/admin/";
        });
      }
    });
  }
</script>
```

### 5.6 Access the CMS

1. Go to `https://cartoolhq.com/admin/` (or your Cloudflare Pages URL)
2. Click "Login with Netlify Identity"
3. Enter the email/password you set up
4. You're in! Start creating content.

---

## Step 6: Post-Deployment Checklist

### SEO Setup

- [ ] Submit sitemap to Google Search Console
  - URL: `https://cartoolhq.com/sitemap.xml`
  - Go to https://search.google.com/search-console
  - Add property → Submit sitemap

- [ ] Set up Cloudflare Web Analytics (free)
  - Cloudflare Dashboard → Web Analytics
  - Add site
  - Copy tracking code (or enable automatic injection)

### Content

- [ ] Replace placeholder product images with real photos
- [ ] Update affiliate links with your Amazon Associates tracking IDs
- [ ] Create 5-10 more listicle posts for critical mass
- [ ] Add privacy policy page
- [ ] Add terms of service page

### Performance

- [ ] Test site speed: https://pagespeed.web.dev
- [ ] Test mobile responsiveness
- [ ] Check all links work
- [ ] Verify hero image loads quickly

### Amazon Associates

- [ ] Sign up for Amazon Associates program
- [ ] Get your tracking ID
- [ ] Update all affiliate links to include your ID
- [ ] Add proper FTC disclosures (already in footer + listicles)

---

## Troubleshooting

### Hugo Build Fails on Cloudflare

**Problem:** Build error about Hugo version

**Solution:** 
- Check Environment Variables include `HUGO_VERSION = 0.121.0`
- Cloudflare requires Hugo Extended for SCSS processing

### Hero Image Not Displaying

**Problem:** Background shows gradient fallback, no image

**Solution:**
- Verify image exists at `static/images/hero-bg.jpg`
- Check file size (should be < 2MB)
- Try hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

### Decap CMS Won't Load

**Problem:** `/admin/` shows blank page or errors

**Solution:**
1. Check browser console for errors (F12)
2. Verify `static/admin/config.yml` exists
3. Ensure Git Gateway is enabled in Netlify Identity
4. Clear browser cache

### CMS Says "Not Authorized"

**Problem:** Can't login to CMS

**Solution:**
- Check you accepted the identity invitation email
- Try "Forgot password" flow
- Verify Git Gateway is connected to correct GitHub account

### CSS Not Loading

**Problem:** Site appears unstyled

**Solution:**
- Check `assets/css/main.css` exists
- Verify Hugo Pipes in `layouts/partials/head.html`
- Try clearing Cloudflare cache: Dashboard → Caching → Purge Everything

---

## Continuous Deployment

Once set up, your workflow is:

### Via Decap CMS (Non-technical)
1. Go to `/admin/`
2. Create or edit content
3. Click "Publish"
4. Decap commits to GitHub
5. Cloudflare auto-deploys (1-2 min)

### Via Git (Technical)
1. Edit files locally
2. `git add .`
3. `git commit -m "Add new listicle"`
4. `git push origin main`
5. Cloudflare auto-deploys

---

## Support Resources

- **Hugo Docs**: https://gohugo.io/documentation/
- **Decap CMS Docs**: https://decapcms.org/docs/
- **Cloudflare Pages**: https://developers.cloudflare.com/pages/
- **CarToolHQ Issues**: https://github.com/YOUR_USERNAME/cartoolhq-hugo/issues

---

**Your site is now live! 🎉**

Next: Create amazing content and watch the affiliate revenue roll in.
