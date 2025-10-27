# Toolpath Studio Hugo Theme

A custom Hugo theme designed specifically for Toolpath Studio with WCAG 2.1 AA accessibility compliance, semantic HTML5 markup, and brand-consistent styling.

## Features

### Accessibility (WCAG 2.1 AA Compliant)
- **Semantic HTML5**: Proper use of `<header>`, `<main>`, `<nav>`, `<article>`, `<section>`, and `<footer>` elements
- **ARIA Landmarks**: Role attributes for screen readers (`role="banner"`, `role="main"`, `role="contentinfo"`)
- **Skip Navigation**: Keyboard-accessible skip link to main content
- **Focus Indicators**: Clear, high-contrast focus states for all interactive elements
- **Alt Text**: Image elements require descriptive alt text
- **Color Contrast**: All text meets WCAG AA contrast ratios (4.5:1 for normal text, 3:1 for large text)
- **Keyboard Navigation**: All interactive elements accessible via keyboard

### SEO Optimized
- Semantic HTML structure for better search engine understanding
- Proper heading hierarchy (H1-H6)
- Meta descriptions and OpenGraph tags
- Clean, descriptive URLs
- Responsive images with proper sizing

### Branding
Follows Toolpath Studio branding guidelines:
- **Primary Color**: Marine Blue (#0078BF)
- **Secondary Color**: Ash Gray (#9B9EA0)
- **Accent Color**: Burnt Orange (#D9772B)
- **Text Color**: Charcoal Black (#2C2C2C)
- **Background**: Soft Gray (#F5F5F5)
- **Typography**: 
  - Headings: Montserrat (Bold/Semi-Bold)
  - Body: Inter (Regular/Medium)
- **Logo**: Toolpath Studio branding integrated in header

### Responsive Design
- Mobile-first approach
- Breakpoints at 768px and 480px
- Flexible layouts that adapt to screen size
- Touch-friendly navigation on mobile devices

### Layout Components

#### Header
- Sticky header with Toolpath Studio logo
- Clean navigation menu
- Responsive collapse on mobile

#### Blog Post Listings
- Card-based layout with left accent border
- Post metadata (date, author, reading time)
- Category and tag badges
- Excerpt or description display
- Hover effects for interactivity

#### Single Post View
- Clear typography and spacing
- Category and tag display
- Reading time estimate
- Proper semantic article structure
- Code syntax highlighting support

#### Footer
- Copyright information
- Site description
- Social media links
- Semantic contentinfo role

## Installation

The theme is already included in the Toolpath Studio repository at `themes/toolpathstudio/`.

To use this theme, ensure your `hugo.toml` contains:

```toml
theme = 'toolpathstudio'
```

## Configuration

### Required Parameters

Add these to your `hugo.toml`:

```toml
[params]
  author = 'Kyle Burns'
  description = 'A multi-channel content platform for learning and sharing knowledge'
  
  [params.social]
    youtube = 'https://youtube.com/@yourusername'
    facebook = 'https://facebook.com/yourpage'
    discord = 'https://discord.gg/yourinvite'
    github = 'https://github.com/yourusername'
```

### Menu Configuration

```toml
[[menu.main]]
  name = 'Home'
  url = '/'
  weight = 1

[[menu.main]]
  name = 'Blog'
  url = '/blog/'
  weight = 2

[[menu.main]]
  name = 'About'
  url = '/about/'
  weight = 3
```

## Content Structure

### Blog Posts

Create blog posts in `content/blog/posts/`:

```bash
hugo new content/blog/posts/my-post.md
```

Front matter example:

```yaml
---
title: "My Blog Post"
date: 2024-01-15T10:00:00-05:00
draft: false
description: "A brief description of the post"
categories: ["Category"]
tags: ["tag1", "tag2"]
author: "Kyle Burns"
---
```

### Required Content

- Homepage content in `content/_index.md`
- Blog section in `content/blog/_index.md`

## Customization

### Colors

Edit CSS variables in `assets/css/main.css`:

```css
:root {
  --color-primary: #0078BF;
  --color-secondary: #9B9EA0;
  --color-accent: #D9772B;
  --color-text: #2C2C2C;
  --color-background: #F5F5F5;
}
```

### Fonts

Update font imports in `layouts/partials/head.html` and CSS variables.

### Logo

Replace logos in `static/logos/png/`:
- `toolpath-studio-light.png` - For light backgrounds
- `toolpath-studio-dark.png` - For dark backgrounds

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Accessibility Testing

The theme has been designed with accessibility in mind:

- Keyboard navigation tested
- Screen reader compatible (NVDA, JAWS, VoiceOver)
- Color contrast verified with WCAG guidelines
- Semantic HTML structure validated

## License

MIT License - See LICENSE file for details

## Credits

Designed and developed for Toolpath Studio by Kyle Burns
- GitHub: https://github.com/kyleburnsdev
- Site: https://kyleburnsdev.github.io/maker-learn-and-share/

## Support

For issues or questions about this theme, please open an issue in the repository.
