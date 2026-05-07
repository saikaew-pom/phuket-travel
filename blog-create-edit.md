# Blog Create/Edit Workflow

Use this project workflow when creating or editing a Phuket Travel 101 blog article.

## 1. Inspect Existing Patterns

- Read the closest existing blog article HTML before editing.
- Match the current layout, typography, navigation, footer, related guides, schema, canonical URL, and WhatsApp CTA pattern.
- Check `blog.html`, `index.html`, and `sitemap.xml` for how articles are listed.

## 2. Create or Edit the Blog Page

- For new long-form articles, copy `master-blog-template.html` to the final article slug first.
- Replace every `TEMPLATE_*` token before publishing.
- Use a clear SEO title, meta description, canonical URL, Open Graph image, and article JSON-LD.
- Keep article structure scannable with useful headings.
- Build internal links naturally into the body content so each article acts as a bridge to other relevant Phuket Travel 101 guides.
- Add related guide cards that match the site style.
- Prefer existing CSS/classes and local patterns over new styling.

## 2A. Internal Linking Requirements

- Before writing or editing the article, scan `blog.html`, `sitemap.xml`, and relevant existing blog files to identify related articles.
- Add contextual internal links inside paragraphs where they genuinely help the reader continue planning.
- Use descriptive anchor text, not generic text such as "click here" or "read more".
- Prioritize links to high-intent related guides, such as transport, beaches, weather, budget, itinerary, visa, money exchange, packing, and local etiquette pages.
- Include at least 3-5 contextual internal links in a long-form article when relevant.
- Also update the "Related Guides" cards with 3 strong internal destinations.
- Do not force links into unrelated sections. Relevance matters more than count.
- When editing an existing blog, look for missed bridge opportunities to newer articles and add them where natural.

Good examples:

```html
If you plan to move around the island without a scooter, read our <a href="grab-vs-bolt-indrive-guide.html">Phuket ride-hailing guide</a> before booking a remote hotel.
```

```html
For a full week plan that balances culture, beaches, and islands, use our <a href="phuket-7-day-itinerary.html">7-day Phuket itinerary</a> as your starting point.
```

Avoid:

```html
For more information, <a href="blog.html">click here</a>.
```

## 3. Generate Blog Images

- Generate a feature image for the article.
- Generate 3-4 body images when the article benefits from supporting visuals.
- Save final images into `images/` with descriptive filenames.
- Use absolute image URLs in HTML:

```html
https://phukettravel101.com/images/example-image.png
```

Update all relevant locations:

- `<img src="...">`
- `og:image`
- Twitter image metadata
- JSON-LD `"image"`
- Blog card image data
- Related guide thumbnails, if changed

## 4. Upload Images to Cloudflare R2

- Upload new image files from `images/` to the `phukettravel101` R2 bucket.
- Preserve object keys such as:

```text
images/example-image.png
```

- Do not paste long-lived secrets into chat. Prefer local environment variables, local config, or a freshly rotated temporary key.
- After upload, test at least one public URL:

```bash
curl -I https://phukettravel101.com/images/example-image.png
```

Expected result: `HTTP 200` with the correct image content type.

## 5. Update Site Discovery

- Add or update the article entry in `blog.html`.
- Add homepage placement in `index.html` only when appropriate.
- Add or update the URL in `sitemap.xml`.
- Confirm the canonical URL matches the final file name.

## 6. Verify Before Completion

Run targeted checks:

```bash
rg --pcre2 -n "(?<!phukettravel101\\.com/)images/" --glob "*.html"
git diff --stat
git status -sb
```

For new article images, confirm:

- Local image files exist in `images/`.
- Public image URLs return `HTTP 200`.
- HTML references use `https://phukettravel101.com/images/...`.
- The article is linked from `blog.html`.
- `sitemap.xml` includes the article URL.

## 7. Commit and Push

- Stage only intended files.
- Commit with a clear message, for example:

```bash
git commit -m "Add Phuket [topic] guide"
```

- Push to GitHub:

```bash
git push origin main
```

Repository:

```text
https://github.com/saikaew-pom/phuket-travel
```
