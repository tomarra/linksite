# LinkSite - Project Context

## Overview

LinkSite is a static LinkTree-style personal landing page designed for GitHub Pages hosting. It allows users to consolidate multiple profile links into a single URL.

## Architecture

This is a zero-build static site. The HTML loads configuration at runtime via fetch() and renders the page dynamically with vanilla JavaScript.

### Files

- **index.html** - Single-page application that loads config and renders the site
- **styles.css** - CSS with custom properties (variables) for theming
- **config.json** - User configuration file (name, bio, avatar, theme, sections/links)

### How It Works

1. `index.html` loads and fetches `config.json`
2. Initial theme is determined: saved localStorage preference > system preference (prefers-color-scheme)
3. Theme colors from config are applied as CSS custom properties on `:root`
4. Profile info and links are rendered into the DOM (supports both `sections` and flat `links` arrays)
5. Font Awesome 6.7.2 icons are loaded from CDN for link icons
6. Theme toggle switch allows manual switching, preference saved to localStorage

## Key Design Decisions

- **No build step**: Users only need to edit JSON, not touch HTML/CSS/JS
- **Runtime config loading**: Allows GitHub Pages deployment without preprocessing
- **CSS custom properties**: Theme colors can be changed without editing CSS
- **Font Awesome CDN**: Provides wide icon coverage without local assets
- **Mobile-first responsive**: Works well on all screen sizes
- **Linik Sans font**: Loaded from CDNFonts for a clean, modern look

## Icon System

Icons are mapped in the `iconMap` object in `index.html`. The map converts simple identifiers (like "github") to Font Awesome 6.7.2 class names (like "fab fa-github").

Currently supported icons: `github`, `bluesky`, `twitter`, `linkedin`, `instagram`, `youtube`, `flickr`, `mastodon`, `twitch`, `discord`, `facebook`, `tiktok`, `spotify`, `medium`, `dev`, `stackoverflow`, `reddit`, `pinterest`, `snapchat`, `whatsapp`, `telegram`, `email`, `globe`, `blog`, `podcast`, `video`, `music`, `store`, `coffee`, `heart`, `star`, `link`

To add new icons:
1. Find the Font Awesome 6.7.2 class name
2. Add an entry to `iconMap` in `index.html`

## Link Structure

The site supports two link formats:

### Sections (Grouped Links)
Links organized into titled sections:
```json
"sections": [
  {
    "title": "Follow Me",
    "links": [
      { "title": "Twitter", "url": "...", "icon": "twitter" }
    ]
  }
]
```

### Flat Links (Backward Compatible)
Simple array of links without grouping:
```json
"links": [
  { "title": "GitHub", "url": "...", "icon": "github" }
]
```

If both `sections` and `links` are present, `sections` takes priority.

## Theming

Theme colors are defined in `config.json` under `theme.light` and `theme.dark` and applied as CSS custom properties:
- `--bg-color`: Page background (or gradient start)
- `--bg-gradient-end`: Optional gradient end color (falls back to `--bg-color` if not set)
- `--card-color`: Link button background
- `--text-color`: All text
- `--accent-color`: Borders, avatar ring
- `--link-hover-color`: Button hover state

### Gradient Backgrounds

The site supports diagonal gradient backgrounds. Set `backgroundGradientEnd` in your theme config to enable:
```json
"light": {
  "backgroundColor": "#ffffff",
  "backgroundGradientEnd": "#e5e5e5"
}
```
If `backgroundGradientEnd` is omitted, the background will be a solid color.

### Light/Dark Mode

The site supports automatic light/dark mode:
1. **System preference**: Defaults to user's OS preference via `prefers-color-scheme`
2. **Manual toggle**: Footer toggle switch allows switching between modes
3. **Persistence**: User's choice is saved to localStorage
4. **Live updates**: Responds to system theme changes if no manual preference set

### Theme Toggle Switch

The toggle is a pill-shaped switch with sun/moon icons:
- Uses a hidden checkbox input for state management
- CSS-only animation (no JS for visuals)
- Knob slides left (light) or right (dark)
- Sun icon visible in dark mode, moon icon visible in light mode
- Styled with CSS custom properties for consistency with theme

## Testing Locally

```bash
npx serve .
```

File protocol (`file://`) won't work due to fetch() CORS restrictions.

## Common Modifications

### Adding a new link type with custom icon
1. Add icon mapping to `iconMap` in `index.html`
2. Use the new icon key in `config.json`

### Changing layout/styling
Edit `styles.css` directly. CSS custom properties handle colors; other styles can be modified as needed.

### Adding new config options
1. Add the option to `config.json`
2. Read and apply it in the `renderSite()` function in `index.html`
