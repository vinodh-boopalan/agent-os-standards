# Next.js CI/CD Standards

## Hosting
- Vercel is the preferred deployment platform for Next.js
- Alternative: Docker + Node.js server (for self-hosted requirements)

## Preview Deployments
- Every PR gets an automatic preview deployment
- Preview URL posted as PR comment for review
- Preview deployments use staging/preview environment variables

## Build Pipeline
- CI steps: lint → type-check → test → build → bundle analysis
- `next build` must succeed with zero errors
- Enable `output: 'standalone'` for Docker deployments

## Bundle Analysis
- Run `@next/bundle-analyzer` in CI on every PR
- Flag PRs that increase bundle size by > 10%
- Monitor and set budgets for initial JS load (< 100KB compressed)

## Performance Monitoring
- Run Lighthouse CI on preview deployments
- Minimum scores: Performance 90, Accessibility 95, Best Practices 95, SEO 95
- Block merge if scores drop below thresholds

## Environment Management
- Use Vercel environment variables for dev/preview/production
- Never hardcode API URLs — use environment variables
- Use `next.config.js` `env` or `.env.local` for local development
