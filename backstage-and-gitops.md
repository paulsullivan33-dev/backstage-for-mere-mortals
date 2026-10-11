# Backstage and GitOps

Backstage and GitOps are neighbors, not the same thing. This guide
draws the boundary: what each does, where they touch, and how they
fit together in a platform.

## The division of labor

| | Backstage | GitOps (e.g., ArgoCD) |
|---|---|---|
| Job | Show and organize | Converge reality to desired state |
| Answers | "What exists? Who owns it? How do I make one?" | "Is it deployed? Is it in sync?" |
| Acts on systems? | No (it displays) | Yes (it applies) |
| Source of truth | The catalog (indexed from git) | The git repo (desired state) |

Backstage doesn't deploy anything. ArgoCD doesn't catalog anything.
Each is the other's missing half: the portal shows the ArgoCD sync
status *on the catalog entry*; the GitOps repo holds the manifests
*the catalog describes*.

## Where they touch

**The ArgoCD plugin.** The most common integration: each service's
Backstage page shows its ArgoCD application — sync status, deploy
history, resource health. The deployment pipeline stays in ArgoCD;
Backstage makes it visible where engineers already look.

**Templates creating GitOps-managed services.** A
[software template](software-templates.md) can scaffold not just the
service repo but its GitOps wiring: the ArgoCD `Application`
manifest, the Kustomize overlays, the catalog entry — one scaffolding
run producing a service that's deployed *and* discoverable from
birth.

**Catalog as inventory for policy.** "Which production services lack
a runbook?" is a catalog query. "Which aren't GitOps-managed?" can
be one too, via annotations. The portal becomes the place you *check*
the standards GitOps *enforces*.

## The shared foundation: git

Both orbit git, differently:

- GitOps: git holds *desired state*; agents converge systems to it.
- Backstage: git holds *descriptions* (`catalog-info.yaml`,
  docs, templates); the portal indexes them.

A healthy setup has both: git describes what should exist (GitOps
makes it so) and what everything is (Backstage shows it).

## Don't conflate them

Adopting Backstage doesn't give you GitOps, and adopting GitOps
doesn't give you a portal. Teams sometimes expect one purchase —
even a free one — to solve both problems. It won't. Plan them as
separate efforts that integrate, which is also how you avoid one
team's portal project blocking another team's deployment work.

Related: [What Backstage Is](what-backstage-is.md),
[Plugins](plugins.md).

## Sources

- [Backstage ArgoCD plugin](https://github.com/roadiehq/backstage-plugin-argo-cd)
- [OpenGitOps principles](https://opengitops.dev/)
