# proxy-dash

Original source of the **proxy pools** dashboard from 9router — frontend page plus its
API routes. Archived here before the page was repurposed into a WARP exit-IP / rotation log.

Extracted from `9router` (base v0.5.99) on 2026-10-23. Unmodified copy.

## Contents

```
src/app/(dashboard)/dashboard/proxy-pools/page.js   # dashboard UI (~1200 lines)
src/app/api/proxy-pools/route.js                    # list / create / bulk import
src/app/api/proxy-pools/[id]/route.js               # get / patch / delete
src/app/api/proxy-pools/[id]/test/route.js          # per-proxy connectivity test
src/app/api/proxy-pools/vercel-deploy/route.js      # deploy proxy worker to Vercel
src/app/api/proxy-pools/cloudflare-deploy/route.js  # deploy proxy worker to Cloudflare
src/app/api/proxy-pools/deno-deploy/route.js        # deploy proxy worker to Deno
src/app/api/proxy-pools/netlify-deploy/route.js     # deploy proxy worker to Netlify
```

## What it did

Managed a pool of outbound HTTP proxies used by connection-level routing in 9router.
Features: bulk import (`host:port`, `host:port:user:pass`, URL, JSON), per-proxy
connectivity test with cooldown marking, drag ordering, and one-click deployment of a
relay worker to Vercel / Cloudflare / Deno / Netlify.

Data lived in the `proxyPools` table (one JSON blob per row, keyed by `id`).

## Why archived

The page was never used in production and is being replaced. Kept here as the original
implementation so the proxy-pool code is not lost when the dashboard route is repurposed.

## Notes

- Depends on 9router internals (`@/lib/localDb`, `@/lib/db/repos`, UI components).
  This is a code archive, not a standalone runnable app.
- No secrets included. The proxy credentials it handled were stored per-row in the local
  database, never in source.
