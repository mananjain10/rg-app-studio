# RG App Studio — website

The public website for **RG App Studio**, the trading name of Manan Bohra, sole proprietor, India.

Live site: **https://rg-app-studio.mananbohra1010.workers.dev**

## Pages

| Path | File | Purpose |
|---|---|---|
| `/` | `index.html` | Studio home — the apps, principles, pricing for Culmo Pro, contact |
| `/privacy/` | `privacy/index.html` | Studio-wide privacy policy, with a per-app section for each app |
| `/terms/` | `terms/index.html` | Terms of use, billing, cancellations, health disclaimer |
| `/refunds/` | `refunds/index.html` | Refund & cancellation policy |

The privacy policy URL (`/privacy/`) is the one submitted to Google Play for **Culmo**
(`com.mananbohra.culmo`).

## How it's built

Deliberately plain: four hand-written, self-contained HTML files. No build step, no framework,
no dependencies, no package.json.

Each page inlines its own CSS and makes **zero external requests** — no web fonts, no CDNs, no
analytics, no scripts on the legal pages. This is intentional: the site's closing line reads
"No cookies. No trackers on this page either," and it is literally true.

Typography uses system font stacks (a serif for display, the system sans for body, system mono for
labels), so nothing is ever fetched from a font host.

## Editing

Open a file in any editor and save. To preview, double-click it — it renders at full fidelity
straight from disk.

Keep in mind when editing the legal pages:

- The Culmo section of `privacy/index.html` must stay factually identical to `PRIVACY_POLICY.md`
  in the Culmo app repo — that file is the source of truth for every Culmo claim.
- Refund and cancellation wording is verified against Google Play's official documentation.
  Don't add a refund promise the studio can't actually honour.
- Studio-wide copy must not promise "no ads" or "no analytics" for every future app — only for
  apps whose own section says so.

## Deploying

Hosted on **Cloudflare** (Workers Static Assets), connected to this repo's `main` branch. Push to
`main` and the site redeploys automatically in well under a minute.

GitHub Pages was tried first and abandoned — its build backend accepted the deployment and then
never published it, failing at the deploy action's 600-second timeout on every attempt.

### The `.assetsignore` file matters

Cloudflare's assets directory is the **repo root**, so it uploads every file it finds. On the first
deploy that included `.git/`, which made the full repository fetchable over HTTP from the live site.

[`.assetsignore`](.assetsignore) is what prevents that. If you add a file to this repo that isn't a
page visitors should be able to open, add it there too. After any deploy, a quick sanity check:

```bash
curl -o /dev/null -w '%{http_code}\n' https://rg-app-studio.mananbohra1010.workers.dev/.git/config
# must print 404
```

## Contact

manangamestudio@gmail.com
