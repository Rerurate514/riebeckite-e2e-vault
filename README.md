# Riebeckite E2E: separate repositories — Vault

The content repository for the **separate repositories** Riebeckite sample. The site code lives in the companion site repository.

- **Published site:** <https://repositories.riebeckite.dev>
- **Site repository:** [Rerurate514/riebeckite-e2e-site](https://github.com/Rerurate514/riebeckite-e2e-site)
- **Riebeckite documentation:** <https://riebeckite.dev>
- **Other samples:** [integrated](https://integrated.riebeckite.dev) · [separate directories](https://directories.riebeckite.dev)

## Purpose

This repository contains only content. It can be opened directly in Obsidian, reviewed by writers, and granted to people who should not touch deployment code.

## Directory structure

```text
.
├── index.md
├── notes/
│   ├── welcome.md
│   ├── japanese.md
│   ├── markdown.md
│   ├── diagram.md
│   └── attachments.md
├── assets/
│   ├── diagram.svg
│   └── sample.txt
└── .github/workflows/
    └── notify-site.yml        Ask the site repository to deploy
```

## Setup

Clone this repository next to the site repository, or clone it into the site's `content/` directory:

```sh
git clone https://github.com/Rerurate514/riebeckite-e2e-site.git
cd riebeckite-e2e-site
git clone https://github.com/Rerurate514/riebeckite-e2e-vault.git content
```

## Local development

Riebeckite runs from the site repository:

```sh
cd riebeckite-e2e-site
npm exec riebeckite dev
```

Edit this Vault, then reload the site.

## Build

Build from the site repository:

```sh
npm run build
```

The site reads this directory through the `content/` checkout. This repository has no build step of its own.

## Deploy

Push to `main`. The `Notify Riebeckite site` workflow sends a `content-updated` repository dispatch to the site repository, which builds and deploys to `repositories.riebeckite.dev`.

To deploy manually, run the site workflow with **Actions → Deploy to Cloudflare Workers → Run workflow**.

## GitHub Actions

`.github/workflows/notify-site.yml` requires either a GitHub App or a fallback PAT:

| Name | Kind | Purpose |
| --- | --- | --- |
| `RIEBECKITE_APP_ID` | Secret | GitHub App ID |
| `RIEBECKITE_APP_PRIVATE_KEY` | Secret | GitHub App private key |
| `SITE_DISPATCH_TOKEN` | Secret | Optional fallback instead of the GitHub App |

The App needs **Contents: read and write** and **Metadata: read-only**, and must be installed only on [the site repository](https://github.com/Rerurate514/riebeckite-e2e-site). The workflow mints a short-lived token and uses it only to call the repository dispatch API.

## Content in this sample

`index.md` explains the split layout. `notes/` demonstrates frontmatter, tags, WikiLinks, backlinks, Markdown links, tables, code, Mermaid, and images. `assets/diagram.svg` is the source image. The downloadable `sample.txt` lives in the site repository's `public/assets/` because it is a static site file, not a note attachment.

## Related documentation

- [Quick Start](https://riebeckite.dev/docs/getting-started/quick-start)
- [Content repositories](https://riebeckite.dev/docs/guides/content-repositories/basics)
- [Separate content repository setup](https://riebeckite.dev/docs/guides/content-repositories/setup)
- [GitHub Actions deployment](https://riebeckite.dev/docs/guides/deployment/github-actions)
- [Troubleshooting](https://riebeckite.dev/docs/guides/deployment/github-actions/troubleshooting)

## License

Apache License 2.0. See [LICENSE](LICENSE).
