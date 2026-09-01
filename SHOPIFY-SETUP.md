# Shopify setup for launch

Everything the theme needs from the Shopify admin. The theme code is done; this is data entry.
Work top to bottom — later steps depend on earlier ones.

## 1. Import the products

`shopify-products.csv` contains all 8 designs with 3 editions each, built from the supplied
dimensions table and copy.

Admin → Products → Import → upload `shopify-products.csv`.

| | |
| --- | --- |
| Products | 8 (`KOVA // SVJ`, `PORSCHE`, `AMG`, `McLAREN`, `VIPER ACR`, `SUPRA MK5`, `GT3 RS`, `CAMARO`) |
| Variants | Studio ₹1,999 · Signature ₹2,999 · Collector's ₹3,999 |
| Option name | `Edition` |
| Inventory | Not tracked, so made-to-order items never show as sold out |
| Weight | Set to 0 — fill in real weights if you ever charge calculated shipping |

Only `KOVA // SVJ` has a design-specific description, because that is the only one you supplied.
The other seven use the shared material, mounting and installation copy. **Send the remaining seven
descriptions and they can be pasted straight into each product.**

## 2. Create the collection

Admin → Products → Collections → Create collection.

- Title: `DROP 001 // VELOCITY`
- **Handle must be `drop-001`** — the theme links to this everywhere
- Type: Automated, condition `Product tag is equal to drop-001` (the CSV already tags them)
- Collection image: optional, used as the Drop banner background

## 3. Product photography

This is the one real gap. There are no photos of the automotive pieces yet, so product cards and
product pages will show a clean placeholder frame until you add them.

For each product: Admin → Products → the product → Media.

- The **first image becomes the grid card image**, so make it the best straight-on shot
- Aim for a consistent crop across all 8 so the grid looks deliberate
- Fill in **alt text** on every image (accessibility and SEO)
- 1600–2000px wide is plenty

## 4. Pages

Admin → Content → Pages. Two are required because the navigation links to them:

| Title | Handle (required) | Theme template |
| --- | --- | --- |
| BUILD | `build` | `build` |
| Manifesto | `manifesto` | `manifesto` |

On each page, set Theme template to the matching name. If BUILD stays on the default page template, the factory video slots will not appear.

Recommended additional pages for the policy copy you supplied:

| Title | Handle | Source file |
| --- | --- | --- |
| Shipping & Delivery | `shipping` | `Full shipping policy draft.txt` |
| Returns & Replacements | `returns` | `DAMAGE REPLACEMENT.txt` |

Paste the supplied text as-is. Shopify also has built-in policy fields under
Settings → Policies, which is where refund/shipping policies belong for checkout.

## 5. Theme editor

Online Store → Themes → Customize.

- **Home → Hero** — default is the ember wordmark (no photo). Optional: assign a hero image here;
  it blends into the field and the orange wash stays on KOVA. Do not upload decorative wall-art
  photos as product images.
- **Home → Featured products** — select the `DROP 001 // VELOCITY` collection.
- **Drop template → Collection banner** — leave "Show image" on; it uses the collection image.
- **BUILD → Process steps** — upload factory clips under Content → Files. Pick the main clip in
  Factory video, then optional short clips on each process step. Nothing plays until you assign a file.
- **Product → detail rows** — Material, Finish and Mounting are already filled with your approved
  wording. These are shared across all products, which is correct since they are the same for every piece.

## 6. Checkout and payments

- Enable **Cash on Delivery**, since the product copy promises it
- Set up **free shipping across India** (Settings → Shipping → flat rate ₹0)
- Confirm guest checkout is on

## 7. Still needed from the client

- Product photography for all 8 designs
- Descriptions for the 7 designs other than SVJ
- Confirmation of the contact details — the supplied file lists them with question marks:
  website `kova.cool`, Instagram `@kova.cool`, email `kovaa.cool@gmail.com`
- A decision on using trademarked model names (Porsche, AMG, McLaren, Supra, Camaro, SVJ)
  for commercial products
