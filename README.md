# Concert Reservation

Browser-based concert reservation application implemented with PHP, HTML, CSS, JavaScript, and MariaDB/MySQL.

[![PHP](https://img.shields.io/badge/Language-PHP-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net/)
[![MariaDB](https://img.shields.io/badge/Database-MariaDB%2FMySQL-003545?style=flat-square&logo=mariadb&logoColor=white)](https://mariadb.org/)
[![Academic Project](https://img.shields.io/badge/Category-Academic%20Project-6C757D?style=flat-square)](#academic-context)
[![Year](https://img.shields.io/badge/Year-2024-6C757D?style=flat-square)](#historical-context)

> [!NOTE]
> This repository contains an academic project originally developed during earlier programming studies. It is preserved as a record of the technical knowledge, design decisions, and development experience acquired at the time rather than as a current production service.

## Overview

The application lets a visitor browse available bands and concert dates, inspect seats for a selected event, and reserve an available seat after signing in. The browser communicates with PHP endpoints that use sessions and `mysqli` to query and update a MariaDB/MySQL database.

## Implemented features

- Lists bands retrieved from the database.
- Lists concert dates for a selected band.
- Displays the venue, date, and seat availability for a selected concert.
- Authenticates users with a username and password through a PHP session.
- Allows an authenticated user to reserve a displayed seat.
- Prevents an authenticated user from reserving more than one ticket for the same concert date.
- Refreshes the seat list periodically in the reservation view.

## Technology stack

- **Frontend:** HTML, CSS, and browser JavaScript using `XMLHttpRequest`.
- **Backend:** PHP scripts returning JSON responses and managing PHP sessions.
- **Database:** MariaDB/MySQL accessed through PHP `mysqli`.
- **Schema:** Bands (`tband`/`tBand`), concert dates (`tdata`/`tData`), reservations (`tprenotazione`), and users (`tutente`).

## Repository variants

The repository contains two related implementations:

| Path | Verified layout |
| --- | --- |
| `locale/` | Self-contained pages, PHP handlers, CSS, and `locale/pren_ulivi.sql`; frontend requests use relative paths. |
| `infrastruttura/` | `presentation/` contains the HTML/CSS frontend and `logic/` contains PHP handlers; `db/pren_ulivi.sql` supplies the database dump. The frontend currently references a fixed private-network HTTP host, so it requires environment-specific adjustment before use elsewhere. |

The SQL dumps are not identical: they reflect the data and schema of their respective variants. Choose the dump that matches the implementation you intend to run.

## Project structure

```text
.
├── db/pren_ulivi.sql
├── infrastruttura/
│   ├── logic/                  # PHP session, authentication, queries, and reservations
│   └── presentation/           # HTML pages and CSS
└── locale/
    ├── *.php                   # PHP handlers
    ├── *.html                  # HTML pages
    ├── css/                    # Stylesheets
    └── pren_ulivi.sql          # Database dump for this variant
```

## Getting started

### Prerequisites

The source requires:

- A PHP runtime with the `mysqli` extension.
- A MariaDB or MySQL server.
- A web server configured to serve PHP files.

The repository does not contain a dependency manifest, framework configuration, container configuration, or automated deployment setup.

### Database setup

1. Create a database named `pren_ulivi`.
2. Import the SQL dump for the chosen variant:

   ```bash
   mariadb -u <database-user> -p pren_ulivi < locale/pren_ulivi.sql
   ```

   Use `db/pren_ulivi.sql` instead when running the `infrastruttura/` variant.
3. Configure the database connection in the corresponding `var_conn.php` before serving the application. Do not commit credentials.

### Run locally

No repository-defined start command is present. Serve the selected directory through a PHP-capable web server and open its `index.html` entry point in a browser:

- `locale/index.html` for the relative-path variant.
- `infrastruttura/presentation/index.html` for the separated variant, after adapting its environment-specific endpoint URLs.

The PHP handlers expect to be reachable under the paths referenced by the selected frontend. The application stores the selected band and concert date in the PHP session while navigating between pages.

## Testing and build status

No test files, build scripts, package manifests, or continuous-integration workflows are present in the repository. Consequently, there is no repository-defined automated test or build command to run.

## Historical context

The repository name identifies the work as a submission, and the two database dumps contain dated April 2024 export metadata. Git history records commits on April 25–26, 2024, consistently supporting **2024** as the original development period.

## Limitations

- The `infrastruttura/` frontend contains environment-specific LAN URLs.
- Database connection settings are stored directly in PHP configuration files and must be adapted per environment.
- Authentication and reservation handlers are educational implementations and should not be treated as production-grade security or deployment guidance.

## License

No license file or explicit license declaration is present in the repository. Licensing status requires human review.
