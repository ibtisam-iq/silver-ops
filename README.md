# silver-ops

> Personal ops control plane for [ibtisam-iq.com](https://ibtisam-iq.com) and its sub-sites.

This repository is the **single source of truth** for all content and data that drives Muhammad Ibtisam's public-facing sites. It holds no application code — only structured data that other repositories consume at build time.

---

## Why This Exists

Sites like [projects.ibtisam-iq.com](https://projects.ibtisam-iq.com) are built with React. Without this repo, adding a new project would mean editing TypeScript source code, committing to the app repo, and triggering a rebuild — every single time.

`silver-ops` eliminates that. You edit a YAML file here. Everything else is automatic.

This is the same principle as MkDocs — **content and code are completely decoupled**.

---

## How It Works

```
You edit data/projects.yaml
        ↓
GitHub Actions detects the change (path filter)
        ↓
Fires a repository_dispatch to ibtisam-iq/projects
        ↓
projects site fetches this YAML, generates TypeScript, builds, deploys
        ↓
projects.ibtisam-iq.com is live with your update (~2 min)
```

---

## Repository Structure

```
silver-ops/
├── data/
│   └── projects.yaml        ← edit this to add/update projects
├── .github/
│   └── workflows/
│       └── sync-projects.yml    ← triggers projects site rebuild
├── AI/                      ← AI tooling notes and configs
├── DevOps/                  ← DevOps reference material
└── README.md
```

---

## To Add a New Project

1. Open `data/projects.yaml`
2. Append a new entry
3. `git commit -m "feat: add project-name" && git push`

Done. The projects site rebuilds and deploys automatically.

See the full YAML schema and field reference in [`ibtisam-iq/projects → docs/architecture.md`](https://github.com/ibtisam-iq/projects/blob/main/docs/architecture.md).

---

## Secrets Required

| Secret | Purpose |
|---|---|
| `PROJECTS_PAT` | Allows `sync-projects.yml` to trigger a rebuild in `ibtisam-iq/projects` |

---

## Related Repositories

| Repository | Purpose |
|---|---|
| [`projects`](https://github.com/ibtisam-iq/projects) | React app — consumes `data/projects.yaml` |
| [`portfolio-site`](https://github.com/ibtisam-iq/portfolio-site) | Main portfolio at `ibtisam-iq.com` |
| [`nectar`](https://github.com/ibtisam-iq/nectar) | Docs site at `nectar.ibtisam-iq.com` |

---

**Muhammad Ibtisam** — [ibtisam-iq.com](https://ibtisam-iq.com) · [LinkedIn](https://linkedin.com/in/ibtisam-iq) · [GitHub](https://github.com/ibtisam-iq)
