# KOVA Project State

Working status only. Decisions live in `KOVA_PROJECT_SPEC.md` unless a later client or user decision overrides them. Do not invent unresolved facts.

## Current phase

**Architecture: COMPLETE. UI refinement: IN PROGRESS.**

V1 surfaces exist for Homepage, PDP, Drop 001, BUILD, Manifesto, Cart, and the global header/footer. Recent work restored the ember homepage hero, made media Shopify-owned, and upgraded the PDP/catalog presentation.

Shopify remains the source of truth for products, variants, prices, inventory, cart, and checkout.

## Completed

- Homepage, PDP, Drop 001, BUILD, Manifesto, Cart architecture
- Global header/footer/navigation shell, shell audit, navigation hardening
- Native Shopify commerce and cart (manually validated)
- Ember homepage hero (wordmark + accent wash; no bundled photo)
- Shopify-owned media model (images and factory videos assigned in Admin / theme editor)
- Amazon-style PDP gallery, 4:5 product frames, card hover second image
- PDP accordions, trust badges under add to cart, footer policy-links section
- `incoming-assets/` gitignored (knowledge only; not shipped with the theme)
- Theme Check passing on last local run

## Locked (do not reopen unless a later phase requires it)

- Homepage section order (`templates/index.json`): hero → drop intro → featured products → pathways → notify
- PDP section order (`templates/product.json`): product → related products
- Drop 001 order: banner → product grid → notify
- BUILD order: page hero → process steps → Drop 001 commerce bridge
- Manifesto order: page hero → statements → Drop 001 commerce bridge
- Cart: native Shopify POST form, no AJAX drawer or custom backend
- Global nav destinations: `/collections/drop-001`, `/pages/build`, `/pages/manifesto`
- Shopify as source of truth for catalog, price, inventory, cart, checkout
- No homepage video
- Instagram stays muted until a URL is confirmed
- Decorative wall-art photos must not be used as product featured images

No longer locked: stacked PDP photography. Multi-image gallery with thumbnails is the current PDP media model. Still no lightbox.

## Current storefront

**Homepage** (`templates/index.json`)

- Order unchanged: hero → drop intro → featured products → pathways → notify
- Heading: `DROP 001 // VELOCITY` / `LIVE NOW`
- Default hero is the unillustrated ember wordmark (graphite field, KOVA low, accent wash). Ember stays even if an image is assigned
- Optional desktop hero image and optional **mobile hero image** (theme editor; mobile used below 750px). No bundled `kova-brand-hero.jpg` path
- Drop intro: eight automotive silhouettes copy; VIEW THE DROP → Drop 001
- Featured products from a selected collection; VIEW ALL → `/collections/drop-001`
- Unresolved: whether Notify stays on Home; assign hero images in Customize when photography is ready

**PDP** (`templates/product.json`, `sections/product.liquid`)

- Order: product → related products
- Gallery: one 4:5 stage (`object-fit: cover`) plus thumbnails when `product.images` has more than one image (thumbs left from 900px, row below on small screens). Clicking a thumb switches the stage. Variant-linked images switch the stage. No lightbox
- Sticky purchase column: drop identity, title, live Shopify price, edition radios, quantity, add to cart
- Trust badges under add to cart (theme-editor; empty lines hide): Secure checkout / Tracked dispatch / Damaged in transit? We replace it.
- Custom size remains WhatsApp enquiry, not a fourth priced variant
- Accordions: Materials & Specs (product description + spec blocks); Shipping & Fulfillment; Warranty & Returns. Last two hide if content is empty. Current defaults match client shipping/replacement copy
- Spec rows: Material 2 mm stainless steel; Finish matte black; Cut fiber-laser, finished all sides; Mounting 15 mm float; Origin designed and made in India
- Related products prefer Drop 001
- Unresolved: remaining seven design-specific product openers (only SVJ copy was supplied); product photography in Shopify Admin

**Product cards** (`snippets/product-card.liquid`)

- Shared by Home, Drop 001, related products
- Uniform **4:5** media frame, `object-fit: cover`
- Second Shopify image reveals on hover (desktop). Touch and reduced-motion keep the first image
- Title, price, sale state from Shopify. Placeholder SVG if no product image

**Drop 001** (`templates/collection.drop-001.json`)

- Order: banner → product grid → notify
- Banner heading override: `VELOCITY`
- Grid 1 / 2 / 3 columns; empty collection does not link to `/collections/all`
- Unresolved: final drop-page copy; whether Notify belongs here; crop once real product photos exist

**BUILD** (`templates/page.build.json`)

- Order: page hero → process steps → Drop 001 commerce bridge
- Hero: `BUILD` / `HOW KOVA IS MADE` plus Made in India description; image off
- Process: CAD / DESIGN → LASER CUTTING → FINISHING → INSPECTION → PACKAGING
- Videos are Shopify-hosted only: one main clip plus optional per-step clips. Hidden until assigned. No bundled factory mp4
- The live BUILD **page** must use the `build` theme template in Admin, or the process/video slots will not appear
- Unresolved: assign factory files in the theme editor; empty step descriptions (CAD, inspection)

**Manifesto** (`templates/page.manifesto.json`)

- Order: page hero → statements → Drop 001 commerce bridge
- Hero: `MANIFESTO` / `STEEL. DESIGNED & REIMAGINED.`
- Four statements from approved manifesto + Made in India origin copy
- Unresolved: whether this heading/statement set is final

**Cart** (`templates/cart.json`)

- Native Shopify cart unchanged
- Empty cart continues to Drop 001
- No invented tax/shipping line on the cart itself (shipping copy lives on the PDP accordion and Shopify policies)

**Global header / footer**

- Header: DROP / BUILD / MANIFESTO / NOTIFY / CART
- Footer: DROP / BUILD / MANIFESTO, muted INSTAGRAM (no URL)
- Policy links section under the footer (`sections/policy-links.liquid`): Terms, Privacy, Shipping, Returns. Uses Shopify Settings → Policies when URLs are empty; otherwise theme-editor URLs. Hidden until at least one destination exists. Privacy currently resolves from the store
- `/collections/all` is not linked from V1 navigation

## Visual system

- Warm bone background, graphite type, ember accent for actions/state (`snippets/css-variables.liquid`, theme settings)
- Not restricted to monochrome
- Client txt files and decorative photos are context. Do not dump them into templates or product media

## Media ownership

Hardcoded: layout, ember/wordmark CSS, nav destinations, KOVA defaults.

Shopify-editable: all images, factory videos, section copy, product data, prices, PDP spec rows, trust lines, accordion bodies, WhatsApp number, Instagram URL, policies.

Do not bundle hero photos or factory videos in `assets/` for display. Unused `kova-brand-hero.jpg` / factory mp4 files may still exist in git from an earlier commit; the theme no longer references them as fallbacks.

## Deferred / pending from merchant

- Product photography for all designs (Admin → Products → Media). First image is the card image; extra images feed gallery + hover
- Optional homepage desktop and mobile hero images (Customize → Hero)
- Factory videos (Customize → BUILD → Process steps). BUILD page template must be `build`
- Remaining seven product descriptions (SVJ opener exists)
- Instagram URL
- Terms / Shipping / Returns policy pages or Shopify policy fields (Privacy already live)
- COD and free India shipping in Shopify Admin if those PDP promises stay

## Unresolved (do not invent)

- Whether Notify stays on Home, Drop 001, and/or the header
- Whether `/collections/all` remains reachable if typed directly
- Instagram URL (footer stays muted)
- Whether manifesto heading/statements are final
- Empty BUILD step copy (CAD, inspection)
- Design-specific openers for the seven non-SVJ products
- Trademark use of model names in product titles (client/legal)
