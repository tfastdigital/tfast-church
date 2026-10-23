# Security policy and server checklist: Tfast Church (ChurchCRM base)

Last reviewed: 23 Oct 2026.

## Reporting a vulnerability
Email info@tfastdigital.com (subject "Security"). Do not open a public issue.

## 1. PHP2Shell (CVE-2026-109618 / CVE-2026-109619): critical, unauthenticated RCE
This is a bug in **PHP itself**, not in this code. Only a patched PHP fixes it.
- Required server PHP: **PHP 8.4.27+ or 8.5.12+ (ChurchCRM requires PHP >= 8.4)**. In Hostinger hPanel > Advanced > PHP Configuration pick that version,
  then check the PHP Info "Build Date" is 21 Oct 2026 or later.
- Defence-in-depth shipped in this repo (reduces exposure, is NOT a fix):
  - `.user.ini`: `session.upload_progress.enabled = 0`, strict sessions, HttpOnly cookies, `display_errors = Off`.
  - `.htaccess`: security headers, `X-Powered-By` removed, secrets/dumps/VCS files denied.
  - Upload/image folders refuse to run scripts.
- `expose_php` is a server-level setting: set it Off in hPanel > PHP Options.
- Check access logs from 17 Oct 2026 onwards for odd `POST` requests carrying `PHP_SESSION_UPLOAD_PROGRESS`,
  and look for new/unknown `.php` files in upload, image and cache folders.

## 2. laravel-lang supply-chain compromise (May 2026)
- `churchcrm/src/composer.lock` checked 23 Oct 2026: no `laravel-lang/*` packages and no `flipboxstudio` IOC.
- Deploy with `composer install --no-dev --optimize-autoloader`; never `composer update` on the server.
- `composer audit` runs in CI on every PR and weekly (fails on high/critical); Dependabot opens weekly update PRs.
- CI (`.github/workflows/security.yml`) greps for the IOC string `flipboxstudio` on every push/PR and weekly.

## 3. Server checklist
- [ ] PHP version patched (see section 1) and `expose_php = Off`.
- [ ] Debug output off in production (`APP_DEBUG=false` for Laravel apps).
- [ ] Daily backups of files + database; take a manual backup before every deploy/merge.
- [ ] Rotate any key/password that was ever committed, pasted into chat or a ticket.
- [ ] Run the host's malware scanner once after patching PHP.
- [ ] Person/family photos live in `churchcrm/src/Images`, which now refuses to run scripts.
- [ ] This repository is PUBLIC: never commit `Config.php`, `.env` or real member data.
