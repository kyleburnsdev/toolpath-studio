# Hugo Blog Publishing Guide

This guide explains how to build and publish your Hugo blog to GitHub Pages so that your content is available as a static website.

## Table of Contents

1. [Overview](#overview)
2. [Publishing Workflow](#publishing-workflow)
3. [Local Build and Testing](#local-build-and-testing)
4. [GitHub Pages Setup](#github-pages-setup)
5. [Manual Publishing](#manual-publishing)
6. [Automated Publishing with GitHub Actions](#automated-publishing-with-github-actions)
7. [Custom Domain Configuration](#custom-domain-configuration)
8. [Troubleshooting](#troubleshooting)

## Overview

### What is GitHub Pages?

GitHub Pages is a static site hosting service that takes files directly from a GitHub repository and publishes them as a website. It's free, fast, and perfect for Hugo-generated static sites.

### Publishing Methods

There are three ways to publish your blog:

1. **Manual Build & Push**: Build locally and push to `gh-pages` branch
2. **GitHub Actions (Recommended)**: Automatic builds on every push
3. **Hybrid**: Local builds for testing, automated for production

## Publishing Workflow

The typical workflow looks like this:

```
Write Content → Preview Locally → Commit Changes → Push to GitHub → Auto-Deploy → Live Site
```

### Workflow Steps

1. **Author content** following the [AUTHORING_GUIDE.md](AUTHORING_GUIDE.md)
2. **Preview locally** using `hugo server -D`
3. **Set draft: false** when ready to publish
4. **Commit and push** to the main branch
5. **GitHub Actions builds** and deploys automatically
6. **Site goes live** at your GitHub Pages URL

## Local Build and Testing

### Build Your Site Locally

Before publishing, always build and test your site locally:

```bash
# Navigate to repository root
cd /path/to/maker-learn-and-share

# Clean previous builds (optional)
rm -rf public/

# Build the site (production mode, no drafts)
hugo

# Build with drafts for testing
hugo -D

# Build with future posts
hugo --buildFuture

# Build with specific base URL
hugo --baseURL "https://yourdomain.com"
```

The `hugo` command generates your static site in the `public/` directory.

### Test the Build Locally

After building, test the generated site:

```bash
# Navigate to the public directory
cd public

# Start a simple HTTP server
python3 -m http.server 8000

# Or use Hugo's built-in server with the generated files
hugo server --navigateToChanged
```

Then open `http://localhost:8000` in your browser.

### Pre-Publishing Checklist

Before publishing, verify:

- [ ] All posts have `draft: false` (or no draft field)
- [ ] Dates are correct and not in the future (unless intentional)
- [ ] Images load correctly
- [ ] Links work (internal and external)
- [ ] Code blocks render properly
- [ ] No broken shortcodes
- [ ] SEO meta descriptions are present
- [ ] Categories and tags are appropriate
- [ ] Featured images are set

### Check for Errors

```bash
# Check for broken links and other issues
hugo check

# Validate your content
hugo check ulimit
```

## GitHub Pages Setup

### Option 1: Deploy from Branch (Manual)

This method involves building locally and pushing the `public/` folder to a `gh-pages` branch.

#### Initial Setup

1. **Add public/ to .gitignore** (it should already be there)

2. **Initialize gh-pages branch:**

```bash
# Build your site
hugo

# Create gh-pages branch in public directory
cd public
git init
git checkout -b gh-pages
git add .
git commit -m "Initial publish"
git remote add origin https://github.com/kyleburnsdev/maker-learn-and-share.git
git push -f origin gh-pages
cd ..
```

3. **Configure GitHub Pages:**
   - Go to your repository on GitHub
   - Navigate to Settings → Pages
   - Under "Source", select "Deploy from a branch"
   - Select `gh-pages` branch and `/` (root) folder
   - Click "Save"

Your site will be available at: `https://kyleburnsdev.github.io/maker-learn-and-share/`

### Option 2: Deploy with GitHub Actions (Recommended)

This method automatically builds and deploys your site whenever you push to the main branch.

#### Step 1: Create GitHub Actions Workflow

Create `.github/workflows/hugo.yml`:

```yaml
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.121.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb

      - name: Install Dart Sass
        run: sudo snap install dart-sass

      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"

      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v3
```

#### Step 2: Configure GitHub Pages for Actions

1. Go to your repository on GitHub
2. Navigate to Settings → Pages
3. Under "Source", select "GitHub Actions"
4. Save the configuration

#### Step 3: Push the Workflow

```bash
git add .github/workflows/hugo.yml
git commit -m "Add GitHub Actions workflow for Hugo deployment"
git push origin main
```

#### Step 4: Monitor the Deployment

1. Go to the "Actions" tab in your repository
2. Watch the workflow run
3. Once complete, your site will be live!

## Manual Publishing

If you prefer manual control or need to publish without GitHub Actions:

### Publishing Script

Create a `publish.sh` script in your repository root:

```bash
#!/bin/bash

echo "Building Hugo site..."
hugo

echo "Navigating to public directory..."
cd public

echo "Committing changes..."
git add .
git commit -m "Publish site $(date '+%Y-%m-%d %H:%M:%S')"

echo "Pushing to gh-pages branch..."
git push origin gh-pages

echo "Done! Site published successfully."
cd ..
```

Make it executable:
```bash
chmod +x publish.sh
```

### Publishing Process

1. **Author and preview your content**
2. **Update draft status** to false
3. **Commit your changes** to main branch
4. **Run the publish script:**

```bash
./publish.sh
```

5. **Verify deployment** at your GitHub Pages URL

### Quick Publish Command

For a one-liner manual publish:

```bash
hugo && cd public && git add . && git commit -m "Publish $(date '+%Y-%m-%d')" && git push origin gh-pages && cd ..
```

## Automated Publishing with GitHub Actions

### How It Works

When you push to the main branch:

1. GitHub Actions detects the push
2. Spins up an Ubuntu runner
3. Installs Hugo
4. Checks out your repository
5. Builds the site with `hugo --minify`
6. Deploys to GitHub Pages
7. Your site is live in ~1-2 minutes

### Monitoring Deployments

**View Deployment Status:**
- Go to Actions tab in your repository
- Click on the latest workflow run
- View logs for each step

**Deployment History:**
- Settings → Pages shows deployment history
- Each deployment has a unique URL for rollback if needed

### Triggering Manual Deploys

You can trigger a deployment without pushing code:

1. Go to Actions tab
2. Select "Deploy Hugo site to Pages"
3. Click "Run workflow"
4. Select the branch and click "Run workflow"

## Custom Domain Configuration

### Adding a Custom Domain

If you want to use your own domain (e.g., `blog.yourdomain.com`):

#### Step 1: Configure DNS

Add a CNAME record in your DNS provider:

```
Type: CNAME
Name: blog (or @ for root domain)
Value: kyleburnsdev.github.io
```

For root domain (yourdomain.com), use A records:

```
Type: A
Name: @
Value: 185.199.108.153
Value: 185.199.109.153
Value: 185.199.110.153
Value: 185.199.111.153
```

#### Step 2: Configure GitHub Pages

1. Go to Settings → Pages
2. Enter your custom domain
3. Check "Enforce HTTPS" (after DNS propagates)
4. Save

#### Step 3: Update Hugo Configuration

Update `hugo.toml`:

```toml
baseURL = 'https://blog.yourdomain.com/'
```

#### Step 4: Create CNAME File

Create `static/CNAME` with your domain:

```
blog.yourdomain.com
```

This ensures the CNAME file persists after builds.

### Verifying Custom Domain

```bash
# Check DNS propagation
dig blog.yourdomain.com

# Verify HTTPS certificate (after propagation)
curl -I https://blog.yourdomain.com
```

## Troubleshooting

### Common Issues and Solutions

#### Issue: Site Builds but Shows 404

**Possible causes:**
- baseURL mismatch in `hugo.toml`
- GitHub Pages not configured correctly
- Content files have `draft: true`

**Solutions:**
```bash
# Check baseURL matches your GitHub Pages URL
# In hugo.toml:
baseURL = 'https://kyleburnsdev.github.io/maker-learn-and-share/'

# Ensure posts aren't drafts
grep -r "draft: true" content/

# Rebuild and redeploy
hugo && cd public && git push origin gh-pages
```

#### Issue: Images Not Loading

**Possible causes:**
- Incorrect image paths
- Images not in correct directory
- Case-sensitive filenames

**Solutions:**
- Use relative paths: `![Image](image.jpg)` for page bundles
- Use absolute paths from static: `![Image](/images/blog/image.jpg)`
- Check file extensions match (`.jpg` vs `.JPG`)
- Verify images are committed to repository

#### Issue: GitHub Actions Workflow Fails

**Common errors:**

1. **Hugo version incompatibility:**
   - Update `HUGO_VERSION` in workflow file
   - Check Hugo release notes for breaking changes

2. **Theme not found:**
   - Ensure theme is committed or added as submodule
   - Check `config.toml` theme name

3. **Permission denied:**
   - Verify Pages permissions in workflow
   - Check repository settings for Pages access

**Debug steps:**
```bash
# Test build locally first
hugo --minify

# Check workflow logs in Actions tab
# Look for specific error messages
```

#### Issue: Styles/CSS Not Loading

**Possible causes:**
- Missing theme
- Incorrect static file paths
- baseURL mismatch

**Solutions:**
- Install a Hugo theme
- Check browser console for 404 errors
- Verify static files are in correct locations

#### Issue: Changes Not Appearing

**Possible causes:**
- Browser cache
- Deployment hasn't completed
- Still marked as draft

**Solutions:**
```bash
# Hard refresh browser (Ctrl+Shift+R or Cmd+Shift+R)

# Check deployment status in Actions tab

# Verify post is published
grep "draft:" content/blog/posts/your-post.md

# Clear Hugo cache
hugo --gc
```

#### Issue: Build Takes Too Long

**Solutions:**
```bash
# Use faster build options for development
hugo server --disableFastRender=false

# Limit content during development
hugo server --buildDrafts --renderToDisk=false

# Clean up unused files
hugo --gc
```

### Debugging Tips

1. **Check Hugo version:**
   ```bash
   hugo version
   ```

2. **Verbose build output:**
   ```bash
   hugo --verbose
   ```

3. **Debug templating issues:**
   ```bash
   hugo --debug
   ```

4. **Validate configuration:**
   ```bash
   hugo config
   ```

5. **List all content:**
   ```bash
   hugo list all
   ```

6. **Check draft status:**
   ```bash
   hugo list drafts
   ```

## Publishing Checklist

Before each publish, verify:

### Content Review
- [ ] All posts have correct front matter
- [ ] Draft status set to false
- [ ] Publication dates are correct
- [ ] Images are optimized and loading
- [ ] Links are working
- [ ] Code blocks are formatted
- [ ] SEO descriptions present

### Build Verification
- [ ] Local build succeeds (`hugo`)
- [ ] No errors in build output
- [ ] Site previews correctly locally
- [ ] All pages accessible
- [ ] Navigation works

### Deployment
- [ ] Changes committed to main branch
- [ ] Changes pushed to GitHub
- [ ] GitHub Actions workflow succeeded
- [ ] Site is live at GitHub Pages URL
- [ ] Verify latest content appears

### Post-Publish
- [ ] Test on multiple devices/browsers
- [ ] Check social media previews
- [ ] Verify analytics tracking (if configured)
- [ ] Share on social platforms
- [ ] Monitor for any issues

## Performance Optimization

### Minification

Hugo can minify your HTML, CSS, and JavaScript:

```bash
hugo --minify
```

This is already included in the GitHub Actions workflow.

### Image Optimization

Before adding images:

```bash
# Install imagemagick
brew install imagemagick

# Optimize JPEGs
mogrify -quality 85 -resize '2000x2000>' *.jpg

# Convert to WebP
cwebp -q 85 image.jpg -o image.webp
```

### Caching

GitHub Pages automatically sets cache headers. For custom domains, configure caching in your CDN.

## Rollback Procedure

If you need to rollback to a previous version:

### Using GitHub Pages Deployments

1. Go to Settings → Pages
2. View deployment history
3. Select a previous deployment
4. Click "Restore"

### Manual Rollback

```bash
# Find the commit you want to rollback to
git log --oneline

# Revert to that commit
git revert <commit-hash>

# Push and let Actions redeploy
git push origin main
```

## Next Steps

Now that you know how to publish:

1. **Choose a Hugo theme** from [themes.gohugo.io](https://themes.gohugo.io/)
2. **Configure analytics** (Google Analytics, Plausible, etc.)
3. **Set up comments** (Disqus, Utterances, etc.)
4. **Configure RSS feeds** for subscribers
5. **Add search functionality** (Algolia, Lunr.js)
6. **Integrate with social media** for auto-posting

## Resources

- [Hugo Hosting & Deployment](https://gohugo.io/hosting-and-deployment/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Hugo Build Configuration](https://gohugo.io/getting-started/configuration/)
- [Hugo Performance Tips](https://gohugo.io/troubleshooting/build-performance/)

## Support

For publishing issues:

1. Check the [Hugo Documentation](https://gohugo.io/documentation/)
2. Visit [Hugo Discourse](https://discourse.gohugo.io/)
3. Review [GitHub Pages Status](https://www.githubstatus.com/)
4. Check workflow logs in Actions tab
5. Join the Toolpath Studio community for help

---

**Remember:** With GitHub Actions, publishing is automatic! Just write, commit, and push. Your content will be live in minutes.
