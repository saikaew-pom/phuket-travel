# 📝 Blog Post & Guide Workflow: PHUKET TRAVEL 101

This document outlines the standard workflow and technical requirements for adding new blog posts or travel guides to the platform. Follow this guide to ensure 99+ Lighthouse scores and UI consistency.

---

## 🏗️ 1. File Setup & Metadata
- **File Naming:** Use kebab-case (e.g., `phi-phi-island-guide.html`).
- **Template:** Start by copying `patong-beach-guide.html` as it contains all standard components.
- **SEO Head Section:**
    - Unique `<title>` (Max 60 chars).
    - Unique `<meta name="description">` (150-160 chars).
    - Update Open Graph (`og:`) and Twitter tags with the correct URL and image path.
    - **JSON-LD Schema:** Update the `Article` schema in the `<script type="application/ld+json">` block.

## 🎨 2. Visuals
- **Hero Image:** 
    - Dimensions: Aspect ratio ~16:9.
    - Location: Store in `/images/`.
    - Optimization: Use `.webp` or compressed `.png`/`.jpg`.
    - Accessibility: Always provide a descriptive `alt` attribute.

## 🧩 3. Standard UI Components (Mandatory)
Every new page MUST include these exact blocks:

### A. Header (Navigation)
Use the standard `<nav>` block from `index.html`.
```html
<nav class="fixed top-0 left-0 right-0 z-50 px-4 md:px-6 py-4">...</nav>
```

### B. Social Sharing
Place this block immediately after the article content.
```html
<!-- Social Sharing -->
<div class="mt-16 pt-8 border-t border-gray-100">...</div>
```

### C. Related Guides
Place this block after Social Sharing. Use 3 relevant internal links.
```html
<!-- Related Guides -->
<div class="mt-24">
    <h2 class="text-2xl font-black tracking-tight mb-8">Related Guides</h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">...</div>
</div>
```

### D. Footer
Use the standard `<footer>` block from `index.html`.
```html
<footer class="bg-black text-white py-20 md:py-24 px-4 md:px-6">...</footer>
```

## 📜 4. Scripting
Ensure the bottom of the `<body>` contains the unified mobile menu script:
```javascript
<script>
    const menuBtn = document.getElementById('menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');
    const menuIcon = document.getElementById('menu-icon');

    menuBtn?.addEventListener('click', () => {
        const isHidden = mobileMenu.classList.contains('hidden');
        if (isHidden) {
            mobileMenu.classList.remove('hidden');
            menuIcon.setAttribute('d', 'M6 18L18 6M6 6l12 12');
        } else {
            mobileMenu.classList.add('hidden');
            menuIcon.setAttribute('d', 'M4 6h16M4 12h16m-7 6h7');
        }
    });

    document.addEventListener('click', (e) => {
        if (menuBtn && !menuBtn.contains(e.target) && mobileMenu && !mobileMenu.contains(e.target)) {
            mobileMenu.classList.add('hidden');
            menuIcon.setAttribute('d', 'M4 6h16M4 12h16m-7 6h7');
        }
    });
</script>
```

## ✅ 5. Pre-Publish Checklist
1. [ ] **Internal Links:** Does the page link to at least 2 other guides?
2. [ ] **Image Alt Text:** Are all images described for accessibility?
3. [ ] **Tailwind Build:** If you added new utility classes, run the build command:
   `npx -y @tailwindcss/cli -i input.css -o styles.css --minify`
4. [ ] **Sitemap:** Add the new URL to `sitemap.xml`.
5. [ ] **Lighthouse Check:** Open in Chrome DevTools and verify 95+ scores for Performance and SEO.
