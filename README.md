# Access ERP

Authentication and authorization testing laboratory using the existing **myapi** Supabase project.

## Database status
Migration `access_erp_isolated_foundation` applied to isolated `access` schema. Three demo organizations, 525 demo records and 140 role permission combinations were seeded. Existing public tables were not modified.

## Security
All five Access tables have RLS enabled. No demo account is automatically granted access. To test, first create an actual Supabase Auth user, assign their UUID to a membership for a demo organization, and configure the `access` schema in Supabase Data API exposed schemas if browser access is required. Verify grants and RLS before enabling exposure.

## Modules
Customers, Inventory, Orders, Purchasing, Employees, Finance, Approvals.

## Roles
Owner, Admin, Manager, Employee, Viewer. Read/create/update/delete permissions stored in `access.role_permissions`. The `access.can_do` function checks the authenticated user's organization membership.

## Next implementation work
- React + TypeScript frontend and authenticated data client
- Tenant membership onboarding and controlled invitation workflows
- Realistic domain-specific tables and data relationships (current sample records are generic test records)
- Auth UI for password, magic link, OTP, Google, Apple, Microsoft, GitHub; configure providers individually
- MFA, SAML/SSO, phone login and passkey capability assessment
- Permission matrix and audit-log UI
- Automated RLS and cross-tenant isolation tests
- Vercel environment variables and deployment

## Important existing project security issue
Supabase reports RLS disabled on existing public tables `bgg_collection`, `heartbeat`, `bg_game`. These were intentionally left untouched to avoid disrupting other applications.
