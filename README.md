# Data in the USA — Income Inequality Across US Counties

An interactive data visualization built with **D3.js** that explores income inequality across more than 3,000 US counties, using data from the **USDA Atlas of Rural and Small-Town America**. The project combines a choropleth map with linked histograms and a scatterplot so users can explore how median household income and poverty rates vary — and correlate — across the country.

## Live Demo

Open `index.html` in a browser (served over a local web server — see [Getting Started](#getting-started)).

## Features

- **Interactive choropleth map** of US counties, rendered with D3's Albers USA projection
  - Toggle between two metrics: **Median Household Income** and **Poverty Rate**
  - Distinct sequential color scales for each metric (YlOrBr for income, PuOr for poverty)
  - Hover tooltips showing county-level values
- **County search** — type a county name to locate and highlight it on the map, with error handling for counties that aren't found
- **Zoom & pan** — scroll to zoom (up to 8×), drag to pan, and a **Reset Zoom** button to return to the default view
- **Brush selection** — enable brush mode to drag-select a region of the map; the histograms and scatterplot update to reflect only the selected counties (linked views)
- **Distribution histograms** for both median household income and poverty rate
- **Scatterplot** showing the correlation between income and poverty across counties

## Project Structure

```
Project-1-Data-in-the-USA/
├── index.html        # Main application (map + charts + brush interaction)
├── main.html         # Earlier version of the visualization (no brush selection)
├── data.csv          # County-level data: median household income & poverty rate
└── us_counties.json  # TopoJSON geometry for US county boundaries
```

## Data

- **`data.csv`** — ~3,270 rows covering US counties (plus state and national aggregates) with three columns:
  | Column | Description |
  |---|---|
  | `County` | County (or state / national) name |
  | `Median_Household_Income` | Median household income in USD |
  | `Poverty_Rate` | Percentage of the population below the poverty line |
- **`us_counties.json`** — TopoJSON file with US county boundary geometry, converted to GeoJSON at runtime via the `topojson` client library
- **Source:** [USDA Atlas of Rural and Small-Town America](https://www.ers.usda.gov/data-products/atlas-of-rural-and-small-town-america/)

## Technologies

- [D3.js v6](https://d3js.org/) — data loading, scales, axes, geo projections, zoom, and brushing
- [TopoJSON v3](https://github.com/topojson/topojson) — decoding county boundary geometry
- Vanilla HTML/CSS/JavaScript — no build step or framework required

## Getting Started

Because the app loads `data.csv` and `us_counties.json` via `fetch`/`d3.csv`, it must be served over HTTP (opening the file directly with `file://` will be blocked by browser CORS rules).

1. Clone or download this repository:
   ```bash
   git clone https://github.com/sakethram132002/Project-1-Data-in-the-USA.git
   cd Project-1-Data-in-the-USA
   ```
2. Start a local web server, for example:
   ```bash
   # Python 3
   python -m http.server 8000
   ```
   or
   ```bash
   # Node.js
   npx http-server -p 8000
   ```
3. Open [http://localhost:8000/index.html](http://localhost:8000/index.html) in your browser.

## How to Use

1. **Pick a metric** from the dropdown to recolor the map by income or poverty rate.
2. **Hover** over any county to see its exact values in a tooltip.
3. **Search** for a county by name to highlight it on the map.
4. **Zoom and pan** to inspect dense regions; click **Reset Zoom** to return to the full view.
5. Click **Enable Brush**, then drag a rectangle over the map — the histograms and scatterplot below will update to show only the counties inside your selection. Click the button again to disable brushing and restore the full dataset.

## Insights You Can Explore

- Which regions of the US have the highest and lowest median household incomes
- How poverty rates cluster geographically (e.g., across the rural South or Appalachia)
- The inverse relationship between household income and poverty rate, visible in the scatterplot

## License

This project was created for academic purposes. Data courtesy of the USDA Economic Research Service.
