# Typography Token Usage Guide

## 🎯 **Perfect Match with Your Figma System**

Your typography tokens now perfectly match your existing Figma text styles! This means **zero breaking changes** when you start adopting tokens in your projects.

## 📋 **Available Text Styles**

### **Headings (h1-h10)**

```css
/* Matches your Figma h1 style */
.title {
  font-family: var(--text-h1-font-family);
  font-size: var(--text-h1-font-size);
  font-weight: var(--text-h1-font-weight);
  line-height: var(--text-h1-line-height);
}

/* All available heading styles */
--text-h1-* (96px)  --text-h6-* (40px)
--text-h2-* (76px)  --text-h7-* (34px)
--text-h3-* (60px)  --text-h8-* (28px)
--text-h4-* (54px)  --text-h9-* (24px)
--text-h5-* (48px)  --text-h10-* (22px)
```

### **Body Text**

```css
/* Primary body text (16px) */
.body-primary {
  font-family: var(--text-body1-font-family);
  font-size: var(--text-body1-font-size);
  font-weight: var(--text-body1-font-weight);
  line-height: var(--text-body1-line-height);
}

/* Secondary body text (14px) */
.body-secondary {
  font-family: var(--text-body2-font-family);
  font-size: var(--text-body2-font-size);
  font-weight: var(--text-body2-font-weight);
  line-height: var(--text-body2-line-height);
}
```

### **Subtitles**

```css
/* Subtitle 1 (20px) */
.subtitle-large {
  font-family: var(--text-subtitle1-font-family);
  font-size: var(--text-subtitle1-font-size);
  font-weight: var(--text-subtitle1-font-weight);
  line-height: var(--text-subtitle1-line-height);
}

/* Subtitle 2 (18px) */
.subtitle-small {
  font-family: var(--text-subtitle2-font-family);
  font-size: var(--text-subtitle2-font-size);
  font-weight: var(--text-subtitle2-font-weight);
  line-height: var(--text-subtitle2-line-height);
}
```

### **Button Text**

```css
/* Small button (16px, medium weight) */
.btn-sm {
  font-family: var(--text-button-sm-font-family);
  font-size: var(--text-button-sm-font-size);
  font-weight: var(--text-button-sm-font-weight);
  line-height: var(--text-button-sm-line-height);
}

/* Available button sizes */
--text-button-sm-* (16px)
--text-button-md-* (24px)
--text-button-lg-* (28px)
```

### **Utility Text**

```css
/* Caption text (12px) */
.caption {
  font-family: var(--text-caption-font-family);
  font-size: var(--text-caption-font-size);
  font-weight: var(--text-caption-font-weight);
  line-height: var(--text-caption-line-height);
}

/* Overline text (10px, uppercase) */
.overline {
  font-family: var(--text-overline-font-family);
  font-size: var(--text-overline-font-size);
  font-weight: var(--text-overline-font-weight);
  line-height: var(--text-overline-line-height);
  text-transform: var(--text-overline-text-case);
}

/* Navigation label (10px, medium weight) */
.nav-label {
  font-family: var(--text-nav-label-font-family);
  font-size: var(--text-nav-label-font-size);
  font-weight: var(--text-nav-label-font-weight);
  line-height: var(--text-nav-label-line-height);
}
```

## 🔄 **Easy Font Testing & Brand Flexibility**

### **Test Different Fonts (Super Easy!)**

```css
/* Override just the base font family to test fonts */
:root {
  --typography-font-family-base: "Inter", system-ui, sans-serif;
  /* OR */
  --typography-font-family-base: "Poppins", system-ui, sans-serif;
  /* OR */
  --typography-font-family-base: "Montserrat", system-ui, sans-serif;
}

/* All text styles automatically use the new font! */
```

### **Brand-Specific Typography**

```css
/* Music brand theme */
.theme-music {
  --typography-font-family-base: "Spotify Mix", "Roboto", sans-serif;
}

/* Karaoke brand theme */
.theme-karaoke {
  --typography-font-family-base: "Sing Along", "Roboto", sans-serif;
}
```

## 📦 **How to Import**

### **Complete Typography System (Recommended)**

```css
/* Import primitives first (foundation) */
@import "@stingray/design-tokens/dist/primitives.css";
/* Then import semantic tokens (your text styles) */
@import "@stingray/design-tokens/dist/semantic.css";
```

### **Primitives Only**

```css
/* Import just primitives if you want to build your own semantics */
@import "@stingray/design-tokens/dist/primitives.css";
```

### **Why Two Files?**

- **`primitives.css`** = Foundation tokens (font sizes, weights, colors)
- **`semantic.css`** = Your actual text styles (h1, body1, button-sm, etc.)

This separation keeps primitives as the single source of truth while allowing semantic tokens to reference them.

## 🚀 **Migration Strategy**

### **Phase 1: Start Using Tokens Gradually**

```css
/* Instead of hardcoded styles */
.my-title {
  font-size: 96px;
  font-weight: 400;
  font-family: Roboto;
  line-height: 1.171875;
}

/* Use tokens (exact same visual result!) */
.my-title {
  font-family: var(--text-h1-font-family);
  font-size: var(--text-h1-font-size);
  font-weight: var(--text-h1-font-weight);
  line-height: var(--text-h1-line-height);
}
```

### **Phase 2: Utility Classes (Optional)**

```css
/* Create utility classes for common patterns */
.text-h1 {
  font-family: var(--text-h1-font-family);
  font-size: var(--text-h1-font-size);
  font-weight: var(--text-h1-font-weight);
  line-height: var(--text-h1-line-height);
}

.text-body1 {
  font-family: var(--text-body1-font-family);
  font-size: var(--text-body1-font-size);
  font-weight: var(--text-body1-font-weight);
  line-height: var(--text-body1-line-height);
}
```

## ✨ **Key Benefits**

✅ **Zero Breaking Changes** - Perfect match with existing Figma styles  
✅ **Easy Font Testing** - Change one variable, test everywhere  
✅ **Brand Flexibility** - Different fonts per brand/theme  
✅ **Maintainable** - Update font sizes in one place  
✅ **Type Safe** - When paired with TypeScript  
✅ **Performance** - CSS variables are fast  
✅ **Designer-Developer Sync** - Same names in Figma and code
