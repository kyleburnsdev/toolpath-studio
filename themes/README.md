# Themes Directory

This directory contains Hugo themes for your site.

## Installing a Theme

### Method 1: Git Submodule (Recommended)

Add a theme as a submodule:

```bash
git submodule add https://github.com/AUTHOR/THEME_NAME.git themes/THEME_NAME
```

Update `hugo.toml`:
```toml
theme = 'THEME_NAME'
```

Initialize submodules when cloning:
```bash
git submodule update --init --recursive
```

### Method 2: Clone Directly

```bash
cd themes
git clone https://github.com/AUTHOR/THEME_NAME.git
```

### Method 3: Download

Download a theme ZIP file and extract it to this directory.

## Recommended Blog Themes

### PaperMod
- Modern, clean design
- Fast and lightweight
- Excellent blog features
- [GitHub](https://github.com/adityatelange/hugo-PaperMod)

```bash
git submodule add --depth=1 --branch master https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### Blowfish
- Highly customizable
- Beautiful design
- Great documentation
- [GitHub](https://github.com/nunocoracao/blowfish)

```bash
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

### Stack
- Card-based layout
- Image-focused design
- Sidebar navigation
- [GitHub](https://github.com/CaiJimmy/hugo-theme-stack)

```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

### Ananke
- Simple and responsive
- Good starter theme
- Officially supported
- [GitHub](https://github.com/theNewDynamic/gohugo-theme-ananke)

```bash
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

## Theme Configuration

After installing a theme:

1. **Update hugo.toml:**
   ```toml
   theme = 'THEME_NAME'
   ```

2. **Check theme documentation** for specific configuration options

3. **Copy example config** if provided by the theme:
   ```bash
   cp themes/THEME_NAME/exampleSite/config.toml hugo.toml
   ```

4. **Customize** colors, fonts, and layout in `hugo.toml`

## Theme Structure

Themes typically contain:

```
themes/THEME_NAME/
├── layouts/          # Template files
├── static/           # Static assets
├── assets/           # Assets for processing
├── archetypes/       # Content templates
├── i18n/             # Translations
├── exampleSite/      # Example configuration
└── README.md         # Theme documentation
```

## Updating Themes

If using submodules:

```bash
# Update a specific theme
git submodule update --remote themes/THEME_NAME

# Update all submodules
git submodule update --remote --merge
```

## Custom Theme

To create your own theme:

```bash
hugo new theme THEME_NAME
```

This creates a basic theme structure in `themes/THEME_NAME/`.

## Theme Overrides

Override theme templates without modifying the theme:

Place custom templates in the root `layouts/` directory with the same path as the theme template.

Example:
```
layouts/_default/single.html  # Overrides theme's single.html
```

## Resources

- [Hugo Themes Gallery](https://themes.gohugo.io/)
- [Creating a Theme](https://gohugo.io/hugo-modules/theme-components/)
- [Theme Components](https://gohugo.io/hugo-modules/theme-components/)

## Current Status

**No theme is currently installed.** You need to install a theme for the site to render properly. See the recommendations above or browse [themes.gohugo.io](https://themes.gohugo.io/).
