# YAER.io

Corporate/product-studio website for YAER LLC. Products inspired by everyday life, built with curiosity and care. PuckPlus is the first product, currently in development. Built with Astro and TypeScript, with static HTML, local assets, a self-hosted Inter font with system fallbacks, and no client-side JavaScript or tracking.

## Local development

Use Node.js 24 LTS (Node 22.12+ is also supported) and npm.

```sh
npm ci
npm run dev
```

Validate and preview the production output:

```sh
ASTRO_TELEMETRY_DISABLED=1 npm run check
ASTRO_TELEMETRY_DISABLED=1 npm run build
ASTRO_TELEMETRY_DISABLED=1 npm run preview
```

Astro telemetry can be disabled with the environment variable above. The preview normally runs at http://localhost:4321. `.npmrc` stores the local npm cache in `/tmp/yaer-npm-cache`; this does not affect site behavior.

## Content and structure

- `src/config.ts`: site metadata and configurable contact email. `contact@yaer.io` has been confirmed to receive mail.
- `src/data/products.ts`: typed product collection; PuckPlus is in development. Its optional `url` is deliberately absent because puckplus.app is registered but the product website is not live. Add `url: 'https://puckplus.app'` when that site is ready to enable the product CTA.
- `src/components/`: header, typography-led hero, product showcase, conceptual phone sketches, philosophy, About, contact CTA, and footer.
- `src/layouts/SiteLayout.astro`: document and per-page metadata.
- `src/pages/`: homepage, website privacy, 404, sitemap.
- `src/styles/global.css`: colors, typography, responsive layout, and reduced-motion support.
- `public/`: favicon, sharing image, robots.txt, domain marker, original PuckPlus app icon, and monochrome Phosphor icons (MIT license included).
- `src/assets/`: original conceptual phone sketch and optimized-build source.

The canonical mobile icon at `public/assets/puckplus/app-icon.png` is copied unchanged from the mobile app project. Preserve it; do not regenerate, recolor, or redraw it. Phone illustrations are conceptual pencil sketches, not unreleased product screenshots. The earlier ribbon hero is not used by the page.
- `.github/workflows/deploy.yml`: production deployment on main pushes or manual dispatch.

The website privacy notice describes this website only. It does not replace a future PuckPlus app privacy policy. Update it if analytics, forms, cookies, or providers change.

## GitHub Pages deployment

The site was unpublished at the user’s request. Source updates are pushed to main; publication requires manually dispatching the deployment workflow. A local backup branch preserves the old deployed version.

The intended repository is `yaerxo/yaer.io`. Commit source and the npm lockfile, not `dist/` or `node_modules/`. In repository **Settings → Pages**, choose **GitHub Actions** as the publishing source. Private repositories require an eligible GitHub plan for Pages; keeping source private and publishing the website publicly are separate settings.

Push `main`. The workflow installs the locked dependencies, checks TypeScript/Astro, builds `dist`, and uploads a Pages artifact. Manually dispatch the workflow to deploy it. Inspect **Actions → Deploy YAER.io** for errors. The `github-pages` environment must allow main-branch deployment.

## Custom domain

Configure **Settings → Pages → Custom domain** as `yaer.io`. `public/CNAME` records the intended domain, but GitHub ignores CNAME files for custom Actions deployments: the repository setting is required.

At the DNS provider, configure these website records (preserve mail/MX/TXT records):

| Type | Name | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | yaerxo.github.io |

Replace conflicting parking records for these hostnames. If apex AAAA records exist, align them with GitHub's documented IPv6 addresses or remove conflicting website AAAA records. Do not add wildcard DNS records.

GitHub automatically redirects www to the apex when both DNS records and the apex custom domain are configured. Enable **Enforce HTTPS** when GitHub's certificate is ready; certificate issuance can take up to 24 hours. Canonical URLs and social metadata use `https://yaer.io`; this build assumes the custom domain, rather than the repository-path preview URL.

Official references: [custom workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages), [custom domains and DNS](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site), [HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https).

## Release verification

Check https://yaer.io, https://www.yaer.io (redirect), and https://yaer.io/privacy/. Verify company identity, product status/ownership, every navigation link, contact delivery, favicon, social image, and phone/tablet/desktop layout. Run Lighthouse against the published site before reporting production scores. A successful local build does not establish public deployment or guarantee Apple enrollment acceptance.
