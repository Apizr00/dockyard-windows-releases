# Changelog

All notable changes to Dockyard. The format follows [Keep a Changelog](https://keepachangelog.com/), and versions
follow [Semantic Versioning](https://semver.org/).

## [0.2.1] - 2026-10-17

### Added
- **MinIO**, an S3-compatible object store for local development (buckets, presigned URLs, the same SDK calls as production). Install it from the Runtimes page; it appears on the Services page and the Dashboard like the other services, with a settings dialog (S3 and console ports, this PC only or the whole network, root user, data folder, and the root password: show, copy, make a new one or type your own). The password is made at the first start and kept in Windows Credential Manager, never in a file. `dockyard minio show|set|password` do the same from a terminal.
  **Read this first:** MinIO stopped publishing community builds in October 2025 and archived its repository in April 2026, so the version Dockyard installs is the *last community release that has a Windows program* (2025-09-07, AGPL-3.0). It is marked end of life, the dialog says so, and a later security fix (a session-policy bypass for service accounts) is not in it. Keep it on this PC for development.

### Changed
- The PHP service is now called "PHP" instead of "PHP pool".

### Fixed
- **An update now replaces the copy of Dockyard that is running.** The installer remembers where it installed in one place for the whole PC, and anything else that ran a copy of it (a test, a second copy) could leave that pointing at another folder, so an update landed there and the app you start stayed as it was. Dockyard now tells the installer which folder it is running from.

## [0.2.0] - 2026-10-17

### Added
- **Packages page: every version of MySQL, MariaDB and PostgreSQL, side by side.** MySQL 5.5 to 9.7, MariaDB 10.6 to 12.3 and PostgreSQL 12 to 18 can be installed together. Each version is its own service (`mysql-8.4`, `postgres-17`) with its own data folder, port, log and settings, and several can run at once. Old and end-of-life versions are marked and hidden until you ask for them. `mysql`, `mariadb` and `postgres` still mean the default version, so scripts, autostart lists and the built-in `local-mysql` style connections keep working.
- **A settings page for each server:** port, who may connect (this PC only, or the whole network once a password is set), data folder, tuning dropdowns and extra configuration lines, and the administrator password (set, remove, or reset a forgotten one). Passwords are kept in Windows Credential Manager. `dockyard packages` and `dockyard db-server list|show|set|password|reset-password` do the same from a terminal.
- A data folder is stamped with its version and a different version refuses to use it; the single data folder of earlier builds is moved into the folder of the version that made it, the first time that version starts. Installing a newer version never changes which version is the default.

### Fixed
- The first-run setup showed the "Pick your stack" list centred, with each switch under its label; the rows now line up.

### Changed
- The Services, Dashboard, Logs and Database pages list one entry per database version.

## [0.1.3] - 2026-10-17

### Added
- **Update popup.** Each time Dockyard starts it quietly checks for a newer version (and again once a day while it keeps running). If there is none, you see nothing. If there is, a popup offers **Update now**, **Remind me later** (it asks again at the next start) or **Skip this version** (quiet until a newer one comes out). Settings shows a skipped version and can offer it again; `dockyard update skip|unskip|remind` do the same from a terminal. The check can still be switched off.

### Changed
- **Redis is real Redis now.** Dockyard installs Redis 8.x, 7.x or 6.2 (the official source built for Windows by the `redis-windows` project), from the Runtimes page, instead of a Redis-compatible server. It keeps its data across restarts, and Lua scripts (which Laravel's queues, locks and rate limiting use), Streams and the other commands work. It idles at about 9 MB. **If you had the earlier Redis-compatible server installed, install Redis from Runtimes: that server is no longer offered or started.**

### Fixed
- `dockyard update auto off` no longer answers "the update was installed".

## [0.1.2] - 2026-10-17

### Added
- **Dashboard**, now the first page: how busy this PC is (processor load as a gauge with the last minute and a half as a chart, memory, the drive Dockyard lives on, network address and speed), your services as tiles you can start and stop, and your websites with open, folder and terminal buttons.
- **About** page: version, check for updates, release notes, report an issue, copy diagnostics.
- `dockyard stats` prints the same numbers in a terminal (`--json` for scripts).

### Changed
- Dockyard opens on the Dashboard instead of Services. The menu scrolls when the window is short, so all nine items stay reachable.

## [0.1.1] - 2026-10-17

### Added
- **MySQL 8.4 LTS** can be installed from the Runtimes page (the service existed, but nothing offered the download).
- The built-in list of runtimes now includes Garnet 2.2.3 (the Redis-compatible server).

### Changed
- **Dockyard opens at a smaller size** (900 × 600, centred) instead of 1280 × 800.

### Fixed
- Right-click menus in the database client no longer run off the edge of a small window.

## [0.1.0] - 2026-10-17

First release. Pre-release quality: see the README for what is and is not verified.

### Added
- **The stack from one tray icon.** nginx, PHP (several versions side by side, a pool of php-cgi workers each), MariaDB or
  MySQL, PostgreSQL, Redis (Garnet) and Mailpit, with start, stop, logs, ports, memory and the name of whatever holds a
  port you need. Stopping Dockyard leaves no orphan processes.
- **Sites.** A folder in `www\` becomes `https://name.test` (or `.localhost`, which needs no administrator rights), with a
  local certificate authority, per-site PHP version, aliases and a checked nginx snippet editor.
- **Runtime manager.** Install, switch and remove PHP, nginx, MariaDB, MySQL, Node, Composer, Mailpit, PostgreSQL, Garnet,
  Xdebug and cloudflared; every download is checked against a SHA-256 first. Optional `php`, `composer`, `node`, `mysql`
  shims on your user PATH.
- **Database client.** Browse, query, edit (one transaction, SQL shown first), change structure, import and export for
  MySQL, MariaDB, PostgreSQL and SQLite; a Redis browser with a console.
- **New app wizard.** Laravel, Symfony, WordPress or blank PHP, with its database, user, `.env` and HTTPS site.
- **Mail, Xdebug, Share.** PHP `mail()` lands in Mailpit; Xdebug per PHP version; a temporary public address for a site.
- **`dockyard` command line** for everything the window does.
- **First-run setup**, in the window or as `dockyard setup`.
- **Installer and portable zip.** Per-user installer (no administrator rights) and a zip that keeps its data beside it.
- **Updates.** Dockyard asks once a day whether a newer version exists (switch it off in Settings) and installs only
  when you press Install; installers and the runtime catalog are checked against Dockyard's signing key.
- **Diagnostics.** *Copy diagnostics* and `dockyard diagnostics --zip` for bug reports; nothing is uploaded.

### Known limits
- The installer is **not code-signed**, so Windows SmartScreen may warn the first time you run it.
- Not yet tested on a fresh virtual machine, and `.test` names (hosts helper, trusting the certificate authority in your
  real store) were verified only in scripted scratch environments.
- Share, and the WordPress and Symfony wizards, are only partly verified.
