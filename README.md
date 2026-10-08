# Tymio agent skills

Official [Agent Skills](https://docs.cursor.com/context/skills) for [Tymio](https://tymio.app) — Cursor, Claude Code, and compatible clients.

**Preferred install path:** the Tymio hub (`https://tymio.app/skills/…`) or `tymio-mcp skill install`. This repo is the public mirror for browsing, forking, and manual copy.

Website: [tymio.app](https://tymio.app) · Context for agents: [llms.txt](https://tymio.app/llms.txt)

## Skills

| Id | Role | Version |
| --- | --- | --- |
| [`tymio-workspace`](./tymio-workspace/) | Connect, OAuth, multi-workspace, hub ontology, closeout | 1.1.1 |
| [`tymio-pm-agent`](./tymio-pm-agent/) | Product Manager — portfolio / roadmap | 1.1.0 |
| [`tymio-po-agent`](./tymio-po-agent/) | Product Owner — initiative / features / requirements | 1.1.0 |
| [`tymio-dev-agent`](./tymio-dev-agent/) | Developer — implement against hub scope + closeout | 1.1.0 |
| [`tymio-devops-agent`](./tymio-devops-agent/) | DevOps — CI/CD, Railway, hub environment | 1.1.0 |

Install **`tymio-workspace`** first; role skills assume it.

## Install (recommended)

### CLI

```bash
npm i -g @tymio/mcp-server   # or: npx @tymio/mcp-server
tymio-mcp skill list
tymio-mcp skill install tymio-workspace --client cursor --scope project
tymio-mcp skill install tymio-dev-agent --client cursor --scope project
```

Clients: `cursor` | `claude` | `codex` | `opencode`  
Scopes: `project` (default) | `user`

### MCP (already connected to Tymio)

1. `tymio_list_skills`
2. User consent, then `tymio_install_skill` with `id`, `client`, `scope`

### Hub HTTP

| Endpoint | Purpose |
| --- | --- |
| `GET https://tymio.app/skills/index.json` | Catalog (no bodies) |
| `GET https://tymio.app/skills/<id>.md` | Raw skill Markdown |
| `GET https://tymio.app/skills/<id>/install-manifest?client=cursor&scope=project` | Path + body for install |

## Install (from this repo)

Cursor (project):

```bash
git clone https://github.com/tymioapp/agent-skills.git /tmp/tymio-skills
mkdir -p .cursor/skills
cp -R /tmp/tymio-skills/tymio-workspace /tmp/tymio-skills/tymio-dev-agent .cursor/skills/
# add tymio-po-agent / tymio-pm-agent / tymio-devops-agent as needed
```

Claude Code (project): same folders under `.claude/skills/<id>/SKILL.md`.

Keep relative `references/` paths intact when copying `tymio-workspace`.

## Connect MCP

Skills need a live Tymio MCP connection. Short path:

1. Add server URL `https://tymio.app/mcp` (discovery) or `https://tymio.app/t/<workspace-slug>/mcp` (full tools).
2. Complete OAuth (`mcp_auth` in Cursor, or `tymio-mcp login`).
3. Pin a workspace URL before backlog CRUD.

Details live in [`tymio-workspace/SKILL.md`](./tymio-workspace/SKILL.md) and [tymio.app/llms.txt](https://tymio.app/llms.txt).

## Source of truth

- **Canonical bodies** for the live hub catalog are maintained in the Tymio product monorepo and published via `GET /skills/*`.
- **This repository** is the public, MIT-licensed mirror for discovery and manual install.
- PRs welcome for typos and clarity; product behavior changes should land in hub-published skills first.

## License

[MIT](./LICENSE) © 2026 tymioapp
