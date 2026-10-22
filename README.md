# Chelsea HVAC Services — website

Static site, ready for GitHub + Vercel. No build step: the repo root is the site root.

Every file lives in the repo root — there are no folders — so uploading through GitHub's web uploader (which flattens folders) keeps every path working.

## Before going live: replace these tokens

| Token | Where | What to put |
|---|---|---|
| `{{WEB3FORMS_ACCESS_KEY}}` | index.html (2 places: booking form and pop-up) | Access key from web3forms.com, with the client's inbox set as the recipient |
| `{{GA4_MEASUREMENT_ID}}` | index.html (2 places) | GA4 ID, e.g. `G-XXXXXXXXXX` |
| `{{POLICY_EFFECTIVE_DATE}}` | privacy.html, terms.html | Date the policies go live |
| `{{RETENTION_PERIOD}}` | privacy.html | e.g. "12 months" |

## Switched off until there is real content

These sections are built but carry the `hidden` attribute in index.html.

- **Reviews (`#reviews`):** paste three genuine Google reviews, word for word and with the customer's permission, in place of the `{{REVIEW_…}}` tokens. Then delete `hidden`. Never write reviews for the client.
- **Our work (`#work`):** add seven job photos to the repo root as `work-01.jpg` to `work-07.jpg` (`work-01` is landscape and spans two columns). Replace the `{{PHOTO_…_DESCRIPTION}}` alt text, then delete `hidden`.

## Needs a human

- **Legal review:** privacy.html and terms.html are drafts. Have a US attorney review them before launch.
- **Confirm with the client:**
  - "Price agreed before work starts" / "nothing starts until you say yes".
  - That they coordinate with supers and building management.
  - The service area: the five boroughs, plus Long Island and New Jersey.
  - The brand list.
  - That they do window-unit removal and winter storage.
  - Years in business, if it's to be mentioned. The old site said "over a decade"; the old logo said "since 2025".
- **Email:** the site uses `chelseahvacservicesny@gmail.com` throughout (strip, footer, form errors, legal pages, structured data). If the client wants `info@chelseahvacservices.com` instead, find-and-replace it.
- **Missing details to add if the client has them:** street address (footer + `address` in the JSON-LD), opening hours, licence number, and any emergency/out-of-hours availability. Don't claim 24/7 unless it's true.
- **Pop-up offer:** the pop-up has no discount. If the client wants one (e.g. "$XX off your first service call"), add it under the pop-up's lede in index.html.
- **Domain:** in Vercel, add both `chelseahvacservices.com` and `www.chelseahvacservices.com`. HTTPS certificates are automatic. `vercel.json` redirects the bare domain to www and sends HSTS.
- **After launch:**
  - Submit `https://www.chelseahvacservices.com/sitemap.xml` in Google Search Console.
  - Run the live URL through pagespeed.web.dev.
  - In GA4, mark `generate_lead` and `phone_call` as key events (`popup_shown` is also sent).

## How the page behaves

| Where | What | Notes |
|---|---|---|
| Header | Logo centred. Desktop: nav split either side, "Book your service" on the right. Phone: call button, logo, menu button | Shrinks and gains a shadow once you scroll |
| Hero headline | "Too hot. / Too cold. / Handled." wipes up line by line on load | |
| Thermostat dial | Marker swings cold → hot → settles at 70° on an 8 s loop; the number counts with it and the label reads Too cold / Too hot / Handled | Purely illustrative; it never claims to read the visitor's thermostat |
| Booking form | Four real radio options (Not cooling / No heat / Install or replace / Seasonal service). The submit button's wording follows the choice | Service links elsewhere on the page pre-select the matching option |
| Call buttons | Every orange call button "breathes" (2.6 s scale + glow ring) and pauses on hover | |
| Sticky call bar | Fixed to the bottom on every screen size; slides up once on load | |
| Pop-up | **Desktop:** exit intent, when the cursor leaves through the top of the window (armed after 4 s). **Phones/tablets:** opens 25 s after load. Once per browser session, and never after a form has been sent | Edit `MOBILE_DELAY` in the script to change the timer |
| Ticker | Building types scroll continuously; pauses on hover | |
| FAQ | Height-animated accordion | |
| Sections | Fade up once as they scroll into view; coloured rules draw in | |

Everything respects `prefers-reduced-motion: reduce`, which turns the motion off and shows final states.

Forms post to Web3Forms with a honeypot field and a 3-second fill-time check against spam. Phone numbers are validated as 10-digit US numbers and auto-formatted.

## Brand palette (taken from the logo)

| Token | Hex | Used for |
|---|---|---|
| `--navy` | `#012653` | "CHELSEA" navy: hero, dark bands, text |
| `--orange` | `#F57300` | "SERVICES" orange: call buttons only, with navy text (white on this orange fails contrast) |
| `--blue` | `#046DD0` | "HVAC" blue: cooling, accents, focus rings |
| `--mist` | `#F5F6FA` | Quiet section backgrounds |

Text variants that pass WCAG AA: `--orange-t #A74E00` and `--blue-t #024481` on white; `--orange-l #F89640` and `--blue-l #68A7E3` on navy.

Type is **Barlow Condensed** (800, uppercase) for headings and **Barlow** (400–700) for body, both from Google Fonts.

## Logo files

The client's logo was lifted off its white background (the sky, clouds and the blue arc were removed), then upscaled 2× with an EDSR super-resolution model. Files:

| File | Use |
|---|---|
| `chelsea-logo-2x.png` | Master, transparent, 2369 × 1281 |
| `chelsea-logo-1x.png` | Transparent cut-out at the original resolution |
| `logo-600.png`, `logo-1200.png` | Web sizes used on the site |

The logo has navy lettering, so it is only placed on white or light backgrounds.
