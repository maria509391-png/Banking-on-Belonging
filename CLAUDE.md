# Banking on Belonging — Project Memory

## What is this?
An interactive global map showing humanitarian projects supporting displaced communities worldwide.

**Live URL:** https://banking-on-belonging.netlify.app
**GitHub:** https://github.com/maria509391-png/Banking-on-Belonging
**Local file:** /Users/mariarehman/banking-on-belonging/index.html

---

## Tech Stack
- Single HTML file (`index.html`) — no framework, no build step
- **Leaflet.js** (v1.9.4) — map rendering
- **Leaflet.markercluster** (v1.5.3) — clustering for UNHCR live layer
- **CartoDB Voyager** — map tiles (English labels, clean style)
- **Playfair Display** (Google Fonts) — stats banner numbers
- **Netlify** — hosting (free, deployed via CLI)
- **GitHub** — version control (repo: `maria509391-png/Banking-on-Belonging`)

---

## Deployment
- Netlify CLI installed at: `/Users/mariarehman/.netlify-cli/node_modules/.bin/netlify`
- GitHub token: stored securely — generate a new classic token at github.com/settings/tokens if needed
- Deploy command:
```bash
cd /Users/mariarehman/banking-on-belonging
git add index.html
git commit -m "your message"
git push https://maria509391-png:YOUR_TOKEN@github.com/maria509391-png/Banking-on-Belonging.git main
/Users/mariarehman/.netlify-cli/node_modules/.bin/netlify deploy --dir . --prod
```

---

## Organisations (10 total)
| Key | Name | Donate URL |
|-----|------|------------|
| `unhcr` | UNHCR | https://donate.unhcr.org/ |
| `mercy` | Mercy Corps | https://www.mercycorps.org/donate |
| `kiva` | Kiva | https://www.kiva.org/lend/kiva-refugees |
| `tech` | Techfugees | https://techfugees.com/donate/ |
| `ri` | Refugees International | https://give.refugeesinternational.org/a/defend-rights-and-refuge-worldwide-2 |
| `nrc` | Norwegian Refugee Council | https://support.nrc.no/give-today/ |
| `global` | Global Refuge | https://secured.globalrefuge.org/page/52920/donate/1 |
| `tent` | Tent Partnership for Refugees | https://www.tent.org/donate/ |
| `drc` | Danish Refugee Council | https://help.refugees.now/en |
| `nrg` | NGO Refugee Group | https://ngorefugeegroup.co.ke |

---

## Region Colors
```js
"Middle East & North Africa": "#D4860A"
"East Africa":                "#1E9E6B"
"Sub-Saharan Africa":         "#D4621A"
"Europe":                     "#2E6FD4"
"South & Central Asia":       "#7E3FBF"
"Americas":                   "#C94040"
"Southeast Asia":             "#0E95B0"
"North America":              "#4A52C4"
```

---

## Features
- **53+ project pins** color-coded by region
- **3 dropdown filters**: Organisation, Region, Type of Support (desktop sidebar + mobile menu)
- **Search bar**: press Enter to filter pins and zoom map to matches
- **Donate buttons**: region-colored, flip to white with colored border on hover, always white text
- **Mobile**: top navbar (`<details>` element) with filters — no JS toggle needed
- **Stats banner** (navy blue, bottom): 53+ Active Projects | $7B+ Combined Annual Funding | 130M+ People of Concern (UNHCR) — count-up animation on load
- **UNHCR Live Settlements toggle**: fetches live data from UNHCR GIS API, clusters up to 4,000 points, color-coded by pop_type (Refugee, Returnee, IDP, Asylum-seeker, Stateless, Others)
- **No grey edges** on zoom-out: `map.whenReady` calculates and locks minimum zoom to screen size
- **No map duplication**: `maxBounds`, `worldCopyJump: false`, `noWrap: true`

---

## Design
- **Sidebar header & buttons**: navy blue `#1B2A4A`
- **Map tiles**: CartoDB Voyager (English, clean, no greenery)
- **Pins**: color-coded by region, SVG teardrops with white circle centre
- **Popup**: region-colored header, white body, region-colored donate button
- **Stats font**: Playfair Display (bold, stylish)
- **No shadows** on pins; light shadow on sidebar and popups

---

## UNHCR GIS API
- Base URL: `https://gis.unhcr.org/arcgis/rest/services/core_v2`
- Layer used: `wrl_prp_p_unhcr_PoC/FeatureServer/0`
- Fields: `gis_name`, `iso3`, `pop_type`, `latitude_d`, `longitude_d`
- Pop type codes: 52=Refugee, 53=Returnee, 54=IDP, 55=Asylum-seeker, 56=Stateless, 57=Others
- Fetches in pages of 500, capped at 4,000 points

---

## Support Types (11)
Emergency Relief, Food Security, Shelter & Housing, Education, Economic Empowerment, Legal Aid & Protection, Healthcare, Technology & Digital Skills, Resettlement, Advocacy & Policy, Microfinance

---

## Known Issues Fixed
- Silent JS crash from missing `match-count` element — fixed with null check
- Map tiles showing non-English labels — fixed by using CartoDB (not OSM standard)
- World map duplicating on zoom-out — fixed with maxBounds + noWrap
- Grey edges on zoom-out — fixed with dynamic minZoom via `map.whenReady`
- Donate button text color overridden by Leaflet — fixed with `.leaflet-container a.donate-btn` selector

---

## User Preferences
- Colors: rich but not eye-straining (not neon, not too dark)
- Design: clean, upbeat, no tacky gradients
- Buttons: navy blue background, white text
- Stats: honest, map-scoped where possible
- No placeholder text in search bar
- Filters as dropdowns (not chips)
- Map: plain and simple, English labels
