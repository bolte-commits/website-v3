# Body Insight Website - Jekyll

This is the Body Insight website converted to Jekyll static site generator.

## Prerequisites

- Ruby 2.7 or higher
- Bundler gem

## Installation

1. Install dependencies:
```bash
bundle install
```

## Development

To run the site locally:

```bash
bundle exec jekyll serve
```

The site will be available at `http://localhost:4000`

To run with live reload:

```bash
bundle exec jekyll serve --livereload
```

## Build

To build the site for production:

```bash
bundle exec jekyll build
```

The generated site will be in the `_site` directory.

## Project Structure

```
.
├── _config.yml           # Jekyll configuration
├── _includes/            # Reusable components
│   ├── head.html        # HTML head with meta tags
│   ├── header.html      # Site header and navigation
│   ├── footer.html      # Site footer
│   └── scripts.html     # JavaScript files
├── _layouts/             # Page layouts
│   ├── default.html     # Main layout with header/footer
│   └── page.html        # Simple page layout
├── assets/              # Static assets (CSS, JS, images)
├── images/              # Image files
├── fonts/               # Font files
├── index.html           # Homepage
├── appointment.html     # Appointment booking page
├── option.html          # Options page
├── email.html           # Email page
├── privacy.html         # Privacy policy
├── terms.html           # Terms of service
└── Gemfile              # Ruby dependencies
```

## Key Features

### Includes

Modular components that can be reused across pages:

- **head.html**: Contains meta tags, SEO tags, Google Analytics, and asset links
- **header.html**: Navigation header with mobile menu support
- **footer.html**: Footer with contact info and social links
- **scripts.html**: JavaScript for interactivity (Swiper, mobile menu, etc.)

### Layouts

- **default.html**: Full page layout with header, footer, and scripts
- **page.html**: Simpler layout for content pages

### Configuration

Edit `_config.yml` to customize:

- Site metadata (title, description, URL)
- Contact information
- Social media links
- API endpoints
- Available cities for booking

### Front Matter

Add front matter to pages to customize their behavior:

```yaml
---
layout: default
title: Your Page Title
description: Your page description for SEO
swiper: true  # Include Swiper slider library
preload_images:  # Images to preload for performance
  - /images/hero.jpg
  - /images/logo.png
---
```

## Converting Additional Pages

To convert an existing HTML page to Jekyll:

1. Create a new file with the same name
2. Add front matter at the top:
   ```yaml
   ---
   layout: page
   title: Page Title
   description: Page description
   ---
   ```
3. Remove the `<head>`, `<header>`, `<footer>`, and `<script>` sections
4. Keep only the main content between `<main>` tags
5. Replace hardcoded URLs with Jekyll helpers:
   - `images/logo.png` → `{{ '/images/logo.png' | relative_url }}`
   - `index.html` → `{{ '/' | relative_url }}`

## Deployment

### GitHub Pages

1. Push to GitHub
2. Enable GitHub Pages in repository settings
3. Select branch and root folder

### Netlify

1. Connect your repository
2. Build command: `jekyll build`
3. Publish directory: `_site`

### Manual Deployment

1. Run `bundle exec jekyll build`
2. Upload contents of `_site` directory to your web server

## Environment Variables

For production deployment, set these in `_config.yml`:

- `url`: Your production URL (e.g., https://bodyinsight.in)
- `baseurl`: Leave empty for root deployment

## Notes

- Original HTML files are backed up with `.backup` extension
- All assets remain in their original locations
- Jekyll processes files with front matter; static files are copied as-is
- Use Liquid template syntax for dynamic content

## Support

For issues or questions, contact support@bodyinsight.in

