# Admin Tool — Experience Block Generator

> File: `admin.html`  
> Purpose: Generate translated HTML blocks for new experience entries without touching `index.html` directly.

---

## What it does

`admin.html` is a local utility — **not meant to be published publicly**.  
You open it in your browser, fill in a form, and it:

1. Calls a free translation API (MyMemory or LibreTranslate)
2. Translates your bullet points to Portuguese and Spanish automatically
3. Generates a ready-to-paste HTML block + the matching translation keys
4. Gives you a preview of how the block will look on the site

---

## How to use it

### Step 1 — Open locally
Double-click `admin.html` in your file explorer, or drag it into a browser tab.  
No server needed. No installation. It runs entirely in the browser.

> ⚠️ Do NOT open it via `file://` if your browser blocks cross-origin fetch requests.  
> If translation fails, use VS Code's Live Server extension or Python's built-in server:
> ```bash
> python -m http.server 8000
> # then open http://localhost:8000/admin.html
> ```

### Step 2 — Fill in the form
| Field | Notes |
|-------|-------|
| Job title | In English — will be translated |
| Employment type | Optional label (Intern, Full-time, etc.) |
| Organization | Company name — **not translated** (proper noun) |
| Location | City, State — **not translated** |
| Start / End date | E.g. `Jan 2026` / leave blank for current role |
| Bullet points | Write in English, one per row, add as many as needed |

### Step 3 — Generate
Click **Translate & Generate**. The tool translates each bullet individually
and generates the HTML output. For 4–5 bullets, expect ~10 seconds.

### Step 4 — Copy & paste into index.html

**Full block tab** → paste inside `<div class="timeline">` in `index.html`,
as the **first child** (most recent job goes at the top).

Then scroll down in `index.html` to the `translations` object and paste:
- The `/* EN */` keys inside `en: { ... }`
- The `/* PT */` keys inside `pt: { ... }`
- The `/* ES */` keys inside `es: { ... }`

### Step 5 — Review translations
Auto-translation is a **draft**. Before committing:
- Read each PT and ES bullet
- Fix any awkward phrasing, especially technical terms
- Job titles sometimes translate poorly — override manually if needed

---

## Translation APIs

### MyMemory (default)
- Free up to ~5,000 words/day
- No API key, no account, no credit card
- Good quality for EN → PT and EN → ES
- Docs: https://mymemory.translated.net/doc/spec.php

### LibreTranslate
- Open source, self-hostable
- Public instance is free but rate-limited
- Slightly slower than MyMemory
- Docs: https://libretranslate.com/docs

**If you need higher volume or better quality**, consider:
- [DeepL Free API](https://www.deepl.com/pro-api) — 500k chars/month free, excellent quality
- To add DeepL: replace the `translate()` function in `admin.html` with a DeepL API call

---

## Translation key naming

Each generated block gets a unique slug based on the job title + timestamp:
```
exp.grc_engineer_inte_1a2b3c.title
exp.grc_engineer_inte_1a2b3c.b1
exp.grc_engineer_inte_1a2b3c.b2
```

This prevents key collisions if you have two similar job titles.

---

## Should I commit admin.html to GitHub?

**Yes, but understand what that means:**
- It will be publicly accessible at `yourusername.github.io/admin.html`
- The tool itself is harmless — it only reads form inputs and calls public APIs
- It does NOT have write access to your repo
- Anyone who finds it can use the generator, but they can't modify your site

If you prefer to keep it private:
- Add `admin.html` to `.gitignore` and keep it only on your local machine
- Or use a private GitHub repo (free) and keep the public repo only for `index.html`

---

## Adding a new language to the generator

1. Open `admin.html`
2. Find the `generate()` function
3. Add a new translation call, e.g.:
   ```js
   const titleFR = await translate(displayTitle, 'fr');
   const bulletsFR = [];
   for (let i = 0; i < bullets.length; i++) {
     bulletsFR.push(await translate(bullets[i], 'fr'));
   }
   ```
4. Add the French keys to `renderOutput()` and add a new tab in the HTML

---

## Limitations

- Translation quality varies — always review before publishing
- MyMemory has a daily free limit; if you hit it, switch to LibreTranslate
- The tool does not write to your repo directly — it only generates HTML to copy
- Organization names, locations, and dates are intentionally NOT translated

---

*Last updated: 2025*
