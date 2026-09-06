# abridgd-site

The public site for [Abridgd](https://github.com/McCal-Codes/abridgd): the launch
page, the privacy policy, and the terms.

Plain HTML, no build step, no dependencies. Open `index.html` in a browser to
edit; there is nothing to install or run.

```
index.html    launch page
privacy.html  required by Google Play, and linked from App Info inside the app
terms.html    linked from App Info inside the app
```

## Why this is a separate repository

The app repository is private-ish working code with its own release process,
branch protection, and CI. The site is public, changes on a different rhythm, and
needs no review gate to publish a typo fix. Keeping them apart means a marketing
change cannot fail an app build, and vice versa.

The trade-off: `privacy.html` and `terms.html` are linked from
`src/config/appInfo.ts` in the app repo, so those two files are a contract
between the repositories. The deploy workflow fails if either goes missing, but
nothing here can stop someone changing the app's URLs. If those links move,
change them in both places.

## Deployment

Every push to `master` deploys via `.github/workflows/deploy.yml`, using the Pages
**Actions** source rather than a `gh-pages` branch.

**One-time setup:** Settings → Pages → Source: **GitHub Actions**. Without it the
deploy step fails.

Publishes to `https://mccal-codes.github.io/abridgd-site/`.

## Custom domain

The app links to `https://abridgd.app/privacy` and `https://abridgd.app/terms`,
and Google Play requires a reachable privacy policy URL — so the domain is a
launch blocker, not a nicety.

To point it here: add a `CNAME` file at the repository root containing
`abridgd.app`, then create a DNS `ALIAS`/`ANAME` record at the apex pointing to
`mccal-codes.github.io` (or four `A` records to GitHub's Pages addresses, if the
registrar has no apex alias support). GitHub provisions the certificate.

Until that resolves, either the App Info links are broken or they should point at
the `github.io` URL. Do not submit a store listing with a privacy URL that does
not load.

## Editing

Two constraints worth keeping:

- **Editorial, not solemn.** Fraunces is the app's real identity; keep it. Prefer
  fewer, punchier sections over exhaustive lists.
- **No "AI", "smart", "powered by", "intelligent" or similar** anywhere on the
  site. Summarising is an optional feature readers supply their own key for. It
  is not the pitch.

The phone mockups in the hero are CSS placeholders, laid out so real screenshots
drop in as `<img>` without restructuring the section.
