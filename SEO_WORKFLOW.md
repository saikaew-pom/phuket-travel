# 🔍 SEO Workflow: PHUKET TRAVEL 101

Maintaining a 95+ SEO score on Lighthouse and ranking for high-intent keywords in 2026 requires a disciplined approach. This document outlines the mandatory SEO steps for every page on the platform.

---

## 🏗️ 1. On-Page Metadata (The "Head" Section)
Every page must have unique and descriptive metadata.

- **Title Tag:** 50–60 characters. Format: `[Primary Keyword] | PHUKET TRAVEL 101`.
- **Meta Description:** 150–160 characters. Must include a call-to-action (CTA) and the primary keyword.
- **Canonical URL:** Always include `<link rel="canonical" href="https://phukettravel101.com/[page-name].html">` to prevent duplicate content issues.

## 🏷️ 2. Semantic HTML & Content Hierarchy
Search engines use headers to understand page structure.
- **H1 Tag:** Exactly one per page. Must contain the primary keyword.
- **H2-H4 Tags:** Use for sub-sections. Maintain a logical hierarchy (don't skip levels).
- **Internal Linking:** Every new post should link to at least **2 existing pages** and be linked TO by at least **1 existing page**.

## 🤖 3. Technical SEO & Schema.org
We use advanced JSON-LD to help Google understand our content.

### A. JSON-LD Implementation
- **For Guides/Articles:** Use the `Article` or `TravelGuide` schema.
- **For Tools:** Use `SoftwareApplication` or `WebApplication` schema.
- **Checklist:** Ensure `author` is always "Pom" and `publisher` is "PHUKET TRAVEL 101".

### B. Image Optimization
- **File Names:** Use descriptive names (e.g., `beach-patong-sunset.jpg` instead of `IMG_123.jpg`).
- **Alt Text:** Mandatory for all images. Describe the image accurately while incorporating secondary keywords where natural.
- **Lazy Loading:** Use `loading="lazy"` for all images below the fold to maintain performance.

## 📱 4. Social SEO (Open Graph & Twitter)
Ensure content looks professional when shared on social media.
- **og:image:** Must be a high-quality 1200x630px image.
- **og:title & og:description:** Can mirror the page metadata but should be optimized for click-throughs on social feeds.

## 📊 5. Analytics & Indexing
- **GA4:** Ensure the Global Site Tag (`G-DTC7ZR7JVK`) is present in the `<head>` of every page.
- **Sitemap:** Every new page must be added to `sitemap.xml` with a `priority` of 0.80 and `monthly` change frequency.
- **Robots.txt:** Verify that no critical pages are being blocked.

## ✅ 6. SEO Validation Checklist
Before considering a page "Done", verify the following:
1. [ ] **Lighthouse:** SEO score is 100/100.
2. [ ] **Rich Results Test:** Pass the JSON-LD through [Google's Rich Results Test](https://search.google.com/test/rich-results).
3. [ ] **Mobile Friendly:** Verify the page is fully responsive and "touch-friendly" for mobile users.
4. [ ] **Keywords:** Primary keyword appears in Title, H1, first paragraph, and at least one H2.
5. [ ] **Broken Links:** Verify all internal and external links are active.
