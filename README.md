# Alpine Resort Explorer

A concept for an "Explore ski resorts" page in a ski-lesson booking flow, built as a single HTML file.

**Live demo:** https://YOUR-USERNAME.github.io/alpine-resort-explorer/

## What it does

- **Alps overview.** 46 of the busiest resorts in France, Switzerland and Italy on one map. Pin size shows how many instructors are active there. Regions, lift-linked ski areas and the nearest airports are marked.
- **Val Thorens in 3D.** A real terrain model you can turn and zoom, with the actual runs (coloured by difficulty), lifts and peaks. A 2D map is one tap away.
- **Meeting points.** Three example meeting points at real lift stations. Tap one to fly to it and see who it suits, which lift it's next to and how far it is from the village centre.
- **Resort card.** Instructor counts by village, the nearest train station and airports, a link to the official piste map, and a search form that opens real instructor results for the chosen dates.
- **Analytics plan.** Every interaction pushes an event to `window.dataLayer`, the way Google Tag Manager expects. A live log and a small funnel at the bottom show what would reach GA4.

## Events

| Event | Fires when |
|---|---|
| `explore_map_view` | The page loads |
| `resort_select` | A resort opens from a pin or the list |
| `piste_map_view` | A resort's piste map opens |
| `map_view_toggle` | Someone switches between 3D and 2D |
| `map_3d_orbit` | Someone turns or zooms the 3D mountain |
| `piste_filter` | A run filter is picked |
| `meeting_point_select` | A meeting point is tapped |
| `official_map_click` | The official piste map link opens |
| `directions_click` | A Google Maps link opens |
| `transfer_cta_click` | The transfer quote button is tapped |
| `instructor_search` | The search sends someone to the instructor list |

The question the funnel is built to answer: do people who see where they'll meet their instructor book more often? The fair way to find out is an A/B test (current resort page vs. explorer), with bookings per visit as the main metric.

## Data

| What | Source | Licence |
|---|---|---|
| Runs, lifts, peaks | OpenStreetMap via the Overpass API | © OpenStreetMap contributors, ODbL |
| Terrain heights | AWS Terrain Tiles (Mapzen; SRTM and other public elevation data), 150 m grid | Open data, attribution in the page |
| Country outlines | `world-atlas` (Natural Earth) | Public domain |
| Instructor counts | Public resort list on maisonsport.com, 22 Oct 2026 | Snapshot for illustration |

OpenStreetMap has piste data for most Alpine resorts, so the same 3D map could be generated automatically for every resort rather than drawn by hand. Official piste maps are copyrighted artwork, so the page links to them instead of copying them.

The meeting points are examples. In a real product each instructor would pin their own.

## How it was built

Built with an AI coding assistant (Claude) in a few hours:

1. Pulled runs and lifts from OpenStreetMap, simplified the lines to about 25 m and converted them to a local metre grid.
2. Decoded elevation tiles (height = R×256 + G + B/256 − 32768 m) into a 72 × 79 height grid.
3. Drew the Alps map in SVG with pan and zoom, and the mountain in 3D with Three.js: a terrain mesh from the height grid, a texture painted with snow, rock on steep slopes and the runs, and lifts as cables between stations.
4. Tested the interactions in a simulated browser and checked the 3D render in headless Chromium.

## Run it

Open `index.html` in a browser. Three.js loads from a CDN; everything else is in the file.

---

Concept by Oskar Krajc. Not affiliated with or endorsed by Maison Sport, bergfex or any resort.
