# Changelog

All notable changes to Dockyard. The format follows [Keep a Changelog](https://keepachangelog.com/), and versions
follow [Semantic Versioning](https://semver.org/).

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
