# Landing Gallery tools and evidence

Discover current MCP tools and read their descriptions and schemas before calling them. The capabilities below were inspected on 2026-10-31 against `https://www.landing.gallery/api/mcp` (server `landing-gallery` 1.0.0); tool schemas take precedence if they change.

The server needs no account or token. It returns only websites already public on Landing Gallery and is rate limited at the edge.

| Research need | Available tool | Expansion |
| --- | --- | --- |
| Pages of one type across many sites | `search_inspiration` | `page` (1–10000) while `page < totalPages`; at most 4 results per page |
| Every capture for one site | `get_website` with a `slug` | None; returns all page types and devices for that site |

`search_inspiration` arguments: `query` (1–100 chars, optional), `pageType` (`landing_page` default, `pricing_page`, `about_page`, `contact_page`, `careers_page`, `not_found_page`), `device` (`desktop` default, `mobile`), `pagebuilder` slug (for example `webflow`, `framer`, `shopify`, `elementor`, `squarespace`, `tilda`, `vev`, `wix`), `framework` slug (for example `next-js`, `nuxt`, `astro`, `gatsby`, `sveltekit`, `hugo`, `remix`, `eleventy`, `vitepress`, `angular`, `docusaurus`), `page`, `limit` (max 4). Results are newest first.

`get_website` can return page types that search cannot filter on, such as `case_study`, `product_page`, `signup_page` and `blog_post`. Use it to see a strong candidate's whole site.

There is no section search, no flow or journey search, no native app screens, no "deep" or semantic matching, no exclusion list and no video. Do not invent parameters, page types or slugs. If the target is unsupported, explain the gap and settle how the available page types relate to it.

## Query construction

`query` matches site names and descriptions, not what is on the page. In testing, "recruiting" found three hiring products, while "hero video" and "testimonials" found nothing or only a testimonial vendor. So:

- Search by domain, product category or buyer: "recruiting", "scheduling", "accounting", "marketplace". Try singular, plural and neighbouring words; "freelance" may miss where "talent" hits.
- Put page type, device, builder and framework in their filters, never in the query.
- Leave `query` empty to browse a page type or stack and find patterns outside the domain. This is the only way to search by visual pattern: browse, then inspect.
- Use one intent per call. Avoid adjectives, negations and keyword lists.

Start with small batches so every image can be inspected. Increase coverage by changing queries and filters and following promising sites, not by paging through hundreds of unexamined results. Deduplicate by `slug` plus `pageType` plus `device`; prefer distinct patterns over multiple copies of one.

## Images and citations

Search results embed preview images for agent inspection. Previews are cropped to the top 720×1080 of the page, so they show the hero and little else. Inspect returned images before describing their content.

Screenshot fields: `previewUrl`, `fullScreenshotUrl`, `sourcePageUrl`, `width` and `height` (desktop captures are 1366 wide, mobile 400). Some captures are full-page (several thousand pixels tall); many are only the first viewport (1366×1024 or 400×896). Never describe content below a fold-only capture as observed.

The `fullScreenshotUrl` ends in `/public`, which in testing served a thumbnail scaled to 768 px tall, too small to read on long pages. The images are on Cloudflare Images, and replacing `/public` with flexible variant options worked in testing:

- Native resolution: `.../width=<width>,quality=85,format=auto`
- Top section: `.../width=<width>,height=<px>,fit=cover,gravity=top,quality=85`
- A section further down: `.../trim=<top>;0;<bottom>;0,quality=85`, where `top` and `bottom` are pixels removed from each edge

These variants are observed behavior, not documented API. If they stop working, fall back to `previewUrl` and the live `sourcePageUrl`, and record the gap.

Each mentioned site needs a Markdown citation to its returned `galleryUrl`; also give `sourcePageUrl` for the live page. Never manufacture source links or cite a search query as a specific reference.

Captures can be mislabelled: a `pricing_page` capture may show the homepage hero if the site redirected. Check that the image shows the page type it claims and reject or flag it otherwise.

Inline previews are for agent inspection. For user-facing media, use the host's permitted native gallery or display method. When saving images into persistent artifacts, save them in the report's assets folder and keep the canonical gallery link next to each one. These are screenshots of third-party sites: keep them for research use and do not commit them to a public repository without the user's agreement. If assets cannot be saved or displayed, provide canonical links and report the limitation.

## Motion and access limits

Screenshots are static captures of a moment. They contain no hover states, scroll-triggered animation, carousels beyond their first slide, video playback or timing. Only describe these as observed when you have inspected the live page or another first-party source, and cite that evidence separately with the date you looked. The live page may differ from the capture.

If rate limits, outages or unsupported capabilities block a branch, record the gap. Retry only after a changed condition or for a transient failure; do not repeatedly retry unchanged failures. Continue independent work, but disclose incomplete coverage and unfinished outputs. Never substitute fabricated examples.
