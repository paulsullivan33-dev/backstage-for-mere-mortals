# Running Backstage

From first local run to production, with the honest version of each
step. Backstage is a Node.js app you build and operate — there is no
"managed Backstage" from the project itself.

## 1. Scaffold the app

```bash
npx @backstage/create-app@latest
```

Answer the prompts (app name, database for local dev). This generates
a full monorepo: frontend, backend, and example config.

```bash
cd my-backstage
yarn install
yarn dev
```

**Check:** the portal opens at `http://localhost:3000` with the
example catalog. You're running Backstage — uncustomized, but running.

## 2. Make it yours (local)

- Edit `app-config.yaml`: name, organization, integrations.
- Add your git host integration (GitHub/GitLab) so the catalog can
  read repos.
- Add plugins: `yarn --cwd packages/app add <plugin>` for frontend,
  backend wiring per the plugin's docs.
- Write your first `catalog-info.yaml` files and watch the catalog
  fill with *your* services.

This is the long phase. Expect weeks of iterating on catalog shape,
templates, and auth before it feels like *your* portal.

## 3. Production concerns

- **Database:** SQLite is dev-only. Production wants PostgreSQL.
- **Auth:** wire your identity provider (GitHub OAuth, Okta, Entra
  ID, Google). Guest access is for demos.
- **Deployment:** build the Docker image (`docker build -f
  packages/backend/Dockerfile .`) and run it on your platform —
  Kubernetes via the community Helm chart is the common path.
- **Upgrades:** monthly releases. The upgrade is part code
  (dependency bumps, occasional breaking changes), part config.
  Budget recurring time; "set and forget" doesn't apply.

## 4. Operating it

Backstage is now production software *you* own:

- Monitor it like any service (health endpoint, error tracking).
- Back up the database (it holds catalog state, template runs,
  TechDocs builds).
- Keep plugins updated — stale plugins are how portals quietly break.

## Honest summary

| Stage | Effort |
|---|---|
| Local demo | An afternoon |
| Useful internal pilot | Weeks |
| Production portal | A platform team, ongoing |

The demo is deceptively easy; the value is in the customization, and
the customization is real engineering work. That's the trade, stated
up front — see [Adoption Pitfalls](adoption-pitfalls.md).

Next: [Backstage and GitOps](backstage-and-gitops.md).

## Sources

- [Backstage getting started](https://backstage.io/docs/getting-started/)
- [Backstage deployment docs](https://backstage.io/docs/deployment/)
