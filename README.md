# DC Plugins

Open-source WordPress plugins developed and maintained by [Dampcig.dk](https://www.dampcig.dk) — Denmark's leading vape & e-cigarette retailer.

Each plugin solves a real production problem on a high-traffic WooCommerce store. They are lightweight, built without external dependencies, and pass WordPress Plugin Check with 0 errors.

---

## Plugins

| Plugin | Description | Version |
|--------|-------------|---------|
| [DC Google Indexing](https://github.com/dc-plugins/dc-google-indexing) | Submit URLs to Google's Web Search Indexing API for instant crawling. Auto-submit on publish, manual batch submission, and a Polling mode that discovers unindexed pages via the URL Inspection API. | 1.0.0 |
| [DC Service Worker Prefetcher](https://github.com/dc-plugins/dc-sw-prefetch) | Caches static assets via service worker and prefetches WooCommerce product pages as they enter the viewport — near-instant navigation without conflicting with W3TC or checkout. | 1.0.0 |
| [DC WebP Converter](https://github.com/dc-plugins/dc-webp-converter) | Converts WooCommerce product images (PNG & JPG) to WebP silently in the background via WP-Cron. Saves bandwidth and improves Core Web Vitals. | 1.2.0 |

---

## Architecture

Each plugin lives in its own repository and is deployed automatically to production on push to `main` via GitHub Actions + rsync over SSH. Tagged releases (`v*`) also build a distributable `.zip` and publish a GitHub Release.

```
dc-plugins/              ← This umbrella repo
├── dc-google-indexing/  ← github.com/dc-plugins/dc-google-indexing
├── dc-sw-prefetch/      ← github.com/dc-plugins/dc-sw-prefetch
└── dc-webp-converter/   ← github.com/dc-plugins/dc-webp-converter
```

## Shared CI/CD

All repos share org-level variables for deployment:

| Variable | Value |
|----------|-------|
| `SSH_HOST` | `linux195.unoeuro.com` |
| `SSH_USER` | `dampcig.dk` |
| `DEPLOY_PATH` | `/var/www/dampcig.dk/public_html/wp-content/plugins/` |

Each repo holds its own `SSH_PRIVATE_KEY` secret (ED25519, no passphrase).

---

## Standards

- PHP 8.0+ · WordPress 6.8+ · WooCommerce 10.4+ compatible
- WordPress coding standards — escaped output, nonce-protected forms, sanitised inputs
- `permissions: contents: write` on all workflows for tagged GitHub Releases
- `.distignore` in each repo keeps dev files (`.git*`) out of Plugin Check and distribution ZIPs

---

## License

GPL-2.0-or-later — same as WordPress core.