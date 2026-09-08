# KOVA Project State

Working status only. Decisions live in `KOVA_PROJECT_SPEC.md` unless a later client or user decision overrides them. Do not invent unresolved facts.

## Current phase

**Architecture: COMPLETE. UI refinement: IN PROGRESS.**

V1 surfaces exist for Homepage, PDP, Drop 001, BUILD, Manifesto, Cart, and the global header/footer. The storefront is a dark industrial system matching the approved KOVA mockup: black field, condensed display type, monospace labels, outlined buttons, and the chrome KOVA logo.

Shopify remains the source of truth for products, variants, prices, inventory, cart, and checkout.

## Completed

- Homepage, PDP, Drop 001, BUILD, Manifesto, Cart architecture
- Global header/footer/navigation shell, shell audit, navigation hardening
- Native Shopify commerce and cart (manually validated)
- Dark industrial restyle (black field, condensed headings, monospace labels, outlined CTAs, chrome logo fallback)
- Shopify-owned media model (images and factory videos assigned in Admin / theme editor)
- Cinematic PDP: buy box, details, sizes, lifestyle, mounting. Gallery thumbs under the stage, Shopify variants and prices, no related products
- `incoming-assets/` gitignored (knowledge only; not shipped with the theme)
- Theme Check passing on last local run

## Locked (do not reopen unless a later phase requires it)

- Homepage section order (`templates/index.json`): hero → drop intro → feature highlights → collection teasers → about story → notify
- PDP section order (`templates/product.json`): product → details → sizes → lifestyle → mounting. Related products are not on the product page.
- Drop 001 order: banner → product grid → notify
- BUILD order: page hero → process steps → Drop 001 commerce bridge
- Manifesto order: about hero → story → pillars → statement → close → Drop 001 commerce bridge
- Cart: native Shopify POST form, no AJAX drawer or custom backend
- Global nav destinations: `/collections/drop-001`, `/pages/build`, `/pages/manifesto`
- Shopify as source of truth for catalog, price, inventory, cart, checkout
- No homepage video
- Instagram stays muted until a URL is confirmed
- Decorative wall-art photos must not be used as product featured images

No longer locked: stacked PDP photography. Multi-image gallery with thumbnails is the current PDP media model. Still no lightbox.

## Current storefront

**Homepage** (`templates/index.json`)

- Order: hero → drop intro → features → collection teasers → about story → notify
- Hero is a split layout (copy left, lifestyle image right) with optional Made-in-India badge image
- Current drop is a full-bleed overlay linking to Drop 001; all copy and photography are theme-editor settings
- Feature highlights and collection teasers are merchant-managed blocks (images, titles, status, links). Coming-soon cards do not link
- About story splits a factory image and manifesto/BUILD CTA; overlay graphic is optional
- Featured products and pathways remain in the theme and can be added back in Customize
- Assign hero, drop, collection, and about images in Customize when photography is ready

**PDP** (`templates/product.json`)

- Order: buy box → details → sizes → in your space → mounting. No related-products / You might also like block
- Gallery: 4:5 stage, origin stamp overlay, `01 / 06` counter, thumbnails in a row under the stage. Variant-linked images switch the stage. No lightbox
- Sticky purchase column: drop identity and index, title, subtitle, product description, live Shopify price with tax note, edition radios (title, `custom.dimensions`, price), add to cart. Quantity is hidden and stays 1
- Trust row under add to cart (theme-editor; empty lines hide): Free shipping / Cash on delivery / Made to order
- Details: heading, optional macro `image_picker`, spec blocks (Material / Finish / Elevation). No invented weights
- Sizes: one column per Shopify variant, featured or variant image scaled up, dimensions from `variant.metafields.custom.dimensions`
- Lifestyle: three `image_picker` frames with placeholders until assigned. Connect product metafields in Customize for per-product shots
- Mounting: 15 mm overview, framed hero image, four install steps, close bar. Step photos assigned in Customize
- Unresolved: remaining seven design-specific product openers (only SVJ copy was supplied); product photography in Shopify Admin; variant dimension metafield values

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

- This is the brand story page. There is no separate About template or About nav item.
- Order: about hero → story → pillars → statement → close → Drop 001 commerce bridge
- Hero: `MANIFESTO` / `WE SAW SOMETHING MISSING.`
- Story includes unique manifesto copy that was not already on About (obsession off-screen, no disposable materials, India production path)
- Close still carries `METAL, REIMAGINED. DESIGNED AND MADE IN INDIA.`
- Unresolved: whether this heading/copy set is final

**Cart** (`templates/cart.json`)

- Native Shopify cart unchanged
- Empty cart continues to Drop 001
- No invented tax/shipping line on the cart itself (shipping copy lives in Shopify policies)

**Global header / footer**

- Header: DROP / BUILD / MANIFESTO / FAQ / CONTACT / CART (n), with the KOVA logo asset as fallback
- Footer: logo, DROP / BUILD / MANIFESTO / FAQ, muted INSTAGRAM (no URL)
- Trust bar above the footer (theme-editor items; empty lines hide): Pan India shipping / COD / 7 day returns / Secure payments
- Policy links section under the footer (`sections/policy-links.liquid`): Terms, Privacy, Shipping, Returns. Uses Shopify Settings → Policies when URLs are empty; otherwise theme-editor URLs. Hidden until at least one destination exists. Privacy currently resolves from the store
- `/collections/all` is not linked from V1 navigation

## Visual system

- Pitch-black background, light type, thin silver/white borders (`snippets/css-variables.liquid`, theme settings)
- Display headings, monospace labels/nav, geometric body — all Shopify font pickers
- Outlined buttons with optional ↗; no ember fill as the default action colour
- Client txt files and decorative photos are context. Do not dump them into templates or product media

## Media ownership

Hardcoded: layout, logo asset fallback, CSS, nav destinations, KOVA defaults.

Shopify-editable: all images, factory videos, section copy, product data, prices, PDP spec rows, trust lines, Instagram URL, policies, header/footer logo overrides.

Do not bundle hero photos or factory videos in `assets/` for display. The KOVA logo (`assets/kova-logo.png`) is identity and ships as a header/footer fallback until a theme-editor logo is assigned.

## Deferred / pending from merchant

- Product photography for all designs (Admin → Products → Media). First image is the card image; extra images feed gallery + hover
- Optional homepage desktop/mobile hero, drop, collection teaser, about, badge, and overlay images (Customize)
- PDP details / lifestyle / mounting / install-step images (Customize)
- Variant `custom.dimensions` metafield values
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
