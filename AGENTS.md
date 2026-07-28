> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP

## Who this site is for

These docs are a **developer** surface. The reader is qualified by the shape of their
problem, not the size of their company: they need *scoped* permissions — per-folder,
per-document, per-tenant — in a TypeScript application, and they already run a database.
Someone who only needs an `isAdmin` column does not need Alfiz, and the docs should say so
plainly rather than sell past it.

The marketing site is a different front door with a different register, and the two must
not converge. Its commercial pillars — "the org chart is part of the system",
"administration centralizes, enforcement never does" — do **not** belong here.

## Terminology

- Lead with **"scoped permissions for TypeScript applications"**, not "authorization
  layer" and not "access governance". The category name never appears on this site.
- The four commitments on `index.mdx` and `introduction.mdx` are the **OSS set**:
  declared in code · checked in your own process · typed end to end · verified in CI.
  Keep those two pages in sync with each other and with the `alfiz-ts` README.
- Write "Alfiz Cloud", not "the cloud" or "the hosted tier", when naming the product.
- Each growth tier — standalone, linked, federated — is a **terminal state**. Never write
  copy implying that stopping at one is stopping short.

## Examples

One running example across every page, and it is deliberately industry-neutral: a shared
**document workspace**. An example that implies a vertical — a school, a clinic, a bank —
reads as a product built for that vertical and quietly excludes everyone else. These docs
previously ran on a learning-management example and it had to be unwound; don't reintroduce
one.

| Thing | Use |
|---|---|
| Namespace | `docs`, with groups `docs.files`, `docs.sharing`, `docs.reports` |
| Scope types | `docs.folder` (nests), `docs.doc` (leaf) |
| Keys | `docs.files.read`, `docs.files.update_file`, `docs.files.share`, `docs.files.delete` |
| Scope instances | `docs.folder:42`, `docs.doc:123` |
| Groups | `group:editors` nested under `group:staff`; `group:senior_editors` under editors |
| Role | `Project Lead` |
| Second application | `billing` — e.g. `billing.invoices.read` |
| External connector | `zoom` — `zoom.host`. Universal SaaS, safe to keep. |

People in examples are Jane Okafor (requester) and M. Reyes (approver).

## Style preferences

{/* Add any project-specific style rules below */}

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

- **Check volume is never a billing dimension** — that is the claim to make, and it is
  permanently true. Do **not** write that checks are "not observable", "unmeterable", or
  that per-check pricing is "impossible by construction": those are claims about
  observability that a usage-metrics feature would falsify. The durable statement is the
  dependency one — Alfiz is never in your request path, so it cannot add latency to a
  check, throttle one, or fail in a way that stops one.
- **Access reviews and certification campaigns are not built.** Nothing on this site may
  imply otherwise. `explain()` is useful *during* a review; that is not the same thing as
  running one. Separation of duties, an orchestrated joiner-mover-leaver flow, and access
  analytics are also not built.
- Connectors are Zoom and Slack **as worked examples**, not a catalog. Alfiz is strong on
  governance for the software you build; for the software you buy it needs connectors like
  everyone else, and we say so.
- "AI-native" and agent-first framing stay out of customer-facing pages. Where coding
  agents are mentioned at all, they are a *consequence* of static verification — the
  verifier is what catches the gate an agent skipped — never an identity or a headline.
