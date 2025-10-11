# Quick Start - Using Jekyll Layouts

## ✅ What's Already Set Up

Your website now has **reusable header and footer** components! Here's what's available:

### 📁 Structure
```
_includes/
  ├── head.html      # SEO, meta tags, CSS
  ├── header.html    # Navigation & logo
  ├── footer.html    # Contact info & social links
  └── scripts.html   # JavaScript functionality

_layouts/
  ├── default.html   # Full layout (header + footer + scripts)
  └── page.html      # Simple layout (header + footer + basic menu)
```

## 🎯 How to Use Layouts

### Before (Old Way)
Every HTML file had duplicate header and footer:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Privacy Policy</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header class="header">
    <nav>...</nav>  <!-- Same in every file! -->
  </header>
  
  <main>
    <!-- Your actual content -->
  </main>
  
  <footer class="footer">
    ...  <!-- Same in every file! -->
  </footer>
  
  <script>...</script>
</body>
</html>
```

### After (New Way with Jekyll)
Just add front matter and your content:

```html
---
layout: page
title: "Privacy Policy"
description: "Your page description"
---

<div class="legal-content">
  <!-- Your actual content -->
  <h1>Privacy Policy</h1>
  <p>Content here...</p>
</div>
```

## 📝 Two Pages Already Converted

I've converted two pages as examples:

### ✅ `privacy.html` 
- Uses `layout: page`
- Has reusable header and footer
- Automatically includes navigation
- Contact email comes from `_config.yml`

### ✅ `terms.html`
- Uses `layout: page`
- Has reusable header and footer
- Automatically includes navigation
- Contact email comes from `_config.yml`

## 🚀 How to Test

1. **Start Jekyll server:**
   ```bash
   bundle install  # First time only
   bundle exec jekyll serve
   ```

2. **View the pages:**
   - Privacy: http://localhost:4000/privacy.html
   - Terms: http://localhost:4000/terms.html

3. **Compare with originals:**
   - They look identical!
   - But now header/footer are reused from `_includes/`

## 🎨 Benefits You Get Now

### 1. **Update Header Once, Apply Everywhere**

Edit `_includes/header.html`:
```html
<a href="{{ '/option.html' | relative_url }}" class="join-btn">
  <h4>BOOK APPOINTMENT</h4>
</a>
```

Changes automatically appear on:
- ✅ privacy.html
- ✅ terms.html
- ✅ Any other page using the layout

### 2. **Update Footer Once, Apply Everywhere**

Edit `_includes/footer.html` or `_config.yml`:
```yaml
contact:
  support_email: newemail@bodyinsight.in
  phone: "+919876543210"
```

Footer updates automatically on ALL pages!

### 3. **Consistent Navigation**

Mobile menu works the same on every page - maintained in one place.

## 📋 Convert More Pages

To convert any HTML page to use the layout:

### Step 1: Add Front Matter
At the very top:
```yaml
---
layout: page  # or 'default' for complex pages
title: "Page Title"
description: "Page description for SEO"
---
```

### Step 2: Keep Only Content
Remove:
- ❌ `<!DOCTYPE html>`
- ❌ `<head>` section
- ❌ `<header>` navigation
- ❌ `<footer>`
- ❌ `<script>` tags

Keep:
- ✅ Just your main content
- ✅ Any page-specific styles
- ✅ Page-specific JavaScript (if needed)

### Step 3: Update URLs
Replace hardcoded paths:
```html
<!-- Before -->
<a href="index.html">Home</a>
<img src="images/logo.png">

<!-- After -->
<a href="{{ '/' | relative_url }}">Home</a>
<img src="{{ '/images/logo.png' | relative_url }}">
```

### Step 4: Use Config Variables
Replace hardcoded values:
```html
<!-- Before -->
<a href="mailto:support@bodyinsight.in">Contact</a>

<!-- After -->
<a href="mailto:{{ site.contact.support_email }}">Contact</a>
```

## 🎯 Which Layout to Use?

### Use `layout: page`
For simple content pages:
- ✅ Privacy Policy
- ✅ Terms of Service
- ✅ About pages
- ✅ Static content

### Use `layout: default`
For interactive pages:
- ✅ Homepage (index.html) - has sliders
- ✅ Complex pages with Swiper
- ✅ Pages with custom JavaScript

### Use no layout (keep as-is)
For special pages:
- ✅ Appointment page (has custom API calls)
- ✅ Email page (has specific functionality)
- ✅ Option page (booking flow)

## 📊 Current Status

| Page | Status | Layout Used |
|------|--------|-------------|
| privacy.html | ✅ Converted | page |
| terms.html | ✅ Converted | page |
| index.html | ⏳ Original | To convert |
| appointment.html | ⏳ Original | To convert |
| option.html | ⏳ Original | To convert |
| email.html | ⏳ Original | To convert |

## 🔧 Customizing Layouts

### Edit Header
File: `_includes/header.html`

Change logo, navigation links, or button text.

### Edit Footer
File: `_includes/footer.html`

Update social links, contact info, or mission statement.

### Edit Configuration
File: `_config.yml`

Update site-wide settings like:
```yaml
title: Body Insight
description: Your description
contact:
  support_email: support@bodyinsight.in
  phone: "+918073399697"
```

## ❓ Common Questions

### Q: Do I have to convert all pages at once?
**A:** No! Pages work with or without Jekyll. Convert gradually.

### Q: What if I break something?
**A:** Original files are backed up as `.html.backup`

### Q: Can I mix old and new pages?
**A:** Yes! Jekyll pages and regular HTML work together.

### Q: How do I deploy?
**A:** Run `jekyll build` - outputs to `_site` folder. Upload that.

## 📚 Next Steps

1. ✅ Test the converted privacy and terms pages
2. ⏭️ Convert simple pages next (option.html, email.html)
3. ⏭️ Then convert homepage (more complex)
4. ⏭️ Keep appointment.html as-is (or convert carefully)

## 🆘 Need Help?

- Check `CONVERSION_GUIDE.md` for detailed instructions
- Check `README.md` for Jekyll commands
- Test locally before deploying

---

**Your header and footer are now reusable!** 🎉

Any changes you make to `_includes/header.html` or `_includes/footer.html` will automatically update on all pages using the layouts.

