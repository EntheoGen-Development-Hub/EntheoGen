# Metabase Dashboard — Wiki Embed Guide

This document describes how to embed a signed Metabase dashboard into a GitHub
Wiki page or any static HTML surface using the Metabase embedding SDK.

> [!WARNING]
> **Never hardcode a JWT token or a Metabase secret key in public HTML or
> committed source files.** The token snippets below are illustrative only.
> Always generate tokens server-side and serve them to the client via a
> short-lived API endpoint.

> [!NOTE]
> The `instanceUrl` in the examples below points to `http://localhost:54321`
> (local dev). Replace it with your production Metabase instance URL before
> using these snippets in any public or shared surface.

---

## How signed embedding works

1. Your **backend** holds the `METABASE_SECRET_KEY` (never exposed to clients).
2. On page load, the client requests a fresh JWT from your backend.
3. The backend signs the payload (dashboard ID, params, 10-minute expiry) and
   returns the token.
4. The client passes that token to `<metabase-dashboard>`.

---

## Backend: generate a signed token (Node.js)

```js
// npm install jsonwebtoken
const jwt = require("jsonwebtoken");

const METABASE_SECRET_KEY = process.env.METABASE_SECRET_KEY; // load from env, never hardcode

const payload = {
  resource: { dashboard: 6 },
  params: {},
  exp: Math.round(Date.now() / 1000) + 10 * 60, // 10-minute expiry
};

const token = jwt.sign(payload, METABASE_SECRET_KEY);
// Return `token` to the client via a short-lived API response
```

---

## Frontend: embed the dashboard

Copy this into a GitHub Wiki page (HTML mode) or a standalone HTML file.
Fetch the token from your backend endpoint — do **not** paste a raw token here.

```html
<!-- Load the Metabase embedding SDK -->
<script defer src="https://your-metabase-instance/app/embed.js"></script>

<script>
  function defineMetabaseConfig(config) {
    window.metabaseConfig = config;
  }
</script>

<script>
  defineMetabaseConfig({
    theme: { preset: "dark" },
    isGuest: true,
    instanceUrl: "https://your-metabase-instance",
  });
</script>

<script>
  // Fetch a fresh signed token from your backend
  fetch("/api/metabase-token")
    .then((r) => r.json())
    .then(({ token }) => {
      const el = document.querySelector("metabase-dashboard");
      if (el) el.setAttribute("token", token);
    });
</script>

<metabase-dashboard
  token=""
  with-title="true"
  with-downloads="true"
></metabase-dashboard>
```

---

## GitHub Wiki limitations

GitHub Wiki pages render HTML, but they **strip `<script>` tags** for security.
The embed above will not execute JavaScript in a raw wiki page.

**Practical alternatives:**

| Option | Notes |
|---|---|
| **GitHub Pages** (`docs/` branch or `gh-pages`) | Full HTML+JS, can host the embed in a static page linked from the wiki |
| **Internal / private wiki** (Notion, Confluence) | Allows script embeds; link from the GitHub wiki |
| **Iframe from a hosted page** | Host the embed page elsewhere and `<iframe>` it; GitHub wiki strips iframes too |
| **Screenshot + link** | Capture the dashboard as a PNG, embed in the wiki, link to the live instance |

The recommended approach for this repo is to host the embed as a GitHub Pages
static page and link it from the wiki.

---

## Local dev (Supabase-hosted Metabase)

When running the dataset-beta Docker Compose stack locally:

- Metabase runs as `metabase_local` on port `54321`.
- Replace `instanceUrl` with `http://localhost:54321`.
- The secret key and dashboard IDs are environment-specific — do not commit
  them. Use `.env` (gitignored) or Doppler secrets.

**Public dashboard URL (local dev):**

```
http://localhost:54321/public/dashboard/2ed79af6-fcf8-4ff4-856f-4729d8b5ea5c
```

This is the no-auth public sharing link for the local Metabase instance. It can
be used for quick access during local development without requiring a signed
token. Do not treat this URL as a production-safe embed — it is local-only and
will not resolve outside the running Docker Compose stack.

See `docs/private-student-beta/README.md` for the full local stack setup.
