# Cloud-Native Aerial Imagery Discovery & Well Water ETL Pipeline

An open-source spatial discovery web application and automated REST-to-Geodatabase ETL pipeline built for **Cambium Inc.** (Environmental & Geotechnical Engineering) to eliminate enterprise GIS licensing bottlenecks and manual database maintenance.

*Developed collaboratively at Fleming College with project partner **Stephen VanDam** (co-developing and testing the Leaflet frontend, with primary ownership of the GDAL-to-COG raster pipeline, Python/GeoJSON ETL scripts, and REST API database architecture).*

🔗 **Live Demo:** [View Interactive Web App](https://edmharris.github.io/P2306-Final-Website/index.html)

---

## Architecture & Technical Highlights

### 1. Cloud-Native Aerial Imagery Web App (Deliverable 2)
Designed to replace a manual, email-driven drafting workflow for a 100GB+ historical aerial photo library without requiring end-users to hold desktop GIS licenses.

* **Raster Pre-Processing & COG Pipeline:** Automated batch conversion of legacy GeoTIFFs into **Cloud Optimized GeoTIFFs (COGs)** with internal tiling and overviews (`gdal_translate -co "TILED=YES" -co "COPY_SRC_OVERVIEWS=YES"`), followed by batch reprojection to Web Mercator (`EPSG:3857`) via `gdalwarp` in the OSGeo4W shell.
* **Metadata & Spatial Indexing:** Engineered a Python ETL script (`arcpy`, `json`, `csv`, `glob`) to join polygon footprints (reprojected to `EPSG:4326`), tabular CSV metadata, and file paths into a unified **GeoJSON** catalog.
* **Client-Side Spatial Querying & Rendering:** Built an interactive **Leaflet** web application featuring:
  * Custom polygon drawing (`Leaflet.draw`) and geocoding (`leaflet-control-geocoder`).
  * Client-side spatial containment/overlap filtering powered by **Turf.js**.
  * Dynamic raster overlay rendering (`georaster-layer-for-leaflet`) with z-index layer reordering and opacity toggling.

### 2. Automated REST API & Stratigraphy ETL Pipeline (Deliverable 1)
Replaced a broken, manually updated Microsoft Access database with a live spatial data pipeline connected directly to the Ontario Ministry of the Environment, Conservation and Parks (MECP).

* **Upstream API Integration:** Wired ArcGIS Pro directly into the public MECP Well Water Information System (WWIS) **REST endpoint** for live spatial querying (Buffer/Intersect).
* **Python & Regex Normalization:** Built an ArcGIS Pro Python toolbox script to parse complex, double-delimited (`|` and `;`) borehole stratigraphy strings into normalized relational tables (`Wells_Type`, `Borehole_Results`, `Borehole_Details`), using **Regular Expressions (Regex)** to standardize imperial measurements (feet, inches, US gallons) into metric values.

---

## AI-Assisted Development Approach
Used generative AI (ChatGPT) as an engineering force-multiplier to prototype JavaScript/Leaflet event listeners, refine GDAL batch parameters, and debug Turf.js spatial boolean logic—critically validating outputs to filter out deprecated libraries and ensure production reliability.

## Tech Stack
* **Geospatial & Raster:** GDAL, OSGeo4W, QGIS, ArcGIS Pro, ArcPy, Cloud Optimized GeoTIFF (COG)
* **Web & Frontend:** JavaScript, jQuery, Leaflet, Leaflet.draw, Turf.js, `georaster-layer-for-leaflet`, HTML5/CSS3
* **Data & Scripting:** Python, Regular Expressions (Regex), GeoJSON, REST APIs

