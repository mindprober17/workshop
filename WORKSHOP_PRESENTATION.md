---
marp: true
theme: default
class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---

# 🚀 Workshop: CI/CD & API Development

**Building a Production-Ready Sensor API with GitHub Actions**

---

# 📋 Workshop Overview

## What We'll Build
- **FastAPI Sensor Management System**
- **Complete CI/CD Pipeline**
- **Environment Management**
- **Automated Versioning**

---

## Learning Objectives
- ✅ GitHub Actions workflows
- ✅ Branch protection & PR management
- ✅ Environment variables & secrets
- ✅ Automated deployments
- ✅ Semantic versioning

---

# 🎯 Task 0: Repository Setup

## Create Your Team Repository
1. **Repository Name**: `workshop-team-X`
2. **Fork** this project template
3. **Clone** your forked repository locally
4. **Set up** remote tracking with upstream
5. **Verify** push/pull functionality

## Git Commands
```bash
git clone https://github.com/your-org/workshop.git
cd workshop-team-X
git remote add upstream https://github.com/original-repo.git
```

---

# 🌿 Task 1: Branches & Protection

## Branch Strategy
- **`dev`** (default) - Development branch
- **`staging`** - Pre-production testing
- **`prod`** - Production releases

---

## Branch Protection Rules
- ✅ Required PR with 1 approval
- ✅ Dismiss stale reviews
- ✅ Require status checks to pass before merging 
- ✅ Restrict pushes to matching branches
- ❌ Disable force pushes & deletions

---

# 🏷️ Task 2: Labels & PR Template

## Required Labels
- **Type**: `feature ✨`, `bugfix 🐛`, `docs 📓`
- **Semver**: `Semver-Major`, `Semver-Minor`, `Semver-Patch`
- **Release**: `pre-release 🚀`, `release 🚀`

---

## PR Template Features
- Description & related issues
- Type of change checklist
- Testing requirements
- Semver label requirement
- Screenshots & notes

---

# 🤖 Task 3: Auto-label by Branch Prefix

## Automated Labeling
```yaml
feature/ → feature ✨
bugfix/ → bugfix 🐛
docs/ → docs 📓
pre-release/ → pre-release 🚀
release/ → release 🚀
```

## Benefits
- ✅ **Consistent labeling**
- ✅ **Reduced manual work**
- ✅ **Better organization**

---

# 📊 Task 4: Require Semver in PR

## Semver Validation
- **Validates** PR has Semver label
- **Fails CI** if missing
- **Comments** on PR with instructions

## Semver Types
- **Major**: Breaking changes
- **Minor**: New features (backward compatible)
- **Patch**: Bug fixes & improvements

---

# 🏷️ Task 5: Automatic Versioning

## Version Management
- **`VERSION`** file starts at `1.0.0`
- **Automatic bump** based on Semver label
- **Git tags** created on merge to `dev`
- **Version file** updated automatically

---

## Workflow
1. PR merged with Semver label
2. Workflow reads label type
3. Bumps version accordingly
4. Creates git tag
5. Updates VERSION file

---

# 🚀 Task 6: Simulated Deploy

## Deployment Workflows
- **Staging**: Push to `staging` branch
- **Production**: Push to `prod` branch
- **Environment-specific** configurations

## Deployment Steps
1. 📦 Install dependencies
2. 🔧 Run configuration
3. 🚀 Start application
4. 🧪 Health checks

---

# 🔄 Task 7: Dependabot Setup

## Automated Dependency Updates
- **Weekly schedule** for updates
- **Python packages** monitoring
- **Security updates** prioritized
- **Auto-merge** for patch updates

## Configuration
```yaml
package-ecosystem: "pip"
schedule:
  interval: "weekly"
  day: "monday"
  time: "09:00"
```

---

# 🔐 Task 8: GitHub Secrets

## Environment Variables
- **`API_HOST`** - Server host
- **`API_PORT`** - Server port
- **`API_TITLE`** - Application title
- **`API_VERSION`** - App version
- **`API_ENV`** - Environment (dev/staging/prod)

---

## Environment-Specific Secrets
- **Staging**: Different port & title
- **Production**: Production values
- **Development**: Default values

---

# 🔌 Task 9: API Implementation

## Sensor Endpoint
**`GET /api/sensors/{mac_address}`**

### Requirements
- **Case-insensitive** MAC address search
- **MAC validation** (AA:BB:CC:DD:EE:FF format)
- **200** with complete Sensor data
- **404** if sensor not found
- **422** for invalid MAC format

---

# 📈 Task 10: Release Flow

## Release Process
1. **Pre-release**: `pre-release/vx.x.x` → `staging`
2. **Release**: `release/vx.x.x` → `prod`

## Branch Flow
```
dev    →   staging   →  prod
 ↑            ↑           ↑
feature  pre-release  release
```

---

# 🚀 Lets get this show on the road!