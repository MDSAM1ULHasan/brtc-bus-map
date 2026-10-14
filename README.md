# BRTC Bus Routes & Timetables — Bangladesh

A free, static interactive map starter for BRTC route and timetable information.

## Current features

- Detailed zoomable street map powered by MapLibre GL JS and OpenFreeMap.
- Responsive layout for desktop and mobile.
- Search imported route and stop feature properties.
- Import GeoJSON FeatureCollections with route lines and stop points.
- Click map features to inspect their properties.
- Map attribution to OpenStreetMap contributors.

## Important data note

This starter does **not** include a verified BRTC route or official timetable dataset yet. Do not use estimated or invented route paths/times as official information. Add route geometry, stop coordinates, schedule data, and source/verification notes from reliable BRTC sources before public use.

## Publish with GitHub Pages

1. Open **Settings** in this repository.
2. Choose **Pages** in the sidebar.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**, then click **Save**.
5. Wait for the deployment to complete. GitHub will display the site URL in the Pages settings.

## GeoJSON format

Import a `FeatureCollection` with:
- `LineString` or `MultiLineString` features for road-following routes.
- `Point` features for bus stops and terminals.

Helpful properties include `route_name`, `stop_name`, `direction`, `departure_time`, `arrival_time`, `service_days`, `fare`, `source`, `verification_status`, and optional `color`.

## Map data and attribution

Base-map tiles are provided by OpenFreeMap; geographic map data is © OpenStreetMap contributors. Follow provider usage terms and keep attribution visible.
