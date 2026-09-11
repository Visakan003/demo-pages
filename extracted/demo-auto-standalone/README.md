# Aireworks Motor Works — automobile demo page

Standalone static demo page. No build step required. Open `index.html` directly or serve with any static file server.

> **Before you use this:** the chat widget on **line 11** of `index.html` points at the **dev** API (`api-dev.csagentiq.com`) with widget ID `cmtx0ow0l00gys6011y194q7t`, which belongs to this page's own `AUTOMOBILE_SERVICE` tenant. Switch the script to the production tenant's embed snippet before any public use, and never borrow another demo's widget ID.

## What it demonstrates

A landing page for a fictional independent garage in Leeds (UK), showing how the CSAgentIQ chat widget sits on an automobile-service site. It follows the same section scaffold as `demo-fsm-standalone`, with its own identity:

- **Look:** graphite and signal orange, hazard-stripe accents, condensed signage type (Barlow Condensed) and IBM Plex Mono for the workshop readouts. The feel is a workshop, not a showroom.
- **Signature element:** a live **workshop board** in the hero showing bay status (MOT in test, awaiting customer OK, scanning, lift free). The Leeds clock is live, and "next free lift" is calculated from the same diary as the booking card.
- **Booking widget:** a **service-bay picker**. You can enter a UK reg on a yellow rear-plate input (optional), then choose the job, day and drop-off time. Each slot shows its bay, and slots are disabled if they're booked, in the past, or too late for the job to finish before closing. The summary line shows the reg, job, date, time, bay and estimated ready time.
- **Services:** diagnostics, brakes, tyres and tracking, servicing (oil and fluids), air-conditioning, pre-purchase inspection, plus a dedicated MOT section.

## Widget and tenant

| | |
|---|---|
| Widget ID | `cmtx0ow0l00gys6011y194q7t` (line 11) |
| Tenant industry | `AUTOMOBILE_SERVICE` |
| Tenant business name (from the widget config) | aireworks motorworks |
| Tenant business hours (from the widget config) | Monday–Sunday 00:00–23:59, America/Los_Angeles |
| Script | `https://api-dev.csagentiq.com/widget/widget.js`, the **dev** API |

**Local database findings (checked 2026-09-11, recorded here but not acted on).** The local Postgres (`home-services-fresh`, the database the app's `.env` points at) has one `AUTOMOBILE_SERVICE` tenant: `cmst34dpq0000u5q8vct8uopc`, named "fdfd", which looks like a test sign-up. It has **no `widget_configs` row**. The whole `widget_configs` table holds a single row, belonging to a `HOME_SERVICES` tenant. The `home-services` database has no automobile tenants at all. A local widget ID wouldn't work here anyway, because the page loads the widget from a hosted API (currently `api-dev.csagentiq.com`), not the local database.

Checked 2026-09-11 against the dev API: the widget script loads (HTTP 200), the config request returns 200, and the chat launcher appears bottom-right at 360, 820 and 1440px, with no console errors and no collisions with page content.

## Images

All photos are downloaded into `demo-assets/` (nothing is hotlinked), cropped to the aspect ratio their slot uses and resized to the width it needs. They're from Pexels, which allows free commercial use without attribution. Credits are recorded here anyway.

| File | Size | Photographer | Source |
|---|---|---|---|
| `hero-mechanic-under-lift.jpg` | 1100×1238, 284 KB | cottonbro studio | https://www.pexels.com/photo/man-in-blue-dress-shirt-holding-red-and-black-power-tool-4489749/ |
| `strip-brake-caliper.jpg` | 800×600, 71 KB | Gustavo Fring | https://www.pexels.com/photo/man-in-blue-uniform-fixing-the-car-s-brake-system-6870307/ |
| `strip-tyre-change.jpg` | 800×600, 126 KB | Gustavo Fring | https://www.pexels.com/photo/man-in-blue-coveralls-standing-beside-an-orange-car-checking-on-the-tire-6870331/ |
| `strip-diagnostics-tablet.jpg` | 800×600, 109 KB | Gustavo Fring | https://www.pexels.com/photo/mechanic-checking-the-engine-of-a-car-6870298/ |
| `band-car-on-lift.jpg` | 1100×880, 160 KB | Artem Podrez | https://www.pexels.com/photo/man-in-blue-coverall-standing-near-a-white-car-8986132/ |
| `auto-favicon.svg` | 32×32, <1 KB | Drawn for this page | — |

`demo-assets/` totals about **768 KB**.

## Placeholders to replace before use

All of these were invented for the demo. The footer disclaimer says so on the page as well.

- **Business name:** Aireworks Motor Works (Ltd)
- **Address:** Unit 4, Wharfside Yard, Armley Road, Leeds LS12 2QX
- **Phone:** 0113 496 0472, from Ofcom's range reserved for drama (Leeds, 0113 496 0000–0999), so it can't reach a real line
- **Email:** workshop@aireworks.example, which uses the reserved `.example` domain, so mail can't reach a stranger
- **Hours:** Mon–Fri 07:30–18:00, Sat 08:00–13:00
- **Credentials:** "DVSA-authorised MOT test station, Class 4 & 7". No authorisation number is shown.
- **Pricing:** MOT £45, Care Plan £14/month, plus the job durations in the booking card
- **Reviews and ratings:** 4.8★ from 900+ reviews, and the testimonials from Sam K., Aisha R. and Gareth T.
- **Workshop board and diary:** masked regs and bay statuses are illustrative. Availability is generated deterministically per date and isn't connected to any real system.

## Preview

```sh
open index.html
```
