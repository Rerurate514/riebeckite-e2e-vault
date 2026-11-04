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

`.github/workflows/notify-site.yml` requires one secret:

| Secret | Purpose |
| --- | --- |
| `SITE_DISPATCH_TOKEN` | Fine-grained token scoped to [the site repository](https://github.com/Rerurate514/riebeckite-e2e-site) with **Contents: read and write**. |

The token is used only to call the repository dispatch API. It is not stored in this repository.

## Content in this sample

`index.md` explains the split layout. `notes/` demonstrates frontmatter, tags, WikiLinks, backlinks, Markdown links, tables, code, Mermaid, and images. `assets/diagram.svg` is the source image. The downloadable `sample.txt` lives in the site repository's `public/assets/` because it is a static site file, not a note attachment.

## Related documentation

- [Quick Start](https://riebeckite.dev/getting-started/quick-start)
- [Separate content repository concepts](https://riebeckite.dev/guides/deployment/separate-content-repository/concepts)
- [Repository split](https://riebeckite.dev/guides/deployment/separate-content-repository/repository-split)
- [Publishing](https://riebeckite.dev/guides/deployment/separate-content-repository/publishing)
- [Troubleshooting](https://riebeckite.dev/guides/deployment/separate-content-repository/troubleshooting)

## License

Apache License 2.0. See [LICENSE](LICENSE).
