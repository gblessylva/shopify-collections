# 🚀 Quick Setup Card - Copy This!

## 📋 3-Minute Setup

### Step 1: Create Template (2 lines!)
**File**: `templates/product.quick.liquid`
```liquid
{% layout none %}
{% render 'quick-view-modal', product: product %}
```

### Step 2: Create Snippet
**File**: `snippets/quick-view-modal.liquid`
- Copy entire content from: `/workspaces/shopify-collections/snippets/quick-view-modal.liquid`

### Step 3: Upload CSS
**File**: `assets/collection-search.css`
- Copy from: `/workspaces/shopify-collections/collection-search.css`

### Step 4: Update Collection Section
**File**: `sections/main-product-grid.liquid`
- Copy from: `/workspaces/shopify-collections/main-product-grid.liquid`

### Step 5: Enable in Settings
1. Theme Customizer → Collection Page
2. View Options → ✅ Enable quick view
3. View Options → ✅ Enable grid/list toggle
4. Live Search → ✅ Enable (optional)
5. **Save**

## ✅ Done!

Test by:
1. Visit any collection
2. Hover over a product
3. Click "Quick View"
4. Should see ONLY product details in modal (not full page)

---

## 🆘 Still seeing full website in modal?

**Fix**: Make sure `templates/product.quick.liquid` has these EXACT 2 lines:
```liquid
{% layout none %}
{% render 'quick-view-modal', product: product %}
```

The `{% layout none %}` is CRITICAL - don't skip it!

---

## 📱 Features You Get

✅ Quick view modal  
✅ Grid/list view toggle  
✅ Live search  
✅ AJAX add to cart  
✅ Variant selection  
✅ Mobile responsive  
✅ Saved preferences  

---

**Questions?** See `INSTALLATION-GUIDE.md` for detailed help.
