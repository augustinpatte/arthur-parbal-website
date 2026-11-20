# Arthur Parbal — official website

Dependency-free static site generator for Cloudflare Pages. `npm run build` produces `dist/`; `npm run check` verifies local links, duplicate titles, canonicals and required SEO files.

## Cloudflare Pages
Connect this repository with production branch `main`, build command `npm run build`, output directory `dist`, Node 20+. Set `PUBLIC_SITE_URL` to the final custom domain after it is verified; otherwise the production Pages URL is used.

### Verified local release checks
```sh
npm ci --ignore-scripts
npm run build
npm run check
find dist -name '*.html' -type f | wc -l
```

### Production deployment — existing Pages project
This site is deployed directly to the existing Cloudflare Pages project, `arthur-parbal-website`, on its `main` branch. Do **not** create another Pages project, change DNS/custom-domain settings, or depend on GitHub Actions for releases.

Run the release flow in this order:

```sh
# Preserve any local work, then synchronize the checked-out main branch.
git fetch origin main
git merge --ff-only origin/main

npm ci --ignore-scripts
npm run build
npm run check
test -d dist
find dist -type f -name '*.html' | wc -l

# Requires an already-authorized Wrangler login.
npx wrangler whoami
npx wrangler pages deploy dist \
  --project-name=arthur-parbal-website \
  --branch=main
```

For content batches, use: **Write → Validate → Build → Commit → Push → Direct deploy → Verify production**. Verify the production sitemap and the newly added URLs after each deployment; a successful upload is not evidence that pages have been indexed. Cloudflare credentials are never stored in this repository.
