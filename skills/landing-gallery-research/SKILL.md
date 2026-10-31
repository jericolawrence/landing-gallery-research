---
name: landing-gallery-research
description: Research landing page and marketing site directions through Landing Gallery, after investigating the current page and grilling on unresolved goals and domain decisions. Deliver 4–5 strong visual references and playable comparison demos before grilling again about direction. Use for evidence-led exploration of homepages, pricing, about, contact, careers and 404 pages before planning or implementation.
---

# Landing Gallery research

Help the user choose a direction through inspected references and playable experiments. Follow this sequence:

**Investigate context → grill and confirm the brief → research → deliver references and demos → grill and confirm the direction → plan only when requested.**

This is the default workflow. Honor an explicit user instruction to skip or reorder a stage; still resolve missing baseline material and capabilities needed for the requested deliverable. Do not treat a vague prompt as a waiver of the initial interview.

Research and isolated demo code are authorized by this skill's invocation. They do not authorize changes to the existing site, external publication, or implementation planning. Keep the decision open until the user has seen the evidence and tried the demos.

## 1. Investigate before interviewing

Read the prompt, supplied images and links, applicable repository instructions, and the relevant page code, CMS content or domain documents. If the current page is live, look at it at desktop and mobile widths. Inspect available tools. Carry settled decisions forward across turns; do not restart the interview.

- Answer facts and straightforward implementation questions through investigation. Ask the user about intent, audience, offer, priorities, and tradeoffs that evidence cannot settle.
- If the current page is missing, first check accessible material. If still unavailable, ask the user for the page and important domain context. Wait before researching alternatives: an unknown baseline makes relevance impossible to judge. A request for missing material can be direct; use numbered grilling rounds for consequential domain or design choices. For a new page, establish the intended visitor, offer and conversion goal instead of requesting a nonexistent baseline.
- Separate preliminary context investigation from the broader Landing Gallery reference search. Do not begin the latter until the research brief is confirmed.

## 2. Grill on consequential decisions

Use a `grilling` skill if one is installed (for example from `mattpocock/skills`). If it is unavailable, follow this equivalent procedure:

1. Map decisions and their prerequisites as a design tree.
2. Ask all currently unblocked, consequential questions in one numbered round. Give a recommended answer for each and wait for replies. Investigate factual prerequisites yourself, using a background agent when available.
3. Recompute the frontier after each answer. Skip decisions already answered by the prompt or investigation; defer questions whose prerequisites remain open.
4. Once the frontier is empty, state the brief and obtain explicit shared-understanding confirmation. A reply confirming that brief is sufficient; do not request a second approval.

Use this format for each question:

> ❓ **Q1** - **Question title**: Question and relevant choices.
>
> ➡️ Recommended answer and reason.

Separate questions with horizontal rules. Do not turn this into a questionnaire of facts the agent can find.

Resolve the goal and audience, page type and section scope, baseline page, desired feel, brand and content constraints, primary conversion action, success criteria, research scope or time limit, and demo format. These are completeness checks, not mandatory questions. State inferred answers in the final brief so the user can correct them.

Choose demo format during this interview. Static HTML/CSS prototypes suit most section and layout comparisons; a prototype in the site's own stack (Webflow, Framer, Next.js and so on) suits decisions that depend on its components, CMS or interactions. Agree whether the demos must be responsive at both desktop and mobile widths. Resolve the choice before researching so the evidence serves the experiment.

## 3. Search broadly and inspect deeply

Read [references/landing-gallery-tools.md](references/landing-gallery-tools.md) when discovering and using Landing Gallery. Use the MCP tools first. If they are unavailable, try permitted browser access to landing.gallery; report access gaps instead of silently replacing the requested library.

Use a `research` skill after confirmation if one is installed. Delegate evidence gathering to a background researcher when available; give it the confirmed brief, source rules, and report destination. Maintain one writer for the report. Continue independent source checks and prototype preparation without outrunning unsettled decisions. If delegation is unavailable, conduct the same research yourself.

Keep a search ledger with query, filters (page type, device, page builder, framework), page number, inspected result slugs and gallery links, pattern found, and keep/reject reason. It supports expansion later without repeating searches.

Walk this search procedure:

1. Translate the problem into page types and sections (hero, pricing table, social proof, FAQ, footer, contact form and so on). Landing Gallery's text search matches site names and descriptions, not visual content, so search with the product's domain and its neighbours ("recruiting", "scheduling", "accounting") and set the page type and device through filters.
2. Explore the exact domain, adjacent domains with a similar offer or buyer, and filter-only browsing of the page type for patterns outside the domain. Use `pagebuilder` or `framework` filters when the build stack matters.
3. Inspect the actual screenshots. Previews are top-cropped; fetch full-resolution crops of the sections that matter before describing them. Use `get_website` on strong candidates to see their other page types and their mobile capture. Expand promising searches through `page` while `totalPages` allows, and exclude duplicates.
4. Check alternatives that challenge the leading direction. A familiar or attractive page is not automatically the best match for the user's goal.
5. Supplement Landing Gallery with the live source page, official platform or accessibility guidance, and first-party material for claims about behavior, motion or performance. Follow claims to the source that owns them.
6. Rank candidates against the confirmed success criteria. Record poor matches, mislabelled captures and evidence gaps; preserve distinct useful candidates beyond the initial shortlist.

Stop when the core sections and constraints have been checked, the strongest candidates are inspected, and two consecutive query expansions yield no new relevant pattern or ranking-changing evidence. Also stop at an agreed budget or an access block. Record why you stopped and what remains unknown; do not claim exhaustive coverage or unlimited retries.

Keep evidence types distinct:

- **Observed:** inspected screenshot content, at the capture shown.
- **Documented:** behavior explicitly supported by official guidance or first-party material.
- **Inferred:** a plausible relationship or behavior that has not been observed directly, including anything below a fold-only capture.
- **Proposed:** layout, copy or motion authored for the demos.

Landing Gallery screenshots are static. They do not establish hover states, scroll effects, animation, load performance or conversion results, and the live page may have changed since capture. Mark these as unverified unless the live page or first-party evidence supports them, and date any live-page observation. Cite visual references as evidence of page structure and content, not proof of conversion outcomes.

## 4. Deliver a small shortlist and working demos

Read [references/delivery.md](references/delivery.md) before building and presenting the package.

Present **4–5 strong references by default**, selected for fit and distinct patterns. Do not pad weak results or confuse the shortlist size with research depth. Keep the broader collection in the saved report; surface additional references when the user asks.

Build **3 distinct playable demos by default** in the agreed format. Reproduce the baseline for comparison when accessible. Keep experiments isolated from site code, use the same offer and content across variants, and label proposed copy and behavior. Demo code tests a direction; it is not production implementation.

Deliver visual samples with canonical source links, a compact comparison, the demos, a recommendation tied to the brief, and a saved Markdown report containing findings, sources, search coverage, additional candidates, and uncertainties. Show the shortlist and playable results first, then link the detailed report. Open the artifacts when supported so the user can inspect them directly.

## 5. Grill about direction before planning

After delivery, run another frontier-based grilling round. Ask about unresolved choices revealed by the evidence and demos: preferred structure, tradeoffs, uncertain audience fit, and evidence needed to choose. Do not repeat the original intake or hide the research behind this second interview.

Confirm the selected direction and its remaining uncertainties once the frontier is empty. Proceed to planning only when the user requests or has already authorized it and that direction is confirmed. Site implementation needs its own authorization. Requests for more examples extend the research ledger and shortlist; they do not reopen settled decisions automatically.
