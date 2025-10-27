# Layouts Directory

This directory is for custom Hugo layouts and templates. Hugo uses a template hierarchy to render content.

## Theme Setup

Currently, no theme is configured. You have two options:

### Option 1: Use an Existing Theme (Recommended)

Browse Hugo themes at [themes.gohugo.io](https://themes.gohugo.io/) and install one:

**As a Git submodule (recommended):**
```bash
git submodule add https://github.com/THEME_AUTHOR/THEME_NAME.git themes/THEME_NAME
```

**Update hugo.toml:**
```toml
theme = 'THEME_NAME'
```

**Popular blog themes:**
- [PaperMod](https://github.com/adityatelange/hugo-PaperMod) - Clean, fast, and feature-rich
- [Blowfish](https://github.com/nunocoracao/blowfish) - Modern and highly customizable
- [Stack](https://github.com/CaiJimmy/hugo-theme-stack) - Card-based design
- [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) - Simple and responsive

### Option 2: Create Custom Layouts

If you prefer to build your own theme, create layouts in this directory:

```
layouts/
├── _default/
│   ├── baseof.html      # Base template
│   ├── list.html        # List page template
│   └── single.html      # Single page template
├── partials/
│   ├── header.html
│   ├── footer.html
│   └── head.html
├── index.html           # Homepage
└── 404.html             # 404 error page
```

## Custom Overrides

Even with a theme, you can override specific templates by placing them in this directory with the same path structure as the theme.

For example, to override a theme's single post template:
```
layouts/_default/single.html
```

## Resources

- [Hugo Templates Documentation](https://gohugo.io/templates/)
- [Hugo Template Hierarchy](https://gohugo.io/templates/lookup-order/)
- [Hugo Themes](https://themes.gohugo.io/)
