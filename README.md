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

### Current direct-upload workflow
The existing `arthur-parbal-website` Pages project supports Cloudflare Dashboard Direct Upload. Build and validate locally, then upload the contents of `dist/` as a ZIP or folder through that project’s **Create deployment** page and choose the intended environment. Do not create a replacement Pages project.

`wrangler pages deploy dist --project-name=arthur-parbal-website --branch=main` is the equivalent CLI command after Wrangler has a valid authorized Cloudflare login. The repository does not store Cloudflare credentials.
