# The Software Catalog

The catalog is the heart of Backstage: a central directory of
everything the engineering org runs and owns — services, libraries,
APIs, databases, even ML models — each with an owner, a lifecycle,
and its dependencies. Everything else in Backstage hangs off the
catalog.

## Entities as code

Each thing in the catalog is described by a small YAML file,
`catalog-info.yaml`, living in that thing's own git repo:

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: orders-api
  description: Handles customer orders
  annotations:
    github.com/project-slug: myorg/orders-api
spec:
  type: service
  lifecycle: production
  owner: group:payments-team
  dependsOn:
    - resource:orders-postgres
```

Backstage collects these files from your repos and builds the
directory. The repo stays the source of truth — the catalog is a
*view* over what's already there, which is why it stays current
without manual curation.

**Check your understanding:** the catalog doesn't *contain* your
services; it *indexes* their descriptions. Delete the YAML and the
service vanishes from the portal (the service itself keeps running).

## The entity model

| Kind | What it is | Example |
|---|---|---|
| Component | A software thing | `orders-api` service |
| Resource | Infrastructure a component needs | `orders-postgres` database |
| Group | A team | `payments-team` |
| User | A person | `ada` |
| System | A collection of components | `checkout` platform |
| Domain | A business area grouping systems | `payments` |

Ownership chains upward: a component names an owner group; groups
contain users. "Who owns this?" resolves to actual people with a
pager.

## Why it matters

- **Discovery.** Search "payments" and find every related service,
  its repo, its docs, its dashboards.
- **Ownership.** Incidents start at the catalog entry, not with a
  chat message asking who owns what.
- **Dependencies.** The `dependsOn` graph shows blast radius: what
  breaks if this database goes down.
- **Standards.** Missing owner? No docs? The catalog makes gaps
  visible, which is the first step to fixing them.

## Keeping it honest

A catalog rots when entries go stale: repos deleted but YAML
lingering, owners pointing at disbanded teams. Backstage helps —
it can verify repos still exist and flag orphans — but someone has
to tend it. Assign catalog hygiene to the platform team explicitly,
or it becomes the spreadsheet it replaced.

Next: [Software Templates](software-templates.md).

## Sources

- [Backstage System Model](https://backstage.io/docs/features/software-catalog/system-model)
- [Catalog file format](https://backstage.io/docs/features/software-catalog/descriptor-format)
