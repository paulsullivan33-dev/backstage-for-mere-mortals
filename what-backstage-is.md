# What Backstage Is

Backstage is an open-source **internal developer portal**: a
company-internal website where engineers discover services, find
owners and docs, and create new services the approved way. Spotify
built it for themselves around 2016 — hundreds of microservices, no
overview, no standard — open-sourced it in 2020, and donated it to
the CNCF, where it sits in incubating status.

## The problem it solves

Past a certain size, every engineering org hits the same wall:
services exist that nobody can find, owned by teams nobody can name,
documented nowhere. Onboarding takes weeks. Incidents start with "who
owns this?" The knowledge is tribal; the tribe keeps changing.

Backstage attacks this with one idea: **a single front door** for the
engineering org. Not another dashboard — the place you start when you
need to find something, make something, or understand something.

## Framework, not product

This distinction matters. Backstage ships as a *framework* you build
your portal on, not a finished product you install:

- You scaffold an app, then add the plugins your org needs.
- You model *your* services, teams, and standards in the catalog.
- You write the software templates that encode *your* golden paths.

Out of the box it's a skeleton. The value comes from the
customization — which is also the cost. See
[Adoption Pitfalls](adoption-pitfalls.md).

## The three pillars

| Pillar | Question it answers | Guide |
|---|---|---|
| Software Catalog | "What exists, who owns it, what does it depend on?" | [catalog](software-catalog.md) |
| Software Templates | "How do I create a new service the right way?" | [templates](software-templates.md) |
| TechDocs | "Where are the docs, and are they current?" | [techdocs](techdocs.md) |

Plugins extend all three — Kubernetes views, CI status, on-call
info, cost data — in one place per service. See [Plugins](plugins.md).

## What it isn't

- **Not a deployment tool.** Backstage doesn't ship code; it *shows*
  you what ArgoCD, Jenkins, or your pipeline did. See
  [Backstage and GitOps](backstage-and-gitops.md).
- **Not monitoring.** It can *display* health from PagerDuty or
  Sentry, but it isn't the alerting system.
- **Not for small teams.** Under ~10 engineers, a wiki and good chat
  habits beat a portal. The overhead only pays off at scale.

Next: [The Software Catalog](software-catalog.md).

## Sources

- [Backstage.io](https://backstage.io/)
- [CNCF Backstage project page](https://www.cncf.io/projects/backstage/)
