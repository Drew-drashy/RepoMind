```markdown
# RepoMind 🧠  
**Context-aware Repository Manager powered by GitHub MCP**

RepoMind is an intelligent repo manager that combines **GitHub’s official MCP server** with a **codebase-understanding MCP** to deliver end-to-end, context-driven development workflows.  

It acts like a semantic assistant for your repositories—bridging **deep codebase understanding** with **safe GitHub actions**. From targeted refactors to CI-guided fixes, RepoMind helps teams accelerate development while keeping humans in the loop.  

---

## 🚀 Features
- 🧠 **Understands your codebase**  
  Indexes the repository, builds semantic embeddings, and provides symbol search, cross-references, and dependency maps.

- 🔄 **Automates changes safely**  
  Generates diffs, creates branches, commits updates, and opens pull requests with structured explanations.

- ✅ **CI-aware feedback loop**  
  Monitors GitHub Actions, fetches failing logs, and proposes fixes iteratively.

- 🔒 **Guardrails first**  
  PR-only mode, least-privilege GitHub PAT usage, and full audit logs for every agent action.

- 📊 **Dashboard**  
  Web UI (Next.js + Tailwind) to monitor repo indexing, agent runs, PR proposals, and approvals.

---

## 🏗️ System Architecture

```

\[User Prompt / Ticket]
|
v
RepoMind Agent (Node.js)
|
+------------+------------+
\|                         |
\[Codebase MCP]          \[GitHub MCP]
(symbols, refs,         (branches, commits,
search, embeddings)     PRs, issues)
\|                         |
v                         v
\[Qdrant Vector DB]       \[GitHub Actions CI]
\[Postgres Metadata]      (status checks)
\[Redis Queues]

````

---

## 📦 Tech Stack

- **Frontend:** Next.js, Tailwind, shadcn/ui (dashboard & approvals)  
- **Backend:** Node.js (NestJS/Fastify), Redis (queues), PostgreSQL (metadata), BullMQ  
- **Vector Search:** Qdrant (semantic code chunks)  
- **MCP Servers:**  
  - GitHub MCP (official, for repo + PR actions)  
  - Codebase MCP (semantic repo indexer)  
- **CI/CD:** GitHub Actions integration  

---

## ⚙️ Getting Started

### 1. Prerequisites
- Docker + Docker Compose  
- GitHub Personal Access Token (PAT) with `repo` and `read:packages` scopes  

### 2. Clone the repo
```bash
git clone https://github.com/your-org/repomind.git
cd repomind
````

### 3. Set environment variables

Create a `.env` file:

```env
GITHUB_TOKEN=ghp_yourtokenhere
POSTGRES_PASSWORD=postgres
```

### 4. Start the stack

```bash
docker compose -f infra/docker-compose.yml up --build
```

This will launch:

* **RepoMind Orchestrator API** ([http://localhost:4000](http://localhost:4000))
* **Web Dashboard** ([http://localhost:3000](http://localhost:3000))
* **GitHub MCP Server** ([http://localhost:3333](http://localhost:3333))
* **Codebase MCP Server** ([http://localhost:3334](http://localhost:3334))
* **Postgres, Redis, Qdrant**

### 5. Open the dashboard

Visit: [http://localhost:3000](http://localhost:3000)

---

## 🧩 Usage Examples

* **Ask RepoMind to refactor a class:**

  * Agent finds all refs via Codebase MCP
  * Generates a minimal patch
  * Opens a branch + PR via GitHub MCP

* **Handle failing CI:**

  * Agent fetches CI logs from PR
  * Localizes failing test
  * Suggests fix + updates branch

---

## 🔒 Security

* Default **PR-only mode** (no direct pushes to main).
* **Least-privilege PATs** recommended (repo-level only).
* Full audit logs of all MCP tool calls.

---

## 📅 Roadmap

* [ ] CLI interface for developers
* [ ] VS Code integration via MCP config
* [ ] Pluggable “playbooks” for refactor/test-gen/docs
* [ ] Multi-repo support

---

## 🤝 Contributing

Contributions are welcome! Please open issues or PRs.
For larger proposals, open a discussion first.

---

## 📜 License

MIT License © 2025 RepoMind Authors

```
