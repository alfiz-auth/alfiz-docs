# Source: https://alfiz-web.vercel.app/

Client 1.0MIT · TypeScript · Postgres, MySQL, SQLite

# Permissions framed in your code, enforced in place.

Declare your permission catalog in TypeScript; your CI proves every surface is gated. Every check runs in-process against your own database — no door in your building asks another building whether it may open.

[Start standalone](https://github.com/alfiz-auth)Talk to us about federation

$ npm i @alfiz-auth/core @alfiz-auth/app

src/authz/catalog.tstsCopy

```
1import { defineCatalog } from "@alfiz-auth/core";2 3export const catalog = defineCatalog({4  namespace: "docs",5  scopeTypes: ["docs.folder", "docs.doc"],6  permissions: {7    "drive.docs.read": { grantableAt: ["*", "docs.folder"] },8    "drive.docs.read_history": { grantableAt: ["docs.folder"] },9    "drive.docs.share_doc": { requestable: true },10    "drive.docs.delete": { grantableAt: ["docs.doc"] },11  },12});
```

app/drive/\[id\]/page.tsxtsCopy

```
// a folder grant covers every doc inside itconst ok = await can(session, "drive.docs.read", doc(id));// one indexed query, in your process, against your database
```

Four commitments

## Few elements, repeated honestly.

The semantics are the product: union-only inheritance, negative-always-wins precedence, forward-inclusive wildcards, a naming floor the linter enforces. They are opinions, stated as decisions, and they are not pluggable.

### The frame is drawn in code

The catalog declares every permission and every scope type. Nothing is inferred from call sites; nothing is dashboard-configured.

### Checks happen at the doorway

Every can() runs in-process, against your own database. Nothing we operate is on your request path, so nothing we do can break your app.

### Openings nest

A grant at any enclosing scope covers everything within it, resolved by walking outward from where you stand. Grants are stored once, never fanned out.

### Growth adds bays

One app or twenty — standalone, linked, or federated — it is the same grant tuple, the same check, the same frame.

The growth path

## Framed on day one. Grows into your whole company.

A building grows by repeating its module — bay after bay, the same arch in the same frame, nothing rebuilt. Alfiz moves the same way — every step below is additive, audited, and reversible.

StandaloneLinkedFederated

Free · complete

### Standalone: one application, one database

The Application is the org root and the only writer. Groups, roles, reporting hierarchy, approval workflows, scoped grants — all of it, locally, with no external dependency beyond the database you already run.

Org root

Your Application

External dependency

None

What you give up

Nothing

application

One frame, carrying its own opening.

Metering

## The check path is unmetered because it is unmeterable.

Runtime checks never touch us in any topology, so per-check pricing is impossible by construction. We meter only the work we perform.

Guarantee

Nothing on the request path of your application is ever counted, priced, or throttled. Hard caps are configurable per dimension; crossing one degrades hosted polish, never a locally-running capability.

Admin seatsAuthenticated dashboard sessions

Linked & federated applicationsRelay and sync endpoints maintained

Provisioned connectorsReconcilers operated, per integration

Retained audit volumeEvents ingested under hosted retention

Runtime checksNot observable. Not metered.

## Every opening carries its own frame.

Free and complete for one application. Add the hosted dashboard when a non-engineer needs to administer access. Federate when the second application arrives.

[Read the docs](https://github.com/alfiz-auth)Talk to us