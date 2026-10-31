# Delivery and comparison demos

Use the format agreed in the initial interview. The defaults below limit the user's review burden without limiting search depth.

## What to show first

1. **4–5 visual references.** For each: site, inspected screenshot or crop of the relevant section, canonical gallery link and live page link, the relevant pattern, why it fits this audience and offer, and its main tradeoff. Use fewer if evidence is weak; state why.
2. **A compact comparison.** Compare the patterns against the brief's success criteria and explain how they inform the demos. Avoid invented numeric scores or conversion claims.
3. **3 playable demos.** Label distinct directions and explain what each experiment tests. Link or open the runnable artifact, not just its source code. Include the baseline for comparison when accessible.
4. **A recommendation.** Name the leading direction, the evidence supporting it, and the uncertainty most likely to change it. A recommendation is not a production plan or ticket list.
5. **The saved report.** Link the Markdown findings and state search coverage, the stop reason, and material gaps. Mention that additional references are available; do not dump them into chat unless requested.

Then begin the post-delivery grilling round. Ask only choices the evidence and demos leave unresolved.

## Demo procedure

- Put demo files in a separate research/prototype directory. Do not edit production pages or CMS content to create a comparison.
- Reuse the same offer, copy, prices and starting state across variants so structure is what the user compares. Vary the section pattern, not just a color or font.
- Provide a clear way to switch between variants. For interactive parts (billing toggles, estimators, accordions, tabs, forms), make them work and resettable.
- Make every demo responsive and check it at a desktop width and a phone width (about 390 px). Landing pages are read on both; a pattern that only works at one width is a finding.
- Keep the page's essential conversion path: the primary call to action, how a visitor reaches it, and what happens on narrow screens. Choose equivalent checks for other page types (contact form fields, careers listing, 404 recovery links).
- Make controls keyboard and touch usable, keep visible focus, and honor reduced motion for any motion. Use the project's units and tokens; default to rem for sizes.
- Label authored copy, prices and motion as proposals. If the baseline cannot be reproduced faithfully, explain the difference rather than presenting a guess as the current page.
- Validate by running each demo and exercising its main path, interactive parts and both widths. Record what ran and what could not be verified. Source that compiles is not proof that a demo works.

If the agreed stack or runtime is unavailable, disclose the limitation and ask which supported demo format to use. Do not silently downgrade, or claim unrun demos were verified.

## Saved findings

Follow the project's research-note convention. If there is none, use `docs/research/<date>-<topic>.md` and keep demos and saved screenshots together in a neighbouring topic directory. In a projectless session, use an accessible output directory and link it explicitly.

Keep one report with:

- The confirmed brief and success criteria.
- The shortlist, comparison, evidence classifications, and recommendation.
- Demo locations, the differences each tests, and validation results.
- A search ledger, deduplicated additional candidates, reject reasons, gallery and live URLs, and stop reason.
- Access limitations, unverified behavior, and questions for the next decision round.

The additional collection should be discoverable without another search. On a follow-up request for more, reveal the next relevant candidates and explain what they add; extend the search only to address missing coverage or a changed goal.

## Sample invocation

> /landing-gallery-research Research a pricing page for our talent marketplace. Companies pay a monthly subscription and a fee per hire, and visitors don't get it from the current page. Investigate the page and the pricing model, then grill me on the important unresolved decisions. Once we agree on the brief, show 4–5 strong Landing Gallery references and 3 playable demos, with a recommendation and saved research report. Grill me again about the direction before planning changes.
