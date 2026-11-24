# Iggy Research

An ecosystem for writing, thinking and publishing. The project consists of separate repositories,
kept side by side in one `iggy-research/` folder:

| Repository | Contents |
|---|---|
| `iggy-research-desktop` | Desktop app (Tauri + TypeScript): editor, AI editor, linked notes library, sync, publishing, RSS reader |
| `iggy-research-api` | Server (Django + DRF): accounts, sync, blogs, newsletter, RSS, stats |
| `iggy-research-web` | Website (React + Vite): product page, authors' blogs, author dashboard |
| `iggy-research-deploy` | VPS deployment: Docker Compose, Postgres, Caddy (HTTPS, custom domains) |
| `iggy-research-docs` | This repository: [philosophy](PHILOSOPHY.md) and [roadmap](ROADMAP.md) |

`iggy-research-web` reads the manifesto from `../iggy-research-docs/PHILOSOPHY.md`, and `iggy-research-deploy`
builds images from the neighbouring folders — so the repositories must sit next to each other:

```sh
mkdir iggy-research && cd iggy-research
for r in desktop api web deploy docs; do git clone git@github.com:iggy-research/iggy-research-$r.git; done
```

Website: [iggy-research.com](https://iggy-research.com)
