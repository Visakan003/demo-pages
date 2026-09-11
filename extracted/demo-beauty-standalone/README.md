# Marram Beauty Rooms — beauty clinic demo page

Standalone static demo page. No build step required. Open `index.html` directly or serve with any static file server.

> **Before you use this:** replace `data-widget-id="REPLACE_ME_WIDGET_ID"` on **line 11** of `index.html` with the widget ID of a real **`BEAUTY_CLINICS`** tenant on production (admin panel → *Customize chat widget*). Until then, the chat launcher will not appear. That's deliberate: never borrow another demo's widget ID, because a working assistant on the wrong page is worse than a visibly missing one.

## What it demonstrates

A landing page for a fictional beauty studio in Stockbridge, Edinburgh, showing how the CSAgentIQ chat widget sits on a beauty-clinic site. It follows the same section scaffold as `demo-fsm-standalone`, but the tone is deliberately the opposite of the reference page's 24/7 urgency: calm, clean and unhurried.

- **Look:** warm linen, clay and sage, Fraunces serif headings with italic accents, and Figtree for body text. Photos have arch and soft-curve crops, and motion is slower and gentler. There's no "24/7" or emergency framing anywhere.
- **Signature element:** a paper **appointment card** in the hero, tilted slightly over the photo. It shows the named senior beautician, a treatment, and her **next opening**, calculated from the live Edinburgh time and the studio's hours. It also shows whether the studio is open, with a slow "breathing" dot.
- **Booking widget:** a **practitioner and time picker**. Choose a treatment, then a beautician by name (a beautician who doesn't offer that treatment is disabled and says so), or "No preference", then a day and a time. The slots follow each day's real hours, including Thursday late opening and Saturday times. The summary line shows the treatment, beautician, date, time, duration and price.
- **Services:** facials, skincare consultations, brows and lashes, waxing and massage, plus gift vouchers. The person doing the work is always a beautician.
- **Modest claims:** treatments are described as cosmetic, the page says results vary, and anything medical is referred to a GP. There are no clinical or medical promises.

## Widget and tenant

| | |
|---|---|
| Widget ID | `REPLACE_ME_WIDGET_ID` (placeholder, line 11) |
| Intended tenant industry | `BEAUTY_CLINICS` (`tenants."signupIndustry"`) |
| Script | `https://api.csagentiq.com/widget/widget.js`, the production API |

**Local database findings (checked 2026-09-11, recorded here but not acted on).** The local Postgres (`home-services-fresh`, the database the app's `.env` points at) has two `BEAUTY_CLINICS` tenants: `cmsrkud660009u574ptxa94l1` ("sdsd") and `cmt6wgpic000ou5iki9gspy8b` ("dsoinh"). Both look like test sign-ups, and **neither has a `widget_configs` row**. The whole `widget_configs` table holds a single row, belonging to a `HOME_SERVICES` tenant. The `home-services` database has no beauty tenants at all. Even if a local widget ID existed, it wouldn't work here: the page loads the widget from `api.csagentiq.com`, which is production. The ID has to come from a production tenant.

With the placeholder in place, the widget script loads (HTTP 200), the config request returns 404, and the widget logs one console warning and shows no launcher. With a valid config (tested by stubbing the config response, without touching any real tenant), the launcher renders bottom-right and doesn't collide with the page.

## Images

All photos are downloaded into `demo-assets/` (nothing is hotlinked), cropped to the aspect ratio their slot uses and resized to the width it needs. They're from Pexels, which allows free commercial use without attribution. Credits are recorded here anyway.

| File | Size | Photographer | Source |
|---|---|---|---|
| `hero-facial-mask.jpg` | 1100×1238, 329 KB | DΛVΞ GΛRCIΛ (@davegarcia) | https://www.pexels.com/photo/relaxing-facial-treatment-at-spa-37229298/ |
| `strip-brow-shaping.jpg` | 800×600, 90 KB | Nataliya Vaitkevich | https://www.pexels.com/photo/a-hand-plucking-the-eyebrow-hair-of-the-client-8558247/ |
| `strip-back-massage.jpg` | 800×600, 94 KB | KoolShooters | https://www.pexels.com/photo/a-woman-having-a-massage-6628599/ |
| `strip-soap-and-towels.jpg` | 800×600, 122 KB | Karolina Grabowska (Kaboompics) | https://www.pexels.com/photo/stack-of-natural-soap-brush-and-towels-4210374/ |
| `band-serum-facial.jpg` | 1100×880, 111 KB | Fall Fall | https://www.pexels.com/photo/woman-doing-a-treatment-at-beautician-19242406/ |
| `beauty-favicon.svg` | 32×32, <1 KB | Drawn for this page | — |

`demo-assets/` totals about **760 KB**.

## Placeholders to replace before use

All of these were invented for the demo. The footer disclaimer says so on the page as well.

- **Business name:** Marram Beauty Rooms
- **Address:** 4 Hamilton Lane, Stockbridge, Edinburgh EH3 5AX
- **Phone:** 0131 496 0318, from Ofcom's range reserved for drama (Edinburgh, 0131 496 0000–0999), so it can't reach a real line
- **Email:** hello@marram.example, which uses the reserved `.example` domain, so mail can't reach a stranger
- **Hours:** Tue–Fri 10:00–19:00 (Thu until 20:00), Sat 09:00–16:00
- **Beauticians:** Isla Fraser (senior beautician), Morven Reid and Anna Kowalska, all fictional
- **Credentials:** "Level 3 qualified, fully insured beauticians". No licence number is shown.
- **Pricing:** every treatment price, and the membership at £62/month
- **Reviews and ratings:** 4.9★ from 300+ reviews, and the testimonials from Fiona M., Priya D. and Hannah L.
- **Diary:** availability is generated deterministically per date and isn't connected to any real system.

## Preview

```sh
open index.html
```
