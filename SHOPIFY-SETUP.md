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

Admin → Content → Pages. These are required because the navigation links to them:

| Title | Handle (required) | Theme template |
| --- | --- | --- |
| BUILD | `build` | `build` |
| Manifesto | `manifesto` | `manifesto` |
| FAQ | `faq` | `faq` |

Do not create a separate About page. Manifesto is the brand story page. If an About page already exists in Admin, unpublish or delete it so navigation only uses `/pages/manifesto`.

On each page, set Theme template to the matching name. If BUILD stays on the default page template, the factory video slots will not appear. If FAQ stays on the default page template, the accordion layout will not appear.

If the header uses a Shopify navigation menu instead of the fallback links, add FAQ between Manifesto and Notify in that menu.

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
- **Product page** — order is buy box → details → sizes → in your space → mounting.
  Assign photography in Customize: details macro, three lifestyle frames, mounting hero, and
  four install-step photos. Empty slots keep a dark placeholder. Product gallery images still
  live on each product in Admin, not in theme `assets/`.
- **Variant dimensions** — Settings → Custom data → Variants → Add definition. Name
  `Dimensions`, namespace and key `custom.dimensions`, type Single line text. Enter each
  variant’s size (for example `27" × 7"`). Size cards and edition boxes read this metafield;
  if it is empty, title and price still show.
- **FAQ** — Custom data definitions and entries (section 6). After they exist, Customize →
  FAQ page can optionally pick and reorder categories. Leave the picker empty to show every
  published category automatically.
- **Product descriptions** — keep the Shopify description to the short buy-box opener. Specs,
  mounting and install copy now live in product-page sections.
- **Product → detail rows** — Material, Finish and Elevation sit in the Details section and are
  shared across all products, which is correct since they are the same for every piece. Leave
  weight empty until you have real numbers.

## 6. FAQ metaobjects

The FAQ page does not ship answers in the theme. Categories and Q&A live in Shopify Custom data.

Admin → Settings → Custom data → Metaobjects.

### Entry definition

1. Add definition. Name `FAQ entry`, type `faq_entry`.
2. Storefront access: **Read**.
3. Fields:

| Name | Key | Type | Required |
| --- | --- | --- | --- |
| Question | `question` | Single line text | Yes |
| Answer | `answer` | Rich text | Yes |

Set display name to Question.

### Category definition

1. Add definition. Name `FAQ category`, type `faq_category`.
2. Storefront access: **Read**.
3. Fields:

| Name | Key | Type | Required |
| --- | --- | --- | --- |
| Title | `title` | Single line text | Yes |
| Entries | `entries` | List of metaobjects → `faq_entry` | No |

Set display name to Title.

### Suggested categories

Create one category entry per row. Do not invent answers — paste only copy you have approved.

| Title | Handle |
| --- | --- |
| PRODUCTS | `products` |
| MOUNTING | `mounting` |
| ORDERS | `orders` |
| RETURNS / REPLACEMENTS | `returns-replacements` |
| COLLECTOR'S EDITION | `collectors-edition` |
| OTHER | `other` |

Then create FAQ entry metaobjects and attach them to the matching category’s Entries list.

Until categories exist, the FAQ page still shows the heading and diagrams, with an empty accordion.

## 7. Checkout and payments

- Enable **Cash on Delivery**, since the product copy promises it
- Set up **free shipping across India** (Settings → Shipping → flat rate ₹0)
- Confirm guest checkout is on

## 8. Still needed from the client

- Product photography for all 8 designs
- Descriptions for the 7 designs other than SVJ
- Confirmation of the contact details — the supplied file lists them with question marks:
  website `kova.cool`, Instagram `@kova.cool`, email `kovaa.cool@gmail.com`
- A decision on using trademarked model names (Porsche, AMG, McLaren, Supra, Camaro, SVJ)
  for commercial products
