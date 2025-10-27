# Static Directory

This directory contains static files that are served as-is without processing by Hugo.

## Purpose

Files in this directory are copied directly to the `public/` folder during the build process and are served from the root of your site.

## Usage

Common use cases:
- Favicon files (`favicon.ico`, `favicon.png`)
- Robots.txt
- Images that don't belong to specific posts
- PDFs and downloadable files
- Custom CSS/JS files
- CNAME file for custom domains

## Directory Structure

Organize static files logically:

```
static/
├── images/
│   ├── logo.png
│   ├── avatar.jpg
│   └── blog/
│       └── shared-image.jpg
├── css/
│   └── custom.css
├── js/
│   └── custom.js
├── fonts/
│   └── custom-font.woff2
├── downloads/
│   └── guide.pdf
├── favicon.ico
├── robots.txt
└── CNAME               # For custom domain
```

## Referencing Static Files

In your content, reference static files from the root:

```markdown
![Logo](/images/logo.png)
[Download Guide](/downloads/guide.pdf)
```

## Custom Domain (CNAME)

If using a custom domain, create `static/CNAME`:

```
blog.yourdomain.com
```

## Robots.txt

Create `static/robots.txt` to control search engine crawling:

```
User-agent: *
Allow: /

Sitemap: https://yourdomain.com/sitemap.xml
```

## Note

For images specific to a blog post, prefer using page bundles instead of this directory. See the AUTHORING_GUIDE.md for details.
