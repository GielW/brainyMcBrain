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
├── sync.sh                          ← Sync script (pull/push/status/discover)
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
./sync.sh status     # Check if project originals have drifted from archive
./sync.sh pull       # Snapshot latest originals into archive
./sync.sh push       # Restore archive copies back to project repos (rare)
./sync.sh discover   # Scan PC for new repos with claude.md files
./sync.sh add <name> <path>  # Track a new project's original file
./sync.sh auto       # Pull + commit + push (cron runs daily at midnight)
```

## Adding a New Project

1. `./sync.sh add ProjectName /path/to/ProjectName/CLAUDE.md` — tracks the original for archive
2. Create `projects/ProjectName.md` — slim project-specific context referencing skills/languages/domains
3. Update this README
4. Optionally add a new language/domain file if the project needs one not yet covered
