# Hugo Blog Quick Start Guide

This repository is now set up with Hugo for creating a static blog website.

## Prerequisites

Install Hugo on your machine:

**macOS:**
```bash
brew install hugo
```

**Windows (Chocolatey):**
```bash
choco install hugo-extended
```

**Linux:**
```bash
sudo apt install hugo
```

Verify installation:
```bash
hugo version
```

## Quick Start

### 1. Install a Theme (Required)

Before you can preview your site, you need to install a theme:

```bash
# Example: Install PaperMod theme
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

# Update hugo.toml to use the theme
# Change: theme = ''
# To:     theme = 'PaperMod'
```

See `themes/README.md` for more theme options.

### 2. Create Your First Blog Post

```bash
hugo new content/blog/posts/my-first-post.md
```

Edit the file, add content, and set `draft: false` when ready.

### 3. Preview Locally

```bash
hugo server -D
```

Open http://localhost:1313 in your browser.

### 4. Publish

When you push to the `main` branch, GitHub Actions automatically builds and deploys your site to GitHub Pages.

Just commit and push:
```bash
git add .
git commit -m "Add new blog post"
git push origin main
```

Your site will be live at: `https://kyleburnsdev.github.io/maker-learn-and-share/`

## Complete Documentation

For detailed instructions, see:

- **[AUTHORING_GUIDE.md](AUTHORING_GUIDE.md)** - Complete guide to writing and authoring blog posts
- **[PUBLISHING_GUIDE.md](PUBLISHING_GUIDE.md)** - Complete guide to building and publishing your blog

## Directory Structure

```
maker-learn-and-share/
├── hugo.toml              # Hugo configuration
├── content/
│   └── blog/
│       ├── _index.md      # Blog section page
│       └── posts/         # Your blog posts go here
├── archetypes/            # Content templates
├── layouts/               # Custom templates (optional)
├── static/                # Static files (images, css, etc.)
├── assets/                # Assets for processing
├── themes/                # Hugo themes
└── .github/
    └── workflows/
        └── hugo.yml       # Automated deployment
```

## Key Files

- `hugo.toml` - Main configuration file
- `content/blog/posts/` - Where all blog posts are created
- `archetypes/blog.md` - Template for new blog posts
- `.github/workflows/hugo.yml` - GitHub Actions workflow for auto-deployment

## Common Commands

```bash
# Create a new blog post
hugo new content/blog/posts/my-post.md

# Start development server with drafts
hugo server -D

# Build the site
hugo

# Build with drafts
hugo -D

# Check for errors
hugo check
```

## Getting Help

- Read the [AUTHORING_GUIDE.md](AUTHORING_GUIDE.md) for writing help
- Read the [PUBLISHING_GUIDE.md](PUBLISHING_GUIDE.md) for deployment help
- Check [Hugo Documentation](https://gohugo.io/documentation/)
- Visit [Hugo Discourse](https://discourse.gohugo.io/)

## Next Steps

1. **Install a theme** (see `themes/README.md`)
2. **Create your first post** (`hugo new content/blog/posts/hello-world.md`)
3. **Customize** `hugo.toml` with your information
4. **Preview locally** with `hugo server -D`
5. **Push to GitHub** to deploy automatically

Happy blogging! 🚀
