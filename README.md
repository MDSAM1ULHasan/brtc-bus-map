# BRTC Bus Routes & Timetables — Bangladesh

A free, interactive street map project for published BRTC route information in Dhaka.

## Important accuracy correction

Earlier prototype data used guessed neighbourhood coordinates for many stops. Those guesses caused markers to appear in narrow residential lanes rather than at mapped bus stops. The current map data has been corrected:

- **Only stop features matched to an OpenStreetMap bus-stop or bus-station feature are placed on the map.**
- **73 unmatched stop records are hidden from the map** instead of being placed at guessed coordinates. Their names remain in the route list so they can be verified later.
- Gray pins are mapped public bus stops where the association with a specific BRTC route has not been confirmed.
- Colored pins have a stop name that appears in a BRTC-published route timetable and a matching OSM stop feature. That still does not prove the exact BRTC boarding bay or side of the road; those must be checked separately.
- A route line is generated only when every stop record for that route has a mapped point and the name is listed for that route in the published BRTC data. The dashed line is an OSRM road-routing estimate, **not an official BRTC GPS trace**.
- Where a stop or route can't be verified, the map deliberately leaves it unpinned or without a line rather than drawing a guess.

## Current dataset

`data/brtc-routes.geojson` contains 22 BRTC route records with 189 route-stop records. The current review has:
- 116 mapped route-stop feature records (some represent the same physical bus stop used by multiple routes).
- 73 stop records hidden because a matching stop/terminal feature hasn't been identified.
- Only 45 route-stop names linked to the published BRTC schedule; route-specific boarding points may still need field verification.

Official source pages:
- BRTC Citizen Charter: https://brtc.gov.bd/site/page/5001091c-e4a6-4949-a6bc-e70bae7bfd63/Citizen
- BRTC Passenger Transport Service: https://brtc.gov.bd/pages/static-pages/6922e0e1933eb65569e29008

The route records are compiled from BRTC publications, but that does not guarantee each listed service still operates today. Confirm times and pickup points with BRTC before travelling.

## Map technology and sources

- Map display: MapLibre GL JS
- Base map: OpenFreeMap
- Underlying geographic data: © OpenStreetMap contributors
- Road-routing estimates: public OSRM demo service

The coordinate provenance for mapped stops is provided in each feature's `coordinate_source_url`, `coordinate_osm_id`, and `coordinate_match_status` fields. Stop association with a specific BRTC service is recorded separately in `route_stop_verified` and `route_stop_status`.

## Adding a verified stop

Add the exact mapped bus-stop or bus-station feature coordinate from OpenStreetMap, and record its OSM reference and source URL. Do not use a neighbourhood centre, junction centre, random road point, or route midpoint in place of a boarding stop. For route line generation, every stop in the stop sequence must have `coordinate_verified=true` and `route_stop_verified=true`; otherwise the route line is intentionally withheld.

## Deployment

GitHub Actions deploys changes to the `main` branch through `.github/workflows/deploy-pages.yml`.

## Stop departures and trip timeline UI

- Tap a mapped bus-stop marker to open a mobile-style departures sheet.
- The departures sheet shows BRTC services linked to that stop in the loaded route dataset. Stop-specific times appear only where a time is present in the published timetable data.
- Tap a service to see its stop-by-stop timeline, Bengali stop names, published times and whether each stop is mapped or still lacks a confirmed coordinate.
- Times in the interface are **scheduled times only**. “Scheduled in …” is calculated against the device clock and is not a live arrival prediction. A past timetable time does not mean the bus actually departed.
- The prototype is BRTC-only. Private operators such as those shown in Google Maps screenshots are not included because verified route/timetable data for those operators has not been loaded.
- No live GPS, GTFS-Realtime or Google Maps transit feed is connected. No real-time bus positions or live ETAs are claimed.

Schedule times are transcribed from the BRTC-published passenger transport/Citizen Charter information. The publication contains dated entries and is not proof that a particular service is operating today. Verify the timetable with BRTC before travel.
