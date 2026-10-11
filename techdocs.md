# TechDocs

TechDocs is Backstage's answer to "where are the docs, and are they
current": documentation written as Markdown **in the service's own
repo**, automatically built and published into the portal next to the
[catalog](software-catalog.md) entry.

## The idea

Docs rot when they live far from the code: a wiki page nobody updates
after the deploy, a Google Doc from 2023 describing last year's
architecture. TechDocs puts the docs in the repo, so:

- Changing code and docs is one pull request.
- Docs are reviewed like code.
- Each service's docs live next to its catalog entry — find the
  service, find the docs.

## How it works

Add Markdown files and a small config to the repo:

```
docs/
  index.md          # the front page
  api.md
  runbook.md
mkdocs.yml          # which pages, in what order
```

```yaml
# mkdocs.yml
site_name: Orders API
nav:
  - Home: index.md
  - API: api.md
  - Runbook: runbook.md
```

Backstage builds the site (via MkDocs) and serves it inside the
portal. The `catalog-info.yaml` annotation points at the docs:

```yaml
metadata:
  annotations:
    backstage.io/techdocs-ref: dir:.
```

Push a docs change, and the portal updates — docs deploy with the
same pipeline as code.

## What makes it stick

- **Proximity.** Docs next to code get updated; docs elsewhere don't.
- **Discoverability.** Every catalog entry links its docs. No more
  "the runbook is in Dave's Notion."
- **Low ceremony.** It's Markdown and a YAML nav file. Engineers
  already know both.

## Honest limits

TechDocs doesn't *write* docs or *enforce* quality — it removes the
excuses for not having them. An empty `docs/` folder renders as an
empty site. Some orgs add catalog checks ("production services must
have a runbook page") to close that gap; Backstage can surface the
missing docs, but humans still write them.

Next: [Plugins](plugins.md).

## Sources

- [Backstage TechDocs](https://backstage.io/docs/features/techdocs/)
