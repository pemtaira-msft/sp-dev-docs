# Copilot Instructions for sp-dev-docs

## Repository Overview

This is a **documentation-only** repository — no application code, no build system, no tests. It contains the Markdown source for the SharePoint developer documentation published to [learn.microsoft.com/sharepoint/dev/](https://learn.microsoft.com/en-us/sharepoint/dev/) via Microsoft Open Publishing (OPS/DocFX).

## Architecture

- `docs/` — All publishable content (Markdown articles + `toc.yml` + `docfx.json`)
- `docs/toc.yml` — Master table of contents; update when adding/removing/renaming articles
- `docs/docfx.json` — DocFX build config and global/file-level metadata
- `includes/snippets/` — Reusable Markdown fragments included via `[!INCLUDE [label](path)]`
- `images/` — Shared images referenced from articles
- `.openpublishing.redirection.json` — URL redirects for moved/deleted pages; add an entry here instead of deleting a page outright
- `.openpublishing.publish.config.json` — OPS publishing pipeline config

The `live` branch is production. PRs target `main`; maintainers periodically merge `main` → `live`.

## Article Front Matter

Every Markdown article requires YAML front matter:

```yaml
---
title: Short title (< 60 chars)
description: Brief description (< 160 chars)
ms.date: MM/DD/YYYY
---
```

**When editing an existing article, always update `ms.date` to the current date in MM/DD/YYYY format.** Additional metadata fields (`ms.localizationpriority`, `author`, `ms.author`, `ms.service`, etc.) are common but vary by section; preserve them when present.

## Markdown Extensions (Microsoft Docs)

This repo uses Microsoft Learn Markdown extensions beyond standard Markdown:

- **Includes**: `[!INCLUDE [label](../../includes/snippets/file.md)]`
- **Alerts**: `> [!NOTE]`, `> [!TIP]`, `> [!WARNING]`, `> [!IMPORTANT]`, `> [!CAUTION]`
- **Embedded video**: `> [!Video https://www.youtube.com/embed/ID]`
- **Zone pivots, tabs, code snippets** — see [Microsoft Docs authoring guide](https://learn.microsoft.com/contribute/markdown-reference)

## Key Conventions

- **Images** go in `images/` at the repo root (or `docs/images/` for topic-specific). Reference with relative paths.
- **Reusable content** goes in `includes/snippets/`. Use `[!INCLUDE ...]` syntax to embed.
- **Moved/deleted pages**: Add a redirect entry to `.openpublishing.redirection.json` with `source_path`, `redirect_url`, and `redirect_document_id`.
- **New articles** must be added to `docs/toc.yml` to appear in the published navigation.
- Article file names use **lowercase-kebab-case**.
