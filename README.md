# Kimai (LazyCat LPK)

Open-source time tracker with projects, activities, customers and reports.

- Upstream: https://github.com/kimai/kimai
- Image: `kimai/kimai2:2.71.0` (mirror mode, digest-matched)
- License: AGPL-3.0 (full text in `content/licenses/LICENSE`)
- Containers: app + MariaDB 10.11

## Notes

- The image's own entrypoint handles install and first admin creation:
  `kimai:install` is idempotent, and `kimai:user:create --ignore-existing admin ...`
  runs only when `ADMINMAIL`/`ADMINPASS` are set — so the admin password comes from a
  deploy param (random by default), not a hardcoded credential. `--ignore-existing`
  means a later password change is never overwritten on restart.
- Admin username is fixed `admin` (upstream behaviour).
- `DATABASE_URL` is a single DSN, not separate DB_* vars. MariaDB 10.11 matches the
  `serverVersion=10.11` hint in the DSN.
- APP_SECRET comes from a platform stable secret.
- No mail service configured (invites / password reset by email unavailable).
- Not yet verified on a real device.
