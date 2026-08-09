# BariCare360

BariCare360 is a modern, multi-tenant property and community management platform designed for apartment buildings, housing societies, property managers, residents, and finance teams. It brings resident services, building operations, billing, accounting, and communication together in one secure Laravel-based application.

## Why BariCare360

BariCare360 helps organizations run day-to-day operations with clarity and control. From onboarding residents and managing properties to issuing invoices and resolving maintenance concerns, the platform provides a structured digital workflow for every stakeholder.

### Core capabilities

- SaaS administration for organizations, plans, subscriptions, and support
- Property, building, block, floor, flat, owner, tenant, and family-member management
- Utility billing, service charges, invoices, payments, receipts, and overdue tracking
- Double-entry accounting, chart of accounts, ledger, and financial reporting
- Maintenance requests, complaints, assignments, expenses, and attachments
- Visitor tracking, security shifts, incidents, vehicles, and parking workflows
- Notices, announcements, documents, committees, meetings, and minutes
- Resident portal for bills, requests, notices, complaints, and maintenance
- In-app, email, and SMS notification workflows
- English and Bengali localization support

## Platform overview

BariCare360 is built around three logical layers:

1. **Platform** – SaaS administrators manage organizations, plans, billing, and support.
2. **Organization** – Building teams manage properties, residents, finances, and operations.
3. **Resident** – Owners and tenants view bills, submit requests, and receive updates.

See the [architecture guide](docs/architecture.md) for deeper context on tenancy, request lifecycle, and modular boundaries.

## Workflow simulation

The following image shows a premium, end-to-end operating model for BariCare360—from resident engagement to coordinated service delivery:

<div align="center">
  <img src="docs/images/bari-care360-workflow.svg" alt="BariCare360 workflow animation" width="920" />
</div>

This premium workflow reflects how BariCare360 connects resident engagement, operational execution, financial accuracy, and timely communication into one intelligent experience.

## Technology stack

- PHP 8.2+
- Laravel 12
- Blade, Bootstrap, Alpine.js, and Vite
- MySQL 8+ for production, SQLite for local development
- Composer 2+
- Node.js 20+ and npm
- Database or Redis queues; Redis is recommended for production

## System requirements

Install the following before setup:

- PHP 8.2 or newer with `mbstring`, `dom`, `xml`, `curl`, `gd`, `zip`, `intl`, `fileinfo`, `openssl`, `bcmath`, and `pdo`
- Composer 2 or newer
- Node.js 20 or newer with npm
- MySQL 8+ or SQLite

## Local installation

From the project directory:

```bash
git clone https://github.com/boltechbd/fms.git
cd fms
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
npm install
npm run build
```

On Windows PowerShell, use this instead of `cp`:

```powershell
Copy-Item .env.example .env
```

The default environment uses SQLite. To use MySQL, update the `DB_*` values in `.env` before running migrations. Never commit `.env` or production credentials.

## Development workflow

Start the application server:

```bash
php artisan serve
```

For the full local experience, including queues, logs, and Vite hot reload:

```bash
composer run dev
```

The application is available at `http://127.0.0.1:8000` unless Laravel reports a different port.

## Frontend commands

```bash
npm run dev      # Vite development server with hot reload
npm run build    # Production frontend build
```

## Testing

Run the Laravel test suite with:

```bash
php artisan test
```

Or use the Composer shortcut:

```bash
composer run test
```

## Queue and scheduler

The default local queue driver is database-backed. Run a worker when testing notifications, invoices, or other queued jobs:

```bash
php artisan queue:work
```

Production deployments must run the scheduler every minute:

```bash
php artisan schedule:run
```

For VPS deployments, use a persistent queue worker managed by Supervisor. See the [deployment guide](docs/deployment.md) for cPanel, VPS, queue, backup, and security instructions.

## Deployment notes

For production, place the Laravel application outside the public web root and point the domain document root to the project's `public` directory.

Recommended steps:

1. Create the database and application user.
2. Upload or clone the repository into the account home directory.
3. Set the web root to the `public` directory.
4. Install production dependencies and configure `.env`.
5. Run migrations, seed data, build assets, and enable storage links.

See the [deployment guide](docs/deployment.md) for full cPanel and VPS instructions.

## Project documentation

- [Architecture](docs/architecture.md)
- [Modules](docs/modules.md)
- [Database](docs/database.md)
- [API](docs/api.md)
- [Permissions](docs/permissions.md)
- [Workflows](docs/workflows.md)
- [Deployment](docs/deployment.md)
- [Security audit](docs/security-audit.md)
- [UI guidelines](docs/ui-guidelines.md)

## Security

Report suspected vulnerabilities privately to the project maintainers. Do not open a public issue containing credentials, personal data, tenant data, or an exploitable proof of concept.

Before production deployment:

- Set `APP_ENV=production` and `APP_DEBUG=false`
- Configure HTTPS and secure session cookies
- Keep uploads on a private storage disk
- Run `composer audit` and keep dependencies current
- Configure database and uploaded-file backups

## License

This project is released under the MIT License. See the project files for the applicable license terms.
