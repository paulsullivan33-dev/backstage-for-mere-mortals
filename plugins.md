# Plugins

Backstage's power is its plugin architecture: the core is small, and
nearly everything useful — Kubernetes views, CI status, on-call info —
is a plugin. Hundreds exist; your portal is the set you choose.

## How plugins work

Plugins come in two halves:

- **Frontend plugins** add pages, cards, and tabs to the portal UI
  (e.g., a "Kubernetes" tab on each service showing its pods).
- **Backend plugins** do the server-side work: the Scaffolder that
  runs [templates](software-templates.md), the TechDocs builder, the
  catalog ingestion.

You add them to your Backstage app like dependencies, configure, and
they appear in the portal. The [new backend system](https://backstage.io/docs/backend-system/)
(since late 2024) made this substantially cleaner than the old way.

## Plugins you'll actually meet

| Plugin | What it shows, per service |
|---|---|
| Kubernetes | Pods, deployments, errors — no kubectl needed |
| ArgoCD | Sync status, deploy history (see [Backstage and GitOps](backstage-and-gitops.md)) |
| GitHub / GitLab | Repo info, CI runs, pull requests |
| PagerDuty / Opsgenie | Who's on call, recent incidents |
| Sentry | Recent errors |
| SonarQube | Code quality gates |
| Cost / FinOps | What this service spends |

The pattern: each plugin pulls data from the system that owns it and
renders it *in the context of the catalog entry*. One page per
service, everything about that service.

## Choosing plugins

- **Start with five.** Catalog, templates, TechDocs, your git host,
  and one deployment view (K8s or ArgoCD). Add more when someone asks
  twice.
- **Prefer maintained plugins.** Check recent commits and open
  issues — the ecosystem has abandoned corners.
- **Each plugin is a dependency.** It needs config, credentials, and
  upgrades. Ten plugins is ten things to maintain. The portal's value
  grows with plugins; so does its upkeep.

## Writing your own

Org-specific needs (internal deploy targets, custom scorecards) become
custom plugins. It's real software engineering — TypeScript, the
Backstage APIs — not configuration. Budget accordingly, and check the
ecosystem first; someone has usually built 80% of it.

Next: [Running Backstage](running-backstage.md).

## Sources

- [Backstage plugin marketplace](https://backstage.io/plugins/)
- [Backend system architecture](https://backstage.io/docs/backend-system/)
