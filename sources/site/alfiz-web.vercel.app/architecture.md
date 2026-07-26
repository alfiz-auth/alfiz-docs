# Source: https://alfiz-web.vercel.app/architecture

Architecture

# Client, Application, Service — the layer line is architectural, not commercial.

A capability belongs to the Client if it is a pure function over provided data; to the Application if one database satisfies it; to the Service only if it requires vantage no single application has. No layer is artificially limited, and the Service never gates a capability that could have run locally.

Enforcement

## Four points, or it is not gated.

Every action or surface gates at four points, and it is not done until all four hold. The four-point checklist is enforced by tooling, not discipline — agents are exactly the users who will skip step three.

1 · The page2 · Navigation visibility3 · Server action4 · Conditional UI

app/…tsCopy

```
// app/(portal)/drive/[id]/page.tsxexport default async function Page({ params }) {  await requirePermission("drive.docs.read", doc(params.id));  ...}
```

1 · The page2 · Navigation visibility3 · Server action4 · Conditional UI

Gate shape

`canAny()` is a visibility affordance only — it decides whether a nav entry appears. The verifier errors when it shows up in a server action or route handler.

Static verification

## Permissions your coding agent can wire and your CI can prove.

Keys are template-literal types derived from the catalog, so every call site is compile-time verified. Coverage linting warns on leaves no gate references and fails the build on an exported server action with no gate at all.

typed keyscoverage lintgate-shape lintcatalog lint

ci · alfiz verifybash

```
$ alfiz verify   catalog   docs — 34 permissions, 2 scope types, 1 requestable  coverage  31/34 leaves gated  warn      drive.docs.read_history referenced by no gate  error     app/actions/export.ts — exported action, no gate  error     app/api/drive/route.ts:12 — canAny() used as a gate   2 errors, 1 warning. Build failed.
```

Semantics

## Maximally opinionated where it counts.

No infrastructure opinions: any conforming provider serves the Client. All semantic opinions: these five are the product, and none of them is configurable.

InheritanceUnion-onlyGroups, roles and object hierarchies can only widen access.

NegationPersonal revokes onlyThe single negative layer in the system. It always wins, at that scope and every descendant.

WildcardsForward-inclusiveA stored docs.drive.\* grant absorbs permissions added under that group later.

HierarchyData, resolved at check timeChecks walk up ancestor chains — O(depth) — and never down subtrees.

StalenessBounded and statedClosures are cached, decisions are not. can.fresh() bypasses every cache.

The core tradeoff

Listing queries need a materialized path column or a closure table on your resource tables. A bit of schema, in exchange for solving listing inside your own database with no synced store. We state it plainly rather than hide it.