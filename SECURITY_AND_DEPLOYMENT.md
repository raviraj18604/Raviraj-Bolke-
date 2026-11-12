# Security and deployment guide

## Do not confuse the prototype with a production admin system
The included `admin.html` uses a client-side demo passphrase and browser localStorage. Anyone who can inspect the source can find the passphrase. Changes only exist in that browser. It is intentionally a functional UI prototype, not secure multi-user content management.

## Production target architecture
Visitor -> Cloudflare DNS/HTTPS/WAF -> static frontend -> authenticated server/API -> database and object storage.

Recommended components:
1. Cloudflare Pages for hosting and Cloudflare DNS/HTTPS/WAF configuration.
2. Supabase Auth for administrator authentication.
3. Supabase Postgres with RLS policies on every content table.
4. Supabase Storage. Use a public bucket only for assets intentionally published to the world. Keep private files in a private bucket and issue short-lived signed URLs only after authorization.
5. Server-side validation for all uploads and content changes. Never rely on hiding admin buttons in JavaScript.
6. Add rate limiting, bot protection, backups, logging, dependency updates and security headers.
7. Store service-role keys only in server-side environment variables. Never put them in frontend JavaScript or a public GitHub repository.

## Suggested deployment sequence
1. Create a GitHub repository and upload the project files.
2. Create a Supabase project.
3. Run `supabase_schema.sql` in the Supabase SQL editor after reviewing it.
4. Create an admin account using Supabase Auth, then insert that user's UUID into `admin_users`.
5. Replace the prototype admin UI's localStorage functions with authenticated Supabase queries and storage uploads. Add server-side authorization for all write actions.
6. Deploy the public frontend to Cloudflare Pages.
7. Add the domain to Cloudflare, enable HTTPS and configure WAF rules appropriate to your app.
8. Add sitemap.xml, robots.txt, page metadata and verify the domain in Google Search Console.
9. Test admin access from a separate browser/device, public visibility, file permissions, upload validation, contact form spam protection and mobile layout.

## SEO
Google indexing is not instant or guaranteed. Use a domain you control, unique page titles, descriptive content, sitemap.xml, robots.txt, canonical URL and Google Search Console. A free subdomain can be used to launch before buying a custom domain.
