# AGENTS.md: coachhec.com

Context for any AI agent or person working in this repo. This is a summary of the planning conversation, so decisions below are settled unless the owner says otherwise.

## Project
A one-page website for a friend of the owner (Jason), a pickleball pro, Hector Garcia ("Coach Hec"), who teaches many lessons. Clients use it to see his lesson options, book time with him, and find his Jimmy Moore Pickleball Complex and Dill Dinkers offerings.

- Domain: `coachhec.com` (availability not yet verified; register at Cloudflare Registrar, or Porkbun/Namecheap)
- Project folder: `/Users/jason/scratch/coachhec`
- Goal: low cost, low maintenance. Weave together free or cheap SaaS and keep custom code minimal.

## Decisions made
- **Site**: hand-written static HTML/CSS/JS (AI-written) instead of Carrd or another builder, for full control of look and feel. No backend, no build step.
- **Hosting**: Cloudflare Pages (free), deployed from a GitHub repo. Domain and DNS also at Cloudflare. GitHub Pages and Netlify were considered and are acceptable fallbacks.
- **Booking**: the coach already has a Calendly account, embedded inline on the page.
- **Contact**: no contact form. A "Message me on Facebook" button links to his Facebook page (open in a new tab), plus a footer Facebook link.
- **Payments**: not in scope for now. Calendly can connect to Stripe or PayPal on a paid plan if wanted later.

## Lesson types
| Type | Format | Booked via |
|---|---|---|
| Private Lesson | One-on-one with the pro | Calendly, 1:1 event type |
| Doubles Match Play with the Pro ("three and me") | Doubles game: coach plus 3 clients, 4 on court. Card copy: "you plus two other players, with the coach playing alongside you" | Calendly group event, capacity 3 (he is not a booking slot) |
| Coached Open Play | Coach supervises three games at once, 12 players on 3 courts | Calendly group event, capacity 12 |

- A minimum attendance (for example 8 for open play) is not enforced by Calendly. He would cancel and notify manually if a session falls short.
- Open question: does he play in open play, or only circulate and coach? Twelve clients fill the courts exactly only if he is not playing.

## Calendly (calendly.com/coachhec)
Existing event types, mapped to site cards (names on Calendly differ from the site):
| Calendly name | Slug | Site card |
|---|---|---|
| One on One | `30min` | Private Lesson |
| Drilling | `one-on-one-clone` | Drilling (format unconfirmed) |
| 3 and Me | `group-clone` | Doubles Match Play with the Pro |
| Group | `group` | Coached Open Play (mapping unconfirmed) |

## Where his bookings live
His schedule spans three places, and the site only controls the first:
1. **Calendly**: private and group lessons booked through the site.
2. **Jimmy Moore Pickleball Complex** (the parks classes; formerly called "county parks" in planning): clients register on the parks WebTrac site (flmelbourneweb.myvscloud.com, a pickleball keyword search). The site shows a button, "Book at Jimmy Moore". The link has the session `_csrf_token` stripped so it does not expire; the site blocks curl, so check it in a browser.
3. **Dill Dinkers Satellite Beach** (the "pro shop" in planning; 1071 S Patrick Drive): clients book on the club's site. The site shows a button, "Book at Dill Dinkers", linking to the location page. The site blocks curl, so check the link in a browser.

Private clients who text him directly also exist.

**Single source of truth: his Google Calendar.** He already uses it. Connect it to Calendly and enable conflict checking. He must add every Jimmy Moore, Dill Dinkers, and direct-booked session to it so Calendly blocks those times and nothing gets double-booked.

## Page structure (index.html, top to bottom)
1. Sticky header with nav (on screens 640px and narrower the links collapse into a ☰ menu button; a small inline script opens and closes it)
2. Hero
3. Lesson types: four Calendly cards, then two outbound cards for Jimmy Moore Pickleball Complex and Dill Dinkers
4. Calendly inline embed (live availability)
5. About Coach Hec
6. Where we play and cancellation policy
7. Contact (Facebook)
8. Footer

Files: `index.html`, `style.css`, `README.md` (deploy steps), this file.

## Status (2026-11-22)
Scaffold created and not yet previewed in a browser. These placeholders still need real values (search the repo for them):
- `FACEBOOK-PAGE`
- `$XX`: prices for each lesson type
- `TODO`: cancellation policy, higher-res photo (`coach.jpg` is a crop from a screenshot of his bio card)

## Next steps
1. Fill in the placeholders above.
2. Preview locally with `python3 -m http.server 8000` and check mobile.
3. Create the three Calendly event types and connect Google Calendar.
4. Push to GitHub, connect Cloudflare Pages, and attach `coachhec.com`.

## Working conventions
- Keep it static: no frameworks, no server code, no form backend.
- Keep external booking links as plain outbound links with `target="_blank" rel="noopener"`.
- Do not invent prices, policies, URLs, or biographical facts. Leave a clearly marked placeholder and ask the owner.
