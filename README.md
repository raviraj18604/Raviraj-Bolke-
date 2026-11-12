# Raviraj Bolke — Cybersecurity Portfolio Starter

A responsive, neon cyber-command-center themed portfolio inspired by the reference image.

## Files
- `index.html` — public portfolio website
- `admin.html` — content management prototype
- `supabase_schema.sql` — starting SQL for a real authenticated backend
- `SECURITY_AND_DEPLOYMENT.md` — important deployment/security steps

## Run locally
Open `index.html` in a browser. For a local web server, run:
`python -m http.server 8000`
Then visit `http://localhost:8000`.

## Admin prototype
Open `admin.html`.
Demo passphrase: `ChangeMe-Admin-2026`.

**Important:** this demo admin is NOT secure authentication. Data is stored in the current browser's localStorage, so it does not sync to public visitors or other devices. It is a UI/content prototype only. Do not deploy it as a secure admin system or upload private documents. Replace it with Supabase Auth + database + storage + Row Level Security before public production use. The passphrase is visible in the source code and must not be treated as a secret.

## Current prototype upload limits
Each uploaded file is limited to 900 KB because it is stored as a browser data URL. Use Supabase Storage or another private object-storage service for production files.

## Personal data
The site starts with only the professional details already supplied in the conversation. Verify every date, institution, experience, certificate and project before publishing. Replace generic placeholders with verified facts. Only publish documents intended for public access; do not publish government IDs, passwords, private contact details, or sensitive academic records.

## Production security architecture
Recommended:
- Cloudflare DNS / HTTPS / WAF / DDoS protections
- Static hosting on Cloudflare Pages or Vercel
- Supabase Auth for admin sign-in
- Supabase Postgres with Row Level Security
- Supabase Storage with private buckets for admin-only files and a separate public bucket for intentionally public assets
- Server-side authorization for every admin mutation
- File type/size validation, rate limiting, backups, audit logging and secret management

See `SECURITY_AND_DEPLOYMENT.md` and `supabase_schema.sql` for the production upgrade starting point.
