# Quick View & Grid/List Toggle - Installation Guide

## 📁 Proper Folder Structure for Shopify

```
your-theme/
├── sections/
│   └── main-product-grid.liquid          (main collection template)
├── snippets/
│   └── quick-view-modal.liquid           (quick view content snippet)
├── templates/
│   └── product.quick.liquid              (alternate product template)
└── assets/
    └── collection-search.css             (styles)
```

## 🚀 Installation Steps

### Step 1: Upload Files to Correct Locations

1. **Sections folder**: 
   - Upload `main-product-grid.liquid` to `sections/`
   - Or replace your existing main collection section

2. **Snippets folder**: 
   - Create a new snippet called `quick-view-modal.liquid`
   - Copy the content from the `snippets/quick-view-modal.liquid` file

3. **Templates folder**: 
   - Create a new alternate template: `product.quick.liquid`
   - Copy this exact content:
   ```liquid
   {% layout none %}
   {% render 'quick-view-modal', product: product %}
   ```

4. **Assets folder**: 
   - Upload `collection-search.css` to your assets folder

### Step 2: Enable Features

1. Go to your Shopify admin
2. Navigate to: **Online Store** > **Themes** > **Customize**
3. Go to a collection page
4. Look for these settings:
   - **Live Search Settings**
     - ✅ Enable live search
     - Set search placeholder text
   - **View Options**
     - ✅ Enable grid/list view toggle
     - ✅ Enable quick view modal
5. Save changes

## ✅ How It Works

### Quick View Modal
- When a user clicks "Quick View" on a product card
- The system fetches `/products/{product-handle}?view=quick`
- Shopify uses the `product.quick.liquid` template (with `{% layout none %}`)
- This renders ONLY the snippet content, not the full page
- The content loads into the modal without any wrapper HTML

### Grid/List Toggle
- Users can switch between grid and list views
- Preference is saved in localStorage
- Automatically restores user's preferred view on return visits

### Live Search
- Filters products in real-time as you type
- Searches product titles and vendor names
- No page reload required

## 🐛 Troubleshooting

### Issue: Full website showing in modal instead of product details

**Cause**: The `product.quick.liquid` template is missing or doesn't have `{% layout none %}`

**Fix**: 
1. Make sure `product.quick.liquid` exists in your `templates/` folder
2. Ensure it contains exactly:
   ```liquid
   {% layout none %}
   {% render 'quick-view-modal', product: product %}
   ```

### Issue: Quick view button not appearing

**Fix**: 
1. Check that "Enable quick view modal" is turned ON in theme settings
2. Clear browser cache and refresh

### Issue: Styles not applying

**Fix**: 
1. Verify `collection-search.css` is in the `assets/` folder
2. Check that the main-product-grid.liquid file includes:
   ```liquid
   {{ 'collection-search.css' | asset_url | stylesheet_tag }}
   ```

## 🎨 Customization

### Change Quick View Button Style
Edit in `collection-search.css` around line 140:
```css
.quick-view-button {
  /* Customize colors, padding, etc. */
}
```

### Modify Modal Size
Edit in `collection-search.css` around line 250:
```css
.quick-view-modal__content {
  max-width: 1000px; /* Change this value */
}
```

### Adjust Grid/List Layout
Edit in `collection-search.css` around line 85:
```css
.product-grid--list .card__media {
  width: 200px; /* Change image size in list view */
}
```

## 📝 Features Included

✅ Live product search (searches as you type)  
✅ Grid/List view toggle with persistence  
✅ Quick view modal with:
- Product images with thumbnail gallery
- Price and compare-at-price
- Variant selection with live price updates
- Add to cart functionality (AJAX)
- Quantity selector
- Link to full product page

## 🔄 Updates & Maintenance

- All JavaScript is self-contained in `main-product-grid.liquid`
- Styles are isolated in `collection-search.css`
- Quick view content can be customized in `snippets/quick-view-modal.liquid`

## 💡 Tips

1. **Test on different devices** - The layout is responsive but always verify
2. **Check variant handling** - Make sure variant switching updates price correctly
3. **Monitor cart integration** - Ensure add-to-cart triggers cart drawer/updates
4. **Consider performance** - If you have 100+ products, consider pagination settings

## 🆘 Need Help?

If you're still seeing the full website in the quick view:
1. Double-check the `{% layout none %}` is in `product.quick.liquid`
2. Verify the snippet name matches exactly: `quick-view-modal.liquid`
3. Clear Shopify theme cache (try in incognito mode)
4. Check browser console for JavaScript errors
