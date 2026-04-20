# QA Agentic Workflows — User Story Evaluation

A proof-of-concept that uses [GitHub Agentic Workflows (gh-aw)](https://githubnext.com/projects/agentics) to automatically evaluate Azure DevOps user stories and bugs against a deterministic quality framework, then publish scored reports as GitHub issues.

---

## How It Works

```
GitHub Actions (workflow_dispatch or issue comment)
        │
        ▼
 GitHub Copilot CLI  ──── sandboxed Ubuntu container (AWF firewall)
        │
        ▼
  User Story Evaluation Agent
        │
        ├── rpdevops MCP  ──────► tfs.realpage.com  (fetch work item)
        ├── safeoutputs MCP ────► GitHub API          (create issue)
        └── gh-aw MCP      ────► Actions integration
```

1. **Trigger** — Run the workflow from the Actions UI supplying a TFS work item ID, or post `/evaluate <id>` in a GitHub issue comment.
2. **Fetch** — The agent calls the `rpdevops` MCP server to pull the work item from Azure DevOps (Consumer Solutions or AOS projects).
3. **Evaluate** — The agent scores the work item across 7 quality categories using a deterministic checklist (9 check-points per category).
4. **Publish** — A scored report is created as a GitHub issue via the `safeoutputs` MCP server.

---

## Evaluation Framework

Work items are scored on a **1–10 scale** across 7 categories:

| # | Category | Default Weight |
|---|----------|---------------|
| 1 | Core Structure | 30% |
| 2 | Functional Requirements | 15% |
| 3 | Validation Specifications | 15% |
| 4 | Non-Functional Requirements | 10% |
| 5 | UI/UX Requirements | 10% |
| 6 | API Requirements | 10% |
| 7 | Database Requirements | 10% |

Categories that are not applicable to a work item are excluded and their weights are redistributed across the remaining categories (16 weight matrices are pre-defined for every combination).

**Quality ratings:**

| Score | Rating |
|-------|--------|
| 1.0 – 3.0 | Poor — missing critical information |
| 3.1 – 6.0 | Adequate — basic details present with gaps |
| 6.1 – 8.0 | Good — mostly complete with minor gaps |
| 8.1 – 10.0 | Excellent — complete and ready to implement |

---

## Repository Structure

```
.github/
  agents/
    agentic-workflows.agent.md   # Dispatcher agent — routes to specialized prompts
  aw/
    actions-lock.json            # gh-aw compiled workflow lock file
  workflows/
    user-story-evaluation.md     # Workflow source (markdown + YAML frontmatter)
    user-story-evaluation.lock.yml  # Compiled GitHub Actions workflow (do not edit by hand)
    copilot-setup-steps.yml      # Container bootstrap for Copilot CLI

activation/                      # Runtime metadata from the last Copilot CLI invocation
agent/                           # Agent execution logs, MCP call logs, output artifacts
detection/                       # Anomaly/issue detection logs
firewall-audit-logs/             # Agent Workflow Firewall (AWF) network audit logs
safe-outputs-items/              # Ledger of safe GitHub API writes

us-eval.md                       # Manual trigger documentation
US-*.md                          # Example evaluation report output files
```

---

## Prerequisites

| Requirement | Details |
|-------------|---------|
| `gh` CLI | GitHub CLI with Copilot extension |
| `gh aw` extension | `gh extension install githubnext/gh-aw` |
| `AZDO_PAT` secret | Azure DevOps personal access token (repo secret) |
| `COPILOT_GITHUB_TOKEN` secret | GitHub token for Copilot CLI auth (repo secret) |
| RealPage Artifactory access | Required to install the `rpdevops` MCP npm package |

---

## Running the Workflow

### Via GitHub Actions UI

1. Go to **Actions → User Story Evaluation**.
2. Click **Run workflow**.
3. Enter the TFS work item ID (e.g., `1727233`).
4. Optionally specify the Azure DevOps project (defaults to `Consumer Solutions`).
5. A GitHub issue with the full evaluation report will be created when the run completes.

### Via Issue Comment

Post a comment on any GitHub issue in this repo:

```
/evaluate 1727233
```

The agent will evaluate work item `1727233` and reply with a link to the generated report issue.

---

## Workflow Development

The **source of truth** for the workflow is [.github/workflows/user-story-evaluation.md](.github/workflows/user-story-evaluation.md). The `.lock.yml` is generated — do not edit it directly.

To recompile after changing the source workflow:

```bash
gh aw compile .github/workflows/user-story-evaluation.md
```

To run locally for testing:

```bash
gh aw run .github/workflows/user-story-evaluation.md --input work_item_id=1727233
```

---

## Security

- All agent network access is restricted by the **Agent Workflow Firewall (AWF)** — only `tfs.realpage.com` and `artifacts.realpage.com` are reachable from within the container.
- All GitHub API writes (issue creation, comments) must go through the `safeoutputs` MCP server; direct `gh` CLI calls are blocked.
- Secrets (`AZDO_PAT`, `COPILOT_GITHUB_TOKEN`) are injected as environment variables at runtime and are never written to logs or outputs.

---

## Tech Stack

- [GitHub Agentic Workflows (gh-aw)](https://githubnext.com/projects/agentics) — workflow definition and compilation
- [GitHub Copilot CLI](https://docs.github.com/en/copilot) — AI execution engine
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io) — tool integration layer
- **rpdevops MCP server** — Azure DevOps / TFS data access
- **safeoutputs MCP server** — sandboxed GitHub API writes
- GitHub Actions — CI/CD orchestration runtime
