# 📋 Workshop Tasks

## 0) Repository Setup
1. Create a new repository: `workshop-mediaprobe-{team-name}`
2. Fork this project template to your new repository
3. Clone your forked repository locally
4. Set up remote tracking with upstream
5. Verify you can push/pull from your repository

## 1) Branches & Protection
1. Create branches: `dev` (default), `staging`, `prod`.
2. Enable protection on all:
   - Required PR, 1 approval
   - Dismiss stale reviews
   - Required checks
   - Restrict pushes to matching branches
   - Allow force pushes: disabled
   - Allow deletions: disabled
3. Set branch rules:
   - `dev`: Only allow pushes via PR
   - `staging`: Only allow pushes via PR
   - `prod`: Only allow pushes via PR

## 1) Labels & PR Template
- Create labels: `feature ✨`, `bugfix 🐛`, `docs 📓`, `Semver-Major`, `Semver-Minor`, `Semver-Patch`, `pre-release 🚀`, `release 🚀`
- Add `.github/PULL_REQUEST_TEMPLATE.md`
- PR: `docs/LBL-setup` → `dev` · Labels: `docs 📓`, `Semver-Patch`

## 2) Auto-label by branch prefix
- Add `label-by-branch.yml`
- PR: `feature/CI-labels` → `dev` · Labels: `feature ✨`, `Semver-Patch`

## 3) Require Semver in PR
- Add `require-semver.yml` workflow
- Validates that PR has one of: `Semver-Major`, `Semver-Minor`, `Semver-Patch`
- Fails CI if no Semver label is present
- PR: `feature/CI-semver` → `dev` · Labels: `feature ✨`, `Semver-Patch`

## 4) Automatic versioning (tag on merge to `dev`)
- `VERSION` file starts at `1.0.0`
- `tag-on-dev.yml` workflow reads Semver label from merged PR and does bump + tag
- PR: `feature/CI-versioning` → `dev` · Labels: `feature ✨`, `Semver-Patch`

## 5) Simulated deploy
- `deploy-staging.yml` (push to `staging`) and `deploy-prod.yml` (push to `prod`)
- Simulates deployment with echo commands and status updates
- Includes environment-specific configurations
- PR: `feature/CI-deploy` → `dev` · Labels: `feature ✨`, `Semver-Patch`

## 6) Dependabot Setup
- Create `.github/dependabot.yml` configuration file
- Enable automated dependency updates for Python packages
- Set update schedule (weekly/monthly)
- Configure security updates and version updates
- PR: `feature/DEP-setup` → `dev` · Labels: `feature ✨`, `Semver-Patch`

## 7) GitHub Secrets Configuration
- Set up repository secrets: `API_HOST`, `API_PORT`, `API_TITLE`, `API_VERSION`, `API_ENV`
- Configure staging environment secrets (different port and title)
- Configure production environment secrets
- Test environment variable usage in workflows
- PR: `feature/SEC-secrets` → `dev` · Labels: `feature ✨`, `Semver-Patch`

## 8) API Task
**Implement:** `GET /api/sensors/{mac_address}` (case-insensitive, validates MAC `AA:BB:CC:DD:EE:FF`)
- **200** with complete `Sensor`, **404** if doesn't exist
- PR: `feature/API-101-get-sensor-by-mac` → `dev` · Labels: `feature ✨`, `Semver-Minor`

## 9) Release flow
1. `pre-release/vx.x.x` (from `dev`) → PR to `staging` (label `pre-release 🚀`)
2. `release/vx.x.x` (from `staging`) → PR to `prod` (label `release 🚀`)
