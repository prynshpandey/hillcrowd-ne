# HillCrowd NE

**From emerging risk to coordinated response.**

A Meghalaya-first crowd safety and emergency **coordination** prototype for event control rooms, field stewards and responders, built around two connected capabilities:

1. **Route resilience before the event.** Test how the venue's approved route network holds up when roads, exits, teams or mobile data fail, so access gaps are found *before* attendees arrive.
2. **Accountable incident coordination during it.** Field reports → verification → explainable prioritisation → assignment with route checks → acknowledgement → resolution, with every stage timed against an agreed target and attributed to whoever must act next.

Crowd-trend monitoring, offline field reporting and post-event replay support that story.

**PLAN → STRESS-TEST → MONITOR → DETECT → VERIFY → PRIORITISE → ASSIGN → RESPOND → REVIEW**

> HillCrowd NE is a coordination aid for authorised event personnel. It is **not** an official emergency authority. It does not forecast weather, issue evacuation orders, close public roads, dispatch ambulances or contact emergency services, and it does not guarantee safe evacuation.

---

## 1. Problem (Meghalaya context)

Events in Shillong and the wider hill region can involve design considerations that matter for crowd safety: hilly terrain and elevation changes, narrow or capacity-constrained approaches, heavy monsoon rainfall that can affect access, uneven mobile connectivity, and the need to coordinate organisers, stewards, medical teams and other responders. These are **considerations to configure and verify per venue**, not assumptions applied to every location.

The gap HillCrowd NE addresses (a problem hypothesis, not a measured finding): after something is reported — congestion at a gate, a medical case, a rain-affected road — the control room has to decide which reports are credible, which approved routes still work, who should respond, and whether they actually did. The prototype makes that sequence faster to understand and fully accountable.

## 2. Target users

| Role | Uses |
|---|---|
| Control-room coordinator | Overview, live map, verify/reject reports, playbooks, assign responders, route and exit status, advisories, analytics |
| Field steward | Mobile reporting app (offline-capable), crowd estimates, own report status, tasks if linked to a steward team |
| Responder | Mobile assignment app: acknowledge, en route, on scene, unable, resolved |
| Administrator | Event/venue configuration, zones and thresholds, route network, approved routes, playbooks, users, audit log |

## 3. What makes it different

- **Route Resilience Engine (signature feature).** Defines the venue's *critical access links* — every zone's walk-out to an assembly point, the medical post to every zone, ambulance access, every approved operational route. It then finds **single points of failure**, links with only one approved route, and **second-failure exposure** (pairs of closures that would cut a link). Coordinators can simulate closures before or during the event without touching live data. Every detour is explained (extra distance, segments, access level, constraints, terrain notes); when the plan has no valid alternative the answer is **"No approved route available"**, never an invented route.
- **Event-readiness stress tests.** Simulate an unusable exit, heavy rain on every rain-exposed section, a team becoming unavailable, or mobile data failing in a zone. The result lists affected links, uncovered zones and missing fallbacks, and is recorded for the readiness review. It never awards a blanket "safe" status.
- **Response accountability.** Each incident's response is split into stages (verification, assignment, acceptance, travel, on-scene resolution, closure confirmation), each with a target set by **severity and incident type**. The queue shows which stage is waiting and who must act next; an overrunning stage escalates once. After a decline, route feasibility is rechecked for every available team before reassignment. Stage times are explicitly *not* performance scores.
- **Explainable, trend-aware risk flags.** Configurable thresholds plus a trend from timestamped manual estimates (rising, stable or falling). Rapid rises are flagged before a threshold is reached, contradictory estimates are flagged, and stale or missing data is never treated as safe. The level is the *maximum* condition, never an average.
- **Trustworthy offline reporting.** Four plain states — *Saved on device*, *Waiting to sync*, *Server confirmed*, *Sync failed — action required* — plus the last successful sync time. Retries are idempotent, so they can't create duplicates.
- **Interactive exercise and replay.** Judges or trainers inject labelled simulated events at any time; afterwards a replay reconstructs what was reported, verified, decided, acknowledged and resolved.

## 4. Features

- **Resilience Lab** — network-health tiles (critical links, single points of failure, single-route links, live access gaps), failure presets (*Lower service road closed*, *…and the ring-road detour fails*, *Monsoon downpour*, *Exit D unusable*, *Medical Team 1 unavailable*, *Mobile data lost in Zone C*), a custom scenario builder, a map of the simulated network with detours and lost routes, an access-link table, single-point-of-failure ranking, second-failure pairs, team coverage per zone, communication fallbacks, and a stress-test log.
- **Live access-gap alerts** — when live closures leave a critical link with no approved route, the Overview shows a red banner, a critical notification and the blocked route on the map. Lost medical access raises the affected zone's risk.
- **Event setup & pre-event planning**:
  - event details, Northeast state/district and risk-rule settings;
  - **response targets by severity with per-type overrides**;
  - a readiness checklist distinguishing *no issue / issue identified / mitigation planned / mitigation verified* — only an administrator can record a verified mitigation;
  - zones with capacity, thresholds, required exits and a **communication fallback**;
  - click-to-place facilities and junctions;
  - route segments with modes, access level, constraint, verified terrain notes and a **rain-exposed** flag;
  - approved operational routes, editable playbooks, and new events.
- **Interactive map** (Leaflet):
  - OSM street basemap, an optional OpenTopoMap terrain-context layer (contours; never used for routing) and a schematic fallback grid;
  - a status chip showing whether tiles loaded or the fallback grid is in use, and whether venue data is live or a cached copy;
  - zones coloured by risk *and* labelled in text;
  - rain-exposed sections, closures, highlighted and alternative routes, legend and a details panel.
- **Field reporting (mobile)** — 9 incident categories, zone buttons or a map pin, severity, urgent flag, quick phrases and an evidence note. Reports and crowd estimates queue on the device while offline.
- **Incident management**:
  - a prioritised queue with a **stage clock** (current stage, time against target, who acts next);
  - unverified/verified labelling and duplicate flagging and merging;
  - verification with confirmed severity, reject/reopen with reasons;
  - a stage timeline, playbook, assignment with route checks, on-behalf updates (e.g. radio confirmation) and full history.
- **Playbooks** for congestion, medical, blocked exit, weather/route disruption, missing person and general issues. Each step shows the approval needed, its target time and status. Safety-authority steps record who authorised them.
- **Route planning** — a planner with mode, access level and avoid-under-review options; approved-route validity with alternatives; segment and exit status controls (reason and source required); closure history.
- **Responders** — status board, current task, acknowledgement and escalation, availability toggle (with a reason), and positions labelled as configured or manually entered (no live GPS).
- **Advisories** — manual entry with issuer, source URL, coverage and issue/expiry time, then verification. Verifying marks rain-affected segments *under review*; it never closes them. No live official feed is integrated.
- **Analytics**:
  - totals, distributions and median report→assignment/acknowledgement/resolution times with sample sizes;
  - per-incident stage breakdown against targets, with context (route length, sync delay);
  - responder acknowledgement, closures, risk-flag history and data-quality indicators;
  - an **exercise replay** and CSV export.
- **Settings & audit** — the audit log, users and roles, and the language selector.
- **Demo mode**:
  - a fictional venue, seeded accounts, and a replayable 9-step scenario with a scoped reset;
  - an **Exercise** button on every control-room page that injects labelled simulated events: congestion, medical incident, conflicting estimate, mobile-data loss, sample rain advisory, lower road closed, ring road closed, Exit D blocked, medical team unavailable.

## 5. Architecture & stack

```
React 18 + Vite + TypeScript (client/)  ──fetch + SSE──▶  Express 4 + Zod (server/)  ──▶  SQLite (node:sqlite, built into Node 22)
         │                                                     │
         └──────────── shared/ (types, risk engine, route engine, workflow, permissions) ────────────┘
```

- Single process in production: Express serves the API and the built client.
- Live updates: Server-Sent Events change notifications + 20 s polling fallback.
- No paid services, no API keys, no native build steps. See [ARCHITECTURE.md](ARCHITECTURE.md).

## 6. Prerequisites

- **Node.js 22.13 or newer** (uses the built-in `node:sqlite` module). Check with `node -v`.
- npm 10+.
- Internet access only for `npm install` and (optionally) map tiles. The demo works without tiles.

## 7. Installation & running

**Quickest path:** install Node.js 22 LTS (22.13+) from https://nodejs.org, then in the project folder run `./setup.sh` (macOS/Linux) or double-click `setup.bat` (Windows). Start with `npm start` (or `start.bat`) and open http://localhost:4000.

Manual steps:

```bash
cd hillcrowd-ne          # the folder you downloaded or cloned
npm install
npm run setup      # creates data/hillcrowd.db, seeds demo data, builds the client
npm start          # http://localhost:4000
```

Development mode (hot reload; API on :4000, web on :5173):

```bash
npm run dev        # open http://localhost:5173
```

### Environment configuration

Defaults work out of the box. To override, copy `.env.example` to `.env` **or** set variables in your shell (the server reads `process.env`; it does not auto-load `.env` files, so export them, e.g. `PORT=5000 npm start`).

| Variable | Default | Meaning |
|---|---|---|
| `PORT` | `4000` | HTTP port |
| `DB_PATH` | `data/hillcrowd.db` | SQLite file (created automatically) |
| `DEMO_MODE` | `true` | Seeds demo accounts/event, enables scenario panel and reset. Set `false` for a non-demo deployment |
| `SESSION_HOURS` | `12` | Session lifetime |
| `COOKIE_SECURE` | `false` | Set `true` behind HTTPS |

### Database & seed data

- The schema is created automatically on start (`server/schema.ts`, version recorded in `meta`).
- `npm run seed` — idempotently seeds playbooks, demo users and the demo event.
- `npm run seed -- --reset` — resets only the demo event.
- To start completely fresh: stop the server and delete `data/hillcrowd.db*`.

## 8. Demo access

With `DEMO_MODE=true`, the sign-in page shows a clearly labelled **DEMO ACCESS** panel; each button signs in through the normal password check. Password for all demo accounts: **`hillcrowd-demo`**.

| Username | Role | Lands on |
|---|---|---|
| `admin.demo` | Administrator | Overview (all configuration) |
| `coord.demo` | Control-room coordinator | Overview |
| `steward.gateb` | Field steward (Gate B) | Field app |
| `steward.market` | Field steward, linked to *Steward Team Bravo* | Field app (+ My tasks) |
| `team.alpha` | Responder (Steward Team Alpha) | Responder app |
| `medic.one` | Responder (Medical Team 1) | Responder app |

Demo accounts are not created when `DEMO_MODE=false`.

### Screenshots

| Sign-in with the demo-access panel | Control-room overview |
|---|---|
| ![Sign-in page showing the demo-access panel](screenshots/running-login.png) | ![Control-room overview with risk tiles and the live map](screenshots/running-overview.png) |

## 9. Replaying the demo and running an exercise

- **Scripted scenario:** sign in as `coord.demo` → **Overview** → *Scenario: escalating congestion during adverse weather*. Press **Run step** for each of the 9 steps, or do them manually — the panel detects progress.
- **Live exercise:** press the purple **Exercise** button (bottom-right on any control-room page) to inject labelled simulated events at any time. Try *Lower service road closed* then *Upper ring road (north–east) closed*: the Overview raises an **ACCESS GAP** banner, and the Resilience Lab shows that the medical vehicle route has no approved alternative.
- **Pre-event stress test:** open **Resilience Lab**, pick a preset or build a scenario, and press **Record** to add it to the readiness log.
- **Review:** open **Analytics → Exercise replay** and press Play.
- **Reset:** **Reset demo scenario** (on the Overview) restores the initial state, deleting only demo-event data.

A timed presenter script is in [DEMO_SCRIPT.md](DEMO_SCRIPT.md). No external API is required.

## 10. Tests

```bash
npm test             # 73 unit + API integration tests (Vitest + Supertest, in-memory DB)
npm run typecheck    # TypeScript, whole project
# Browser smoke test (needs a running server and a Chromium binary):
npm run build && npm start &
BASE_URL=http://localhost:4000 CHROMIUM_PATH=/path/to/chrome npm run test:e2e
```

Details and latest results: [TESTING.md](TESTING.md).

## 11. Known limitations

- **Fictional venue.** The demo layout, its roads, handover point and capacities are invented and only positioned illustratively in the Shillong area. No real venue plan, facility or emergency resource is represented.
- **No live official advisory feed.** Advisories are entered and verified manually; the demo advisory is a labelled SAMPLE.
- **No live GPS.** Responder positions are base posts or manually entered.
- **Terrain.** OpenTopoMap contours are visual context only; slope/terrain constraints are text notes entered by venue staff. No elevation-based routing.
- **Routing** uses configured distances on a small curated graph (bidirectional segments, shortest distance among permitted segments). It does not model travel time, congestion or one-way rules.
- **Occupancy** comes from manual estimates; no sensors or CCTV integration. Rate-of-change is a simple linear projection, labelled as such.
- **Offline support is implemented but has only been tested with browser offline emulation**, not under real field connectivity (weak signal, captive portals, long outages). The field app queues reports and crowd estimates in browser storage; the production build caches the app shell and viewed map tiles. A first visit must be online. Responder status updates need a connection. Clearing browser storage discards undelivered items. There is no image upload (an evidence-note field is provided).
- **Real map tiles were not verified in the development environment** (tile servers were unreachable there); only the schematic fallback was exercised. Check tiles on the presentation machine.
- **Resilience analysis** covers only the configured network and the failures you simulate; it does not model travel time, congestion, one-way rules or physical safety.
- **Crowd trends** are straight-line fits over manual estimates — not forecasts or measured density. Gate entry/exit counts can be entered as an estimate source but are not reconciled automatically.
- **Languages**: English only. The i18n structure supports Khasi, Garo and others, but no translations are shipped because none have been verified by competent speakers.
- **Scale/ops**: single-process SQLite prototype; in-memory login throttling and SSE bus; no SSO, MFA, password reset, backups or high availability.
- `node:sqlite` is marked experimental in Node 22.

## 12. Security considerations

- scrypt password hashing; random session tokens stored only as SHA-256 hashes; `HttpOnly`, `SameSite=Lax` cookies (`Secure` configurable); login throttling.
- CSRF mitigation: state-changing requests require a custom header (forces a CORS pre-flight cross-site; CORS is not enabled).
- Every mutating route validates input with Zod and checks permissions and event membership **on the server**; the client only hides controls.
- Stewards see only their own reports; responders only their assignments; coordinators cannot change verified venue configuration, users or verified mitigations; admins cannot change their own role.
- The audit log and incident history cannot be edited or deleted **through the application**: SQLite triggers reject UPDATE/DELETE, incidents cannot be deleted, and the demo reset can purge only rows flagged as demo data. This is *not* tamper-proof: anyone with direct access to the database file (or who can drop the triggers) could still alter records. A production deployment would add write-once external log storage or hash-chained, signed entries.
- CSP and other security headers in production; CSV export neutralises spreadsheet formula injection.
- Minimal personal data: display names only; the map shows no personal details.
- No secrets are needed or stored in the repository.

## 13. Roadmap

1. Pilot with a real organiser using their verified venue plan, route network and safety plan; co-design thresholds and playbooks with their safety officer.
2. Verified Khasi and Garo interface translations reviewed by competent speakers; plain-language field prompts.
3. Integration with official advisory feeds **only where an authorised, documented interface exists**, with attribution and timestamps.
4. Optional people-counting inputs (gate counters) with data-quality flags.
5. SMS/USSD or radio-gateway fallback for field reports in no-data areas.
6. Travel-time-aware routing, one-way rules, and verified elevation data for steep-approach constraints.
7. PostgreSQL, SSO/MFA, backups and multi-control-room deployments for district-level use across Northeast states.

## 14. Repository layout

```
shared/        Domain types, risk engine, route engine, workflow, permissions (pure, unit-tested)
server/        Express app, SQLite schema & store, services, demo seed
client/        React app: control-room pages, field & responder apps, map, i18n, service worker
tests/         Vitest unit/API tests; tests/e2e/smoke.ts browser smoke test
```

Licensed under the [MIT License](LICENSE).
