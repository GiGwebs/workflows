# GiGwebs Reusable GitHub Actions Workflows

This is the central workflow repository for all GiGwebs projects. Instead of duplicating CI/CD logic in every repo, each project calls these workflows with a single thin caller file.

## Available Workflows

| Workflow | File | Use For |
|---|---|---|
| Vercel | `deploy-vercel.yml` | Next.js / React web frontends |
| EAS | `deploy-eas.yml` | Expo mobile + web apps |
| Railway | `deploy-railway.yml` | Backend APIs and workers |

## How to Use in Your Project

Create `.github/workflows/deploy.yml` in your project repo with just:

### For a Next.js app (Vercel):
```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    uses: GiGwebs/workflows/.github/workflows/deploy-vercel.yml@main
    secrets:
      VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
      VERCEL_ORG_ID: ${{ secrets.VERCEL_ORG_ID }}
      VERCEL_PROJECT_ID: ${{ secrets.VERCEL_PROJECT_ID }}
```

### For an Expo app (EAS):
```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    uses: GiGwebs/workflows/.github/workflows/deploy-eas.yml@main
    with:
      platform: all
      profile: production
    secrets:
      EXPO_TOKEN: ${{ secrets.EXPO_TOKEN }}
```

### For a backend API (Railway):
```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    uses: GiGwebs/workflows/.github/workflows/deploy-railway.yml@main
    secrets:
      RAILWAY_TOKEN: ${{ secrets.RAILWAY_TOKEN }}
```
