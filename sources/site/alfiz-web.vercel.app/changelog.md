# Source: https://alfiz-web.vercel.app/changelog

Changelog

# What changed, and why we decided it.

1.0.02026-07-14

### Client 1.0

The semantics are frozen: union-only inheritance, negative-always-wins precedence, forward-inclusive wildcards, the naming floor. Template-literal key types derived from the catalog are now stable API.

Added can.fresh() for destructive surfaces and time-bound elevations

Coverage linting now errors — not warns — on an exported server action with no gate

defineCatalog() gained per-scope-type grantability

0.9.22026-06-30

### Cycle paths in errors

Interactive edits that would create a cycle are hard-rejected with the full path named. A bare “cycle detected” is undebuggable.

Group parentage errors now read A → B → C → A

Directory imports auto-condense strongly connected components into a virtual parent, with a warning

0.9.02026-06-11

### Org root, promotion and demotion

Organizational-domain data has exactly one writer. The org root now moves by audited handoff in both directions.

Promotion imports a standalone Application’s groups, roles and global grants through the directory-import validation path

Reporting hierarchies are surfaced for human resolution — trees are not union-safe

Demotion snapshots the dataset back down with full provenance

0.8.42026-05-22

### Tombstones, not deletes

A key an application stops publishing may still be referenced by central roles. Hard deletion silently rewrote role meanings; it no longer happens.

Registry emits a drift report: “role X references 3 permissions no longer published”

Tombstoned keys stop matching checks, remain visible in editors as deprecated