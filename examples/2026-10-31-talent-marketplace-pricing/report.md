# Talent marketplace pricing: Landing Gallery research

Sample run of `landing-gallery-research`, 2026-10-31. Source: Landing Gallery MCP
(`https://www.landing.gallery/api/mcp`), called directly.

## Brief (assumed for this sample)

This sample skips both grilling rounds, so the brief below is an assumption, not a confirmed one.

- **Page:** pricing page for a talent marketplace where companies hire vetted people.
- **Pricing model:** a free way in, a monthly plan, a fee per successful hire, and a custom tier.
- **Problem:** visitors don't understand how the subscription and per-hire fee combine.
- **Audience:** founders and hiring managers at startups, desktop first, many arriving on phones from social.
- **Primary action:** start free; secondary, talk to sales.
- **Success criteria:** a visitor can (1) tell what they'll pay for one hire, (2) see which plan fits them without reading every feature, (3) reach the call to action on a phone without hunting.
- **Demo format:** one static, responsive HTML file with three variants. Prices are placeholders.

## Shortlist

| # | Site | Pattern | Fits because | Tradeoff |
| --- | --- | --- | --- | --- |
| 1 | [Pallet](https://www.landing.gallery/websites/pallet) ([live](https://www.pallet.com/pricing)) | Three tiers (Basic, Pay as you go, Custom), each with a "Who is this for?" line keyed to how many roles you're filling. Middle tier states "$200/month + 15% first year salary" in one line. | Same hybrid model as the brief: subscription plus success fee shown together. Audience self-selection by role count. | Percentage-of-salary fee leaves the total cost for one hire to the visitor's maths. |
| 2 | [Jack & Jill](https://www.landing.gallery/websites/jack-jill-where-remarkable-people-meet-ambitious-companies) ([live](https://www.jackandjill.ai/pricing)) | Price per active role per month ($0 / $199 / Talk to us), annual–monthly toggle with the annual saving stated, a regional pricing note. | Hiring product that prices on the unit the buyer thinks in (open roles). | Per-role pricing hides what happens once a role is filled. |
| 3 | [Careswitch](https://www.landing.gallery/websites/careswitch) ([live](https://www.careswitch.com/pricing)) | Free core product first, paid modules as add-on cards, a "What's the catch? Is it really free?" block, and an "Estimate your monthly bill" calculator. | Answers the cost question directly with a calculator, and handles the "free" objection in place. | Long page (4,134 px capture); the estimator only works if the inputs are few. |
| 4 | [Pinpoint](https://www.landing.gallery/websites/leading-global-applicant-tracking-system-pinpoint-ats) ([live](https://www.pinpointhq.com/plans)) | No prices: "See the product and get pricing" with a form and a "What to expect from the call" list beside it. | Challenger: the sales-led route, for when per-hire fees vary too much to publish. | Fails success criterion 1 by design. |
| 5 | [Cal.com](https://www.landing.gallery/websites/cal) ([live](https://cal.com/pricing)) | Four columns (Individuals, Teams, Ultimate, Platform) with a yearly toggle; the Platform tier names "hiring marketplace" as a use case. | Clean baseline for a classic tier table, and a marketplace-builder tier. | Pure seat pricing; nothing for a per-hire fee. |

Evidence: all five are **observed** from desktop `pricing_page` captures. Pallet and Careswitch were
inspected as full-page captures; Jack & Jill, Pinpoint and Cal.com are fold-only captures
(1366×1024), so anything below the first viewport is **unknown**. The Careswitch estimator's
behavior is **inferred** from its static rows ($0.00, "Calculate Pricing"); it was not run. No live
pages were visited, so none of the pages' current state, motion or hover behavior is verified.

## Comparison against the success criteria

| | Cost of one hire is clear | Self-selection | Mobile path to CTA |
| --- | --- | --- | --- |
| Pallet: hybrid tiers | Partly: fee formula visible, total not computed | Strong: "Who is this for?" by role count | Unknown: mobile capture not inspected |
| Jack & Jill: per role | Partly: per role per month, hire fee absent | Medium: three tiers by name | Unknown |
| Careswitch: free core + estimator | Strong: calculator gives a number | Weak: modules, not personas | Unknown |
| Pinpoint: gated | No | N/A | Unknown |
| Cal.com: tier table | No per-hire concept | Medium: tiers named by audience | Unknown |

## Demos

[demos/index.html](demos/index.html): one page, the same offer and placeholder prices, three
variants behind a switcher. All copy and prices are **proposed**.

- **A. Hybrid tiers** (from Pallet): three tiers, each with "Who is this for?", the subscription and per-hire fee stated together, and the cost of one hire spelled out per tier. Tests whether self-selection plus an explicit "your first hire costs" line is enough.
- **B. Per open role** (from Jack & Jill): price per open role per month with an annual–monthly toggle and the hire fee as a separate line. Tests pricing on the buyer's unit.
- **C. Free core + estimator** (from Careswitch): free to browse, then an estimator (open roles, hires this year, billing) that totals the year, with a "What's the catch?" block. Tests whether a number beats a table.

All three ran at desktop and 390 px widths; details under "Validation" at the end.

## Recommendation

Lead with **A (hybrid tiers)**, borrowing C's single "your first hire costs" number. Pallet is the
only reference with the same subscription-plus-fee model, and its "Who is this for?" line meets the
self-selection criterion without a feature grid. The uncertainty most likely to change this: if
per-hire fees vary by role, a fixed number per tier is misleading, and C's estimator (or Pinpoint's
sales-led route for the top tier) becomes the better fit.

## Questions for the direction round

1. Is the per-hire fee a flat amount or a share of salary? This decides between A's fixed line and C's estimator.
2. Should the free tier allow a hire, or only browsing?
3. Is a "Talk to us" tier needed, or does it push serious buyers away from self-serve?

## Search ledger

| # | Tool | Query and filters | Results (total) | Kept | Notes |
| --- | --- | --- | --- | --- | --- |
| 1 | search_inspiration | `recruiting`, pricing_page, desktop | 1 | puck | |
| 2 | search_inspiration | `hiring`, pricing_page, desktop | 4 | jack-jill, pinpoint | hunarai, puck also returned |
| 3 | search_inspiration | `talent`, pricing_page, desktop | 3 | pallet | maven-clinic rejected (healthcare benefits) |
| 4 | search_inspiration | `freelance`, `freelancers`, pricing_page | 0, 0 | | |
| 5 | search_inspiration | `agency`, pricing_page | 1 | careswitch | Home care, not hiring; kept for the pricing pattern |
| 6 | search_inspiration | `marketplace`, pricing_page | 3 | cal | podcast marketplace, atomchat rejected (weak fit) |
| 7 | search_inspiration | `staffing`, `contractors`, pricing_page | 0, 0 | | |
| 8 | search_inspiration | `experts`, pricing_page | 3 | | zamp kept as additional; osome rejected (mislabelled) |
| 9 | get_website | 9 slugs above | | | Pulled pricing captures; listed each site's page types |
| 10 | search_inspiration | `candidates`, `jobs`, `salary`, `hire`, `people`, pricing_page | 0, 0, 0, 1, 10 | | Expansion 1: only pallet again, and general people-ops tools |
| 11 | search_inspiration | `hiring`, pricing_page, mobile | 4 | | Expansion 2: same sites as #2; no new pattern |

**Stop reason:** two consecutive expansions (#10, #11) found no new relevant pattern. Coverage is
small: Landing Gallery holds about 270 desktop pricing pages, and its text search only matches site
descriptions, so hiring products described in other words may be missed. Filter-only browsing of
`pricing_page` beyond page 1 was not done in this sample.

## Additional candidates

- [Puck](https://www.landing.gallery/websites/talent-acquisition-software-for-recruiting-teams-puck) ([live](https://www.careerpuck.com/pricing)): four tiers ($300 / $600 / $1,000 / Let's talk) with usage overage written into the feature line ("up to 200/mo, then $3/interview"). Useful if the per-hire fee works like overage.
- [Zamp](https://www.landing.gallery/websites/zamp-sales-tax-compliance-software-fully-managed) ([live](https://zamp.com/pricing)): three tiers with an email field and "Get started" inside each card. Shortens the path to signup.

## Rejected

- [Hunar.ai](https://www.landing.gallery/websites/ai-hrs-for-frontline-workforce-management-hunarai): the `pricing_page` capture shows the homepage hero, not pricing.
- [Osome](https://www.landing.gallery/websites/osome-hassle-free-incorporation-and-accounting-experts-for-your-business): the `pricing_page` capture shows the homepage hero, not pricing.
- Maven Clinic, podcast sponsorship marketplace, AtomChat: matched a keyword, not the offer.

## Limitations

- Screenshots are static and dated by Landing Gallery, not by this run. Live pages were not visited.
- Fold-only captures hide everything below 1024 px.
- Mobile pricing captures were listed but not inspected.
- Saved screenshots in `assets/` are third-party; they are git-ignored and for research use.

## Validation

Run on 2026-10-31 in the Claude desktop in-app browser, from the local file.

- Switcher shows one variant at a time: passed for A, B and C.
- B billing toggle: monthly shows $100, annual $80 per open role: passed.
- C estimator: default (2 roles, 3 hires) picks Growth, $11,100 a year, $3,700 per hire; 6 roles and 12 hires picks Scale, $28,800; 1 role and 1 hire picks Free, $4,000; Reset returns to $11,100: passed.
- No horizontal scroll at 390 px for any variant: passed.
- Finding at 390 px: in C the total sits below the sliders, off screen while you drag them. If C goes forward, the total needs to stay in view on phones (sticky summary or total above the inputs).
- Not checked: screen reader output, reduced motion (the demos have no motion), real devices.
