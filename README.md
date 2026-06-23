### make-site-in-2026

# Site & System Development 101

## Overview
This document contains essential tools and services for building a modern website, web application, or system.

---

# Analytics

Track website traffic, performance, user behavior, and search visibility.

### Google Search Console
Monitor search performance, indexing status, and website health.

- https://search.google.com/search-console

Features:
- Search performance reports
- Index coverage monitoring
- Sitemap submission
- Core Web Vitals tracking
- Search appearance insights

---

# SEO

Improve search engine rankings and optimize metadata.

### SEO Generator
Generate SEO metadata, Open Graph tags, and structured content.

- https://actwu.github.io/gen/seo/

Recommended Usage:
- Page titles
- Meta descriptions
- Open Graph images
- Social media previews
- Structured SEO content



---

# Realtime Collaboration

Enable multiplayer experiences and realtime synchronization.

### Liveblocks
Add collaborative features such as shared cursors, comments, notifications, and realtime editing.

- https://liveblocks.io/

Liveblock Template Code



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

  /* Staggered Animation Styles */
  @keyframes slideIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .lb-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
    opacity: 0; /* Starts hidden for animation */
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

    // Global delete function
    window.deleteItem = (index) => {
      items.delete(index);
    };

    const render = () => {
      const data = items.toArray();
      listUI.innerHTML = ""; // Clear for re-render don't render js codes
      
      // We reverse the array but keep track of the original index for deletion
      data.map((item, index) => ({ ...item, originalIndex: index }))
          .reverse()
          .forEach((i, idx) => {
            const li = document.createElement("li");
            li.className = "lb-item";
            // Stagger delay calculation
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
    inputUI.onkeypress = (e) => { if(e.key === 'Enter') saveData(); };
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

Use Cases:
- Collaborative editors
- Team dashboards
- Shared workspaces
- Live commenting systems
- Realtime applications

---

# Authentication

Manage user authentication and account systems.

### Clerk
Authentication platform for modern applications.

- https://clerk.com

Clerk Template Code
---

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
clerk .cl-modalContent,clerk .cl-userButtonPopoverCard,clerk .cl-card,  clerk .cl-modalBackdrop,   clerk .cl-modalBackdrop::before,   clerk .cl-modalBackdrop::after, 
clerk .cl-cardBox,
clerk .cl-modalContent *,
clerk .cl-userButtonPopoverMain *,
clerk .cl-userButtonPopoverMain,
clerk .cl-userButtonPopoverCard.cl-card.cl-userButton-popover 
{background-color: #131314 !important;color: #fafafa !important;border: none !important;box-shadow: none !important;font-family: 'Jakarta Plus Sans', Arial, Helvetica, sans-serif;}
clerk .cl-formInputInput,
clerk .cl-input,
clerk .cl-formInputContainer,
clerk .cl-selectButton,
clerk .cl-alternativeMethodsButton,
clerk .cl-identityPreview {background-color: #131314 !important;color: #ffffff !important;border: 1px solid #1a1a1b !important;}
clerk .cl-formInputInput:focus,clerk .cl-input:focus {background-color: #1a1a1b !important;border-color: #ffffff !important;}
clerk .cl-formFieldLabel,clerk .cl-formFieldHintText,clerk .cl-formFieldSuccessText,clerk .cl-formFieldErrorText {color: #fafafa !important;}
clerk .cl-navbarButton,clerk .cl-scrollBox,clerk .cl-userButtonPopoverRootBox {color-scheme: dark;color: #ffffff;background-color: #131314 !important;}
clerk .cl-userButtonAvatarBox .cl-avatarBox *,clerk .cl-userPreviewAvatarContainer .cl-avatarBox * {filter: invert(1) hue-rotate(180deg) !important;}
clerk .cl-dividerRow, clerk .cl-dividerLine, clerk .cl-internal-f6u85a,clerk .cl-internal-1dauvpw, clerk .cl-internal-b3fm6y, clerk [class*="PoweredBy"],clerk .cl-rootBox > .cl-card > div:last-of-type,clerk .cl-footer > div:last-child,clerk .cl-userButtonPopoverFooter {display: none !important;}
clerk .cl-navbar, clerk .cl-sidebar {border: none !important;}
clerk .cl-formButtonPrimary {background-color: #ffffff !important; color: #131314 !important; border: none !important;font-weight: 900 !important;}
clerk .cl-navbar>div {background: unset;}
</style>

<script>
const CLERK_PUBLISHABLE_KEY = 
`

`
;

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
window.user.account = () => { if (window.Clerk?.user) {const btn = document.querySelector('#auth-root .cl-userButtonTrigger, #auth-root button'); if (btn) btn.click();} else {document.querySelector('clerk').setAttribute('active', '');} };

window.user.profile = {
avatar: Clerk.user.imageUrl,
email: Clerk.user.primaryEmailAddress?.emailAddress || null,
phone: Clerk.user.primaryPhoneNumber?.phoneNumber || null,
add: (target) => {
const targetEl = typeof target === 'string' ? document.querySelector(target) : target;
if (targetEl && root) {
targetEl.insertBefore(root, targetEl.firstChild);
}
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

--

Features:
- Sign in / Sign up
- Social logins
- User management
- Session management
- Multi-factor authentication
- Organizations and teams

---

# Prompt Samples

Reference prompt examples and AI workflow experiments.

### Prompt Collection
```
Apple website, Simple, Flat, Minimal



--

Make me my seo

<title>MansanasPH</title>

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

Possible Uses:
- AI workflow inspiration
- Prompt engineering examples
- System prompt references
- Automation ideas

---

# Suggested Stack

| Category | Tool |
|----------|------|
| Analytics | Google Search Console |
| SEO | SEO Generator |
| Realtime Features | Liveblocks |
| Authentication | Clerk |

---

# Development Flow

1. Build Website/System
2. Configure Authentication (Clerk)
3. Add Realtime Features (Liveblocks)
4. Generate SEO Metadata
5. Submit Site to Google Search Console
6. Monitor Performance & Indexing
7. Optimize SEO and User Experience
8. Scale Features Based on Analytics Data

--


Add
YN's Security

```html

       <security-yn1>
<link rel="preconnect" href="https://ynpasc.vercel.app" crossorigin>
<link rel="preload" href="https://ynpasc.vercel.app/security/patch/jf93dkojskalokskl/2026/10.js" as="script">

<script defer src="https://ynpasc.vercel.app/security/patch/public/base.js"></script>
  </security-yn1>
  

  ```


