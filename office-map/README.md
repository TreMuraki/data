# Pacific Financial Group — Interactive Office Map

A self-contained, atlist-style interactive map (`index.html`) showing branch and
private office locations, built for embedding in a Framer site.

**Features**

- Clean light basemap (free CARTO tiles via Leaflet — no API key, no usage fees)
- Custom branded map pins, color-coded by office type (blue = branch, gold = private)
- Filter pills — All / Branch / Private — with live counts
- Slide-in office list panel; clicking a card flies the map to that office
- Click a pin → popup card with banner photo, tag chip, address, phone
  (tap-to-call), and a Get Directions button that opens Google Maps
- Fully responsive: list becomes a bottom sheet on phones

---

## Editing the offices

All content lives in the `OFFICES` array near the top of the `<script>` block in
`index.html`. Each office looks like this:

```js
{
  id: "honolulu",                      // unique, no spaces
  name: "Honolulu Branch",
  city: "Honolulu, HI",                // shown on the popup banner
  tag: "branch",                       // "branch" or "private"
  address: "1003 Bishop Street, Suite 1910",
  cityStateZip: "Honolulu, HI 96813",
  phone: "(808) 545-2225",             // "" hides the phone row + Call button
  photo: "",                           // banner image URL; "" = branded gradient
  coords: [21.3095, -157.8610],        // [latitude, longitude]
},
```

### Adding private offices

Copy the commented-out template at the bottom of the `OFFICES` array, set
`tag: "private"`, and fill it in. The gold "Private" filter pill and gold pins
appear automatically as soon as at least one private office exists.

### Getting exact coordinates

Right-click the building on [Google Maps](https://maps.google.com) → click the
coordinates at the top of the menu to copy them, then paste into `coords`.
The current coordinates are approximate (street-level accurate, not
rooftop-accurate) — worth fine-tuning this way.

### Adding banner photos

Set `photo` to any hosted image URL (roughly 600×250px crops best):

1. In Framer, drop the photo onto any (even unpublished) page, publish, then
   copy the image's URL (right-click → Copy image address), **or** host the
   images in this repo/any static host.
2. Paste the URL into the office's `photo` field.

With `photo: ""` the popup shows a branded gradient banner instead, so the map
never looks broken while photos are pending.

### Branding

Colors are defined once in the `:root` CSS block (`--brand-blue`,
`--brand-navy`, `--brand-gold`) and in the `TAGS` object in the script. Change
them there to restyle pins, pills, tags, and buttons together.

---

## ⚠️ Data to verify before going live

| Office | What to check |
| --- | --- |
| Roseville | Phone number (currently blank — row is hidden) |
| Mercer Island | Street address + suite (best guess: 7900 SE 28th St, Suite 300) and phone |
| All | Fine-tune pin coordinates (see above) |

Honolulu, San Jose, and Lake Oswego addresses/phones were sourced from public
Prudential Advisors listings — worth a quick confirmation too.

---

## Embedding in Framer

Framer's **Embed** component loads an external page, so the map needs a URL.

### Option A — GitHub Pages (free, recommended)

1. In this repo on GitHub: **Settings → Pages → Deploy from a branch**, pick
   your branch and `/ (root)`.
2. The map will be served at
   `https://<username>.github.io/<repo>/office-map/`.
3. In Framer: **Insert → Utility → Embed**, set **Type: URL**, paste that URL,
   then size the frame (e.g. 100% × 600px). Done.

> Any static host works the same way (Netlify, Vercel, Cloudflare Pages, S3…).

### Option B — paste as HTML

The Embed component also accepts raw HTML. Pasting the whole file works, but a
hosted URL (Option A) is easier to maintain — you edit one file and every page
using it updates.

### Sizing tip

The map fills whatever frame it's given (`100dvh` of the iframe). A
full-width frame 550–650px tall reads well on desktop; Framer's responsive
settings handle mobile automatically.

---

## Local preview

Just open `index.html` in a browser — no build step, no server required.
(Leaflet loads from the unpkg CDN, so you need to be online.)
