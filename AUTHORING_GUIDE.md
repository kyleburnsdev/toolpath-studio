# Hugo Blog Authoring Guide

This guide explains how to create and author blog posts for the Level Up Lab blog using Hugo.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Creating a New Blog Post](#creating-a-new-blog-post)
3. [Front Matter Configuration](#front-matter-configuration)
4. [Writing Content](#writing-content)
5. [Working with Images](#working-with-images)
6. [Preview Your Post](#preview-your-post)
7. [Managing Drafts](#managing-drafts)
8. [Best Practices](#best-practices)

## Prerequisites

Before you begin authoring content, ensure you have:

1. **Hugo installed**: Download from [gohugo.io](https://gohugo.io/installation/)
2. **Git installed**: For version control
3. **A text editor**: VS Code, Sublime Text, or any markdown editor
4. **Basic markdown knowledge**: See [Markdown Guide](https://www.markdownguide.org/)

### Installing Hugo

**macOS:**
```bash
brew install hugo
```

**Windows (using Chocolatey):**
```bash
choco install hugo-extended
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt install hugo
```

**Verify installation:**
```bash
hugo version
```

## Creating a New Blog Post

### Method 1: Using Hugo Command (Recommended)

Hugo provides a command to create new posts with the correct structure and front matter:

```bash
# Navigate to the repository root
cd /path/to/maker-learn-and-share

# Create a new blog post
hugo new content/blog/posts/my-awesome-project.md
```

This command:
- Creates a new markdown file with the proper front matter
- Uses the blog archetype template
- Sets the creation date automatically
- Marks the post as a draft by default

### Method 2: Manual Creation

If you prefer to create posts manually:

1. Navigate to `content/blog/posts/`
2. Create a new markdown file with a descriptive name (use hyphens, not spaces)
3. Add the front matter (see below)

**File naming convention:**
- Use lowercase
- Use hyphens instead of spaces
- Be descriptive: `building-arduino-robot.md` not `post1.md`
- Avoid special characters

### Using Page Bundles (Recommended for posts with images)

Page bundles allow you to keep images and content together:

```bash
# Create a page bundle
mkdir content/blog/posts/my-awesome-project
touch content/blog/posts/my-awesome-project/index.md

# Add images to the same directory
# content/blog/posts/my-awesome-project/
#   ├── index.md
#   ├── cover-image.jpg
#   ├── diagram-1.png
#   └── photo-2.jpg
```

## Front Matter Configuration

Front matter is metadata at the top of your markdown file, enclosed in `---` markers. Hugo uses this to configure how your post is displayed and organized.

### Required Fields

```yaml
---
title: "Building My First Arduino Robot"
date: 2024-01-15T10:00:00-05:00
draft: true
---
```

### Recommended Fields

```yaml
---
title: "Building My First Arduino Robot"
date: 2024-01-15T10:00:00-05:00
draft: true
description: "A step-by-step guide to building an obstacle-avoiding robot with Arduino and ultrasonic sensors"
categories: ["Tutorial", "Projects"]
tags: ["arduino", "robotics", "electronics", "maker"]
author: "Kyle Burns"
featured_image: "cover-image.jpg"
---
```

### Field Descriptions

- **title**: The post title (displayed as H1)
- **date**: Publication date in ISO 8601 format
- **draft**: Set to `true` for drafts, `false` to publish
- **description**: SEO meta description (150-160 characters)
- **categories**: High-level content types (Tutorial, Project, Review, Reflection, Update)
- **tags**: Specific topics and keywords
- **author**: Author name
- **featured_image**: Main image for the post (filename or path)

### Optional Fields

```yaml
slug: "custom-url-slug"  # Override the URL slug
aliases: ["/old-url/"]    # Redirect from old URLs
series: ["Arduino Basics"] # Part of a series
weight: 1                  # Order within a section
toc: true                  # Show table of contents
```

## Writing Content

### Markdown Basics

Hugo uses standard markdown with some extensions:

```markdown
## Heading 2
### Heading 3

**Bold text**
*Italic text*

- Unordered list item
- Another item

1. Ordered list item
2. Another item

[Link text](https://example.com)

![Image alt text](image.jpg)
```

### Code Blocks

Use fenced code blocks with syntax highlighting:

````markdown
```python
def hello_world():
    print("Hello, World!")
```
````

Supported languages include: python, javascript, bash, go, html, css, yaml, json, and many more.

### Inline Code

Use backticks for inline code: `arduino.digitalWrite(13, HIGH)`

### Callouts and Notes

Use blockquotes for important notes:

```markdown
> **Note:** Make sure to check the polarity before connecting the battery!
```

### Tables

```markdown
| Component      | Quantity | Price  |
|----------------|----------|--------|
| Arduino Uno    | 1        | $25.00 |
| Servo Motor    | 2        | $8.00  |
| Ultrasonic Sensor | 1     | $5.00  |
```

### Shortcodes

Hugo shortcodes allow you to embed dynamic content:

```markdown
{{< youtube VIDEO_ID >}}

{{< figure src="image.jpg" title="Image caption" >}}
```

## Working with Images

### Image Organization

**Option 1: Page Bundles (Recommended)**

Store images alongside the post content:

```
content/blog/posts/my-project/
  ├── index.md
  ├── cover.jpg
  ├── step-1.jpg
  └── step-2.jpg
```

Reference images in markdown:
```markdown
![Step 1](step-1.jpg)
```

**Option 2: Shared Images Directory**

Store images in `content/blog/images/`:

```markdown
![My Image](../images/my-image.jpg)
```

**Option 3: Static Directory**

Store images in `static/images/blog/`:

```markdown
![My Image](/images/blog/my-image.jpg)
```

### Image Best Practices

1. **Optimize images** before adding them:
   - Use JPEG for photos (compress to 85% quality)
   - Use PNG for screenshots and diagrams
   - Use WebP for better compression (when possible)
   - Resize images to reasonable dimensions (max 2000px wide)

2. **Use descriptive filenames**: `arduino-circuit-diagram.jpg` not `img001.jpg`

3. **Always include alt text** for accessibility:
   ```markdown
   ![Arduino connected to breadboard with LED circuit](circuit-setup.jpg)
   ```

4. **Add captions** when helpful:
   ```markdown
   {{< figure src="robot.jpg" title="The completed robot with ultrasonic sensor mounted" >}}
   ```

### Featured Images

Set a featured image in the front matter:

```yaml
featured_image: "cover-image.jpg"
```

This image will be used as:
- The main image for the post
- Social media preview image
- Blog listing thumbnail

## Preview Your Post

### Start the Hugo Development Server

```bash
# Navigate to the repository root
cd /path/to/maker-learn-and-share

# Start the server (includes drafts)
hugo server -D

# Or with specific options
hugo server --buildDrafts --buildFuture --bind 0.0.0.0
```

Options:
- `-D` or `--buildDrafts`: Include draft posts
- `--buildFuture`: Include posts with future dates
- `--bind 0.0.0.0`: Allow access from other devices on your network

### Access Your Site

Open your browser and navigate to:
```
http://localhost:1313
```

Hugo automatically reloads when you save changes to your content!

### Preview Specific Post

Navigate to:
```
http://localhost:1313/blog/YYYY/MM/your-post-slug/
```

## Managing Drafts

### Working with Drafts

All new posts start as drafts (`draft: true` in front matter).

**View drafts locally:**
```bash
hugo server -D
```

**Drafts are NOT included in production builds** unless you explicitly include them.

### Publishing a Post

When ready to publish, change the draft status:

```yaml
---
title: "My Awesome Post"
date: 2024-01-15T10:00:00-05:00
draft: false  # Changed from true to false
---
```

Or remove the draft line entirely (defaults to published).

### Post Scheduling

Schedule a post for future publication by setting a future date:

```yaml
---
title: "My Future Post"
date: 2024-12-25T09:00:00-05:00
draft: false
---
```

The post won't appear in production builds until the date arrives (unless you use `--buildFuture`).

## Best Practices

### Content Writing

1. **Write for your audience**: Use clear, accessible language
2. **Break up long sections**: Use headings, lists, and short paragraphs
3. **Include practical examples**: Code snippets, photos, diagrams
4. **Add context**: Explain why, not just how
5. **Link to related content**: Other posts, videos, podcasts
6. **Proofread**: Check spelling, grammar, and formatting

### SEO Optimization

1. **Write descriptive titles**: Include main keywords, keep under 60 characters
2. **Craft meta descriptions**: Summarize the post in 150-160 characters
3. **Use headings properly**: H2 for main sections, H3 for subsections
4. **Choose relevant tags**: 3-7 specific tags per post
5. **Add alt text to images**: Helps with accessibility and SEO
6. **Internal linking**: Link to related posts on your site

### Accessibility

1. **Use semantic HTML**: Proper heading hierarchy (H1 → H2 → H3)
2. **Add alt text**: Describe images for screen readers
3. **Use descriptive link text**: "Read the tutorial" not "click here"
4. **Ensure sufficient contrast**: For any custom styling
5. **Test with keyboard navigation**: Tab through your content

### Version Control

1. **Commit frequently**: After completing sections
2. **Write meaningful commit messages**: "Add Arduino robot tutorial" not "update"
3. **Use branches**: For major edits or experiments
4. **Keep drafts in version control**: Track your progress

### File Organization

1. **One post per file**: Don't combine multiple posts
2. **Use page bundles**: For posts with multiple images
3. **Organize by topic**: Use categories and tags consistently
4. **Archive old drafts**: Move abandoned drafts to an archive folder

### Cross-Platform Integration

Remember to integrate your blog with other Level Up Lab content:

1. **Link to YouTube videos**: Embed or link to related video content
2. **Reference podcast episodes**: Add links to podcast discussions
3. **Promote on social media**: Share blog posts on Facebook, Discord
4. **Enable comments**: Foster community engagement
5. **Create content series**: Link related tutorials and projects

### Templates and Consistency

Use the blog archetype to maintain consistency:

```bash
hugo new content/blog/posts/new-post.md
```

This ensures:
- Consistent front matter structure
- Standard content sections
- Proper formatting from the start

## Quick Reference

### Common Commands

```bash
# Create new post
hugo new content/blog/posts/my-post.md

# Start development server
hugo server -D

# Build site
hugo

# Build with drafts
hugo -D

# Check for broken links
hugo check
```

### Front Matter Template

```yaml
---
title: ""
date: {{ .Date }}
draft: true
description: ""
categories: []
tags: []
author: "Kyle Burns"
featured_image: ""
---
```

### Markdown Cheatsheet

| Element | Syntax |
|---------|--------|
| Heading | `## Heading 2` |
| Bold | `**bold**` |
| Italic | `*italic*` |
| Link | `[text](url)` |
| Image | `![alt](image.jpg)` |
| Code | `` `code` `` |
| Code Block | ` ```language ` |
| List | `- item` |
| Quote | `> quote` |
| Table | `\| col1 \| col2 \|` |

## Next Steps

Once you've authored your content, see the [PUBLISHING_GUIDE.md](PUBLISHING_GUIDE.md) for instructions on building and deploying your blog to GitHub Pages.

## Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Hugo Themes](https://themes.gohugo.io/)
- [Front Matter Documentation](https://gohugo.io/content-management/front-matter/)
- [Hugo Shortcodes](https://gohugo.io/content-management/shortcodes/)

## Need Help?

- Check the [Hugo Documentation](https://gohugo.io/documentation/)
- Visit the [Hugo Discourse Forum](https://discourse.gohugo.io/)
- Review existing blog posts in `content/blog/posts/` for examples
- Join the Level Up Lab Discord community for support
