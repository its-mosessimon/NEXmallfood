# NEX Care-Bear Food Directory

A single-page, Care Bears–themed food directory for NEX mall (Serangoon). Search, halal filter,
cuisine grouping, tap-to-call reservations, and website/menu links. Pure static HTML/CSS/JS —
no build step, no dependencies.

## Project structure

```
nex-food-directory/
├── index.html      ← the whole app (static, no build needed)
├── vercel.json      ← static deployment config
└── README.md
```

## Deploy: GitHub → Vercel

**1. Push to GitHub**

```bash
cd nex-food-directory
git init
git add .
git commit -m "Initial commit: NEX food directory"
git branch -M main
git remote add origin https://github.com/<your-username>/nex-food-directory.git
git push -u origin main
```

(Create the empty repo first at github.com/new — don't initialize it with a README there,
to avoid a merge conflict with this one.)

**2. Import into Vercel**

1. Go to [vercel.com/new](https://vercel.com/new)
2. Click **Import Git Repository** and select `nex-food-directory`
3. Framework Preset: choose **Other** (no build command needed — it's static HTML)
4. Leave Build Command and Output Directory blank
5. Click **Deploy**

Vercel will serve `index.html` at your project's root URL immediately. Every future `git push`
to `main` auto-redeploys.

## Editing the data

All outlet data lives in the `OUTLETS` array near the bottom of `index.html`, inside the
`<script>` tag. Each entry looks like:

```js
{ name: "Din Tai Fung", stall: "#B1-10/11/12", cuisine: "Chinese (Taiwanese)",
  halal: false, phone: "+65 6634 7787", website: "https://www.dintaifung.com.sg" }
```

- `phone: null` → card shows "Walk-in only" instead of a call button
- `website: null` → menu/website button is hidden
- Cuisine colors and chips are generated automatically from whatever values appear in `cuisine`

Current dataset (24 outlets) is a starter set sourced from the official NEX directory
(nex.com.sg) as of Aug 2026 — stall numbers and hours can change, so verify before publishing
live.
