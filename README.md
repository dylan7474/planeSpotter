# planeSpotter

planeSpotter is a browser-based ADS-B spotter dashboard that combines live aircraft telemetry with your local camera feed to automatically capture photos when planes enter your camera field of view.

It is designed for hobby plane spotting setups that have:
- a Dump1090-compatible ADS-B receiver on the local network, and
- a webcam or phone camera available to the browser.

## Features

- Live airspace scanner/radar visualization.
- Plane list with bearing, distance, and altitude.
- Auto-snap mode when aircraft are in view.
- Manual snapshot capture.
- Optional weather-aware snapping (clear skies only).
- Local in-browser gallery with one-click image download.

## Quick Start (Build / Run)

This project is a static web app (no backend build step).

1. Clone the repo.
2. Serve the project root with any static HTTP server.
3. Open `index.html` from that server in a modern browser.

Example using Python:

```bash
python3 -m http.server 8081
```

Then open:

```text
http://localhost:8081
```

> Note: Webcam access generally requires `http://localhost` or `https`.

### Cloudflare Zero Trust / Tunnel setup note

If you deploy with `./deploy.sh`, the generated container now proxies `/dump1090-fa/*` to your local Dump1090 host internally.  
Default upstream is `http://192.168.50.100:8080`, and you can override it when starting the container with:

```bash
DUMP1090_BASE_URL=http://192.168.50.100:8080 ./deploy.sh 3013
```

With this setup, your single Cloudflare Zero Trust public URL only needs to expose the Plane Spotter web container; the browser fetches `/dump1090-fa/data/aircraft.json` from that same origin.

## Basic Controls

- **Start Monitoring**: Starts/stops polling your Dump1090 JSON feed.
- **Dump1090 Proxy Path (Optional)**: Browser requests stay same-origin. Default is `dump1090-fa`, so the UI fetches `dump1090-fa/data/aircraft.json` (then `data/aircraft.json` fallback) from the Plane Spotter server, and that server proxies to your Dump1090 host.
- **Your Lat / Your Lon**: Your observer position used for distance/bearing calculations.
- **Cam Azimuth (East=90)**: Camera direction in degrees.
- **Max Capture Distance**: Limits auto-capture to nearby aircraft.
- **Test Camera / Hide Camera**: Toggle camera preview panel visibility.
- **Manual Snap**: Capture a photo immediately.
- **Auto-Snap**: Enable/disable automatic capture for in-view aircraft.
- **Clear skies only**: Prevent auto-capture in poor/cloudy weather conditions.
- **Show: All / Radar Only**: Filter the visible planes list.
- **Clear All (gallery)**: Remove all thumbnails from the current session.

## Roadmap

Short-term improvements:
- Add a first-run setup helper for location, azimuth calibration, and connectivity checks.
- Persist gallery metadata and settings with optional export/import.
- Add configurable auto-snap cooldown rules and per-aircraft filters.

Medium-term ideas:
- Add map mode (leaflet) alongside radar mode.
- Support multiple camera profiles and FOV calibration tools.
- Add optional object detection overlay for aircraft in captured frames.

## License

This project is licensed under the MIT License. See [LICENSE](./LICENSE).
