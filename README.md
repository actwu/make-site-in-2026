# make-site-in-2026

[With Clerk and DB Liveblocks](oth.md)

A practical reference for building a modern website or web system from scratch. Covers the full stack: auth, realtime, SEO, analytics, security, and web standards.

---

## Basics
<details>
  <summary><strong>Expand</strong></summary>
  <br>

  1. `index.html` is first file
  2. `404.html` is all path file

  Codes is here
  [github.new](github.new)
  - Private pls
  - put your `index.html` here.

  Deploy is here
  [vercel.com](vercel.com)
  1. Project 
  2. Import
  
</details>


## 1. What we will use. at a Glance
<details>
  <summary><strong>Expand</strong></summary>
  <br>
  
| What | Tool | Link |
|------|------|------|
| SEO | SEO Generator | https://actwu.github.io/gen/seo/ |
| Analytics | Google Search Console | https://search.google.com/search-console |
| Security | YN Security Patch | 
  
</details>
---

## 2. Development Flow

<details>
  <summary><strong>Expand</strong></summary>
  <br>
  
1. Build the site or system
4. Generate and fill in SEO metadata
5. Submit the sitemap to Google Search Console
6. Monitor performance and indexing
7. Iterate on SEO and UX
8. Scale features based on analytics

</details>
---

---

## SEO

<details>
  <summary><strong>Expand</strong></summary>
  <br>
Use the generator to fill in all metadata fields before going live.

**Generator:** https://actwu.github.io/gen/seo/

**Template to fill in:**

```html
<title>Site Name</title>

<meta name="description" content="">
<meta name="keywords" content="">
<meta name="author" content="">
<meta name="robots" content="index, follow">
<meta name="googlebot" content="index, follow">
<meta name="referrer" content="no-referrer-when-downgrade">

<link rel="icon" href="">
<link rel="canonical" href="">

<meta property="og:title" content="">
<meta property="og:description" content="">
<meta property="og:image" content="">
<meta property="og:url" content="">
<meta property="og:type" content="">
<meta property="og:site_name" content="">
<meta property="og:locale" content="">

<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="">
<meta name="twitter:description" content="">
<meta name="twitter:image" content="">
<meta name="twitter:site" content="">
<meta name="twitter:creator" content="">

<meta name="google-site-verification" content="">
<meta name="msvalidate.01" content="">

<link rel="manifest" href="manifest.json">

<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Organization","name":"","url":"","logo":"","description":""}
</script>
```

</details>

## Prompt

<details>
  <summary><strong>Expand</strong></summary>
  <br>
  
**Sample prompt to generate SEO:**

```
 One file 
 website, Simple, Flat, Minimal
--

Tailwind, CSS, Iconify CDN use Mingcute, JS, Html
--

Make me my seo

<title> MY title </title>

<title></title>
<meta name="description" content="">
<meta name="keywords" content="">
<meta name="author" content="">
<meta name="robots" content="index, follow">
<meta name="googlebot" content="index, follow">
<meta name="referrer" content="no-referrer-when-downgrade">
<link rel="icon" href="">
<link rel="canonical" href="">
<meta property="og:title" content="">
<meta property="og:description" content="">
<meta property="og:image" content="">
<meta property="og:url" content="">
<meta property="og:type" content="">
<meta property="og:site_name" content="">
<meta property="og:locale" content="">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="">
<meta name="twitter:description" content="">
<meta name="twitter:image" content="">
<meta name="twitter:site" content="">
<meta name="twitter:creator" content="">

<meta name='google-site-verification' content=''>
<meta name='msvalidate.01' content=''>

<link rel="manifest" href="manifest.json">

<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Organization","name":"","url":"","logo":"","description":""}</script>

--

The navigation is compress and remains fully transparent while the user is inside the hero fold, 
smoothly fade to navigation and into the background once they scroll down past hero.

Hero with Video as Background 
Cycle this video with fade then play again
https://cdn.pixabay.com/video/2022/09/30/133133-755975202_large.mp4
https://cdn.pixabay.com/video/2023/08/17/176489-855554923_large.mp4


Hero content is on bottom left
3 Content only
- Title
- Tagline
- CTA

--

Here is the setup 
- Video Hero
- Trust Badges
- Featured In
- About
- Services / Products
- Benefits
- How It Works
- Results
- Testimonials
- Case Studies
- Team
- FAQ
- Contact
- Footer


--



One file
```

---

</details>

## Analytics — Google Search Console

https://search.google.com/search-console

Submit your sitemap here after launch. Monitors search performance, index coverage, Core Web Vitals, and search appearance.

<details>
  <summary><strong>Expand</strong></summary>
  <br>
  
**Post-launch checklist:**
- Submit `sitemap.xml`
- Verify ownership via meta tag or DNS
- Check index coverage for errors
- Monitor Core Web Vitals (LCP, INP, CLS)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>http://ynpasc.vercel.app</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/press</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/privacy</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/terms</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-1-subscription-1</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-2-subscription-2</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-3-subscription-3</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-4-subscription-4</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-5-subscription-5</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-6-subscription-6</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-1-subscription-1/join</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-2-subscription-2/join</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-3-subscription-3/join</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-4-subscription-4/join</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-5-subscription-5/join</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>http://ynpasc.vercel.app/provider-6-subscription-6/join</loc>
    <lastmod>2011-12-06T17:38:21+00:00</lastmod>
    <priority>0.5</priority>
    <changefreq>weekly</changefreq>
  </url>
</urlset>
```
---

</details>


<details>
  <summary><strong>Expand</strong></summary>
  <br>
  
## Security — YN Security Patch

Drop this into every page. Loads before content via `defer`.

Base Flavor 
```html
<security-yn1>
  <link rel="preconnect" href="https://ynpasc.vercel.app" crossorigin>
  <link rel="preload" href="https://ynpasc.vercel.app/security/patch/public/base.js" as="script">
  <script defer src="https://ynpasc.vercel.app/security/patch/public/base.js"></script>
</security-yn1>
```

One Flavor

```html
<security-yn1>
  <link rel="preconnect" href="https://ynpasc.vercel.app" crossorigin>
  <link rel="preload" href="https://ynpasc.vercel.app/security/patch/public/one.js" as="script">
  <script defer src="https://ynpasc.vercel.app/security/patch/public/one.js"></script>
</security-yn1>
```

---

</details>


## Web Standards Checklist

A condensed version of the full spec at https://websitechecklists.io.

<details>
  <summary><strong>Expand</strong></summary>
  <br>
  
### Foundations (Required)

- `<!doctype html>` as the very first line
- `<html lang="en">` with a valid BCP 47 language tag
- `<meta charset="UTF-8">` within the first 1024 bytes
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- A non-empty `<title>` element
- `rel="canonical"` on every page

### SEO (Recommended)

- `robots.txt` at site root
- `sitemap.xml` submitted to Search Console
- Clean URL structure: lowercase, hyphenated, shallow
- Proper 301/308 redirects for any moved content
- Server-side rendered primary content (not client-side only)
- JSON-LD structured data on key pages
- No soft 404s (pages that return 200 but show a not-found message)

### Accessibility (Required)

- Sufficient color contrast on all text
- `alt` attributes on every `<img>`
- Labels on every form input
- Full keyboard navigation, no focus traps
- Visible focus indicators
- Skip-to-content link as the first focusable element
- Semantic HTML: `<header>`, `<nav>`, `<main>`, `<footer>`
- Descriptive link text (no "click here")
- `<html lang>` set correctly
- `prefers-reduced-motion` respected

### Security (Required)

- HTTPS on all pages, HTTP redirects to HTTPS
- `Strict-Transport-Security` header with `max-age`, `includeSubDomains`, `preload`
- `X-Content-Type-Options: nosniff`
- `Content-Security-Policy` header
- Clickjacking protection via `frame-ancestors` CSP directive
- Cookies set with `Secure`, `HttpOnly`, `SameSite`

### Performance (Required)

- Images in WebP or AVIF with explicit dimensions
- Cache-Control headers: immutable + long max-age for fingerprinted assets
- Compressed responses (brotli or gzip)
- LCP under 2.5s, INP under 200ms, CLS under 0.1

### Agent Readiness (Recommended)

- `robots.txt` entries for known AI crawlers
- JSON-LD structured data matching schema.org
- Stable, permanent URLs
- `/llms.txt` file at site root listing key pages

---

</details>


<details>
  <summary><strong>Expand</strong></summary>
  <br>
Please Rounded Button

Copy-paste button style for any dark UI.

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 10px 20px;
  border-radius: 999px;
  border: none;
  background: #ffffff;
  color: #131314;
  font-weight: 700;
  font-size: 14px;
  cursor: pointer;
  box-shadow:
    inset 0 1px 0 rgba(255,255,255,0.15),
    0 2px 8px rgba(0,0,0,0.4);
  transition: opacity 0.15s ease;
}

.btn:hover { opacity: 0.85; }
.btn:active { opacity: 0.7; }

.btn-dark {
  background: #1e1e1e;
  color: #ffffff;
}
```

```html
<button class="btn">Get Started</button>
<button class="btn btn-dark">Learn More</button>
```

</details>
