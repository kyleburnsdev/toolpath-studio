# Blog Content

This folder contains written content for blog posts and articles, structured for Hugo static site generator.

## Quick Start

**Create a new blog post:**
```bash
hugo new content/blog/posts/my-new-post.md
```

**Preview your blog locally:**
```bash
hugo server -D
```

**For detailed instructions, see:**
- [AUTHORING_GUIDE.md](../../AUTHORING_GUIDE.md) - How to write and author blog posts
- [PUBLISHING_GUIDE.md](../../PUBLISHING_GUIDE.md) - How to build and publish to GitHub Pages

## Content Types

- **Project Documentation**: Written guides for completed projects
- **Tutorials**: Step-by-step written instructions
- **Reflections**: Personal insights and lessons learned
- **Tool Guides**: Written reviews and how-to guides
- **Updates**: Project progress and announcements

## Directory Structure

```
content/blog/
├── _index.md           # Blog section landing page
├── posts/              # All blog posts go here
│   ├── my-post.md      # Simple post (markdown file)
│   └── my-project/     # Page bundle (post with images)
│       ├── index.md    # Post content
│       ├── cover.jpg   # Images stored with post
│       └── diagram.png
├── images/             # Shared images (optional)
├── drafts/             # Legacy drafts folder (for reference)
└── published/          # Legacy published folder (for reference)
```

## Hugo Conventions

### Blog Posts

Blog posts should be created in `content/blog/posts/` and include front matter:

```yaml
---
title: "My Awesome Post"
date: 2024-01-15T10:00:00-05:00
draft: true
description: "A brief description for SEO"
categories: ["Tutorial"]
tags: ["hugo", "web-development"]
author: "Kyle Burns"
featured_image: "cover.jpg"
---
```

### Drafts vs Published

- Posts with `draft: true` are only visible when running `hugo server -D`
- Posts with `draft: false` (or no draft field) are included in production builds
- Use `hugo server -D` during development to preview drafts

### Page Bundles (Recommended for posts with images)

Create a directory for posts with multiple images:

```
content/blog/posts/my-project/
├── index.md        # Your post content
├── cover.jpg       # Featured image
└── photo-1.jpg     # Additional images
```

Reference images in your markdown:
```markdown
![My Image](cover.jpg)
```

## Best Practices

### Writing
- Write in an accessible, conversational style
- Use proper heading hierarchy (H2, H3, etc.)
- Include clear images and diagrams
- Add alt text to all images for accessibility
- Link to related YouTube videos and podcast episodes

### SEO
- Write descriptive titles (under 60 characters)
- Add meta descriptions (150-160 characters)
- Use relevant tags and categories
- Optimize images (compress and resize)
- Use descriptive image filenames

### Organization
- Use descriptive filenames with hyphens: `building-arduino-robot.md`
- Keep related content together using page bundles
- Use consistent categories and tags
- Add featured images to posts
- Cross-reference related posts

## Workflows

### Creating a New Post

1. Create the post:
   ```bash
   hugo new content/blog/posts/my-post.md
   ```

2. Edit the front matter and add content

3. Preview locally:
   ```bash
   hugo server -D
   ```

4. When ready, set `draft: false`

5. Commit and push to publish (if using GitHub Actions)

### Working with Images

**Option 1: Page Bundle (Recommended)**
```bash
mkdir content/blog/posts/my-project
hugo new content/blog/posts/my-project/index.md
# Add images to the my-project/ directory
```

**Option 2: Shared Images**
Place images in `content/blog/images/` and reference as:
```markdown
![Image](../images/my-image.jpg)
```

**Option 3: Static Images**
Place in `static/images/blog/` and reference as:
```markdown
![Image](/images/blog/my-image.jpg)
```

## Migration Notes

The previous `drafts/` and `published/` directories are kept for reference, but new content should follow Hugo conventions:

- **Old way**: Separate drafts and published folders
- **New way**: All posts in `posts/`, draft status in front matter

Legacy content can be migrated by:
1. Moving files to `content/blog/posts/`
2. Adding proper Hugo front matter
3. Setting appropriate draft status

## Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [Markdown Guide](https://www.markdownguide.org/)
- [AUTHORING_GUIDE.md](../../AUTHORING_GUIDE.md)
- [PUBLISHING_GUIDE.md](../../PUBLISHING_GUIDE.md)

## Need Help?

Refer to the comprehensive guides:
- **[AUTHORING_GUIDE.md](../../AUTHORING_GUIDE.md)** - Complete authoring instructions
- **[PUBLISHING_GUIDE.md](../../PUBLISHING_GUIDE.md)** - Deployment and publishing instructions
