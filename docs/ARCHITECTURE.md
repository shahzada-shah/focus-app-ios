# Architecture

KAZI Focus is a SwiftUI app with a Metal planet renderer and RealityKit ships. All data stays on the device.

## Layers

| Layer | What it holds |
|---|---|
| **Screens** | Cockpit (map, routes, preflight), FlightView (countdown, progress), Hangar (ships, unlocks), Flight log (stats, ranks, milestones). |
| **Session** | `FlightSession` (timer and phases), `FlightDiscipline` (Cruise, Autopilot, Hard burn), Live Activity, App Intents for Siri and Control Center. |
| **Model** | On-device store: XP, flights, streaks; destinations and route gates; ranks; milestones; discovered worlds. |
| **Render** | `ProceduralPlanet` (Metal shader), hulls (USDZ in RealityKit), the star sky, console chrome. |

## Decisions

- **One sun.** Planets and ships share a light direction, so every scene reads as one photograph.
- **Progress drives the scene.** The destination planet grows with flight progress; the size curve is defined once and reused by the Live Activity glyph.
- **Earned, not bought.** Every unlock comes from focus time. There are no purchases.
- **Honest copy.** The flight plan is a list you write; the app never claims to block apps. An optional iOS Focus link does the silencing.
- **Calm motion.** Transform and opacity only, no loop faster than 0.8 s, and every infinite loop stops under Reduce Motion.
