# Blog Create/Edit Workflow

Use this workflow when creating or updating a Phuket Travel 101 blog article.

The goal is simple:

- produce strong original content
- keep the technical SEO clean
- avoid duplicate work
- finish with one reliable verification pass

## Core Principles

- Match the current site pattern before inventing anything new.
- Prefer one clean workflow over multiple optional branches.
- Use internal links and related guides to turn each article into a bridge to other useful pages.
- Keep visuals intentional. Generate new images only when they materially improve the article.
- Verify changing facts before publishing. Topics like visas, regulations, prices, and tools can age quickly.

## 1. Start With Repo Context

Before editing:

1. Check repo state with `git status -sb`.
2. Confirm `origin` still points to the Phuket Travel 101 repo.
3. Read the closest matching live article and `master-blog-template.html`.
4. Check `blog.html`, `index.html`, and `sitemap.xml` so you know how the article should be surfaced.

Use `master-blog-template.html` by default for a new long-form article.

If a newer live article is a better structural match than the master template, copy that article instead and adapt it carefully.

## 2. Decide The Article Scope Before Writing

Before touching HTML, decide:

- the target search intent
- the reader type
- whether the topic depends on changing facts
- whether the article really needs new images
- which 3-5 internal links will naturally help the reader next

Every article should answer one main decision clearly. Do not overload one article with multiple unrelated goals.

## 3. Build The Page

For new articles:

1. Copy `master-blog-template.html` to the final slug.
2. Replace every `TEMPLATE_*` token.
3. Keep the current site layout, navigation, footer, WhatsApp CTA, schema pattern, and related guides style.

For edited articles:

1. Preserve the existing working layout unless the redesign is intentional.
2. Look for outdated metadata, weak internal links, broken image paths, and stale factual claims.

Required technical fields:

- unique `<title>`
- unique meta description
- canonical URL matching the final filename
- Open Graph title, description, and image
- Twitter image metadata
- valid JSON-LD
- one clear `h1`

Required content quality:

- strong opening that explains who the article is for
- scannable sections with useful subheads
- practical local context, not generic travel filler
- natural internal links inside the body
- 3 related guide cards that actually fit the topic
- article-specific WhatsApp CTA copy when appropriate

## 4. Internal Linking Rules

Each article should help the reader take the next useful step.

Do this:

- scan `blog.html`, `sitemap.xml`, and relevant live guides before writing
- add 3-5 contextual internal links in long-form articles when relevant
- use descriptive anchor text
- update related guide cards with 3 strong destinations
- when editing older posts, add links to newer relevant articles where natural

Prioritize high-intent links such as:

- transport
- beaches
- weather
- budget
- itinerary
- entry or visa guides
- money exchange
- packing
- local etiquette

Good example:

```html
If you plan to move around the island without a scooter, read our <a href="grab-vs-bolt-indrive-guide.html">Phuket ride-hailing guide</a> before booking a remote hotel.
```

Avoid generic anchors:

```html
For more information, <a href="blog.html">click here</a>.
```

## 5. Image Strategy

Only create new images when they improve the page meaningfully.

Typical use:

- feature image for new flagship or pillar articles
- 3-4 body images for long-form visual guides
- no forced image generation for every article

Save generated working files in:

```text
images/generated/
```

Use descriptive filenames such as:

```text
images/generated/kata-family-sunrise-1600.jpg
```

Image quality rules:

- use natural alt text
- include width and height
- use `loading="lazy"` for body images
- use `fetchpriority="high"` only for the main hero image

## 6. Image URL Rules

This repo currently uses two valid production image patterns:

1. First-party site images:

```text
https://phukettravel101.com/images/example-image.jpg
```

2. Public Cloudflare R2 image URLs:

```text
https://pub-<bucket-id>.r2.dev/images/generated/example-image.jpg
```

Use one rule consistently inside a given article.

Recommended default:

- existing site asset already in `/images`: use `https://phukettravel101.com/images/...`
- newly generated article images uploaded to R2: use the live R2 URL that returns `200`

After choosing the final image URL, update all relevant locations:

- `<img src="...">`
- `og:image`
- Twitter image metadata
- JSON-LD `"image"`
- blog card image entry in `blog.html`
- related guide thumbnails, if changed

Do not leave local workspace paths in published HTML.

## 7. Upload Images To Cloudflare R2

Only do this when the article uses newly generated images.

Workflow:

1. Upload the final generated files from `images/generated/` to the `phukettravel101` R2 bucket.
2. Preserve object keys such as:

```text
images/generated/example-image.jpg
```

3. Verify the public R2 URL:

```bash
curl -I https://pub-<bucket-id>.r2.dev/images/generated/example-image.jpg
```

Expected result: `HTTP 200` with the correct image content type.

4. Only then update the article to use the live URL.

Secret handling:

- do not paste long-lived secrets into chat
- prefer local environment variables, local config, or CLI login

## 8. Update Site Discovery

For every new article:

1. Add the entry in `blog.html`.
2. Add the URL to `sitemap.xml`.
3. Add homepage placement in `index.html` only if the article deserves explicit homepage presence.
4. Confirm the canonical URL matches the final slug exactly.

For updated articles:

- refresh `blog.html` card copy or image only if the article positioning changed
- update `sitemap.xml` only if the URL changed or you intentionally maintain fresh `lastmod`

## 9. Verification Gate

Run this before calling the article complete.

### Content and Template Checks

```bash
rg -n 'TEMPLATE_' <article>.html
rg -n '\*\*' <article>.html
```

Expected result:

- no `TEMPLATE_` tokens left
- no accidental markdown markers like `**`

### Structure Checks

```bash
rg -o '<h1\\b' <article>.html | wc -l
rg -n '<link rel="canonical"|og:image|application/ld\\+json' <article>.html
```

Expected result:

- exactly 1 `h1`
- canonical, OG image, and JSON-LD all present

### Image Path Checks

Use this to catch local relative image references that were left behind accidentally:

```bash
rg --pcre2 -n '(?<!https://phukettravel101\\.com/)(?<!https://pub-[^"]+\\.r2\\.dev/)images/' --glob '*.html'
```

Review the matches carefully.

The goal is not "zero matches at any cost." The goal is to catch accidental unpublished paths.

### Discovery Checks

Confirm:

- the article is linked from `blog.html`
- `sitemap.xml` includes the article URL

### Diff and Status Checks

```bash
git diff --stat
git diff --check
git status -sb
```

### Optional Factual Check

For topics with changing facts, confirm reliable sources again right before finalizing. Use that research to improve accuracy in the article body, metadata, and recommendations, but do not add a reader-facing "Research Notes," "Editorial Note," or source-log section to the published page.

- visa or entry rules
- legal or tax references
- prices
- transport providers
- opening status

## 10. Quality Bar Before Publish

The article is ready only if all of these are true:

- it answers the search intent clearly
- the opening is useful within the first screenful
- headings are scannable and not repetitive
- internal links help the reader naturally
- related guides are relevant
- metadata is complete and specific
- image URLs are final and working
- structured data is valid
- no placeholder or template tokens remain

## 11. Commit and Push

Stage only intended files.

Example commit:

```bash
git commit -m "Add Phuket [topic] guide"
```

Push:

```bash
git push origin main
```

Repository:

```text
https://github.com/saikaew-pom/phuket-travel
```
