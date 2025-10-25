
# Cora Shopify Custom Theme Sections

This repository contains a collection of **professionally developed Shopify 2.0 sections** built for the **Cora Frontend Design Evaluation**.  
The project demonstrates a systematic, scalable, and token-driven approach to theme development using **Liquid**, **CSS**, and **Shopify design standards**.

---
## 📽️ Preview & Comparison Video

To help visualize design accuracy and responsiveness, we’ve included a short preview and comparison video.  
This demonstrates the final implementation against the provided Figma design.

🎬 **Video Reference:** [`PreviewCompareVideo.mp4`](./PreviewCompareVideo.mp4)
<video width="100%" controls poster="./assets/video-poster.png">
  <source src="./PreviewCompareVideo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

> _The video showcases all sections (Hero, Product Info, Science, Footer) across desktop and mobile breakpoints, verifying responsiveness and fidelity._

---
## 🧭 Project Approach

Our approach was guided by three key principles:

### 1. **Scalability Through Modularity**
Each section was built as an **independent, self-contained component** (`.liquid` + `.css`), allowing developers to reuse or update sections without affecting others.  
CSS uses **global tokens** (spacing, color, font, gradients) for consistency and easier theming.

### 2. **Performance and Professionalism**
- Minimal dependencies — no JavaScript libraries.  
- Layouts rely on `flex` and `gap` instead of excessive margin stacking.  
- Responsiveness achieved through mobile-first CSS with precise breakpoints.  
- Accessibility considerations like `aria-labels`, semantic HTML, and `alt` attributes.  
- Code validated using Shopify’s `theme-check`.

### 3. **Maintainability**
- Consistent naming convention: all custom sections are prefixed with `cora-`.  
- Global CSS variables for color, typography, and spacing.  
- Gradient tokens defined once and reused.  
- Cleanly structured Liquid schema for each section, fully configurable via Theme Editor.

---

## 🧩 Included Sections

| Section | File | Purpose |
|----------|------|----------|
| **Cora Hero** | `/sections/cora-hero.liquid` | Primary hero banner with gradient heading, social proof, and responsive layout. |
| **Cora Product Info** | `/sections/cora-product-info.liquid` | Center-aligned product introduction section with heading, description, and CTA. |
| **Cora Science** | `/sections/cora-science.liquid` | Left image, right content section emphasizing science-backed features. |
| **Cora Footer** | `/sections/cora-footer.liquid` | Professional footer with menus, social icons, payment methods, and color customization. |

---

## 🧱 File Structure

The project follows a modular architecture — each section has its own `.liquid` and `.css` file for maintainability.  
All icons are stored as snippets, and design tokens live inside `global.css`.

```plaintext
cora-theme/
│
├── assets/          # Stylesheets and global tokens
│   ├── cora-hero.css
│   ├── cora-product-info.css
│   ├── cora-science.css
│   ├── cora-footer.css
│   └── global.css
│
├── sections/      # Custom Shopify 2.0 sections
│   ├── cora-hero.liquid
│   ├── cora-product-info.liquid
│   ├── cora-science.liquid
│   └── cora-footer.liquid
│
├── snippets/     # SVG icons and reusable snippets
│   ├── icon-medical.liquid
│   ├── icon-union.liquid
│   ├── icon-union-two.liquid
│   ├── icon-facebook.liquid
│   ├── icon-instagram.liquid
│   ├── icon-linkedin.liquid
│   └── icon-x.liquid
├──

```

## ⚙️ Implementation Guide

1. Copy each section file (`.liquid`) into your Shopify theme `/sections` directory.  
2. Upload the related CSS files to `/assets`.  
3. Add icon snippets to `/snippets`.  
4. Add the sections via Shopify **Theme Customizer → Add Section → Cora Custom Sections**.  
5. Configure fonts and global tokens in `global.css`.

---

## 🎨 Global Design Tokens

All sections depend on a shared global token system defined in `/assets/global.css`:

```css
:root {
  /* Typography */
  --font-family-heading: "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-body: "Product Sans", sans-serif;

  /* Colors */
  --color-bg: #ffffff;
  --color-heading: #1b1b1b;
  --color-body: #444444;

  /* Gradients */
  --gradient-one: linear-gradient(90deg, #8C8DC6, #282460);
  --gradient-two: linear-gradient(90deg, #090810, #ffffff, #ffffff, #090810);

  /* Spacing */
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 40px;
  --space-2xl: 64px;
  --space-3xl: 96px;
}

```


## 🧩 Section Details


### 1. **Cora Hero Section**

A high-impact hero banner for the homepage — designed to capture attention with gradient typography, social proof, and mobile-responsive imagery.

**Key Features**
- Dual images (Desktop + Mobile)
- Badge with embedded SVG icons
- Gradient heading using `[highlight]` shortcode
- Social proof avatars with text
- Responsive button group with equal width

**Example Configurable Fields**

| Field | Description |
|--------|-------------|
| **Badge Text** | Small label shown above the heading with optional icons |
| **Heading** | Supports `[highlight]` shortcode for gradient-styled text |
| **Description** | Rich text description with support for line breaks |
| **CTA Buttons** | Two customizable CTAs — Primary and Secondary |
| **Hero Images** | Separate uploads for Desktop and Mobile versions |

---

### 2. **Cora Product Info Section**

A clean, centered section used to introduce the product — focuses on clarity, simplicity, and alignment with brand typography.

**Key Features**
- Minimal, centered layout
- Gradient heading text (applied to text, not background)
- Product image with soft shadow
- Centered CTA button below description

**Example Configurable Fields**

| Field | Description |
|--------|-------------|
| **Subheading** | Optional label for context above the main title |
| **Heading** | Supports gradient text using `var(--gradient-one)` |
| **Description** | Short product overview or marketing message |
| **Product Image** | Main product visual (supports `.png` / `.jpg` / `.webp`) |
| **CTA Button** | “Buy Now” or custom link to the product page |

---

✨ _Both sections are mobile-first, built with flex and gap for alignment, and styled with global design tokens for consistent typography and color theming._




## 📱 Responsive Behavior

- Centered text layout  
- Images scale within their containers  
- Text and CTA grouped using **flex** + **gap** (no margin stacking)

---

## 3. **Cora Science Section**

A storytelling component designed to explain the science or logic behind the product.  
Features an image anchored to the **left** (absolute positioning) and a **content column** on the right.

**Key Features**
- Left-anchored image (absolute positioning)
- Right-aligned text column
- Gradient heading text
- Fully responsive — collapses into single column on mobile

**Configurable Fields**

| Field | Description |
|--------|-------------|
| **Subheading** | Optional top label above the main heading |
| **Heading** | Supports `[highlight]` shortcode for gradient text |
| **Description** | Paragraph or rich text field |
| **Image** | Upload for left-side visual element |
| **CTA** | Button label and link |

---

## 4. **Cora Footer Section**

A flexible four-column footer designed to host navigation links, social profiles, and payment icons.  
It supports configurable background colors and dynamic menu linking via Shopify’s editor.

**Key Features**
- Four-column layout (Shop, Help, About, More)
- Integrated social media icons
- Auto-rendered payment icons
- Configurable background color

**Customizable Fields**

| Field | Description |
|--------|-------------|
| **Menus** | Up to four Shopify menus |
| **Social Links** | Add URLs for Facebook, Instagram, LinkedIn, and X |
| **Payment Icons** | Automatically generated via Shopify payment types |
| **Footer Background** | Selectable color (via theme color picker) |

---

## 📱 **Responsive Behavior Summary**

| Device | Layout Behavior |
|---------|-----------------|
| **Desktop** | Two- or four-column layouts with consistent spacing |
| **Tablet (≤1024px)** | Columns adjust or stack gracefully |
| **Mobile (≤600px)** | Single-column layout with image above text |
| **Buttons** | Expand to full width on smaller screens |
| **Images** | Scale responsively while maintaining aspect ratio |

---

## 🧩 **Dependencies & Requirements**

| Dependency | Details |
|-------------|----------|
| **Shopify Online Store 2.0** | Required for dynamic, JSON-based sections |
| **Global CSS Tokens** | Ensure `global.css` is included in `/assets/` for colors, spacing, and typography |
| **Snippets** | All referenced SVG icons must exist in `/snippets/` |
| **Fonts** | Headings use *Helvetica Neue*, body text uses *Product Sans* |

---

## ✅ **Evaluation Notes**

- Built entirely in **Liquid + CSS** (no JavaScript dependencies)  
- Follows a **mobile-first, responsive** design system  
- Uses **flex and gap** instead of margin stacking  
- Fully compliant with **Shopify’s theme-check** standards  
- **Gradient applied only to text**, not background  
- All images include explicit `width` and `height` attributes for performance and CLS optimization  

---

## 🧠 **Summary**

This project demonstrates a **modular, scalable, and production-ready** Shopify section architecture:

- Clean, maintainable Liquid structure  
- Global design tokens for consistent theming  
- Responsive, mobile-first layout system  
- Editor configurability for all key components  
- Real-world alignment with **Shopify Online Store 2.0** standards  

Each section is optimized for performance, accessibility, and scalability — ready for real-world deployment and evaluation.



