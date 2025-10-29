# Hugo Blog Structure Overview

This document provides a visual overview of the Hugo blog setup for Toolpath Studio.

## Directory Structure

```
maker-learn-and-share/
│
├── hugo.toml                      # Main Hugo configuration
│
├── content/                       # All content goes here
│   └── blog/
│       ├── _index.md              # Blog section landing page
│       ├── posts/                 # ✨ CREATE BLOG POSTS HERE ✨
│       │   ├── my-post.md         # Single file post
│       │   └── my-project/        # Page bundle (post + images)
│       │       ├── index.md       # Post content
│       │       ├── cover.jpg      # Post images
│       │       └── photo.png
│       ├── images/                # Shared images (optional)
│       ├── drafts/                # Legacy (for reference)
│       └── published/             # Legacy (for reference)
│
├── archetypes/                    # Content templates
│   ├── blog.md                    # Blog post template
│   └── default.md                 # Default template
│
├── layouts/                       # Custom templates (optional)
│   └── README.md                  # Instructions for layouts
│
├── static/                        # Static files (served as-is)
│   └── README.md                  # favicon, robots.txt, CNAME, etc.
│
├── assets/                        # Assets for processing
│   └── README.md                  # SCSS, JS, images to process
│
├── themes/                        # Hugo themes
│   └── README.md                  # ⚠️ INSTALL A THEME FIRST
│
├── .github/
│   └── workflows/
│       └── hugo.yml               # 🚀 Auto-deploy to GitHub Pages
│
├── AUTHORING_GUIDE.md             # 📖 Complete authoring guide
├── PUBLISHING_GUIDE.md            # 📖 Complete publishing guide
└── HUGO_QUICKSTART.md             # 🚀 Quick start reference
```

## Content Creation Workflow

```
┌─────────────────────────────────────────────────────────────┐
│  1. Create New Post                                         │
│     hugo new content/blog/posts/my-post.md                  │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│  2. Edit Content                                            │
│     - Add front matter (title, date, tags, etc.)           │
│     - Write markdown content                                │
│     - Add images if needed                                  │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│  3. Preview Locally                                         │
│     hugo server -D                                          │
│     Open http://localhost:1313                              │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│  4. Set draft: false (when ready to publish)                │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│  5. Commit and Push                                         │
│     git add .                                               │
│     git commit -m "Add new blog post"                       │
│     git push origin main                                    │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│  6. GitHub Actions Automatically:                           │
│     - Checks out code                                       │
│     - Installs Hugo                                         │
│     - Builds site (hugo --minify)                          │
│     - Deploys to GitHub Pages                               │
└─────────────────┬───────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│  7. Site Live! 🎉                                           │
│     https://kyleburnsdev.github.io/toolpath-studio/   │
└─────────────────────────────────────────────────────────────┘
```

## Blog Post Structure

### Simple Post (Single File)

```
content/blog/posts/my-post.md
```

Content:
```yaml
---
title: "My Awesome Post"
date: 2024-01-15T10:00:00-05:00
draft: false
description: "A brief description"
categories: ["Tutorial"]
tags: ["hugo", "blogging"]
author: "Kyle Burns"
---

## Introduction
Your content here...
```

### Page Bundle (Post with Images)

```
content/blog/posts/my-project/
├── index.md       # Post content
├── cover.jpg      # Featured image
├── step1.png      # Additional images
└── step2.png
```

Content (index.md):
```yaml
---
title: "My Project"
date: 2024-01-15T10:00:00-05:00
draft: false
description: "A project tutorial"
categories: ["Projects"]
tags: ["arduino", "electronics"]
author: "Kyle Burns"
featured_image: "cover.jpg"
---

## Step 1
![Step 1](step1.png)

## Step 2
![Step 2](step2.png)
```

## Hugo Commands Quick Reference

| Command | Description |
|---------|-------------|
| `hugo new content/blog/posts/my-post.md` | Create new blog post |
| `hugo server -D` | Start dev server with drafts |
| `hugo server` | Start dev server (published only) |
| `hugo` | Build site to `public/` |
| `hugo -D` | Build site including drafts |
| `hugo check` | Check for errors |
| `hugo list all` | List all content |
| `hugo list drafts` | List draft posts |

## Front Matter Fields

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| title | Yes | Post title | "Building a Robot" |
| date | Yes | Publication date | 2024-01-15T10:00:00-05:00 |
| draft | Recommended | Draft status | true/false |
| description | Recommended | SEO meta description | "Learn to build..." |
| categories | Recommended | Content categories | ["Tutorial", "Projects"] |
| tags | Recommended | Topic tags | ["arduino", "robot"] |
| author | Optional | Author name | "Kyle Burns" |
| featured_image | Optional | Main image | "cover.jpg" |

## Configuration Overview

`hugo.toml` contains:

- **baseURL**: Your site's URL
- **title**: Site title
- **theme**: Theme name (install theme first!)
- **permalinks**: URL structure for posts
- **taxonomies**: Categories and tags
- **params**: Custom parameters (author, social links, etc.)
- **menu**: Site navigation
- **markup**: Markdown settings

## Deployment Methods

### Automatic (Recommended) ✅

**GitHub Actions** (already configured):
- Push to `main` branch
- GitHub Actions builds and deploys
- Site live in ~1-2 minutes

### Manual

**Build and deploy manually:**
```bash
hugo                    # Build site
cd public
git init
git add .
git commit -m "Publish"
git push -f origin gh-pages
```

## File Organization Best Practices

### ✅ DO:
- Use page bundles for posts with multiple images
- Name files with hyphens: `my-awesome-post.md`
- Keep images with their posts (page bundles)
- Use descriptive filenames
- Set `draft: false` when ready to publish
- Use categories and tags consistently

### ❌ DON'T:
- Use spaces in filenames
- Store large videos in the repo (link externally)
- Commit the `public/` directory (it's in .gitignore)
- Edit theme files directly (override in `layouts/`)
- Forget to set featured images

## Theme Selection

You **must** install a theme before the site will render properly.

**Recommended themes:**

1. **PaperMod** - Clean, fast, modern
   ```bash
   git submodule add --depth=1 --branch master https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
   ```

2. **Blowfish** - Highly customizable
   ```bash
   git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
   ```

3. **Stack** - Card-based, image-focused
   ```bash
   git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
   ```

After installing, update `hugo.toml`:
```toml
theme = 'PaperMod'  # or your chosen theme
```

See `themes/README.md` for more options.

## GitHub Pages Setup

### Configuration

1. Go to repository Settings → Pages
2. Source: "GitHub Actions"
3. Save

### Site URL

Your blog will be available at:
```
https://kyleburnsdev.github.io/maker-learn-and-share/
```

### Custom Domain (Optional)

To use a custom domain:
1. Add CNAME record in DNS
2. Create `static/CNAME` file
3. Update `baseURL` in `hugo.toml`

See PUBLISHING_GUIDE.md for details.

## Troubleshooting

### Site shows 404
- Check `baseURL` in `hugo.toml`
- Ensure posts have `draft: false`
- Verify GitHub Pages is enabled

### Images not loading
- Use correct paths: `![Image](image.jpg)` for page bundles
- Check file extensions (case-sensitive)
- Verify images are committed

### Styles not loading
- Install a theme!
- Check theme is specified in `hugo.toml`
- Verify theme files exist

### Changes not appearing
- Clear browser cache (Ctrl+Shift+R)
- Check GitHub Actions completed successfully
- Verify post is not a draft

## Key Documents

| Document | Purpose | When to Use |
|----------|---------|-------------|
| HUGO_QUICKSTART.md | Quick start guide | First time setup |
| AUTHORING_GUIDE.md | Complete authoring guide | Writing blog posts |
| PUBLISHING_GUIDE.md | Deployment guide | Publishing to web |
| themes/README.md | Theme installation | Choosing a theme |
| layouts/README.md | Custom layouts | Customizing design |

## Support Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [Hugo Themes Gallery](https://themes.gohugo.io/)
- [Markdown Guide](https://www.markdownguide.org/)
- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [Hugo Discourse Forum](https://discourse.gohugo.io/)

---

## Quick Start Checklist

- [ ] Install Hugo locally (`brew install hugo` or similar)
- [ ] Install a theme (see `themes/README.md`)
- [ ] Update `hugo.toml` with your info
- [ ] Create first post: `hugo new content/blog/posts/hello-world.md`
- [ ] Preview locally: `hugo server -D`
- [ ] Set `draft: false` when ready
- [ ] Push to GitHub (auto-deploys!)
- [ ] Verify site at GitHub Pages URL

**You're all set! Start creating content! 🚀**
