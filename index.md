---
publish: true
title: Home
tags:
  - sample
---

# Riebeckite sample: separate repositories

This is the **separate repositories** sample. The site and the Vault are two independent repositories:

- Site: [Rerurate514/riebeckite-e2e-site](https://github.com/Rerurate514/riebeckite-e2e-site)
- Vault: [Rerurate514/riebeckite-e2e-vault](https://github.com/Rerurate514/riebeckite-e2e-vault)
- Published site: <https://repositories.riebeckite.dev>

Everything you are reading comes from the Vault repository. The site repository contains only code and deployment configuration.

## How this layout works

The site repository keeps `content.directory` at `content/`. During a GitHub Actions run, the workflow checks out the Vault repository into `content/`. A second workflow in the Vault repository sends a `content-updated` dispatch to the site, so editing Markdown starts a new deployment even though the code repository did not change.

For local development, clone both repositories and place the Vault checkout at `content/` inside the site checkout.

## Start here

- [[welcome]] — frontmatter, tags, WikiLinks, and backlinks
- [[japanese]] — Japanese content and internal links
- [[markdown]] — Markdown links, tables, and code
- [[diagram]] — a Mermaid diagram
- [[attachments]] — images and a downloadable attachment

## Compare the other layouts

- [Integrated sample](https://integrated.riebeckite.dev)
- [Separate directories sample](https://directories.riebeckite.dev)

## Riebeckite documentation

- [Quick Start](https://riebeckite.dev/getting-started/quick-start)
- [Content location](https://riebeckite.dev/guides/content-repositories/basics)
