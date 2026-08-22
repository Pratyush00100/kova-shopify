# KOVA Project State

Working status only. Decisions live in `KOVA_PROJECT_SPEC.md`. Do not invent unresolved facts.

## Current phase

**Architecture phase: COMPLETE.**

V1 architecture is complete for Homepage, PDP, Drop 001, BUILD, Manifesto, Cart, and the global header/footer/navigation shell.

Next: UI refinement phase. Do not reopen completed architecture.

## Completed

- Homepage architecture
- PDP Phase 1 — commerce (manually validated)
- PDP Phase 2 — visual / conversion refinement (manually validated)
- Drop 001 Phase 3 — collection / catalog refinement
- BUILD V1 architecture
- Manifesto V1 architecture
- Cart V1 architecture
- Global header/footer/navigation shell
- Global shell audit
- Navigation hardening
- Commerce testing
- Cart testing

## Locked

- Homepage architecture (`templates/index.json`)
- PDP architecture (`sections/product.liquid`, `templates/product.json`)
- Drop 001 architecture (`templates/collection.drop-001.json`, `sections/collection.liquid`, `sections/collection-banner.liquid`)
- BUILD architecture (`templates/page.build.json`, `sections/process-steps.liquid`, `sections/build-commerce.liquid`)
- Manifesto architecture (`templates/page.manifesto.json`, `sections/statements.liquid`, `sections/manifesto-commerce.liquid`)
- Cart architecture (`templates/cart.json`, `sections/cart.liquid`)
- Global header/footer/navigation shell (`layout/theme.liquid`, `sections/header.liquid`, `snippets/header-nav-links.liquid`, `sections/header-group.json`, `sections/footer.liquid`, `sections/footer-group.json`)
- Shared product card (`snippets/product-card.liquid`)
- Shared editorial hero (`sections/page-hero.liquid`)
- Shopify as source of truth for products, variants, price, inventory, cart, checkout
- Stacked PDP photography (no carousel / lightbox)
- V1 shopping destination: `/collections/drop-001`

Do not reopen locked surfaces unless a later phase explicitly requires it.

## Current storefront

**Homepage** (`templates/index.json`)

Architecturally complete.

- Order: hero → drop intro → featured products → pathways → notify
- Marquee removed
- Heading: `DROP 001 // VELOCITY`
- Pathways to Drop 001, BUILD, Manifesto
- Featured products pull from a selected collection; VIEW ALL no longer falls back to `/collections/all`
- Hero image blend treatment is implemented (masked, lightened, no image card); the hero image asset and factory video are still missing
- Unresolved: whether Notify stays on Home; final photography/video; leftover drop-intro copy still includes “A limited run of KOVA pieces.”

**PDP** (`templates/product.json`)

Architecturally complete.

- Order: product → related products
- Two-column stacked gallery + sticky purchase column
- Live Shopify title, drop identity, price, variants, quantity, add to cart, description
- Spec rows only when theme-editor values exist
- Related products prefer Drop 001 when the product belongs to it; `/collections/all` is not used as the related-products destination
- Intentionally no carousel or lightbox
- Unresolved: edition option naming; Collection Edition “coming soon”; official material/finish/origin wording; later gallery refinement toward a smaller/multi-image presentation

**Drop 001** (`templates/collection.drop-001.json`)

Architecturally complete.

- Order: banner → product grid → notify
- Banner uses Shopify collection data; empty optional fields stay hidden
- Grid is 1 / 2 / 3 columns
- Empty collection does not link to `/collections/all`
- Notify left in place because Drop 002 capture is unresolved
- Unresolved: final drop-page copy; whether banner heading override stays `VELOCITY`; whether Notify belongs here; later imagery/crop refinement

**BUILD** (`templates/page.build.json`)

Architecturally complete.

- Order: page hero → process steps (video + five stages) → Drop 001 commerce bridge
- Hero: `BUILD` / `HOW KOVA IS MADE`; no description; image off
- Process: CAD / DESIGN → LASER CUTTING → FINISHING → INSPECTION → PACKAGING
- Step descriptions and placeholder images are hidden when empty
- Process layout is 1 column below 1100px and 5 columns from 1100px (no 2-column orphan)
- One Shopify-hosted factory video setting in `process-steps`; muted, inline, looping, viewport-triggered; honors reduced motion
- Notify and Shopify page body are not on BUILD
- Commerce bridge: `DROP 001 // VELOCITY` → `EXPLORE DROP 001` → `/collections/drop-001`
- Unresolved: final BUILD/process copy; video playback currently shows poster/blur rather than confirmed play (needs later investigation); whether more than one manufacturing video is required later; whether the same video is also used on Home

**Manifesto** (`templates/page.manifesto.json`)

Architecturally complete.

- Order: page hero → principles → Drop 001 commerce bridge
- Hero: `MANIFESTO` / `WHAT WE STAND FOR`; no description; image off
- Principles currently shown: “Metal should feel considered, not decorative.” and “We release in drops, not seasons.” Supporting descriptions are empty and do not open empty columns
- Unapproved origin line (“Made in India, built for anywhere.”) is not rendered
- Notify and Shopify page body are not on Manifesto
- Commerce bridge: `DROP 001 // VELOCITY` → `EXPLORE DROP 001` → `/collections/drop-001`
- Unresolved: final manifesto text; whether the current heading and two headlines are locked; whether origin copy is ever approved

**Cart** (`templates/cart.json`)

Architecturally complete.

- Native Shopify cart architecture preserved: one section, native POST form, `cart.items`, native quantity updates, native remove URLs, Shopify checkout handoff, Shopify inventory enforcement
- Empty cart continues shopping to Drop 001 (`collections['drop-001']`, fallback `/collections/drop-001`)
- Line items show product name, meaningful edition/variant (`has_only_default_variant`, not title-contains-“Default”), unit price, quantity, and line total
- Native discount handling: strikethrough original price only when discounted; line-level discount names when present
- Order summary: subtotal and cart-level discount rows only when a cart-level discount exists, then Total
- Responsive layout breakpoint aligned to 900px
- Accessibility: visually-hidden quantity and line-total labels; explicit remove `aria-label`s
- No JavaScript, AJAX cart, drawer, custom backend, or dependencies
- Theme Check passed
- Unapproved tax/shipping copy is not rendered
- Unresolved: shipping, refund, lead time, and delivery promises remain globally unresolved and were not invented here

**Global header / footer / navigation shell**

Architecturally complete. Global shell audit and navigation hardening are done.

- Header: DROP / BUILD / MANIFESTO / NOTIFY / CART
- Footer: DROP / BUILD / MANIFESTO, plus muted INSTAGRAM label (no URL)
- Footer no longer exposes `/collections/all`; SHOP destination removed
- Related products prefer Drop 001
- 404 shopping CTA goes to Drop 001
- Featured products no longer fall back to `/collections/all`
- Invalid `#shop` / `#build` / `#manifesto` defaults were removed or replaced
- Live NOTIFY behavior unchanged (`/#notify`)
- Native Shopify commerce remains unchanged
- Unresolved: remaining V1 shopping label; whether NOTIFY stays in the header; whether footer should match the header exactly; Instagram URL; whether `/collections/all` remains reachable if typed directly

## UI REFINEMENT BACKLOG

Architecture is closed. These items belong to the UI refinement phase only. Do not treat them as architecture reopenings. Do not resolve them here.

1. PDP gallery — replace the current large stacked presentation with a more premium multi-image/smaller-image experience.
2. BUILD video — investigate why the Shopify-hosted video currently shows the poster/blur state instead of confirmed playback.
3. BUILD media model — decide whether/how the 5–6 factory videos should be presented instead of the current single-video slot.
4. BUILD video poster/aspect ratio/mobile treatment.
5. Drop 001 product-image sizing/crop refinement.
6. Homepage hero photography integration once final photography arrives.
7. Homepage overall visual refinement.
8. Typography/font refinement.
9. Global spacing and responsive polish.
10. Product-card visual refinement.
11. Final mobile/desktop visual QA.

## Deferred / pending assets

- Final product photography
- Hero image asset
- Factory / laser-cutting video playback confirmation
- Final drop, BUILD, and manifesto copy

## Next

1. UI refinement phase (see backlog above)
2. Do not invent missing copy or reopen locked architecture

## Unresolved (do not invent)

- Final drop-page copy and whether banner heading override stays `VELOCITY`
- Whether Notify belongs on Drop 001 / homepage / header
- Whether `/collections/all` remains reachable if typed directly (it is no longer linked from V1 navigation)
- V1 nav label after Drop and Shop are merged
- Whether footer should match the reduced V1 header exactly
- Edition option naming; Collection Edition “coming soon”
- Material, finish, origin / “Made in India”
- Shipping, refund, lead time, delivery promises
- Instagram URL
- Final manifesto text; whether current Manifesto headlines are locked
- Final BUILD process copy
- Whether the laser-cutting video lives on BUILD, homepage, or both
- Whether more than one BUILD video is required later
