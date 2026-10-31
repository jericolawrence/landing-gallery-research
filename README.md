# landing-gallery-research

A skill that makes your coding agent research landing page and marketing site directions on
[Landing Gallery](https://www.landing.gallery) before anyone writes site code. It reads your current
page, interviews you on the decisions that matter, searches Landing Gallery broadly, and hands back
4–5 strong references plus 3 playable demos to compare. Then it asks you to pick a direction.

It is the marketing-site sibling of
[mobbin-research](https://github.com/jericolawrence/mobbin-research), with the same workflow and
output, using Landing Gallery's MCP server instead of Mobbin.

Works with Claude Code, Codex and Cursor.

## Set up the Landing Gallery MCP

The server is free and public: no account, no token. One endpoint for every client:
`https://www.landing.gallery/api/mcp`.

**Claude Code**, run once:

```bash
claude mcp add --transport http landing-gallery https://www.landing.gallery/api/mcp
```

Installing this repo as a Claude Code plugin also registers the server through `.mcp.json`.

**Codex**, in `~/.codex/config.toml`:

```toml
[mcp_servers.landing-gallery]
url = "https://www.landing.gallery/api/mcp"
```

**Cursor**, in `.cursor/mcp.json` or `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "landing-gallery": { "url": "https://www.landing.gallery/api/mcp" }
  }
}
```

Check it works by asking your agent to "list Landing Gallery pricing pages". You should get four
sites with preview images.

## Install the skill

**Claude Code plugin**

```
/plugin marketplace add jericolawrence/landing-gallery-research
/plugin install landing-gallery-research@landing-gallery-research
```

**Skills CLI** (Claude Code, Codex, Cursor), run from the root of your repo:

```bash
npx skills add jericolawrence/landing-gallery-research -a claude-code
```

Add `-a codex -a cursor` for those agents.

**Manual**: copy `skills/landing-gallery-research/` into `~/.claude/skills/` (or your repo's
`.claude/skills/`).

## Use it

```
/landing-gallery-research Research a pricing page for our talent marketplace. Companies pay a
subscription plus a fee per hire and visitors don't get it. Show me references and demos.
```

In Codex, use `$landing-gallery-research`.

## What it does

1. **Investigates first.** Reads the prompt, screenshots, repo instructions and the current page. Asks only what evidence can't settle.
2. **Grills you on the brief.** Numbered questions, each with a recommended answer, until audience, page type, baseline, feel, conversion goal, constraints, success criteria and demo format are agreed.
3. **Searches broadly, inspects deeply.** Domain searches and filter browsing by page type, device, page builder and framework, with a search ledger, deduplication and a stop rule. It pulls full-resolution crops of the sections that matter rather than judging from top-cropped previews.
4. **Delivers a short list.** 4–5 cited references, a comparison, 3 responsive playable demos kept apart from site code, a recommendation and a saved Markdown report.
5. **Grills you on direction.** Plans or builds only when you say so.

It keeps evidence honest: what was observed, documented, inferred or proposed stays labelled, and
static screenshots are never passed off as proof of motion, hover states or conversion.

## What Landing Gallery gives the agent

Two read-only tools:

- `search_inspiration`: text, page type (`landing_page`, `pricing_page`, `about_page`, `contact_page`, `careers_page`, `not_found_page`), device (`desktop`, `mobile`), page builder and framework filters. Up to 4 results per page, newest first, with top-cropped previews, the original page URL and a full screenshot. About 1,900 desktop landing pages and 270 desktop pricing pages on 2026-10-31.
- `get_website`: every page and device capture for one site slug.

See [the tools reference](skills/landing-gallery-research/references/landing-gallery-tools.md) for
query tips, image sizes and citation rules.

## Differences from mobbin-research

Mobbin features with no Landing Gallery equivalent, and what this skill does instead:

| mobbin-research | landing-gallery-research |
| --- | --- |
| `search_screens` for interface states | `search_inspiration` filtered by page type and device. |
| Semantic and `deep` screen search on what is in the image | Dropped. Text search only matches site names and descriptions, so the skill searches by domain and browses filters, then inspects images itself. |
| `search_flows` for ordered journeys | Dropped: Landing Gallery has no flows. `get_website` shows one site's set of pages (home, pricing, about, careers, and so on), which is the nearest thing to a site journey, but it is not an ordered user flow. |
| `search_sections` for website sections | Dropped: no section search. The skill crops full screenshots to the section it needs. |
| iOS app screens | Dropped. `mobile` here means a 400 px mobile web capture, not a native app. |
| `exclude_screen_ids` | Dropped. Deduplicates by slug, page type and device in the ledger. |
| `output_destination`, `output_tool`, `task_intent` metadata | Dropped: the server takes no task metadata. |
| `ai_usage_notice` block | Dropped: the server returns none. |
| Mobbin account and connector | Not needed: public server, no auth. Edge rate limits apply. |
| Image URLs expire after 30 days | No expiry is documented. The skill still saves the images it relies on and keeps the gallery link. |
| Native vs browser demo choice for gestures and system controls | Replaced by stack choice (static HTML or the site's own builder or framework) and a desktop plus phone width check. |
| Flow stills don't prove animation timing | Same rule for screenshots: no hover, scroll or motion evidence, and the live page may have changed. |

New in this version: guidance on fold-only captures, full-resolution and section crops via
Cloudflare Images variants (observed, not documented), and checking for mislabelled captures.

## Example

[examples/2026-10-31-talent-marketplace-pricing](examples/2026-10-31-talent-marketplace-pricing)
holds one sample run: a report with search ledger and shortlist, and three playable pricing
section demos. The brief was assumed rather than grilled, so it shows the research and delivery
stages only. Saved screenshots stay out of git (see `.gitignore`); the report links to each
gallery entry.

## Requirements

- The **Landing Gallery MCP** (above). Without it the skill falls back to permitted browser access to landing.gallery and reports gaps.
- Optional: a `grilling` skill and a `research` skill (for example from [mattpocock/skills](https://github.com/mattpocock/skills)). The skill carries its own fallback for both.

## License

MIT
