# make-site-in-2026

A practical reference for building a modern website or web system from scratch. Covers the full stack: auth, realtime, SEO, analytics, security, and web standards.

---

## 1. What we will use. at a Glance

| What | Tool | Link |
|------|------|------|
| Auth | Clerk | https://clerk.com |
| Realtime | Liveblocks | https://liveblocks.io |
| SEO | SEO Generator | https://actwu.github.io/gen/seo/ |
| Analytics | Google Search Console | https://search.google.com/search-console |
| Security | YN Security Patch | 

---

## 2. Development Flow

1. Build the site or system
 - Add authentication via Clerk
 - Add realtime features via Liveblocks
4. Generate and fill in SEO metadata
5. Submit the sitemap to Google Search Console
6. Monitor performance and indexing
7. Iterate on SEO and UX
8. Scale features based on analytics

---

## Authentication — Clerk

Drop the block below into any page. Fill in `CLERK_PUBLISHABLE_KEY`.

```html
<clerk>
<div id="auth-root"></div>

<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:ital,wght@0,400;0,500;0,700;0,900;1,400&display=swap" rel="stylesheet">
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<style>
clerk {display: unset;}
clerk[active] {background: #131314;height: 100dvh;width: 100dvw;display: flex;top: 0;left: 0;right: 0;bottom: 0;position: fixed;justify-content: center;align-items: center;z-index: 999999;}
clerk #auth-root {display: flex;justify-content: center;padding: 20px;font-family: 'Plus Jakarta Sans', Arial, Helvetica, sans-serif;}
clerk .cl-modalContent,clerk .cl-userButtonPopoverCard,clerk .cl-card,clerk .cl-modalBackdrop,clerk .cl-modalBackdrop::before,clerk .cl-modalBackdrop::after,
clerk .cl-cardBox,clerk .cl-modalContent *,clerk .cl-userButtonPopoverMain *,clerk .cl-userButtonPopoverMain,
clerk .cl-userButtonPopoverCard.cl-card.cl-userButton-popover
{background-color: #131314 !important;color: #fafafa !important;border: none !important;box-shadow: none !important;font-family: 'Plus Jakarta Sans', Arial, Helvetica, sans-serif;}
clerk .cl-formInputInput,clerk .cl-input,clerk .cl-formInputContainer,clerk .cl-selectButton,
clerk .cl-alternativeMethodsButton,clerk .cl-identityPreview
{background-color: #131314 !important;color: #ffffff !important;border: 1px solid #1a1a1b !important;}
clerk .cl-formInputInput:focus,clerk .cl-input:focus {background-color: #1a1a1b !important;border-color: #ffffff !important;}
clerk .cl-formFieldLabel,clerk .cl-formFieldHintText,clerk .cl-formFieldSuccessText,clerk .cl-formFieldErrorText {color: #fafafa !important;}
clerk .cl-navbarButton,clerk .cl-scrollBox,clerk .cl-userButtonPopoverRootBox {color-scheme: dark;color: #ffffff;background-color: #131314 !important;}
clerk .cl-userButtonAvatarBox .cl-avatarBox *,clerk .cl-userPreviewAvatarContainer .cl-avatarBox * {filter: invert(1) hue-rotate(180deg) !important;}
clerk .cl-dividerRow,clerk .cl-dividerLine,clerk .cl-internal-f6u85a,clerk .cl-internal-1dauvpw,clerk .cl-internal-b3fm6y,
clerk [class*="PoweredBy"],clerk .cl-rootBox > .cl-card > div:last-of-type,clerk .cl-footer > div:last-child,
clerk .cl-userButtonPopoverFooter {display: none !important;}
clerk .cl-navbar,clerk .cl-sidebar {border: none !important;}
clerk .cl-formButtonPrimary {background-color: #ffffff !important;color: #131314 !important;border: none !important;font-weight: 900 !important;}
clerk .cl-navbar>div {background: unset;}
</style>

<script>
const CLERK_PUBLISHABLE_KEY = `YOUR_KEY_HERE`;

window.user = window.user || {};

(function loadClerk() {
  if (window.Clerk) return;

  const script = document.createElement('script');
  script.setAttribute('data-clerk-publishable-key', CLERK_PUBLISHABLE_KEY);
  script.async = true;
  script.src = `https://allowed-marlin-45.clerk.accounts.dev/npm/@clerk/clerk-js@latest/dist/clerk.browser.js`;

  script.onload = async function() {
    await Clerk.load({
      appearance: {
        baseTheme: undefined,
        variables: {
          colorBackground: '#131314',
          colorPrimary: '#ffffff',
          colorText: '#ffffff',
          colorInputBackground: '#1a1a1b',
          colorInputText: '#ffffff'
        }
      }
    });

    const clerkContainer = document.querySelector('clerk');
    const root = document.querySelector('clerk #auth-root');

    if (Clerk.user) {
      clerkContainer.removeAttribute('active');
      clerkContainer.style.display = 'block';

      window.user.themself = Clerk.user.id;
      window.user.firstName = Clerk.user.firstName;
      window.user.lastName = Clerk.user.lastName;
      window.user.username = Clerk.user.username;
      window.user.isLoggedIn = true;
      window.user.account = () => {
        if (window.Clerk?.user) {
          const btn = document.querySelector('#auth-root .cl-userButtonTrigger, #auth-root button');
          if (btn) btn.click();
        } else {
          document.querySelector('clerk').setAttribute('active', '');
        }
      };

      window.user.profile = {
        avatar: Clerk.user.imageUrl,
        email: Clerk.user.primaryEmailAddress?.emailAddress || null,
        phone: Clerk.user.primaryPhoneNumber?.phoneNumber || null,
        add: (target) => {
          const targetEl = typeof target === 'string' ? document.querySelector(target) : target;
          if (targetEl && root) targetEl.insertBefore(root, targetEl.firstChild);
        }
      };

      Clerk.mountUserButton(root, {
        showMultiUserEntries: true,
        afterSignOutUrl: window.location.href
      });
    } else {
      clerkContainer.setAttribute('active', '');

      window.user.themself = null;
      window.user.firstName = null;
      window.user.lastName = null;
      window.user.username = null;
      window.user.isLoggedIn = false;
      window.user.profile = {
        add: () => clerkContainer.setAttribute('active', '')
      };

      Clerk.mountSignIn(root);
    }
  };

  document.head.appendChild(script);
})();
</script>
</clerk>
```

**What it exposes on `window.user`:**

| Property | Type | Description |
|----------|------|-------------|
| `themself` | string | Clerk user ID |
| `firstName` | string | First name |
| `lastName` | string | Last name |
| `username` | string | Username |
| `isLoggedIn` | boolean | Auth state |
| `account()` | function | Opens account panel |
| `profile.avatar` | string | Image URL |
| `profile.email` | string | Primary email |
| `profile.add(target)` | function | Mounts user button into a target element |

**Features:** Sign in / Sign up, social logins, user management, session management, MFA, organizations

---

## Realtime — Liveblocks

Drop the block below. Fill in `LB_PUBLIC_KEY`. Requires `window.themself` to be set first (Clerk handles this).

```html
<liveblocks>

<div id="lb-component-root" style="display:none; border:unset; padding:20px; border-radius:12px; color:white; max-width:400px;">
  <div style="display:flex; gap:10px; margin-bottom:15px;">
    <input type="text" id="lb-input-field" placeholder="Save to database..."
           style="flex:1; background:#101010; border:unset; color:#fff; padding:8px; border-radius:6px;">
    <button id="lb-save-btn" style="background:#fff; color:#000; border:none; padding:8px 15px; border-radius:6px; font-weight:bold; cursor:pointer;">Save</button>
  </div>
  <ul id="lb-data-list" style="list-style:none; padding:0; font-family:Arial, Helvetica, sans-serif; font-size:13px;"></ul>
</div>

<style>
  #liveblocks-badge { display: none !important; }

  @keyframes slideIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .lb-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
    opacity: 0;
    animation: slideIn 0.4s ease forwards;
  }

  .delete-btn {
    cursor: pointer;
    color: #ff4d4d;
    font-weight: bold;
    padding: 0 10px;
    transition: opacity 0.2s;
  }

  .delete-btn:hover { opacity: 0.7; }
</style>

<script type="module">
  import { createClient, LiveList } from "https://esm.sh/@liveblocks/client";

  const LB_PUBLIC_KEY = ""

  const initLiveblocks = async (userId, userName) => {
    const client = createClient({ publicApiKey: LB_PUBLIC_KEY });
    const rootUI = document.getElementById("lb-component-root");
    const listUI = document.getElementById("lb-data-list");
    const inputUI = document.getElementById("lb-input-field");
    const btnUI = document.getElementById("lb-save-btn");

    rootUI.style.display = "block";

    const { room } = client.enterRoom(userId, {
      initialStorage: { items: new LiveList([]) },
    });

    const { root } = await room.getStorage();
    const items = root.get("items");

    window.deleteItem = (index) => { items.delete(index); };

    const render = () => {
      const data = items.toArray();
      listUI.innerHTML = "";

      data.map((item, index) => ({ ...item, originalIndex: index }))
          .reverse()
          .forEach((i, idx) => {
            const li = document.createElement("li");
            li.className = "lb-item";
            li.style.animationDelay = `${idx * 0.05}s`;
            li.innerHTML = `
              <span>${i.text}</span>
              <span class="delete-btn" onclick="deleteItem(${i.originalIndex})">✕</span>
            `;
            listUI.appendChild(li);
          });
    };

    room.subscribe(items, () => render());
    render();

    const saveData = () => {
      const content = inputUI.value.trim();
      if (!content) return;
      items.push({ text: content, author: userName, time: Date.now() });
      inputUI.value = "";
    };

    btnUI.onclick = saveData;
    inputUI.onkeypress = (e) => { if (e.key === 'Enter') saveData(); };
  };

  const watcher = setInterval(() => {
    if (window.themself) {
      clearInterval(watcher);
      initLiveblocks(window.themself, window.firstName || "User");
    }
  }, 500);
</script>

</liveblocks>
```

**Use cases:** Collaborative editors, team dashboards, shared workspaces, live commenting, any realtime sync

---

## SEO

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

**Sample Clerk prompt to generate SEO:**

```
Apple website, Simple, Flat, Minimal

--

Make me my seo

<title>MansanasPH</title>
[paste template here]

--

mansanas PH, apple store, apple shop

--

Video hero
Cycle this video with fade
https://cdn.pixabay.com/video/2023/08/17/176489-855554923_large.mp4

--

Tailwind, CSS, Iconify CDN use Mingcute, JS, Html

--

one file
```

---

## Analytics — Google Search Console

https://search.google.com/search-console

Submit your sitemap here after launch. Monitors search performance, index coverage, Core Web Vitals, and search appearance.

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

## Security — YN Security Patch

Drop this into every page. Loads before content via `defer`.

```html
<security-yn1>
  <link rel="preconnect" href="https://ynpasc.vercel.app" crossorigin>
  <link rel="preload" href="https://ynpasc.vercel.app/security/patch/public/base.js" as="script">
  <script defer src="https://ynpasc.vercel.app/security/patch/public/base.js"></script>
</security-yn1>
```

---

## Web Standards Checklist

A condensed version of the full spec at https://websitechecklists.io.

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

## Rounded Button

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
