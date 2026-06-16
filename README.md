# Johannes Castellano — Personal Portfolio

> Live site: **https://YOUR-USERNAME.github.io**

Personal portfolio and digital résumé built as a single-page HTML/CSS/JS app.  
Supports **English, Portuguese, and Spanish** with a one-click language switcher.

---

## 📁 Project structure

```
/
├── index.html        ← Entire site (HTML + CSS + JS, all-in-one)
├── admin.html        ← Local tool: generates translated experience blocks
├── README.md         ← This file
├── ADMIN.md          ← Documentation for the admin tool
└── CHANGELOG.md      ← History of updates
```

This project is intentionally kept as **plain HTML files** — no build tools,
no Node.js, no dependencies. Everything runs in the browser.

---

## 🌐 Hosting

Hosted for free on **GitHub Pages**.

To enable GitHub Pages on a new repo:
1. Go to **Settings → Pages**
2. Source: `Deploy from a branch`
3. Branch: `main` / `root`
4. Save — your site will be live at `https://YOUR-USERNAME.github.io` within ~2 minutes

> `admin.html` will also be publicly accessible at `/admin.html`. It is harmless
> (read-only, no credentials, no repo access), but if you prefer to keep it private,
> add it to `.gitignore` and run it only locally.

---

## ✏️ How to add a new experience entry (recommended workflow)

Use the **admin tool** so you never have to write HTML manually:

1. Open `admin.html` in your browser (double-click or use a local server)
2. Fill in the job title, org, dates, and bullet points in English
3. Click **Translate & Generate** — it auto-translates to PT and ES
4. Copy the **Full block** output
5. Paste the HTML into `index.html` inside `<div class="timeline">` (top = most recent)
6. Paste the translation keys into the `translations` object in `index.html`
7. Review the auto-translations, fix if needed, commit

See `ADMIN.md` for full details on the admin tool.

---

## ✏️ How to update other content

### Small edits — directly on GitHub
1. Open `index.html` on GitHub
2. Click the pencil icon (Edit)
3. Make your changes
4. Click **Commit changes** → the site updates in ~2 min

### Larger edits — locally
```bash
git clone https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io
# edit files
git add .
git commit -m "update: added new certification"
git push
```

---

## 🌍 How translations work

All translations live inside the `translations` object at the bottom of `index.html`:

```js
const translations = {
  en: { "key": "English text", ... },
  pt: { "key": "Texto em português", ... },
  es: { "key": "Texto en español", ... },
}
```

Every HTML element that should change language has a `data-i18n="key"` attribute.
The `setLang()` function swaps all text at once. Language preference is saved to
`localStorage` so returning visitors see their last-used language.

### To add a new language (e.g. French)
1. Copy the `en: { ... }` block, paste as `fr: { ... }`, translate all values
2. Add a button to the nav: `<button class="lang-btn" onclick="setLang('fr')">FR</button>`
3. Add the language to the `titles` object inside `setLang()`

---

## 🎨 Design decisions

| Choice | Reason |
|--------|--------|
| Dark theme | Appropriate for cybersecurity audience |
| DM Serif Display + Inter | Editorial + clean readability |
| Single HTML file | Zero build complexity, easy GitHub editing |
| CSS variables | Easy to retheme; just update `:root` |
| `localStorage` for language | Remembers user preference across sessions |
| IntersectionObserver | Scroll-reveal animations without libraries |
| Free translation APIs | MyMemory / LibreTranslate — no cost, no key |

### To change the accent color
Find `:root` at the top of the `<style>` block:
```css
:root {
  --accent:  #38bdf8;   /* primary accent — change this */
  --accent2: #22d3a8;   /* secondary accent — change this */
}
```

---

## 📋 Checklist for common updates

- [ ] **New job** → use `admin.html` to generate the block
- [ ] **New certification** → add a `.cert-card` in the Certifications section + add keys in all 3 language objects
- [ ] **Graduated** → update Education dates directly in `index.html`
- [ ] **New contact info** → update `href` on contact buttons and the matching `data-i18n` values
- [ ] **Changed summary/bio** → update `hero.subtitle` and `about.p1–p4` in all 3 language objects
- [ ] **After any change** → add a note to `CHANGELOG.md`

---

## 🔮 Future project ideas

To expand this into a multi-project portfolio:

```
/
├── index.html              ← Main portfolio
├── admin.html              ← Admin tool (local use)
├── projects/
│   ├── soc-dashboard/
│   │   └── index.html
│   └── grc-tracker/
│       └── index.html
└── README.md
```

Add a "Projects" nav link and a new section in `index.html` with cards linking to each project subfolder.

---

## 🛠 Built with

- Vanilla HTML, CSS, JavaScript — no frameworks
- [DM Serif Display](https://fonts.google.com/specimen/DM+Serif+Display) + [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts
- [MyMemory API](https://mymemory.translated.net) for auto-translation (free)
- GitHub Pages for hosting

---

*Last updated: 2025*
