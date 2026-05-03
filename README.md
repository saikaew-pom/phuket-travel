# 🏝️ PHUKET TRAVEL 101 - The Ultimate Standalone Travel Guide

A high-performance, SEO-optimized, standalone travel platform built with **Vanilla HTML5, CSS, and JS**. This project serves as a comprehensive guide for travelers visiting Phuket in 2026, featuring interactive tools and expert-curated content.

## 🚀 Quick Start
To view the site locally, simply open `index.html` in any modern web browser. 

For development (Tailwind CSS compilation):
1. Ensure you have Node.js installed.
2. Run the build command to update styles:
   ```bash
   npx -y @tailwindcss/cli -i input.css -o styles.css --minify
   ```

## 🛠️ Tech Stack
- **Architecture**: Pure Vanilla (No frameworks) for 99+ Performance Scores.
- **Styling**: Tailwind CSS 4.0 with Custom Glass-morphism Utilities.
- **Interactivity**: Modern ES6+ JavaScript.
- **SEO**: Advanced JSON-LD (Schema.org), Open Graph, and Twitter Metadata.
- **Typography**: Plus Jakarta Sans.

## 📁 Project Structure

### 🧠 Interactive Tools
- **Beach Finder** (`beach-finder.html`): Filterable discovery tool for Phuket's 30+ beaches.
- **Budget Calculator** (`budget-calculator.html`): Real-time expense estimator for 2026 prices.
- **Visa Checker** (`visa-checker.html`): Automated entry requirements tool (incl. TDAC info).
- **HKT Transfer Tool** (`airport-transfer-guide.html`): Fare estimator for airport transfers.

### 📖 Essential Guides
- **Transport**: `grab-vs-bolt-indrive-guide.html`, `airport-transfer-guide.html`.
- **Logistics**: `money-exchange-guide.html`, `phuket-entry-guide-2026.html`.
- **Culture & Costs**: `tipping-guide.html`, `phuket-cost-guide-2026.html`, `elephant-sanctuaries.html`, `old-town-cafes.html`.

### 🏖️ Beach Guides (Detailed)
- `patong-beach-guide.html` - The Hub
- `kata-beach-guide.html` - Family Favorite
- `surin-beach-guide.html` - Natural Elegance
- `bang-tao-beach-guide.html` - Luxury & Space
- `nai-harn-beach-guide.html` - Local Gem
- `mai-khao-beach-guide.html` - Peace & Quiet
- `hidden-coves.html` - Secret Spots

## 📊 Analytics Setup (GA4)
To enable Google Analytics 4 tracking:
1. Obtain your **Measurement ID** (G-XXXXXXXXXX) from the Google Analytics dashboard.
2. Insert the tracking script into the `<head>` of all HTML files.
3. *Note: The Gemini CLI can automate this batch insertion for you.*

## 📈 SEO & Maintenance
Every new page should follow the template found in `surin-beach-guide.html`:
1. **Title/Meta**: Must be unique and include "PHUKET TRAVEL 101".
2. **Schema**: Update the `Article` or `WebApplication` JSON-LD block.
3. **Sitemap**: Add new URLs to `sitemap.xml` and update the `lastmod` date.

---
© 2026 PHUKET TRAVEL 101 • Optimized for the 2026 Travel Season.
