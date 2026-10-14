# BRTC Bus Routes & Timetables — Bangladesh

A free, color-coded interactive map project for Dhaka city and metro BRTC route information.

## Map features

- Detailed, zoomable road map powered by MapLibre GL JS and OpenFreeMap.
- Bengali/English place labels where the basemap provides them.
- A unique color for each route and its stop markers.
- Search by route name, Bangla route name, stop name, and route notes.
- Click any stop or route line to inspect route and timetable information.
- GeoJSON import for adding more route datasets.
- Road-following route estimates generated through ordered stop waypoints using the public OSRM demo router.

## Included route dataset

`data/brtc-routes.geojson` contains **22 Dhaka city and metro-commuter route records**, with 189 route-stop waypoint features at the time of this update. The list was assembled from BRTC's published **Citizen Charter (3rd quarter FY 2024–25; page updated 4 June 2025)** and BRTC Passenger Transport Service tables.

Official source:
- BRTC Citizen Charter: https://brtc.gov.bd/site/page/5001091c-e4a6-4949-a6bc-e70bae7bfd63/Citizen
- BRTC Passenger Transport Service: https://brtc.gov.bd/pages/static-pages/6922e0e1933eb65569e29008

**Coverage limitation:** This is a consolidated list of Dhaka city and metro-commuter route entries found in BRTC publications, not a guarantee that every route currently operates. Some BRTC tables conflict on times, route distances and service details. Check with BRTC before travelling.

## Important route-geometry and location note

- Stop coordinates are approximate geographic waypoints to create a useful first map. They must be checked against the exact boarding point.
- Colored route lines are automatically generated road-routing estimates through the listed waypoints, not official BRTC GPS traces or confirmation of the precise bus path.
- The routing service can be temporarily unavailable or rate-limited; the map may show stop points without a route line if that happens.
- Timetable notes retain the published source and flag information that needs reconfirmation. Do not interpret missing data as “no service”.

## Regional route archive

The earlier Dhaka–Faridpur pilot data is preserved in `data/brtc-regional-routes.geojson`.

## How to add another route

Add a Point feature for each ordered stop to `data/brtc-routes.geojson`. Every point should include:
- `route_id` — shared by all stops on the same route.
- `route_name` and optional `route_name_bn`.
- `color` — hex color unique to the route.
- `route_order` — ascending stop order starting with 1.
- `stop_type` — `origin`, `intermediate` or `destination`.
- `stop_name`, `stop_name_en`, and `[longitude, latitude]` geometry.
- `timetable_note`, `official_source`, `official_source_url`, and `source_status`.

On page load, the app requests a road route through each route's ordered stop coordinates and draws each line in the corresponding color. The public OSRM demo service has no uptime guarantee and must not be treated as unlimited production routing infrastructure.

## Deployment

GitHub Actions deploys changes on `main` to GitHub Pages using `.github/workflows/deploy-pages.yml`.

## Attributions

Base-map tiles: OpenFreeMap. Geographic data: © OpenStreetMap contributors. Road routing: public OSRM demo service. Follow each provider's usage, fair-use and attribution rules.
