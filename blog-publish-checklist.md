# Blog Publish Checklist

Use this as the fast execution checklist for new or updated Phuket Travel 101 blog articles.

For the full reasoning and standards, see `blog-create-edit.md`.

## 1. Prepare

- Check repo state with `git status -sb`
- Confirm `origin` is correct
- Read the closest matching live article
- Check `blog.html`, `index.html`, and `sitemap.xml`
- Decide whether to start from `master-blog-template.html` or the closest recent article

## 2. Define The Article

- Confirm the target search intent
- Confirm the reader type
- Confirm whether the topic has changing facts that need fresh verification
- Choose 3-5 likely internal links before writing
- Decide whether the article really needs new images

## 3. Build The Article

- Copy template or source article to the final slug
- Replace all `TEMPLATE_*` tokens
- Write a unique `<title>`
- Write a unique meta description
- Set the canonical URL to the final slug
- Set Open Graph title, description, and image
- Set Twitter image metadata
- Keep valid JSON-LD
- Keep exactly 1 `h1`
- Write a strong opening for the target reader
- Keep sections scannable with practical subheads
- Add 3-5 contextual internal links when relevant
- Add 3 related guide cards that fit the topic
- Keep the WhatsApp CTA relevant to the article topic
- Do not add reader-facing "Research Notes," "Editorial Note," or source-log sections

## 4. Handle Images

- Reuse existing site images if they are already strong enough
- Generate new images only when they improve the article meaningfully
- Save new working images to `images/generated/`
- Use natural alt text
- Set width and height
- Use `loading="lazy"` for body images
- Use `fetchpriority="high"` only for the main hero image

## 5. Choose Final Image URLs

- Existing site asset in `/images`: use `https://phukettravel101.com/images/...`
- Newly generated image uploaded to R2: use the live public R2 URL that returns `200`
- Use one consistent image strategy inside the article
- Update image URLs in:
- `<img src="...">`
- `og:image`
- Twitter image metadata
- JSON-LD `"image"`
- `blog.html` card entry
- related guide thumbnails if needed

## 6. Upload To R2 If Needed

Only do this for newly generated images.

- Upload final generated files from `images/generated/`
- Preserve keys like `images/generated/example-image.jpg`
- Use the S3-compatible R2 upload path by default:

```bash
for f in $(git show --name-only --format= HEAD -- images/generated | sort); do
  case "$f" in
    *.jpg) ct='image/jpeg' ;;
    *.png) ct='image/png' ;;
    *) ct='application/octet-stream' ;;
  esac
  code=$(/usr/bin/curl -sS -o /dev/null -w '%{http_code}' \
    -X PUT \
    --aws-sigv4 'aws:amz:auto:s3' \
    --user "$R2_ACCESS_KEY_ID:$R2_SECRET_ACCESS_KEY" \
    --upload-file "$f" \
    -H "Content-Type: $ct" \
    -H "Cache-Control: public, max-age=31536000, immutable" \
    "https://8d3b88fb762aaac5e9feca0421310dfb.r2.cloudflarestorage.com/phukettravel101/$f")
  printf '%s %s\n' "$code" "$f"
done
```

- Upload result should be `200`
- Verify public URL:

```bash
curl -I https://pub-d7a7c52607b0453182010699e6e55dc7.r2.dev/images/generated/example-image.jpg
```

- For batch verification:

```bash
for f in $(git show --name-only --format= HEAD -- images/generated | sort); do
  code=$(/usr/bin/curl -s -o /dev/null -w '%{http_code}' "https://pub-d7a7c52607b0453182010699e6e55dc7.r2.dev/$f")
  printf '%s %s\n' "$code" "$f"
done
```

- Confirm public `HTTP 200` before using the URL in HTML
- Avoid `wrangler r2 object put` unless the Cloudflare API token has confirmed R2 write permission for the correct account

## 7. Update Site Discovery

- Add or update the article entry in `blog.html`
- Add or update the URL in `sitemap.xml`
- Update `index.html` only if homepage placement is appropriate
- Confirm canonical matches the final slug exactly

## 8. Run Final Checks

### Template and content cleanup

```bash
rg -n 'TEMPLATE_' <article>.html
rg -n '\*\*' <article>.html
```

Expected:

- no `TEMPLATE_`
- no accidental markdown markers

### Structure checks

```bash
rg -o '<h1\\b' <article>.html | wc -l
rg -n '<link rel="canonical"|og:image|application/ld\\+json' <article>.html
```

Expected:

- exactly 1 `h1`
- canonical, OG image, and JSON-LD present

### Image path sanity

```bash
rg --pcre2 -n '(?<!https://phukettravel101\\.com/)(?<!https://pub-[^"]+\\.r2\\.dev/)images/' --glob '*.html'
```

Review matches carefully and fix accidental unpublished paths.

### Discovery and diff checks

- Confirm article is linked from `blog.html`
- Confirm article URL is in `sitemap.xml`

```bash
git diff --stat
git diff --check
git status -sb
```

## 9. Quality Gate

Before calling it done, confirm:

- the article answers one clear search intent
- the opening is useful immediately
- headings are scannable
- internal links help the next reader decision
- related guides are relevant
- metadata is complete
- image URLs are final and working
- no placeholders remain
- changing facts were verified if needed

## 10. Commit And Push

- Stage only intended files
- Commit with a clear message
- Push to `origin main`

Example:

```bash
git commit -m "Add Phuket [topic] guide"
git push origin main
```
