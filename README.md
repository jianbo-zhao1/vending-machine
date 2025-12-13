# Vend-nier – OSU Vending Machine Finder

https://vend-nier.onrender.com/

A Flask web application that helps students and staff at The Ohio State University find nearby vending machines, filter by services and payment methods, see them on a map, and get walking directions – with a Gemini-powered natural language helper.

## Features

- **Search (Elasticsearch)**
  - Keyword search across store name, address, provider, services.
  - Filters on services, payment methods, provider, campus, ZIP, status, special access.
- **Map & Routing**
  - Interactive map with Leaflet.js.
  - Click markers to view machine details.
  - Walking route from start to machine using OpenRouteService, with step-by-step directions.
- **AI Assistant (Gemini)**
  - Chat widget: type queries like “I’m hungry” or “Find me a Coke”.
  - Gemini converts natural language into structured filters and triggers a search.
- **Info Page**
  - Simple “About” page describing the project and tech stack.

## Tech Stack

- **Backend:** Python, Flask
- **Search:** Elasticsearch (geospatial + filter queries)
- **Routing:** OpenRouteService Directions API
- **AI:** Google Gemini (`google-generativeai`)
- **Frontend:** HTML, CSS, vanilla JavaScript, Leaflet.js
- **Config:** `python-dotenv` for `.env` loading

## Project Structure (Core)

- `UI.py`  
  Flask app entrypoint and APIs:
  - `GET /` – main UI
  - `GET /aboutus` – info page
  - `GET /api/machines/search` – vending machine search (Elasticsearch)
  - `POST /route` – walking route (OpenRouteService)
  - `POST /api/interpret` – natural language → filters (Gemini)
- `templates/index.html` – main UI (search panel, results list, map, chat widget).
- `templates/aboutus.html` – About/Info page.
- `assets/` – static assets (e.g., `vendnier_logo.png`, `vendnier_hero.png`).
- `elastic-start-local/` – local Elasticsearch setup and data:
  - `docker-compose.yml`
  - `vending_bulk.ndjson` sample bulk data.

## Prerequisites

- Python 3.9+
- Docker & Docker Compose (recommended for local Elasticsearch)
- API keys:
  - Elasticsearch username/password (e.g. `elastic` user)
  - OpenRouteService API key
  - Google Gemini API key

## Installation

From the project root:

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
# source .venv/bin/activate

pip install flask python-dotenv requests polyline google-generativeai
