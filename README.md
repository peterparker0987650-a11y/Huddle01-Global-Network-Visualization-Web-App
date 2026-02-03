# Huddle01 Global Network Visualization Web App

A real-time network observability experience for the Huddle01 decentralized meeting network. The app renders a rotating 3D Earth, plots node markers, and streams live stats for nodes, meetings, and users.

## Goals
- Provide a public-facing demo that proves Huddle01’s infrastructure is global and live.
- Offer a technical explorer for node distribution and activity.

## Core Features (Phase 1)
- Rotating 3D Earth (react-three-fiber + drei)
- Node markers plotted via latitude/longitude
- Active vs inactive node styling
- Live stats panel (total nodes, active nodes, active meetings, active users)
- Real-time updates via WebSocket
- Minimal UI that explains Huddle01 and its importance

## Phase 2+ Enhancements
- Pulses/animations for meeting start events
- Node load visualization
- Region aggregation
- Mobile fallback (2D map)

## Tech Stack
**Frontend**
- React (Vite)
- Three.js, @react-three/fiber, @react-three/drei
- TailwindCSS
- Zustand
- WebSocket client

**Backend**
- Node.js (Express or Fastify)
- ws (WebSocket server)
- Optional Redis caching

## Data Model
### Node
```json
{
  "id": "node-123",
  "lat": 37.7749,
  "lng": -122.4194,
  "region": "NA",
  "active": true,
  "activeMeetings": 4,
  "activeUsers": 32
}
```

### Global Stats
```json
{
  "totalNodes": 120,
  "activeNodes": 94,
  "activeMeetings": 318,
  "activeUsers": 1284,
  "timestamp": 1700000000
}
```

## WebSocket Payload
```json
{
  "stats": {
    "totalNodes": 120,
    "activeNodes": 94,
    "activeMeetings": 318,
    "activeUsers": 1284
  },
  "nodes": [
    {
      "id": "node-123",
      "lat": 37.7749,
      "lng": -122.4194,
      "region": "NA",
      "active": true,
      "activeMeetings": 4,
      "activeUsers": 32
    }
  ]
}
```

## UI Structure
```
App
 ├─ Header (logo + title)
 ├─ StatsPanel
 ├─ GlobeScene
 │   ├─ Earth
 │   ├─ NodeMarkers
 │   └─ Lighting
 ├─ Legend
 └─ Footer (About Huddle01 + links)
```

## Privacy & Geo Data
All geo coordinates should be approximate (city-level or region-level), never precise, to avoid privacy leaks.

## Deployment Targets
- **Frontend:** Vercel / Netlify
- **Backend:** Fly.io / Railway
- **WebSocket:** WSS with environment-based configuration
