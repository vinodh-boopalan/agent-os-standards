# Node.js API Database Standards

## ORM
- Prisma preferred for new projects (type safety, migrations, studio)
- Drizzle acceptable for performance-critical or edge-deployed services
- Always use the ORM's query builder — never write raw SQL unless absolutely necessary

## Migrations
- All schema changes via version-controlled migrations
- One migration per logical change — don't batch unrelated changes
- Migrations must be reversible (include down migration)
- Never edit an existing migration that has been applied — create a new one
- Run migrations in CI to verify they apply cleanly

## Connection Management
- Use connection pooling in production (PgBouncer or Prisma's built-in pool)
- Set appropriate pool size based on serverless vs. long-running server
- Handle connection errors gracefully with retries

## Data Patterns
- Use transactions for multi-table writes — never leave data in inconsistent state
- Implement soft deletes for user-facing data (`deletedAt` timestamp)
- Add database indexes on all foreign keys and commonly queried columns
- Use UUIDs for public-facing IDs, auto-increment for internal references

## Seeding
- Maintain seed scripts for local development
- Seeds must be idempotent (safe to run multiple times)
- Keep seed data realistic but not copied from production

## Backups & Safety
- Automated daily backups for staging and production
- Test restore procedure quarterly
- Never run destructive migrations without a backup
