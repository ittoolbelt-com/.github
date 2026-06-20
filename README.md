# ittoolbelt-com/.github

Shared GitHub Actions reusable workflows for the `ittoolbelt-com` organisation.

## Reusable workflows

Call these from any repo in the org with `uses: ittoolbelt-com/.github/.github/workflows/<name>.yml@main`.

| Workflow | Purpose |
|----------|---------|
| `reusable-terraform-plan.yml` | Terraform init + fmt check + validate + plan, posts output to PR comment |
| `reusable-terraform-apply.yml` | Terraform init + apply with environment gate |
| `reusable-lambda-deploy.yml` | Build Docker image, push to ECR (registry account), update Lambda (platform account) |
| `reusable-python-ci.yml` | Ruff lint + pytest with optional LocalStack |
| `reusable-release-please.yml` | Automated changelog + version bump + GitHub Release via release-please |
| `reusable-node-ci.yml` | npm ci + vitest/jest test run + optional build verification |
| `reusable-spa-deploy.yml` | Vite build → S3 sync (cache headers) → CloudFront invalidation |

## Cascade workflows

| Workflow | Trigger | Dispatches to |
|----------|---------|---------------|
| `cascade-api-released.yml` | `repository_dispatch: api-released` (from control-plane) | `platform-cli` (API compat PR), `app-www` (rebuild) |

## Conventions

- All automated commits include `[skip ci]` to prevent workflow loops
- Cross-repo triggers use `repository_dispatch` with named `event_type` values
- Environments: `dev` (auto-deploy on main), `preprod` / `prod` (require reviewer approval)
- OIDC authentication only — no static AWS keys

## Conventional commits

All repos adopt [Conventional Commits](https://www.conventionalcommits.org/):

| Prefix | Version bump | Appears in changelog |
|--------|-------------|---------------------|
| `feat:` | minor | Yes |
| `fix:` | patch | Yes |
| `perf:` | patch | Yes |
| `feat!:` or `BREAKING CHANGE:` footer | major | Yes |
| `docs:` | none | No (hidden) |
| `chore:` | none | No (hidden) |
| `refactor:` | none | No (hidden) |
