# brainyMcBrain

Central repository for Giel's `CLAUDE.md` brain — a modular instruction system for AI assistants across all projects, hobbies, and tasks.

## How It Works

One master `CLAUDE.md` references **skills** (universal rules), **languages** (per-language conventions), **domains** (subject-matter expertise), and **projects** (project-specific context). Claude Code loads all referenced files automatically via `@`-imports.

New knowledge gets added to the **Inbox** in `CLAUDE.md`, categorised, then promoted to the correct module.

## Structure

```
brainyMcBrain/
├── CLAUDE.md                        ← Master file (identity + router + inbox)
├── skills/                          ← Universal rules (apply to ALL projects)
│   ├── identity.md                  ← Who is Giel, Belgium, languages, tools
│   ├── git-workflow.md              ← Conventional commits, branching, PRs
│   ├── documentation.md             ← Markdown style, YAML frontmatter, links
│   ├── project-tracking.md          ← TODOs, session logs, phases, checklists
│   ├── code-quality.md              ← Lint/format/analyze rules, naming, imports
│   ├── ci-cd.md                     ← GitHub Actions, pipelines, releases, SBOM
│   ├── security.md                  ← Credentials, secrets, scanning, encryption
│   └── testing.md                   ← Test conventions, coverage, test plans
├── languages/                       ← Language-specific skills (per project)
│   ├── python.md                    ← Ruff, black, mypy, pytest, FastAPI
│   ├── dart-flutter.md              ← Flutter analyze, package imports, platforms
│   └── web-pwa.md                   ← ESLint, Prettier, PWA patterns
├── domains/                         ← Subject-matter expertise (when relevant)
│   ├── obsidian-vault.md            ← MOCs, graph colours, tags, templates
│   ├── belgian-legal.md             ← GDPR, GBA/APD, NIS2, retention periods
│   ├── iot-hardware.md              ← ESP32, AVR, MQTT, serial, production
│   └── event-planning.md            ← Logistics, venue, budget, cross-linking
├── projects/                        ← Project-specific context (slim files)
│   ├── 40Jarigen.md                 ← Immersive party — chess pieces, puzzles
│   ├── DPO-Dashboard.md             ← GDPR compliance dashboard — 15 modules
│   └── ilumenTool.md                ← IoT production tool — Flutter, Firebase
├── projects-archive/                ← Original full claude.md files (reference)
│   ├── 40Jarigen/claude.md
│   ├── DPO-Dashboard/CLAUDE.md
│   └── ilumenTool/claude.md
├── skills-external/                 ← External skill repos (git submodules)
│   └── anthropic/                   ← github.com/anthropics/skills
│       └── skills/                  ← 17 community skills (auto-updated)
├── sync.sh                          ← Sync script (pull/push/status/discover/update-external)
├── .sync-config.json                ← Project → path mappings
└── README.md
```

## Tracked Projects

| Project | Languages | Domains | Source |
|---------|-----------|---------|--------|
| 40Jarigen | web-pwa | event-planning, obsidian-vault, iot-hardware | `GielW/40Jarigen` |
| DPO-Dashboard | python | obsidian-vault, belgian-legal | `GielW/DPO-Dashboard` |
| ilumenTool | dart-flutter | iot-hardware | `RdFutech/ilumenTool` |

## How Knowledge Flows

brainyMcBrain is the **source of truth**. The workflow:

1. You're working in a project (e.g., ilumenTool)
2. You establish a new convention or fix a recurring pattern
3. **Claude flags it**: _"This looks like reusable knowledge. It should be added to brainyMcBrain."_
4. Switch to brainyMcBrain → add to the **Inbox** in `CLAUDE.md`
5. Categorise it (use the Category Quick Reference table)
6. Promote it to the correct skill/language/domain file
7. Delete from inbox

This replaces the old approach of syncing monolithic claude.md files back and forth.

## Archive Sync (backup role)

The `sync.sh` script now serves a **backup/reference** role — it snapshots the original project claude.md files into `projects-archive/`. This is NOT the source of truth; the modular files are.

```bash
./sync.sh status           # Check if project originals have drifted from archive
./sync.sh pull             # Snapshot latest originals into archive
./sync.sh push             # Restore archive copies back to project repos (rare)
./sync.sh discover         # Scan PC for new repos with claude.md files
./sync.sh add <name> <path>  # Track a new project's original file
./sync.sh update-external  # Update external skill repos (submodules)
./sync.sh auto             # Pull + update externals + commit + push (cron daily)
```

### GitHub Action — Push to Projects

A manual GitHub Action lets you push updated claude.md files from brainyMcBrain to any project repo — without needing local access.

1. Go to **Actions → Sync claude.md to projects**
2. Click **Run workflow**
3. Pick a specific project or `all`
4. The action commits the update directly to the project's default branch

**Setup:** Add a Personal Access Token as `BRAIN_SYNC_PAT` in this repo's secrets. The token needs `repo` scope (or fine-grained: Contents read/write) for the target repos.

### GitHub Action — Sync TODOs to GitHub Issues

A second Action parses TODO/progress markdown files from each project and creates/updates/closes GitHub Issues to match.

1. Go to **Actions → Sync TODOs to GitHub Issues**
2. Click **Run workflow**
3. Pick a project or `all`, and optionally enable **Dry run** to preview
4. The action creates issues with labels (`phase:P1-core`, `priority:high`, `synced-from-todo`) and closes issues whose TODO status is "Done"

**Supported formats:**
- ilumenTool-style: `| # | Phase | Status | Priority | Description |`
- DPO-Dashboard-style: `| Task | ✅ Done / ⬜ Not started | Date |`

The parser script lives at `tools/todo-to-issues.py` and can also be run locally:
```bash
python3 tools/todo-to-issues.py --dry-run          # Preview all projects
python3 tools/todo-to-issues.py ilumenTool          # Sync one project
python3 tools/todo-to-issues.py all                 # Sync all projects
```

**Setup:** Same `BRAIN_SYNC_PAT` secret — needs `repo` scope + Issues write permission.

## External Skills

The [anthropics/skills](https://github.com/anthropics/skills) repo is tracked as a git submodule in `skills-external/anthropic/`. It's updated automatically during the daily cron sync.

To update manually:
```bash
./sync.sh update-external
```

To use an external skill in a project, reference it via:
```
@skills-external/anthropic/skills/<skill-name>/SKILL.md
```

Available skills: algorithmic-art, brand-guidelines, canvas-design, claude-api, doc-coauthoring, docx, frontend-design, internal-comms, mcp-builder, pdf, pptx, skill-creator, slack-gif-creator, theme-factory, web-artifacts-builder, webapp-testing, xlsx

## Adding a New Project

1. `./sync.sh add ProjectName /path/to/ProjectName/CLAUDE.md` — tracks the original for archive
2. Create `projects/ProjectName.md` — slim project-specific context referencing skills/languages/domains
3. Update this README
4. Optionally add a new language/domain file if the project needs one not yet covered
