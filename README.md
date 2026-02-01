# LinkSite

A simple, customizable LinkTree-style static site for GitHub Pages. No build step required - just edit the config file and deploy.

## Quick Start

1. Edit `config.json` with your information
2. Serve locally with `npx serve .`

## Configuration

All customization is done through `config.json`:

```json
{
  "name": "Your Name",
  "bio": "A short bio about yourself",
  "avatar": "https://example.com/your-photo.jpg",
  "theme": {
    "light": {
      "backgroundColor": "#ffffff",
      "backgroundGradientEnd": "#e5e5e5",
      "cardColor": "#ffffff",
      "textColor": "#1a1a2e",
      "accentColor": "#e94560",
      "linkHoverColor": "#e8e8e8"
    },
    "dark": {
      "backgroundColor": "#1a1a2e",
      "backgroundGradientEnd": "#2d2d44",
      "cardColor": "#16213e",
      "textColor": "#ffffff",
      "accentColor": "#e94560",
      "linkHoverColor": "#0f3460"
    }
  },
  "sections": [
    {
      "title": "Social",
      "links": [
        {
          "title": "GitHub",
          "url": "https://github.com/yourusername",
          "icon": "github"
        },
        {
          "title": "Twitter",
          "url": "https://twitter.com/yourusername",
          "icon": "twitter"
        }
      ]
    },
    {
      "title": "Contact",
      "links": [
        {
          "title": "Email",
          "url": "mailto:you@example.com",
          "icon": "email"
        }
      ]
    }
  ],
  "footer": {
    "text": "© 2025"
  }
}
```

### Configuration Options

| Field         | Description                                  |
| ------------- | -------------------------------------------- |
| `name`        | Your display name shown at the top           |
| `bio`         | Short description below your name            |
| `avatar`      | URL or path to your profile picture          |
| `theme`       | Light and dark theme colors                  |
| `sections`    | Array of link sections (grouped links)       |
| `links`       | Array of link objects (flat, for simplicity) |
| `footer.text` | Text shown at the bottom                     |

You can use either `sections` (grouped links with titles) or `links` (flat array). If both are present, `sections` takes priority.

### Theme Colors

The site supports both light and dark modes. Define colors for each under `theme.light` and `theme.dark`:

| Property                | Description                                      |
| ----------------------- | ------------------------------------------------ |
| `backgroundColor`       | Page background color (or gradient start)        |
| `backgroundGradientEnd` | Optional gradient end color for diagonal effect  |
| `cardColor`             | Link button background color                     |
| `textColor`             | Text color throughout the site                   |
| `accentColor`           | Accent color for borders and avatar ring         |
| `linkHoverColor`        | Link button color on hover                       |

If `backgroundGradientEnd` is omitted, the background will be a solid color.

### Light/Dark Mode

The site automatically detects your system's color scheme preference. Users can also manually toggle between light and dark mode using the switch in the footer. The preference is saved to localStorage.

### Sections

Links can be organized into sections with titles:

```json
"sections": [
  {
    "title": "Section Title",
    "links": [
      { "title": "Link Name", "url": "https://...", "icon": "github" }
    ]
  }
]
```

### Link Object

Each link has:

| Field   | Description                           |
| ------- | ------------------------------------- |
| `title` | Text displayed on the button          |
| `url`   | Where the link goes                   |
| `icon`  | Icon identifier (see available icons) |

### Available Icons

Icons are powered by Font Awesome 6.7.2.

**Social Platforms:**

- `github`, `twitter`, `linkedin`, `instagram`, `youtube`, `twitch`, `discord`, `facebook`, `tiktok`, `spotify`, `medium`, `dev`, `stackoverflow`, `reddit`, `pinterest`, `snapchat`, `whatsapp`, `telegram`, `bluesky`, `mastodon`, `flickr`

**General:**

- `email`, `globe`, `blog`, `podcast`, `video`, `music`, `store`, `coffee`, `heart`, `star`, `link`
