# Aireworks Motor Works — automobile demo page

Standalone static demo page. No build step required. Open `index.html` directly or serve with any static file server.

> **Before you use this:** replace `data-widget-id="REPLACE_ME_WIDGET_ID"` on **line 11** of `index.html` with the widget ID of a real **`AUTOMOBILE_SERVICE`** tenant on production (admin panel → *Customize chat widget*). Until then, the chat launcher will not appear. That's deliberate: never borrow another demo's widget ID, because a working assistant on the wrong page is worse than a visibly missing one.

## What it demonstrates

A landing page for a fictional independent garage in Leeds (UK), showing how the CSAgentIQ chat widget sits on an automobile-service site. It follows the same section scaffold as `demo-fsm-standalone`, with its own identity:

- **Look:** graphite and signal orange, hazard-stripe accents, condensed signage type (Barlow Condensed) and IBM Plex Mono for the workshop readouts. The feel is a workshop, not a showroom.
- **Signature element:** a live **workshop board** in the hero showing bay status (MOT in test, awaiting customer OK, scanning, lift free). The Leeds clock is live, and "next free lift" is calculated from the same diary as the booking card.
- **Booking widget:** a **service-bay picker**. You can enter a UK reg on a yellow rear-plate input (optional), then choose the job, day and drop-off time. Each slot shows its bay, and slots are disabled if they're booked, in the past, or too late for the job to finish before closing. The summary line shows the reg, job, date, time, bay and estimated ready time.
- **Services:** diagnostics, brakes, tyres and tracking, servicing (oil and fluids), air-conditioning, pre-purchase inspection, plus a dedicated MOT section.

## Widget and tenant

| | |
|---|---|
| Widget ID | `REPLACE_ME_WIDGET_ID` (placeholder, line 11) |
| Intended tenant industry | `AUTOMOBILE_SERVICE` (`tenants."signupIndustry"`) |
| Script | `https://api.csagentiq.com/widget/widget.js`, the production API |

**Local database findings (checked 2026-09-11, recorded here but not acted on).** The local Postgres (`home-services-fresh`, the database the app's `.env` points at) has one `AUTOMOBILE_SERVICE` tenant: `cmst34dpq0000u5q8vct8uopc`, named "fdfd", which looks like a test sign-up. It has **no `widget_configs` row**. The whole `widget_configs` table holds a single row, belonging to a `HOME_SERVICES` tenant. The `home-services` database has no automobile tenants at all. Even if a local widget ID existed, it wouldn't work here: the page loads the widget from `api.csagentiq.com`, which is production. The ID has to come from a production tenant.

With the placeholder in place, the widget script loads (HTTP 200), the config request returns 404, and the widget logs one console warning and shows no launcher. With a valid config (tested by stubbing the config response, without touching any real tenant), the launcher renders bottom-right and doesn't collide with the page.

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
