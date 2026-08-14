[README.md](https://github.com/user-attachments/files/31050642/README.md)
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
{ name: "Din Tai Fung", stall: "#B1-10/11/12", cuisine: "Chinese",
  detail: "Taiwanese dumplings & noodles", halal: false,
  phone: "+65 6634 7787", website: "https://www.dintaifung.com.sg" }
```

- `phone: null` → card shows "Walk-in only" instead of a call button
- `website: null` → menu/website button is hidden
- `grab: false` → hides the "Order on Grab" button (used for Starbucks/Coffee Bean, which run
  their own delivery apps in Singapore instead of partnering with Grab)
- Cuisine colors and chips are generated automatically from whatever values appear in `cuisine`

Current dataset (28 outlets) is a starter set sourced from the official NEX directory
(nex.com.sg) as of Aug 2026 — stall numbers and hours can change, so verify before publishing
live.

## Live Google star ratings (optional)

Each card can show a real, current Google rating (`★★★★☆ 4.3 (612)`) instead of a "tap to
check" link — but this needs your own Google Places API key, since there's no reliable way to
bake accurate ratings into the file (they change constantly, and third-party sites often show
Tripadvisor/Yelp numbers mislabeled as Google's).

**Setup:**
1. Go to [console.cloud.google.com/google/maps-apis](https://console.cloud.google.com/google/maps-apis)
   and create/select a project.
2. Enable **Places API (New)**.
3. Create an API key, then restrict it (Application restrictions → **Websites**) to your
   deployed domain, e.g. `nex-food-directory.vercel.app/*` — this stops anyone else from using
   your key if they inspect the page source.
4. Open `index.html`, find this line near the top of the `<script>` block, and paste your key:
   ```js
   const GOOGLE_PLACES_API_KEY = ""; // <-- paste your key here
   ```
5. Redeploy (`git push`). Ratings now hydrate live on every card and on the spin-wheel result.

**Cost:** Places API (New) Text Search is roughly $32 per 1,000 requests, with a recurring
$200/month free credit from Google — for personal/light use this stays well within the free
tier, but keep an eye on it if you share the link widely. Leave the key blank to skip all of
this and keep the plain "tap to check" links.
