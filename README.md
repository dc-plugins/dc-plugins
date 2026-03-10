# DC Plugins

Open-source WordPress plugins developed and maintained by [Dampcig.dk](https://dampcig.dk).

---

## Plugins

| Plugin | Description | Version | WP.org |
|--------|-------------|---------|--------|
| [DC Service Worker Prefetcher](https://github.com/dc-plugins/dc-sw-prefetch) | Registers a Service Worker that prefetches WooCommerce product pages for instant navigation | 1.0.0 | *Pending* |
| [DC WebP Converter](https://github.com/dc-plugins/dc-webp-converter) | Converts PNG & JPG product images to WebP in the background via WP-Cron | 1.0.0 | *Pending* |

---

## Architecture

Each plugin lives in its own repository and is deployed automatically to production on push to `main` via GitHub Actions + rsync over SSH.

```
dc-plugins/           ← This umbrella repo (org profile)
├── dc-sw-prefetch/   ← github.com/dc-plugins/dc-sw-prefetch
└── dc-webp-converter/← github.com/dc-plugins/dc-webp-converter
```

## Shared GitHub Secrets (per repo)

| Secret | Value |
|--------|-------|
| `SSH_PRIVATE_KEY` | Contents of `Private.pem` |
| `SSH_HOST` | `linux195.unoeuro.com` |
| `SSH_USER` | `dampcig.dk` |
| `DEPLOY_PATH` | `/var/www/dampcig.dk/public_html/wp-content/plugins` |

---

## License

GPL-2.0-or-later — same as WordPress core.
