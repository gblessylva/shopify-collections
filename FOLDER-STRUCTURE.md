# 📂 Shopify Theme File Structure

## Current Repository Structure

```
shopify-collections/
│
├── 📄 main-product-grid.liquid          ← Main collection section
├── 📄 collection-search.css             ← Styles for all features
├── 📄 INSTALLATION-GUIDE.md             ← Installation instructions
├── 📄 README.md                         ← Project overview
│
├── 📁 snippets/
│   └── 📄 quick-view-modal.liquid       ← Quick view content
│
└── 📁 templates/
    └── 📄 product.quick.liquid          ← Alternate product template
```

## ➡️ Where to Upload in Your Shopify Theme

### In Shopify Admin:

1. **Online Store** → **Themes** → **Actions** → **Edit code**

2. Upload files to these locations:

```
YOUR-THEME/
│
├── 📁 sections/
│   └── main-product-grid.liquid          ← Upload or replace here
│
├── 📁 assets/
│   └── collection-search.css             ← Upload here
│
├── 📁 snippets/
│   └── quick-view-modal.liquid           ← Create new snippet
│
└── 📁 templates/
    └── product.quick.liquid              ← Create new template
```

## 🔄 How Files Work Together

```
┌─────────────────────────────────────────────────┐
│  Collection Page (main-product-grid.liquid)     │
│  ┌───────────────────────────────────────────┐  │
│  │ • Search Bar                              │  │
│  │ • Grid/List Toggle                        │  │
│  │ • Product Cards                           │  │
│  │   └─→ Quick View Button (click)           │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
                      ↓
         User clicks "Quick View"
                      ↓
┌─────────────────────────────────────────────────┐
│  JavaScript fetches:                            │
│  /products/{handle}?view=quick                  │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│  Shopify uses: product.quick.liquid             │
│  ┌───────────────────────────────────────────┐  │
│  │ {% layout none %}  ← No theme wrapper    │  │
│  │ {% render 'quick-view-modal' %}           │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│  Renders: quick-view-modal.liquid (snippet)     │
│  ┌───────────────────────────────────────────┐  │
│  │ • Product images                          │  │
│  │ • Price & variants                        │  │
│  │ • Add to cart button                      │  │
│  │ • Inline styles & scripts                 │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
                      ↓
       Returns ONLY the HTML content
       (No full page, no iframe issue!)
                      ↓
┌─────────────────────────────────────────────────┐
│  Modal displays clean product content          │
└─────────────────────────────────────────────────┘
```

## 🎯 Key Points

### Why `{% layout none %}`?
- Shopify normally wraps all pages in `theme.liquid` (header, footer, etc.)
- `{% layout none %}` tells Shopify: "Just return THIS content, nothing else"
- This prevents the full website from loading in the modal

### Why separate files?
- **product.quick.liquid**: Tells Shopify what template to use
- **quick-view-modal.liquid**: Contains the actual content
- **Separation benefits**: Easy to update content without touching template logic

### File Naming
- `product.quick.liquid` → Creates an alternate view: `?view=quick`
- Could also be `product.modal.liquid` → Would use `?view=modal`
- The name after the dot becomes the view parameter

## 📋 Quick Checklist

Before going live, verify:

- [ ] `product.quick.liquid` is in `templates/` folder
- [ ] Contains exactly: `{% layout none %}` and `{% render 'quick-view-modal', product: product %}`
- [ ] `quick-view-modal.liquid` is in `snippets/` folder
- [ ] `collection-search.css` is in `assets/` folder
- [ ] Main collection section includes the CSS file
- [ ] Theme settings have quick view enabled
- [ ] Test in incognito mode (clears cache)

## 🆘 Common Issues & Fixes

| Issue | Cause | Solution |
|-------|-------|----------|
| Full page in modal | Missing `{% layout none %}` | Add to product.quick.liquid |
| 404 error | Template not found | Check template file name exactly |
| Styles not working | CSS not loaded | Verify asset tag in main file |
| Button doesn't appear | Setting disabled | Enable in theme customizer |
| Wrong product loads | Handle mismatch | Check data-product-handle attribute |

---

**Need help?** Check the INSTALLATION-GUIDE.md for detailed troubleshooting steps.
