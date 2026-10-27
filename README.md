# celesium-site

Brand website for **CelesiumAI LLC**, the technology arm of Celesium Capital.

Live at: [celesium.ai](https://celesium.ai)

## Stack

Static HTML / CSS / vanilla JS. Shared styles (tokens, nav, footer, page hero, buttons) live in `css/site.css`; each page's `<style>` block holds only what is specific to that page, plus the scroll-reveal rules, which must come after the page's own rules. The privacy page has its own minimal styles. Deployed on Vercel, with one serverless function for the contact form.

## Structure

```
.
├── index.html          Home
├── portfolio.html      Solutions: the nine live platforms
├── approach.html       How it works: proof chain, build sequence, boundaries
├── security.html       Security & trust
├── leadership.html     Leadership team and company structure
├── contact.html        Demo request form + office info
├── privacy.html        Privacy policy
├── api/contact.js      Contact form handler (sends via Resend)
├── css/fonts.css       Self-hosted fonts (files in fonts/)
├── css/site.css        Shared styles for every page except privacy
├── img/                Share images (og-<page>.jpg, 1200×630) and platform card art (<platform>.svg)
├── scripts/smoke.mjs   Build check (run by Vercel as `npm run build`)
├── favicon.svg
├── robots.txt
├── sitemap.xml
├── vercel.json         cleanUrls, /library rewrite, security headers
└── .archive/v1/        Previous version of the site (not deployed)
```

## Local preview

The site uses clean URLs (`/portfolio`, not `/portfolio.html`), so use a server that supports them:

```bash
npx serve .
# then open http://localhost:3000
```

`/library` is proxied to a separate app in production and won't load locally.

## Build check

```bash
npm ci
npm run smoke
```

Checks that every page parses, `sitemap.xml` is valid, `api/contact.js` has valid syntax, and every internal link resolves to a file. Vercel runs it on every deploy, so a broken link fails the build.

## Deploy

Pushes to `main` auto-deploy to production on Vercel. Pushes to any other branch create a preview URL (behind Vercel login).

## Contact form

`contact.html` POSTs to `/api/contact`, which emails the submission through [Resend](https://resend.com). Environment variables in Vercel:

- `RESEND_API_KEY` (required)
- `NOTIFICATION_EMAIL`: where submissions go (defaults to `pphan@celesium.com`)

## Design tokens

Defined in each page's `:root`:

- Ink (dark sections): `#141720` · Warm background: `#F7F6F3`
- Accents: teal `#0D7377` / `#12978C`, ocean `#1A6B9A`, violet `#6B5CE7`, bronze `#C49A3C`
- Type: Inter (text), JetBrains Mono (labels and stats)
