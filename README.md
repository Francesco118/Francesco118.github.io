# Johannes Castellano — Personal Portfolio

> Live site: **https://YOUR-USERNAME.github.io**

Personal portfolio and digital résumé built as a single-page HTML/CSS/JS app.  
Supports **English, Portuguese, and Spanish** with a one-click language switcher.

---

## 📁 Project structure

```
/
├── index.html        ← Entire site (HTML + CSS + JS, all-in-one)
├── README.md         ← This file
└── CHANGELOG.md      ← History of updates
```

This project is intentionally kept as a **single file** (`index.html`) to make
hosting, editing, and version control as simple as possible. No build tools,
no dependencies, no Node.js required.

---

## 🌐 Hosting

Hosted for free on **GitHub Pages**.

To enable GitHub Pages on a new repo:
1. Go to **Settings → Pages**
2. Source: `Deploy from a branch`
3. Branch: `main` / `root`
4. Save — your site will be live at `https://YOUR-USERNAME.github.io` within ~2 minutes

---

## ✏️ How to update content

### Option A — Edit directly on GitHub (recommended for small edits)
1. Open `index.html` on GitHub
2. Click the pencil icon (Edit)
3. Make your changes
4. Click **Commit changes** → the site updates in ~2 min

### Option B — Edit locally
```bash
git clone https://github.com/YOUR-USERNAME/YOUR-USERNAME.github.io
# edit index.html with any text editor
git add index.html
git commit -m "update: added new certification"
git push
```

---

## 🌍 Adding or editing translations

All translations live inside the `translations` object near the bottom of
`index.html`, structured as:

```js
const translations = {
  en: { "key": "English text", ... },
  pt: { "key": "Texto em português", ... },
  es: { "key": "Texto en español", ... },
}
```

### To update a translation
Find the key you want (e.g. `"contact.sub"`) and update its value in the
relevant language object.

### To add a new language (e.g. French)
1. Copy the entire `en: { ... }` block
2. Paste it below `es: { ... }` with the key `fr`
3. Translate every value string
4. Add a button in the `<div class="lang-switcher">` section:
   ```html
   <button class="lang-btn" onclick="setLang('fr')">FR</button>
   ```

### To mark an HTML element as translatable
Add a `data-i18n="your.key"` attribute:
```html
<p data-i18n="your.key">Default text</p>
```
Then add `"your.key": "Translation"` to each language object.

> ⚠️ Note: `innerHTML` is used for translation injection, which allows `<strong>` tags.
> Only use this for trusted content — never inject user-supplied text this way.

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

### To change the color accent
Find `:root` near the top of the `<style>` block and update `--accent`:
```css
:root {
  --accent: #38bdf8;   /* ← change this hex */
  --accent2: #22d3a8;  /* ← and this one */
}
```

---

## 🔮 Future project ideas

If you add new projects to this site, consider this structure:

```
/
├── index.html              ← Main portfolio
├── projects/
│   ├── soc-dashboard/
│   │   └── index.html
│   └── threat-map/
│       └── index.html
└── README.md
```

Link from the main portfolio with a "Projects" nav item and a new section in `index.html`.

---

## 📋 Checklist for common updates

- [ ] **New job** → add a `.timeline-item` block in the Experience section + update all 3 language objects
- [ ] **New certification** → add a `.cert-card` in the Certifications section + translate `certs.heading` if needed
- [ ] **Graduated** → update the Education section dates
- [ ] **New contact info** → update `href` on the contact buttons (both the attribute and the `data-i18n` value)
- [ ] **Changed objective/summary** → update `hero.subtitle` and `about.p1–p4` in all 3 languages

---

## 🛠 Built with

- Vanilla HTML, CSS, JavaScript — no frameworks
- [DM Serif Display](https://fonts.google.com/specimen/DM+Serif+Display) + [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts
- GitHub Pages for hosting

---

*Last updated: 2025*
