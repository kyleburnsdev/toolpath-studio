# Assets Directory

This directory contains files that will be processed by Hugo Pipes (Hugo's asset pipeline).

## Purpose

Unlike the `static/` directory, files in `assets/` can be:
- Processed and transformed by Hugo
- Minified
- Bundled
- Fingerprinted for cache busting

## Common Use Cases

### SCSS/SASS Files
```
assets/scss/
├── main.scss
├── _variables.scss
└── _components.scss
```

### JavaScript
```
assets/js/
├── main.js
└── modules/
    └── navigation.js
```

### Images for Processing
Images that need resizing or format conversion:
```
assets/images/
└── hero-banner.jpg
```

## Processing in Templates

Access and process assets in your templates:

**SCSS:**
```html
{{ $styles := resources.Get "scss/main.scss" | toCSS | minify | fingerprint }}
<link rel="stylesheet" href="{{ $styles.Permalink }}">
```

**JavaScript:**
```html
{{ $js := resources.Get "js/main.js" | minify | fingerprint }}
<script src="{{ $js.Permalink }}"></script>
```

**Images:**
```html
{{ $image := resources.Get "images/hero.jpg" }}
{{ $resized := $image.Resize "800x" }}
<img src="{{ $resized.Permalink }}" alt="Hero">
```

## Static vs Assets

**Use `static/` for:**
- Files served as-is
- Files that don't need processing
- Favicons, robots.txt, etc.

**Use `assets/` for:**
- Files that need processing
- SCSS/SASS files
- JavaScript to be bundled/minified
- Images requiring transformation

## Resources

- [Hugo Pipes Documentation](https://gohugo.io/hugo-pipes/)
- [Asset Processing](https://gohugo.io/categories/asset-management)
