# Software Templates

Templates are how Backstage creates new things: pre-built,
organization-approved starting points for services, libraries,
pipelines, and more. The industry term is **golden paths** — the
paved road you want engineers to take by default.

## The idea

Without templates, creating a service means copy-pasting the last
service someone made and hoping it's current. The copy drifts:
old base images, missing monitoring, no docs skeleton, CI wired
slightly differently each time.

A software template asks a few questions (name, owner, language),
then generates a repo with everything the org expects:

- Source skeleton for the chosen stack.
- Dockerfile and CI pipeline, wired to the org's standards.
- `catalog-info.yaml` so the service appears in the
  [catalog](software-catalog.md) from birth.
- Monitoring, alerting, and docs scaffolding.

The developer gets a working, compliant service in minutes. The
platform team gets consistency without being a ticket queue.

## How it works

Templates are defined in YAML and executed by the **Scaffolder**, a
Backstage backend plugin. A template lists *steps* — fetch a skeleton,
publish to GitHub, register in the catalog, trigger a CI run — with
parameters collected from a form in the portal UI.

```yaml
# simplified template sketch
apiVersion: scaffolder.backstage.io/v1beta3
kind: Template
metadata:
  name: python-service
  title: Python Service
spec:
  parameters:
    - title: Service details
      properties:
        name:
          title: Service name
          type: string
        owner:
          title: Owner team
          type: string
  steps:
    - id: fetch
      name: Fetch skeleton
      action: fetch:template
      input:
        url: ./skeleton
    - id: publish
      name: Publish to GitHub
      action: publish:github
```

The Scaffolder runs the steps, and the new repo lands in the org
with catalog entry included.

## Golden paths, honestly

Templates encode *decisions the org has already made*: which base
image, which pipeline, which observability. They work when those
decisions are real and maintained. They fail when:

- The template rots (skeleton references last year's base image).
- Teams can't deviate when they legitimately need to — the golden
  path becomes a cage. Good template systems allow escape hatches.
- Nobody owns the templates. They're code; they need maintainers.

**Rule of thumb:** a template should save the developer time *and*
encode a decision the org will defend. If it does neither, delete it.

Next: [TechDocs](techdocs.md).

## Sources

- [Backstage Software Templates](https://backstage.io/docs/features/software-templates/)
