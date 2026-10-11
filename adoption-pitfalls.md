# Adoption Pitfalls

What goes wrong with Backstage adoptions, collected so you can dodge
it. None of these are reasons to avoid Backstage — they're reasons to
adopt it with eyes open.

## 1. Underestimating the customization

The demo takes an afternoon; the useful portal takes months. The
catalog model, the templates, auth, plugins, upgrades — it's a
software project, not an installation. Orgs that budget "a sprint"
end up with a demo nobody uses. Budget a team, or don't start.

## 2. No platform team to own it

Backstage needs owners: upgrading monthly releases, maintaining
templates, tending catalog hygiene, supporting plugin issues. Without
a named team, it becomes everyone's side project, which means no
one's. The portal decays, trust erodes, engineers go back to chat
archaeology.

## 3. Catalog rot

Stale entries are worse than no catalog — engineers learn the portal
lies and stop checking. Causes: repos deleted without removing YAML,
owners pointing at disbanded teams, `dependsOn` never updated.
Mitigations: automated orphan detection, required owner reviews,
making catalog accuracy someone's explicit job.

## 4. Template sprawl or template cage

Too many templates (one per team per language per framework) and
nobody can find the right one. Too rigid, and teams route around the
portal entirely. Aim for a small set of maintained golden paths with
documented escape hatches — see
[Software Templates](software-templates.md).

## 5. Plugin sprawl

Every plugin is a dependency with config, credentials, and upgrades.
Portals accumulate plugins like browser toolbars until upgrades
become archaeology. Rule: add a plugin when asked twice, remove when
unused for a quarter.

## 6. Adopting below the scale threshold

Under ~10 engineers, or with a handful of services, the portal's
overhead exceeds its value. A wiki, good repo READMEs, and chat
discipline do the job. Backstage pays off when discovery is
genuinely painful — that's the signal to adopt, not headcount alone.

## 7. Expecting it to fix culture

Backstage surfaces ownership gaps, missing docs, and inconsistent
standards — it doesn't fill them. If no one writes docs, TechDocs
hosts empty pages beautifully. The portal is leverage for a platform
team with a mandate, not a substitute for one.

## The pre-adoption checklist

- [ ] A named team owns the portal, with real capacity.
- [ ] Pain is real: engineers waste time on discovery *today*.
- [ ] Auth story decided (your identity provider, not guest mode).
- [ ] Five-plugin start scoped (catalog, templates, TechDocs, git
      host, one deployment view).
- [ ] Upgrade cadence accepted (monthly releases, ongoing work).
- [ ] Catalog hygiene assigned to someone specific.

Related: [Running Backstage](running-backstage.md),
[Glossary](glossary.md).
