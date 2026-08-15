# KOVA Project Spec

This file is the current product and experience spec for KOVA V1.

Use it with `.cursor/rules/kova.mdc` (always-on agent rules) and `AGENTS.md` (Shopify Skeleton / Liquid architecture). Do not rewrite `AGENTS.md` here.

If this spec conflicts with older prompts or with the current storefront, **the latest KOVA decision in this spec wins**. If a fact is not decided, it is listed as unresolved. Do not invent an answer.

The storefront is **not yet aligned** with several latest decisions. This spec records both the decided direction and the lagging implementation so later UI work can follow the decision, not the outdated theme copy.

---

## 1. Brand and commerce

**Decided**

* KOVA is a premium design brand creating precision-cut metal objects for interiors.
* Domain: kova.cool
* Shopify development store: kova-9882
* GitHub repository: kova-shopify
* Shopify is the commerce platform and source of truth for products, variants, inventory, customers, carts, checkout, orders, payments, shipping, discounts, and store administration.
* Do not build a custom backend for normal commerce.
* Do not recreate Shopify checkout, payment processing, cart state, or order management.
* Guest checkout is preferred for V1.
* Do not invent shipping, tax, refund, or delivery policies.
* Do not invent production, shipping, or delivery promises.

**Customer-facing language**

Do not call KOVA products "metal wall art". Prefer, by context:

* design pieces
* wall pieces
* objects
* editions
* KOVA pieces

---

## 2. V1 product

**Decided**

* First release: **DROP 001 // VELOCITY**
* Naming format is `DROP 001 // VELOCITY`. Do not use `DROP 001 — VELOCITY`.
* Initial go-live catalog: **maximum 8 products**.
* Products are primarily automotive-inspired, plus other original design pieces.
* Material/finish is fixed in V1 unless a specific product requires otherwise.
* Products are primarily made to order after a small amount of sample stock.
* New drops are expected about monthly to every two months.
* Small objects from production remnants/offcuts may exist later as complimentary **KOVA Fragments**.

**Sizing / editions**

V1 pieces are sold as editions, not as an open size system:

| Edition | Dimensions | V1 status |
| --- | --- | --- |
| Studio Edition | 27 inches × 2.3 feet | For sale |
| Signature Edition | 37 inches × 3.3 feet | For sale |
| Collection Edition | not specified | Coming soon |

When Shopify data exists, editions should be variants. Do not hardcode edition prices or inventory in the theme.

**Not decided**

* Product names, handles, SKUs, and prices
* How many of the maximum 8 products ship in the first live catalog
* Which pieces are automotive-inspired vs other original designs
* The exact V1 material and finish names
* Whether KOVA Fragments appear anywhere on the V1 site
* How Collection Edition is shown on product pages, if at all

---

## 3. Navigation

**Decided page types**

* Home
* Drop / Collection
* Product
* BUILD
* Manifesto
* Cart

**V1 navigation decision**

* In V1, Drop 001 and Shop are **one shopping destination**.
* Do not create separate Drop and Shop destinations until multiple drops exist (V2).
* Cart remains a header action, not a primary story page.
* BUILD and Manifesto are dedicated pages, not homepage-only sections.

**Currently implemented (lags the decision)**

Header fallback links:

* DROP → `/collections/drop-001`
* SHOP → `/collections/all`
* BUILD → `/pages/build`
* MANIFESTO → `/pages/manifesto`
* NOTIFY → `/#notify`
* CART → Shopify cart URL

Footer fallback links currently repeat DROP / SHOP / BUILD / MANIFESTO, plus INSTAGRAM.

**Not decided**

* The remaining V1 shopping label after Drop and Shop are merged (`DROP`, `DROP 001`, `SHOP`, or something else)
* Whether NOTIFY stays in the header once Drop/Shop are merged
* Instagram URL
* Whether footer should match the reduced V1 header exactly

---

## 4. Homepage

**Decided role**

The homepage is a curated entry point. It should:

* Create curiosity
* Introduce the current drop
* Showcase selected products
* Establish trust
* Tease manufacturing
* Introduce KOVA's philosophy
* Encourage the next action

It should sell the brand and the current release. Detailed shopping information belongs on product/collection pages. Detailed manufacturing belongs on BUILD. Detailed philosophy belongs on Manifesto.

**Decided V1 hero**

* Predominantly black
* Large KOVA wordmark, positioned lower in the composition
* A real automotive/product image blended into the black background
* Not a separate rectangular image card
* Collection name: `DROP 001 // VELOCITY`

**Decided motion / media**

* No scrolling/moving marquee
* Motion only when it supports the product or story
* Authentic product photography and real factory video as primary visual assets
* One short laser-cutting video may autoplay, muted and looped, when its section enters the viewport
* Honor `prefers-reduced-motion`

**Currently implemented (lags the decision)**

Homepage template order:

1. Hero — heading still `DROP 001 — VELOCITY`, subheading `LIVE NOW`, CTA `EXPLORE DROP 001`
2. Marquee — still present
3. Drop intro — still describes "Laser-cut metal wall art"
4. Featured products — `SELECTED PIECES`, up to 3 from a chosen collection
5. Pathways — DROP 001 / BUILD / MANIFESTO
6. Notify — `BE FIRST ON DROP 002`

Hero currently supports an optional image overlay; it does not yet implement the lower wordmark + blended automotive treatment.

**Not decided**

* Final homepage section order after the marquee is removed
* Whether notify remains on the homepage, only in the header, or both
* The exact hero image asset
* The exact laser-cutting video asset and which homepage or BUILD section it lives in

---

## 5. Collection / Drop page

**Decided**

* V1 shopping happens in one destination: Drop 001 / VELOCITY.
* `/collections/drop-001` is the current drop template (`templates/collection.drop-001.json`).
* Product and collection data must come from Shopify.
* No marquee.

**Currently implemented**

Drop 001 template:

1. Collection banner — `DROP 001` / `VELOCITY`
2. Marquee — still present
3. Product grid
4. Notify

Default collection template is a generic banner + grid and is not the V1 shopping destination.

**Not decided**

* Whether `/collections/all` should redirect, be hidden, or stop being linked
* Final drop-page copy

---

## 6. Product page

**Decided**

Product pages are detailed and commerce-focused. Specialist ecommerce sites such as Modello Turbo may inform information hierarchy only. Do not copy another brand's design.

Each product page must communicate:

* Product name
* Drop
* Images
* Price
* Size / edition
* Exact dimensions
* Material
* Finish
* Production information
* Add to cart

Photography is the primary visual asset. Do not keep designing around placeholders once real photography exists.

Price, inventory, and variant/edition data must come from Shopify when available.

**Currently implemented**

* Media gallery or Shopify placeholder
* Drop eyebrow (template default: `DROP 001`)
* Title and Shopify price
* Variant select only when a product has more than one variant
* Quantity and add to cart
* Product description
* Hardcoded detail blocks: Material `Powder-coated mild steel`, Finish `Matte black`, Made in `India`
* Related products from the same drop

The current page does not yet present editions, exact dimensions, or production information as first-class V1 content.

**Not decided**

* Shopify option name for editions (`Edition` vs `Size` vs something else)
* How Collection Edition "coming soon" appears on the product page
* Which production facts are allowed on the product page
* Whether "Made in India" is approved customer-facing copy
* Gallery behavior beyond a simple stacked image list

---

## 7. BUILD

**Decided**

BUILD is a major trust and differentiation asset. It is a dedicated page.

The process to communicate:

**CAD/design → laser cutting → finishing → inspection → packaging**

Use authentic factory imagery/video when available. Do not invent manufacturing claims.

**Currently implemented (lags the decision)**

BUILD template (`templates/page.build.json`):

1. Page hero — `HOW KOVA IS MADE`
2. Process steps still framed as **DRAW / CUT / FINISH / SHIP**
3. Shopify page body
4. Notify

Current step copy includes unverified claims (powder-coating, numbered drop cards, packing with mounting hardware). Treat those as placeholders unless separately confirmed.

**Not decided**

* Final BUILD copy for each of the five decided stages
* Whether the laser-cutting video lives on BUILD, the homepage, or both
* What inspection and packaging may claim without inventing process detail

---

## 8. Video

**Decided**

* Primary motion asset: one short laser-cutting / factory video
* Autoplay, muted, looped
* Starts when its section enters the viewport
* Authentic factory footage, not stock
* Honor reduced-motion preferences
* Do not add extra decorative video or animation

**Currently implemented**

No storefront video section or asset is wired yet. Homepage and collection pages still use a CSS marquee instead.

**Not decided**

* Video file, duration, and aspect ratio
* Exact section placement
* Poster image
* Whether the video is a Shopify file, theme asset, or external host

---

## 9. Sizing

**Decided**

See the edition table in [V1 product](#2-v1-product).

Studio and Signature are the sellable V1 sizes. Collection Edition is coming soon.

**Not decided**

* Which value is width vs height
* Why the two dimensions use mixed units (inches and feet)
* Thickness / depth / standoff from the wall
* Mounting method
* Whether dimensions are shown as `27" × 2.3'` or converted to a single unit
* How editions map onto Shopify variant options and inventory

---

## 10. Manifesto, cart, and other pages

**Decided**

* Manifesto is the dedicated philosophy page.
* Cart uses Shopify cart behavior. Do not rebuild checkout.
* Guest checkout is preferred for V1.

**Currently implemented**

Manifesto template:

* Hero `WHAT WE STAND FOR`
* Three placeholder principles, including "Made in India, built for anywhere."
* Shopify page body

Cart template: Shopify cart list, quantity updates, subtotal, checkout. Taxes/shipping note is Shopify's generic checkout sentence, not a KOVA policy.

**Not decided**

* Final manifesto text
* Whether origin/"Made in India" is a locked brand claim
* Refund, shipping, and delivery copy

---

## 11. V1 vs V2

### V1 — build this

* One drop: DROP 001 // VELOCITY
* Maximum 8 products
* One shopping destination (no separate Drop and Shop)
* Studio and Signature editions for sale
* Collection Edition marked coming soon only if a later decision says to show it
* Guest checkout
* Fixed material/finish unless a product requires otherwise
* Homepage as curated brand/drop entry
* Product pages as the detailed commerce surface
* BUILD as CAD → laser cutting → finishing → inspection → packaging
* One short laser-cutting video
* No marquee
* No "metal wall art" copy
* No invented shipping, tax, production, or delivery promises

### V2 — do not build yet

* Separate Drop and Shop navigation once multiple drops exist
* Collection Edition as a sellable size
* Richer BUILD with more authentic factory imagery/video
* Additional drops on the monthly-to-two-month cadence
* Any broader catalog, account, or merchandising behavior not required for the first release

---

## 12. Design system (current theme tokens)

These are implemented theme defaults, not new business claims:

* Type: Archivo
* Background: `#EDEDEC`
* Foreground: `#0A0A0A`
* Wide page width default: `110rem`
* Header is sticky
* Visual direction: industrial, editorial, minimal, premium, strong type, generous whitespace, restrained motion

Do not add glassmorphism, excessive gradients, decorative blobs, generic stock photography, or AI-template layout patterns. The current header `backdrop-filter` blur is a lagging implementation detail and should not be treated as a locked design decision.

---

## 13. Unresolved business ambiguity

Do not fill these in during UI work. Ask, or leave them configurable.

1. Exact V1 nav label for the single shopping destination after Drop and Shop are merged.
2. Whether NOTIFY remains in the header/footer.
3. Product names, count within the max of 8, prices, and handles.
4. Official V1 material and finish wording.
5. Whether "Made in India" / Indian origin is approved customer-facing copy.
6. Edition orientation (which side is 27 inches vs 2.3 feet) and whether mixed units are intentional.
7. Wall depth, mounting method, and included hardware.
8. How Collection Edition "coming soon" is presented, or whether it is hidden in V1.
9. Shopify variant option naming for editions.
10. Whether KOVA Fragments appear in V1.
11. Final BUILD copy for inspection and packaging; current SHIP/hardware/drop-card copy is unverified.
12. Laser-cutting video asset, duration, poster, and placement.
13. Hero image asset.
14. Instagram URL.
15. Shipping, tax, refund, lead time, and delivery promises.
16. Whether `/collections/all` remains reachable.
17. Final manifesto text.
18. Whether the notify capture for Drop 002 is required for V1 go-live.

---

## 14. Implementation lag checklist

The current theme still contains these superseded patterns. They are **not** the latest direction:

* `DROP 001 — VELOCITY` instead of `DROP 001 // VELOCITY`
* Separate DROP and SHOP destinations
* Homepage and Drop 001 marquees
* "Laser-cut metal wall art" in drop intro copy
* BUILD steps as DRAW / CUT / FINISH / SHIP
* Product details hardcoded instead of Shopify edition/dimension data
* No viewport-triggered factory video
* Header blur/glass treatment

Do not copy those patterns forward when making the next UI changes.
