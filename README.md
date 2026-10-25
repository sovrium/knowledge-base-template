# Corvel handbook

> A private company handbook: markdown articles in sections, a managers' section, a search and an assistant — behind sign-in.

Built with [Sovrium](https://sovrium.com) — a configuration-as-code interpreter: one config
file in, a complete self-hosted web application out.

## Use this template

Click **Use this template** on GitHub to copy this app into your own repository (clean
history, yours to modify), or scaffold it locally:

```bash
curl -fsSL https://sovrium.com/install | sh
sovrium init my-knowledge-base --template knowledge-base
```

## What's inside

- **Welcome** (`/`) — the public door: the three sections, by name and purpose, and one way
  in. It names no article.
- **Sign-in** (`/sign-in`) — a work email and a password. Sign-up is closed: a new colleague
  is added by their manager.
- **The handbook** (`/kb`) — the start page: where to begin and what changed recently.
  Beside every article, the sections; above it, a search box; in it, the outline, the date it
  was last updated, and previous / next that follow the sidebar across sections. A policy
  past its review date carries a warning callout.
- **For managers** (`/kb/managers/…`) — hiring and pay reviews. Managers and the admin see it
  in their sidebar; a member's page carries none of its links, the search never offers them,
  and asking for one sends them to sign in.
- **Ask the handbook** (`/assistant`) — an assistant that answers from the five articles
  everyone may read. It needs an AI provider.
- **Not found** — an address the handbook does not hold answers 404 with three ways on: the
  start page, the policies and the assistant. It is the `not-found-with-links` block from
  the Sovrium library (`sovrium library add block/not-found-with-links`), pointed at this
  handbook.

Every article is a plain markdown file under [`content/`](./content), versioned with the
rest of the app; `/llms.txt` and the sitemap list none of them, because the handbook is
private. Everything else is declared in [`app.yaml`](./app.yaml) and the
[`config/`](./config) tree — no application code. Edit a file, restart, done.

## What to try

Create the two demo accounts first:

```bash
SOVRIUM_SEED_PASSWORD=choose-a-password sovrium seed app.yaml
sovrium start app.yaml
```

1. Sign in as **lea.bernard@corvel.example** (a member, on her first week). The handbook
   opens on its start page: the three sections and what changed recently.
2. Open **Your first week**: the outline beside it, the date it was last updated, and next —
   **Setting up your laptop**, in the IT section.
3. Open the **Expense policy**: a warning says it is past its review date.
4. Search for **expense** in the bar: the policy is among the answers.
5. Sign in as **hannah.okafor@corvel.example** (the admin who owns the handbook). A **For
   managers** section appears under the sidebar; Léa never sees it.

To add an article, write a markdown file under `content/kb/<section>/` with a `title`, a
`category`, an `order` and an `updated` date in its frontmatter.

## Run locally

```bash
curl -fsSL https://sovrium.com/install | sh
cp .env.example .env
sovrium seed app.yaml        # needs SOVRIUM_SEED_PASSWORD in .env
sovrium start app.yaml --watch
```

Zero-config: embedded SQLite, local file storage, no variable required to boot.
[`.env.example`](./.env.example) lists the optional ones this app reads.
The first administrator comes from `AUTH_ADMIN_EMAIL` and `AUTH_ADMIN_PASSWORD` on the
first start, or from `sovrium admin create <email>`.
`--watch` reloads the app each time you save a config file.

## Deploy

Ship it to Sovrium Cloud from this directory: sign in once, then deploy. The CLI finds or
creates the app it deploys to, checks the variables it needs, bundles and uploads it, and
ends only once the app answers at its address.

```bash
sovrium login
sovrium deploy
```

Any other host works the same way: run the `sovrium` binary with this config (see the
[deployment guides](https://sovrium.com/en/docs/installation)).

> **The demo accounts are for trying the app, not for running it.** The seed gives every
> account it creates, the admin included, the one password in `SOVRIUM_SEED_PASSWORD`, and
> their addresses are in `seed/`. Before anyone else can reach the app, choose a long
> password or skip the seed, and change or delete the demo admin.

## About this repository

This repository is **auto-published from the
[Sovrium monorepo](https://github.com/sovrium/sovrium)** on every release
(source: [`src/templates/knowledge-base`](https://github.com/sovrium/sovrium/tree/main/src/templates/knowledge-base)).
Issues are welcome here; please send code contributions upstream to the monorepo so the
template stays in sync with the engine. The pinned engine release lives in
`.sovrium-version`.

License: [MIT](./LICENSE). The Sovrium engine itself is licensed separately
([BSL 1.1](https://github.com/sovrium/sovrium/blob/main/LICENSE.md)).
