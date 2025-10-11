# Jekyll Conversion Guide

This guide explains how to convert the existing HTML files to use Jekyll templates.

## What Has Been Set Up

### 1. Jekyll Configuration (`_config.yml`)
- Site metadata (title, description, URL)
- Contact information
- Social media links
- API configuration
- Available cities for appointments
- SEO settings

### 2. Layouts (`_layouts/`)

#### `default.html`
Full page layout with:
- Header with navigation
- Footer with contact info
- All JavaScript functionality
- Used for homepage and interactive pages

#### `page.html`
Simple page layout with:
- Header and footer
- Basic mobile menu
- Used for content-only pages (terms, privacy, etc.)

### 3. Includes (`_includes/`)

#### `head.html`
- Google Analytics integration
- SEO meta tags (Open Graph, Twitter Cards)
- Favicon and CSS links
- Conditional Swiper CSS loading
- Preload directives for critical images
- Google Fonts loading

#### `header.html`
- Site navigation
- Mobile menu
- "Book Appointment" button
- Uses site config for logo and links

#### `footer.html`
- Contact information from config
- Social media links
- Company mission statement
- Copyright notice

#### `scripts.html`
- Header scroll behavior
- Mobile menu functionality
- Progressive darkening effect
- Swiper slider initialization
- Category pills functionality
- Built section accordion

### 4. Dependencies (`Gemfile`)
- Jekyll 4.3
- SEO plugin
- Sitemap generator
- Feed generator

## How to Convert a Page

### Step 1: Add Front Matter

At the very top of your HTML file, add:

```yaml
---
layout: default  # or 'page' for simpler pages
title: "Your Page Title"
description: "Your page description for SEO"
keywords: "keyword1, keyword2, keyword3"
robots: "index, follow"  # or "noindex, nofollow" for private pages
swiper: true  # if the page uses Swiper sliders
preload_images:  # optional, for performance
  - /images/hero.jpg
  - /images/logo.png
structured_data:  # optional, for rich snippets
  "@context": "https://schema.org"
  "@type": "WebPage"
  "name": "Page Name"
---
```

### Step 2: Remove Header Section

Delete from your HTML:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  ... everything in head ...
</head>
```

And replace the opening `<body>` and header with nothing - the layout will handle it.

### Step 3: Remove Header Navigation

Delete:
```html
<header class="header">
  ... entire header ...
</header>

<div class="mobile-nav-overlay">
  ... entire mobile nav ...
</div>
```

### Step 4: Keep Only Main Content

Keep everything between (but not including) the `<main>` tags:
```html
<!-- Keep everything here -->
```

### Step 5: Remove Footer

Delete:
```html
<footer class="footer">
  ... entire footer ...
</footer>
```

### Step 6: Remove Scripts

Delete all `<script>` tags at the bottom of the file.

### Step 7: Update URLs

Replace hardcoded URLs with Jekyll helpers:

**Before:**
```html
<a href="index.html">Home</a>
<img src="images/logo.png" alt="Logo">
<link rel="stylesheet" href="styles.css">
```

**After:**
```html
<a href="{{ '/' | relative_url }}">Home</a>
<img src="{{ '/images/logo.png' | relative_url }}" alt="Logo">
<link rel="stylesheet" href="{{ '/styles.css' | relative_url }}">
```

### Step 8: Use Site Config Variables

Replace hardcoded values with config variables:

**Before:**
```html
<a href="mailto:support@bodyinsight.in">support@bodyinsight.in</a>
<a href="tel:+918073399697">+918073399697</a>
```

**After:**
```html
<a href="mailto:{{ site.contact.support_email }}">{{ site.contact.support_email }}</a>
<a href="tel:{{ site.contact.phone }}">{{ site.contact.phone }}</a>
```

## Example Conversion

### Before (appointment.html):
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Book Appointment</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header class="header">
        <nav>...</nav>
    </header>
    
    <main class="main-content">
        <!-- Your content here -->
        <h1>Book Your Appointment</h1>
        <p>Schedule your test...</p>
    </main>
    
    <footer class="footer">
        ...
    </footer>
    
    <script src="scripts.js"></script>
</body>
</html>
```

### After (appointment.html):
```html
---
layout: default
title: "Book Your Appointment"
description: "Schedule your Body Insight health test appointment"
---

<main class="main-content">
    <!-- Your content here -->
    <h1>Book Your Appointment</h1>
    <p>Schedule your test...</p>
</main>
```

## Special Cases

### Homepage (index.html)

The homepage has complex functionality with:
- Hero section with scroll effects
- Multiple Swiper sliders
- Category pills
- Client testimonials

Keep the homepage as-is initially, or convert it carefully with:
```yaml
---
layout: default
swiper: true
preload_images:
  - /images/truck.jpg
  - /images/truck-mobile.jpg
structured_data:
  "@context": "https://schema.org"
  "@type": "MedicalBusiness"
  ...
---
```

### Appointment Page

Has custom JavaScript for API calls. Keep the scripts in the page content:
```yaml
---
layout: page  # Use simpler layout to avoid script conflicts
title: "Book Appointment"
description: "Schedule your appointment"
---

<main class="appointment-page">
  <!-- Keep appointment form and API scripts here -->
  <script>
    // API calls and booking logic
  </script>
</main>
```

### Terms & Privacy Pages

These are perfect candidates for the `page` layout:
```yaml
---
layout: page
title: "Privacy Policy"
description: "Body Insight privacy policy"
robots: "index, follow"
---

<div class="legal-content">
  <!-- Terms/Privacy content -->
</div>
```

## Testing Your Conversion

1. Start Jekyll server:
   ```bash
   bundle exec jekyll serve
   ```

2. Visit `http://localhost:4000/your-page.html`

3. Check for:
   - Proper header and footer display
   - Working navigation links
   - Correct image loading
   - Mobile menu functionality
   - No console errors

4. Test mobile responsiveness

## Common Issues & Solutions

### Images Not Loading
- Use `{{ '/images/filename.jpg' | relative_url }}`
- Check file exists in `/images/` directory

### Links Broken
- Use `{{ '/page.html' | relative_url }}` for internal links
- Use `{{ '/' | relative_url }}` for homepage

### Styles Not Applied
- CSS is automatically included in layouts
- Check `styles.css` is in root directory

### Scripts Not Working
- For complex pages, keep scripts in page content
- Use `page` layout to avoid duplicate script loading

### Front Matter Syntax Errors
- YAML is strict about indentation (use 2 spaces)
- Quote strings with special characters
- Check for proper `---` delimiters

## Development Workflow

1. **Backup**: Always keep `.backup` files until conversion is tested
2. **Convert One Page**: Start with simplest pages (terms, privacy)
3. **Test Thoroughly**: Check all functionality before moving to next page
4. **Commit Changes**: Use git to track each successful conversion
5. **Move to Complex Pages**: Save homepage and appointment for last

## Rollback Plan

If Jekyll conversion causes issues:

1. Restore from backup:
   ```bash
   cp index.html.backup index.html
   cp appointment.html.backup appointment.html
   ```

2. Or serve the `_site` directory as static HTML

3. Or disable Jekyll processing by renaming `_config.yml`

## Benefits of Jekyll Conversion

✅ **DRY (Don't Repeat Yourself)**
- Update header/footer once, changes apply everywhere
- Consistent navigation across all pages

✅ **Better SEO**
- Automatic sitemap generation
- Built-in SEO meta tags
- Canonical URLs

✅ **Easier Maintenance**
- Change contact info in one place (`_config.yml`)
- Update styles without touching every page
- Add new pages quickly

✅ **Version Control Friendly**
- Smaller file diffs
- Cleaner git history
- Easier code reviews

✅ **Performance**
- Precompiled static HTML
- Optimized asset loading
- CDN-friendly output

## Next Steps

1. ✅ Jekyll is set up and ready to use
2. ⏭️ Convert simple pages first (privacy.html, terms.html)
3. ⏭️ Convert option.html and email.html
4. ⏭️ Convert appointment.html (keep custom scripts)
5. ⏭️ Convert index.html last (most complex)
6. ⏭️ Test entire site thoroughly
7. ⏭️ Deploy to production

## Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Liquid Template Language](https://shopify.github.io/liquid/)
- [Jekyll SEO Tag](https://github.com/jekyll/jekyll-seo-tag)
- [Jekyll Sitemap](https://github.com/jekyll/jekyll-sitemap)

## Support

For questions or issues during conversion:
- Check Jekyll logs: `bundle exec jekyll serve --verbose`
- Review this guide
- Contact: support@bodyinsight.in

