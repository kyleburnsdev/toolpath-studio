# Level Up Lab Theme Guide

This guide provides information about the custom Hugo theme created for Level Up Lab.

## Theme Overview

The Level Up Lab theme (`themes/leveluplab/`) is a custom Hugo theme designed specifically for this blog with:

- **WCAG 2.1 AA Accessibility Compliance**: Ensuring the site is usable by everyone
- **Semantic HTML5 Markup**: For better SEO and assistive technologies
- **Brand Consistency**: Following the Level Up Lab branding guidelines
- **Responsive Design**: Mobile-first approach that works on all devices

## Quick Start

The theme is already configured in `hugo.toml`:

```toml
theme = 'leveluplab'
```

To preview your site with the theme:

```bash
hugo server -D
```

## Theme Features

### 1. Accessibility Features

The theme implements WCAG 2.1 AA accessibility standards:

#### Skip Navigation
- A "Skip to main content" link appears when users press Tab
- Allows keyboard users to bypass navigation and jump to main content

#### Semantic HTML
- Proper use of HTML5 landmarks: `<header>`, `<main>`, `<footer>`, `<nav>`, `<article>`
- ARIA roles for better screen reader support
- Semantic heading hierarchy (H1-H6)

#### Keyboard Navigation
- All interactive elements accessible via keyboard
- Visible focus indicators on all focusable elements
- Logical tab order throughout the page

#### Color Contrast
- All text meets WCAG AA contrast ratios
- Primary text: 4.5:1 minimum contrast
- Large text: 3:1 minimum contrast

### 2. Branding

The theme implements the Level Up Lab brand identity:

#### Colors
- **Primary**: Marine Blue (#0078BF) - Links, headers, accents
- **Secondary**: Ash Gray (#9B9EA0) - Metadata, subtle text
- **Accent**: Burnt Orange (#D9772B) - Hover states, call-to-action
- **Text**: Charcoal Black (#2C2C2C) - Main content text
- **Background**: Soft Gray (#F5F5F5) - Page background

#### Typography
- **Headings**: Montserrat (Bold/Semi-Bold weight)
  - Clean, modern sans-serif for strong visual hierarchy
- **Body**: Inter (Regular/Medium weight)
  - Highly legible sans-serif optimized for screen reading

#### Logo
- Level Up Lab logo displays in the header
- Automatically uses the light version on light backgrounds
- Logo is also used as the home page link

### 3. Layout Components

#### Header
- Sticky header that stays visible while scrolling
- Logo with home page link
- Navigation menu with current page indicator
- Responsive - collapses for mobile

#### Homepage
- Hero section with site title and description
- Recent posts section showing latest blog entries
- Each post shows title, date, author, description, categories, and tags

#### Blog Listing Page
- List of all blog posts
- Post cards with left accent border (brand primary color)
- Metadata including date and author
- Categories and tags as clickable badges
- Hover effects for better interactivity

#### Single Post View
- Full article content with proper semantic structure
- Post header with title, date, author, and reading time
- Category and tag badges
- Optimized typography for reading
- Code syntax highlighting support

#### Footer
- Copyright information
- Site description
- Social media links (YouTube, Facebook, Discord, GitHub)
- Dark background with light text for visual separation

### 4. Responsive Design

The theme uses a mobile-first approach:

#### Breakpoints
- **Mobile**: < 480px (base styles)
- **Tablet**: 480px - 768px
- **Desktop**: > 768px

#### Responsive Features
- Flexible grid layouts
- Collapsing navigation on mobile
- Appropriately sized touch targets
- Readable font sizes across all devices
- Optimized spacing for different screen sizes

### 5. SEO Optimization

#### Meta Tags
- Page titles with site name
- Meta descriptions for all pages
- OpenGraph tags for social media sharing
- Author and content metadata

#### Semantic Structure
- Proper heading hierarchy
- Meaningful HTML elements
- Structured data ready
- Clean, descriptive URLs

#### Performance
- Minified CSS and JavaScript in production
- Optimized asset loading
- Fast page rendering

## Customization

### Changing Colors

Edit `/themes/leveluplab/assets/css/main.css` and modify the CSS variables:

```css
:root {
  --color-primary: #0078BF;      /* Your primary color */
  --color-secondary: #9B9EA0;    /* Your secondary color */
  --color-accent: #D9772B;       /* Your accent color */
  --color-text: #2C2C2C;         /* Your text color */
  --color-background: #F5F5F5;   /* Your background color */
}
```

### Changing Fonts

1. Update the Google Fonts link in `/themes/leveluplab/layouts/partials/head.html`
2. Update the font-family variables in `/themes/leveluplab/assets/css/main.css`:

```css
:root {
  --font-heading: 'Your Heading Font', sans-serif;
  --font-body: 'Your Body Font', sans-serif;
}
```

### Adding Custom CSS

Create a file at `/assets/css/custom.css` in your site root (not in the theme) and add:

```css
/* Your custom styles here */
```

Hugo will automatically include it.

### Overriding Templates

To override a theme template without modifying the theme:

1. Copy the template from `/themes/leveluplab/layouts/` 
2. Place it in `/layouts/` with the same path
3. Modify as needed

Example: To customize the footer, copy:
- From: `/themes/leveluplab/layouts/partials/footer.html`
- To: `/layouts/partials/footer.html`

## Content Guidelines

### Blog Post Front Matter

Use this template for blog posts:

```yaml
---
title: "Your Post Title"
date: 2024-01-15T10:00:00-05:00
draft: false
description: "A brief, SEO-friendly description"
categories: ["Category Name"]
tags: ["tag1", "tag2", "tag3"]
author: "Your Name"
---
```

### Writing Accessible Content

1. **Use Descriptive Link Text**: Instead of "click here", use "read the installation guide"
2. **Add Alt Text to Images**: Describe what the image shows
3. **Use Proper Headings**: Don't skip heading levels (H1 → H2 → H3)
4. **Write Clear Descriptions**: Help users understand what content is about
5. **Use Lists**: For sequential or related items

### Code Blocks

Use fenced code blocks with language specification:

```markdown
\`\`\`python
def hello_world():
    print("Hello, World!")
\`\`\`
```

## Testing Your Site

### Build Test

```bash
hugo --gc --minify
```

Should complete without errors.

### Local Preview

```bash
hugo server -D
```

Check:
- All pages load correctly
- Navigation works
- Links function properly
- Images display
- Styles apply correctly

### Accessibility Testing

1. **Keyboard Navigation**: Press Tab and navigate without a mouse
2. **Color Contrast**: Use a contrast checker on text
3. **Screen Reader**: Test with NVDA (Windows) or VoiceOver (Mac)
4. **Mobile**: Test on actual mobile devices

## Browser Support

The theme is tested and supported on:

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Troubleshooting

### Theme Not Applying

Check `hugo.toml` contains:
```toml
theme = 'leveluplab'
```

### Styles Not Loading

1. Clear Hugo's cache: `hugo --gc`
2. Rebuild: `hugo`
3. Check browser console for errors

### Logo Not Displaying

Verify logo files exist at:
- `/themes/leveluplab/static/logos/png/level-up-lab-light.png`
- `/themes/leveluplab/static/logos/png/level-up-lab-dark.png`

## Additional Resources

- **Hugo Documentation**: https://gohugo.io/documentation/
- **WCAG Guidelines**: https://www.w3.org/WAI/WCAG21/quickref/
- **WebAIM**: https://webaim.org/ (Accessibility resources)
- **Theme README**: `/themes/leveluplab/README.md`

## Support

For issues or questions about the theme:
1. Check the theme README: `/themes/leveluplab/README.md`
2. Review Hugo documentation
3. Open an issue in the repository

## Credits

Theme designed and developed by Kyle Burns for Level Up Lab
- Following Level Up Lab branding guidelines
- Implementing WCAG 2.1 AA accessibility standards
- Using semantic HTML5 for SEO optimization
