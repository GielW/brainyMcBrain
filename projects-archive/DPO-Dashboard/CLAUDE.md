# CLAUDE.md — DPO-Dashboard

> **Auto-compiled from [brainyMcBrain](https://github.com/GielW/brainyMcBrain).**
> Do not edit directly — changes will be overwritten on next sync.

---

## Identity

### Identity — Who Is Giel

#### Owner

- **Name**: Giel W.
- **Location**: Belgium (Flanders)
- **Languages**: Dutch (native), English (fluent), French (working)
- **GitHub**: [GielW](https://github.com/GielW)

#### Roles

- **DPO / DPA** — Data Protection Officer & Data Protection Authority expertise
- **Cybersecurity enthusiast** — NIST, ISO 27001, CIS, NIS2
- **IoT / Embedded developer** — ESP32, AVR, MQTT, production tooling
- **Creative producer** — Immersive experiences, event design, narrative

#### Environment

- **OS**: Linux (primary), Windows (secondary/cross-platform testing)
- **Editor**: VS Code with GitHub Copilot
- **AI assistant**: Claude Code
- **Shell**: Bash
- **Version control**: Git + GitHub
- **CLI tools**: `gh` (GitHub CLI), `jq`, standard GNU tools
- **Knowledge management**: Obsidian

#### Language Preferences

- **Code**: Always English (variable names, comments, commit messages, docs)
- **User-facing text**: Dutch (NL) for Belgian audience, or as specified per project
- **Technical docs**: English
- **Logistics / guest-facing**: Dutch, matching existing file language

#### Work Style

- Prefers local-first tools — no cloud dependency unless explicitly chosen
- Follows conventional commits across all projects
- Uses Obsidian vaults for knowledge management in documentation-heavy projects
- Tracks TODOs in dedicated files, not inline code comments
- Values automation — CI/CD, release scripts, sync tools


---

## Universal Skills

### Git Workflow

#### Commit Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/) in **all** repositories:

```
<type>(<scope>): <description>

<optional body>
```

##### Types

| Type | Use for |
|------|---------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code change that neither fixes nor adds |
| `test` | Adding/updating tests |
| `chore` | Maintenance (deps, CI, config) |
| `style` | Formatting, no logic change |
| `sync` | Sync operations (claude.md, config files) |

##### Rules

- Scope is optional but encouraged — use the module/area name
- Description is imperative, lowercase, no trailing period: `add user auth`, not `Added user auth.`
- Body for breaking changes or detailed context

#### Branching

- `main` is the default branch and always deployable
- Feature branches: `feat/<short-name>` or `fix/<short-name>`
- No direct force-push to `main`

#### Common Git Commands

```bash
git add -A && git status              # Stage & review
git commit -m "feat(scope): description"  # Commit
git push origin main                  # Push
git log --oneline -10                 # Quick history
```

#### Pull Requests

- Title follows conventional commit format
- Reference related issues: `Closes #123`
- Squash merge preferred for clean history


---

### Documentation Standards

#### Markdown Conventions

- **Headers**: `# Title` → `## Section` → `### Subsection` (max 3 levels in most docs)
- **Tables** for structured data; **code blocks** with language hints (```python, ```bash, ```dart, ```text)
- **Compact table style** — no column padding:
  - Header separator: `| --- | --- | --- |` (not padded)
  - Data cells: `| value | value |` (not padded)
- **Line length**: No hard wrap for prose; let editor soft-wrap
- **Lists**: Blank line before and after list blocks (MD032)
- **Code fences**: Blank line before and after (MD031), always specify language (MD040), use `text` for plain text

#### YAML Frontmatter

Every documentation `.md` file should have YAML frontmatter:

```yaml
---
tags:
  - type/note
  - status/draft
  - domain/some-domain
aliases:
  - Short Name
created: 2026-03-09
---
```

#### Links

- **Obsidian vault notes**: Use `[[wikilinks]]` — `[[path/to/note|Display Text]]`
- **Root-level docs** (README, CONTRIBUTING, CHANGELOG): Use standard Markdown links `[text](path)` for GitHub compatibility
- **Cross-references**: Before finishing any edit, search for `[[filename]]` and `[text](path)` references to changed files and verify they still make sense

#### File & Folder Naming

- Documentation files: `kebab-case.md` or `UPPER-CASE.md` for root-level standards
- Use descriptive names: `01-PROJECT-CHARTER.md` with numeric prefixes for ordered docs

#### Changelog Format

- Follow [Keep a Changelog](https://keepachangelog.com/)
- Sections: Added, Changed, Deprecated, Removed, Fixed, Security
- Reference issue IDs and commit scopes in entries

#### Version Numbering

- Follow [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`
- Keep version in sync across: project config, CHANGELOG, CLAUDE.md, and any charter/progress docs

#### Source Attribution

- **Always reference data sources** — when using external knowledge, templates, prompts, frameworks, or data, record where it came from
- Credit format: a simple `Source:` line, footnote, or link to the original
- This applies to: research findings, copied/adapted prompts, design patterns borrowed from other projects, legal references, third-party templates
- For brainyMcBrain specifically: when a skill or convention originates from an external source (blog post, GitHub repo, community prompt), note it at the top of the file or inline
- Give credit where credit is due — don't pass off external work as your own


---

### Project Tracking

#### Planning Discipline

- **Plan before building** — Enter plan mode for any non-trivial task (3+ steps or architectural decisions)
- Write a brief spec or checklist before you start coding
- If something goes sideways mid-task, **STOP and re-plan** — don't keep pushing a broken approach
- Use planning for verification steps too, not just building

#### TODO Management

- All task tracking lives in **dedicated files** (e.g., `docs/TODO.md`, `meta/session-progress.md`)
- **Never add `// TODO` comments in source code** — they get lost
- Use consistent table format:

```markdown
| # | Phase | Status | Priority | Description |
| --- | --- | --- | --- | --- |
| 1 | P1 | Open | High | Short, clear description |
```

##### Status Values

`Open` → `In Progress` → `Done`

##### Priority Values

`High` | `Medium` | `Low`

##### Phase Convention

- `P0` — Security / critical
- `P1` — Core features / cleanup
- `P2` — Architecture / refactoring
- `P3` — Decomposition / restructuring
- `P4` — Testing / logging / CI / documentation
- `PX` — Extras (independent of core phases)

#### Session Tracking

When working in sessions (e.g., with Claude Code):
- Track progress in a session log file
- Add numbered entries under the date section
- Update "Up Next" / "Current Phase" sections to reflect state
- Mark TODOs as done in their **source files** when completed (don't just log it)

#### After Every Change — Checklist Pattern

Every project should define its "linked files" that must be updated together. The universal pattern:

##### On Every Commit

- [ ] **TODO/Progress file** — Update task status
- [ ] **CHANGELOG** — Add entry under `[Unreleased]`
- [ ] **Commit message** — Follows conventional commits
- [ ] **GitHub Issues sync** — If TODO items changed, run the TODO-to-Issues sync (see below)

##### On Version Bump

- [ ] Project config file (e.g., `pyproject.toml`, `pubspec.yaml`) — update version
- [ ] CHANGELOG — Move `[Unreleased]` to new version heading
- [ ] CLAUDE.md — Update version reference

##### On New Feature/Module

- [ ] Requirements/specs docs — add/update spec
- [ ] Progress tracking — add to module table
- [ ] README — update features and structure
- [ ] CLAUDE.md — update module reference

#### Verification Before Done

- **Never mark a task complete without proving it works** — run tests, check logs, demonstrate correctness
- Diff behaviour between `main` and your changes when relevant
- Ask yourself: "Would a senior engineer approve this?"
- For CI-visible work, verify the pipeline is green before moving on

#### Self-Improvement Loop

- After **any correction** from the user, capture the pattern in the project's `tasks/lessons.md` (or equivalent)
- Write rules for yourself that prevent the same mistake recurring
- Review lessons at the start of each session for the active project
- If the lesson is cross-project, route it to the brainyMcBrain Inbox (see Brain Update Rule)

#### Roadmap Format

Track project phases in a table:

```markdown
| Phase | Status | Focus |
| ----- | ------ | ----- |
| Phase 0 | ✅ Done | Description |
| Phase 1 | 🟡 In Progress | Description |
| Phase 2 | Not started | Description |
```

#### TODO → GitHub Issues Sync

All TODO items in project markdown files are synced to GitHub Issues via brainyMcBrain's `tools/todo-to-issues.py` script. This keeps GitHub Issues as the single visible backlog across all projects.

##### How It Works

- The script parses TODO tables from each project's tracking file (configured in `.sync-config.json` → `todo_file`)
- Creates GitHub Issues with labels: `synced-from-todo`, `phase:P1-core`, `priority:high`, etc.
- Updates existing issues when descriptions change
- Closes issues when TODO status is "Done"
- Title format: `[TODO #N] Description`

##### Supported Table Formats

**Format A** (preferred — ilumenTool-style):
```markdown
| # | Phase | Status | Priority | Description |
| 1 | P1    | Open   | High     | Short description |
```

**Format B** (DPO-Dashboard-style):
```markdown
| Task name | ✅ Done / ⬜ Not started | Date |
```

##### When to Sync

- **After adding/completing TODO items** — run the sync to keep Issues in sync
- **Locally**: `python3 tools/todo-to-issues.py <project-name>` (from brainyMcBrain)
- **Via GitHub Action**: Actions → "Sync TODOs to GitHub Issues" → Run workflow
- **Dry run first**: Add `--dry-run` flag or check the dry run box in the Action

##### Convention

- The TODO markdown file is the **source of truth** — edit there, then sync to Issues
- Never edit synced Issues directly (they'll be overwritten on next sync)
- Issues created manually (without `synced-from-todo` label) are unaffected


---

### Code Quality

#### Universal Rules

- **Zero warnings, zero errors** is the baseline — maintain it
- Run the project's linter/analyzer **before every commit**
- Fix warnings immediately; don't accumulate tech debt

#### Linting & Formatting

Every project must have a configured linter and formatter:

| Language | Linter | Formatter | Type Checker |
|----------|--------|-----------|-------------|
| Python | `ruff` | `black` | `mypy` (strict) |
| Dart | `flutter analyze` | `dart format` | Built-in |
| JavaScript/TypeScript | `eslint` | `prettier` | `tsc` |

#### Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Files (Python) | `snake_case.py` | `data_service.py` |
| Files (Dart) | `snake_case.dart` | `build_order.dart` |
| Files (JS/TS) | `camelCase.ts` or `kebab-case.ts` | per project config |
| Classes | `PascalCase` | `BuildOrder`, `DpiaEngine` |
| Functions/methods | `snake_case` (Python) / `camelCase` (Dart/JS) | |
| Variables | `snake_case` (Python) / `camelCase` (Dart/JS) | |
| Constants | `UPPER_SNAKE_CASE` | `MAX_RETRIES` |
| Private members | `_` prefix | `_internalState` |

#### Dead Code

- **Delete dead code** — don't comment it out
- If keeping for reference, move to an `old_files/` or `archive/` directory (gitignored)
- For intentionally unused code, use language-specific `// ignore:` annotations

#### Imports

- Always use sorted, grouped imports
- Prefer absolute/package imports over relative paths
- Group: stdlib → third-party → local

#### Error Handling

- **Always add error handling** in new code (try-catch, Result types, etc.)
- Never swallow errors silently — silent failures make debugging in production nearly impossible because the symptom appears far from the cause
- Log errors with context (but never log credentials — see `security.md`)

#### Execution Discipline

##### Core Principles

- **Simplicity first** — Make every change as simple as possible. Impact minimal code
- **No laziness** — Find root causes. No temporary fixes. Senior developer standards
- **Minimal impact** — Changes should only touch what's necessary. Avoid introducing bugs

##### Demand Elegance (Balanced)

- For non-trivial changes, pause and ask: "Is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes — don't over-engineer
- Challenge your own work before presenting it

##### Autonomous Problem Solving

- When given a bug report: just fix it — don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them
- Zero context switching required from the user
- Fix failing CI tests without being told how

#### Analyzer Hygiene

- When removing a field/variable, grep for **all references** (assignments, reads, comments) and clean up in the same change
- Never suppress warnings on truly dead code — delete it instead
- Only use `// ignore:` for intentionally kept unused code, with a comment explaining why


---

### CI/CD

#### GitHub Actions — Standard Patterns

##### Trigger Patterns

```yaml
### On push to main
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

### On version tag
on:
  push:
    tags: ['v*']

### Scheduled (weekly)
on:
  schedule:
    - cron: '0 6 * * 1'  # Monday 06:00 UTC
```

##### Standard Jobs

| Job | Purpose | Tools |
|-----|---------|-------|
| Lint | Code quality gate | ruff, flutter analyze, eslint |
| Test | Run test suite | pytest, flutter test, jest |
| Security scan | Dependency vulnerabilities | pip-audit, trivy, npm audit |
| Build | Compile/package | language-specific |
| SBOM | Software Bill of Materials | cyclonedx-bom, syft |
| Release | Create GitHub Release | gh, artifact upload |

##### Artifacts

- Upload scan results, reports, and builds as GitHub Actions artifacts
- Use 90-day retention for security reports
- Post summary verdicts to step summary (🟢 ALL CLEAR / 🔴 ACTION REQUIRED)

#### Release Pipelines

For projects with release scripts:
1. Version bump (config files + CHANGELOG)
2. Build (all target platforms)
3. Package (zip/tar/installer)
4. Git commit + tag
5. GitHub Release (with assets)
6. Post-release update (e.g., Firebase version doc, npm publish)

#### Dependabot

Enable Dependabot for automatic dependency update PRs:

```yaml
### .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "pip"  # or "pub", "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```


---

### WAT Framework — Workflows, Agents, Tools

> Architecture for AI-assisted execution. Separates probabilistic reasoning (agent) from deterministic execution (tools), orchestrated by human-written instructions (workflows).

---

#### Core Principle

When AI handles every step directly, accuracy compounds negatively (90% per step → 59% after five). Offload execution to deterministic scripts; focus the agent on orchestration and decision-making.

#### The Three Layers

##### Layer 1: Workflows (The Instructions)

- Markdown SOPs stored in `workflows/`
- Each workflow defines: objective, required inputs, which tools to use, expected outputs, edge case handling
- Written in plain language — the same way you'd brief a team member

##### Layer 2: Agent (The Decision-Maker)

- Read the relevant workflow, run tools in the correct sequence, handle failures gracefully, ask clarifying questions when needed
- Connect intent to execution without trying to do everything directly
- Example: need to scrape a website? Read `workflows/scrape_website.md`, determine inputs, then execute `tools/scrape_single_site.py`

##### Layer 3: Tools (The Execution)

- Python scripts in `tools/` that do the actual work
- API calls, data transformations, file operations, database queries
- Credentials and API keys live in `.env` — never stored anywhere else
- Scripts are consistent, testable, and fast

#### Subagent Strategy

- **Use subagents liberally** to keep the main context window clean and focused
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it — spin up subagents rather than cramming everything into one context
- **One task per subagent** for focused execution and cleaner results
- Keep the main agent for orchestration and decision-making; let subagents do the heavy lifting

#### Operating Rules

##### 1. Tool-First

Before building anything new, check `tools/` based on what the workflow requires. Only create new scripts when nothing exists for that task.

##### 2. Learn and Adapt on Failure

When you hit an error:
1. Read the full error message and trace
2. Fix the script and retest (if it uses paid API calls or credits, **check with the user before re-running**)
3. Document what you learned in the workflow (rate limits, timing quirks, unexpected behavior)
4. Example: rate-limited on an API → discover batch endpoint → refactor tool → verify → update workflow

##### 3. Keep Workflows Current

- Workflows evolve as you learn — update them when you find better methods, discover constraints, or encounter recurring issues
- **Never create or overwrite workflows without asking** unless explicitly told to
- Workflows are instructions to be preserved and refined, not discarded after one use

#### The Self-Improvement Loop

Every failure makes the system stronger — fix the tool, update the workflow, move on with a more robust system:

1. Identify what broke
2. Fix the tool
3. Verify the fix works
4. Update the workflow with the new approach

For the broader learning capture pattern (lessons files, cross-project routing), see the Self-Improvement Loop in `project-tracking.md`.

#### Standard Directory Layout

```
.tmp/           # Temporary/intermediate files (disposable, regenerated as needed)
tools/          # Python scripts for deterministic execution
workflows/      # Markdown SOPs defining what to do and how
.env            # API keys and environment variables (NEVER elsewhere)
```

**Core file principle:** Local files are for processing. Deliverables go to cloud services (Google Sheets, Slides, etc.) where the user can access them directly. Everything in `.tmp/` is disposable.


---

### Web Design — Frontend Craft Skill

> Universal rules for frontend website design. Apply whenever building or reviewing visual web pages.

---

#### Session Start

**Invoke this skill before writing any frontend code — every session, no exceptions.**

#### Reference Image Workflow

##### When a reference image is provided
- Match layout, spacing, typography, and color **exactly**
- Swap in placeholder content (images via `https://placehold.co/`, generic copy)
- Do **not** improve or add to the design

##### When no reference image is provided
- Design from scratch with high craft (see Anti-Generic Guardrails below)

##### Comparison Loop
1. Screenshot your output
2. Compare against the reference — be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
3. Fix mismatches, re-screenshot
4. Do **at least 2 comparison rounds**. Stop only when no visible differences remain or user says so

##### What to Check
- Spacing / padding
- Font size / weight / line-height
- Colors (exact hex)
- Alignment
- Border-radius
- Shadows
- Image sizing

#### Local Server Rule

- **Always serve on localhost** — never screenshot a `file:///` URL
- Start the dev server in the background before taking any screenshots
- If the server is already running, do not start a second instance
- Project-specific server command goes in the project file (e.g., `node serve.mjs`)

#### Screenshot Tooling

- Use Puppeteer (or project-specific screenshot script) to capture from `localhost`
- Screenshots should auto-increment (`screenshot-N.png`) and never overwrite
- After screenshotting, read the PNG with the image analysis tool to compare
- Project-specific paths (Puppeteer cache, script location) belong in the project file, not here

#### Output Defaults

- Single `index.html` file, all styles inline, unless user says otherwise
- **Tailwind CSS via CDN**: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- **Mobile-first responsive**

#### Brand Assets

- Always check the `brand_assets/` folder (or equivalent) before designing
- May contain logos, color guides, style guides, or images
- If assets exist, **use them** — do not use placeholders where real assets are available
- If a logo is present, use it. If a color palette is defined, use those exact values — do not invent brand colors

#### Anti-Generic Guardrails

| Element | Rule |
|---------|------|
| **Colors** | Never use default Tailwind palette (indigo-500, blue-600, etc.). Pick a custom brand color and derive from it |
| **Shadows** | Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity |
| **Typography** | Never use the same font for headings and body. Pair a display/serif with a clean sans. Tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body |
| **Gradients** | Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth |
| **Animations** | Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing |
| **Interactive states** | Every clickable element needs hover, focus-visible, and active states — no exceptions |
| **Images** | Add gradient overlay (`bg-gradient-to-t from-black/60`) and color treatment layer with `mix-blend-multiply` |
| **Spacing** | Use intentional, consistent spacing tokens — not random Tailwind steps |
| **Depth** | Surfaces need a layering system (base → elevated → floating) — not all at the same z-plane |

#### Hard Rules

- Do **not** add sections, features, or content not in the reference — scope creep breaks client trust and makes comparison impossible
- Do **not** "improve" a reference design — match it. The client chose that design; unsolicited changes waste review cycles
- Do **not** stop after one screenshot pass — first passes always miss spacing/color details that only show up on comparison
- Do **not** use `transition-all` — it triggers expensive layout recalculations and animates properties you didn't intend (width, height, padding)
- Do **not** use default Tailwind blue/indigo as primary color — it instantly signals "undesigned template" to anyone who's seen Tailwind defaults


---

### Security

#### Credentials & Secrets

##### Golden Rules

1. **Never hardcode credentials in source code** — not even temporarily. A single committed secret persists in git history forever, even after deletion
2. **Never log credentials** — logs get aggregated to SIEMs, shipped to third parties, and retained beyond your control. Use `[REDACTED]` or character-count only:
   ```
   print("token: [REDACTED] ({len(token)} chars)")
   ```
3. **Never commit secrets to git** — even if you delete them later, they're in history. Rotation is the only fix and it's expensive
4. **Use environment variables** or a secrets manager (Firestore, Vault, .env files) — this keeps secrets out of the codebase and makes rotation a config change, not a code change
5. **`.env` files are always gitignored** — commit `.env.example` with placeholder values so new developers know what's needed without seeing real secrets

##### If Credentials Were Exposed

- Rotate immediately (or as soon as all deployments support the new path)
- Scan git history with `trufflehog` or `gitleaks`
- Document rotation status in the project's known issues section

##### API Keys

- Distinguish between **public keys** (safe to embed, security via backend rules) and **secret keys** (never expose)
- Document which keys are which in the project's security section

#### Encryption

- Prefer encryption at rest for sensitive data (SQLCipher, encrypted Firestore, etc.)
- Use industry-standard algorithms — never roll your own crypto
- Store encryption keys separately from encrypted data

#### Scanning Tools

| Tool | Purpose | Language |
|------|---------|----------|
| `pip-audit` | Python dependency CVEs | Python |
| `safety` | Python dependency CVEs | Python |
| `trivy` | Filesystem & container scanning | Universal |
| `npm audit` | Node.js dependency CVEs | JavaScript |
| `trufflehog` | Secret scanning in git history | Universal |
| `gitleaks` | Secret scanning in git history | Universal |

#### Audit Trail

- Log security-relevant actions (auth, access, changes) with timestamps
- Never log PII or credentials in audit logs
- Retain audit logs per applicable regulation (GDPR: purpose-limited retention)


---

### Testing

#### Conventions

- **Test file naming**: `test_<module>.py` (Python), `<module>_test.dart` (Dart), `<module>.test.ts` (JS/TS)
- **Test location**: `tests/` (Python), `test/` (Dart), `__tests__/` or alongside source (JS/TS)
- **Coverage target**: 80%+ on business logic; 100% on security-critical paths

#### Test Types

| Type | Purpose | When |
|------|---------|------|
| Unit tests | Isolated function/class testing | Every module |
| Integration tests | Cross-module, database, API | Key workflows |
| E2E tests | Full user flows | Critical paths |
| Manual test plans | Hardware, UI, edge cases | When automation isn't feasible |

#### Test Plan Format

For projects with manual test plans, use this table format:

```markdown
| ID | Category | Test Case | Steps | Expected | Status |
| --- | --- | --- | --- | --- | --- |
| T01 | Auth | Login with valid creds | 1. Open app 2. Enter creds 3. Submit | Dashboard loads | PASS |
```

##### Status Values

`PASS` | `FAIL` | `SKIP` | `BLOCKED` | `NOT RUN`

#### Fixtures & Setup

- Use framework fixtures (`pytest` fixtures, `setUp`/`tearDown`) for test setup
- Prefer factories over shared mutable state
- Use `httpx.AsyncClient` (Python) or equivalent for API tests
- Mock external services; never call real APIs in unit tests

#### Running Tests

```bash
### Python
pytest                                # All tests
pytest -x                             # Stop on first failure
pytest --cov=src --cov-report=html    # With coverage
pytest -k "test_specific"             # Run specific

### Dart/Flutter
flutter test                          # All tests
flutter test --coverage               # With coverage

### JavaScript/TypeScript
npm test                              # All tests
npm run test:coverage                 # With coverage
```


---

### Council of Masters — Multi-Expert Deliberation

> When one perspective isn't enough, convene a council. Each master brings deep expertise in a different facet of the problem. They deliberate, challenge each other, and converge on a synthesis that no single expert could reach alone.

---

#### When to Convene the Council

This technique shines when the problem has **multiple valid angles** that interact:

- Architecture or design decisions with competing trade-offs
- Debugging mysteries where the root cause could live in several layers
- Strategy questions that touch business, technical, and user dimensions
- "Should we...?" questions where the answer genuinely depends on perspective
- Risk assessment across domains (security vs. usability vs. cost vs. timeline)
- Ethical or regulatory dilemmas with legitimate tension between priorities

Skip it for straightforward questions with a clear factual answer. A council deliberating "what's the syntax for a for-loop" wastes everyone's time.

#### How It Works

##### Phase 1: Assess the Question

Read the user's question and identify the **distinct domains** it touches. A good council has tension — masters who will naturally disagree because they optimise for different things.

##### Phase 2: Assemble the Council (3–5 Masters)

Select masters dynamically based on the question. Each master has:
- A **title** describing their expertise
- A **lens** — what they optimise for and what they watch out for
- A clear reason they're at the table (they must earn their seat)

The council should include at least one **contrarian** — someone likely to push back on the obvious answer. Groupthink is the enemy.

**Example roster for "Should we rewrite the monolith in microservices?":**

| Master | Lens |
|--------|------|
| Systems Architect | Scalability, separation of concerns, long-term maintainability |
| Pragmatic Engineer | Delivery speed, team capacity, migration risk |
| Security Lead | Attack surface, secret management, inter-service auth |
| Product Strategist | Business value, user impact, opportunity cost |

**Bad council selection** — 4 masters who all think the same way. If you're picking "Frontend Expert, CSS Expert, UI Expert, Design Expert" for a CSS question, you don't need a council.

##### Phase 3: Individual Analysis

Each master gives their take **independently** before seeing the others' views. This prevents anchoring bias. Each analysis should be concise (3–5 sentences) and include:

1. Their assessment of the core problem as seen through their lens
2. What they'd recommend
3. What risk or blind spot they see that others might miss

##### Phase 4: Deliberation

The masters respond to each other. This is where the value happens:

- **Challenge**: "The Architect says decouple everything, but with a 3-person team that's a maintenance nightmare" (Pragmatic Engineer)
- **Build on**: "I agree with the security concern, and I'd add that the compliance timeline makes this urgent" (Product Strategist)
- **Reframe**: "You're all debating build vs. buy, but the real question is whether this feature even belongs in our product" (contrarian)

Keep deliberation focused — one round of responses is usually enough. Two rounds if there's genuine unresolved tension.

##### Phase 5: Synthesis

Produce a unified recommendation that:

1. **States the verdict** — lead with the answer, not the process
2. **Shows the reasoning** — which arguments won and why
3. **Acknowledges dissent** — if a master was outvoted, explain their concern and why it was accepted as a known risk or mitigated
4. **Defines conditions** — "This recommendation holds if X. If Y changes, revisit"

#### Output Format

```markdown
#### Council Verdict: [one-line answer]

##### The Council
- **[Master 1 title]** — [lens in 5 words]
- **[Master 2 title]** — [lens in 5 words]
- **[Master 3 title]** — [lens in 5 words]

##### Key Arguments
[2–4 bullet points capturing the strongest arguments that shaped the verdict]

##### Dissent
[Which master(s) disagreed and why — this is valuable signal, not noise]

##### Recommendation
[Concrete, actionable next steps]

##### Conditions
[When to revisit this decision]
```

#### Principles

- **Earn your seat** — every master must bring a genuinely different perspective. Overlapping experts dilute the council's value
- **Tension is the point** — if all masters agree immediately, either the question was too easy or the council was poorly assembled
- **Brevity over theatre** — the deliberation should be tight and useful, not a roleplay exercise. Skip the "As the Security Master, I must say..." preamble
- **Dissent is signal** — a minority opinion that gets recorded is more valuable than false unanimity. The dissenter might be right and you'll want that record later
- **Dynamic assembly** — never use the same council for every question. The whole point is matching expertise to the problem

#### Example

**User question**: "We need to add multi-language support to the DPO-Dashboard. Should we use i18n library, database-driven translations, or hardcoded JSON files?"

**Council assembled**:
- **DPO/Compliance Lead** — regulatory accuracy in NL/FR/EN
- **Python Architect** — maintainability, developer experience
- **UX Specialist** — translator workflow, end-user experience
- **Pragmatic Engineer** — delivery speed, current team capacity

**Synthesis** (abbreviated):
> **Verdict**: JSON files with a thin i18n wrapper — start simple, migrate later if scale demands it.
>
> The Compliance Lead insisted translations must be reviewed by legal before deployment (ruling out community/crowdsource). The Architect preferred a proper i18n library (gettext/babel) for plural rules, but the Pragmatic Engineer noted the team is 1 person and the app has 3 target languages — a library adds ceremony without proportional value yet. The UX Specialist flagged that JSON files let non-developers contribute translations via PR. Dissent from the Architect: "You'll hit edge cases with plurals and gendered nouns in French — plan migration to babel once you exceed 500 translation keys."


---

## Language Skills

### Python — Language Skill

> Activate for projects using Python (e.g., DPO-Dashboard).

#### Style

- **Line length**: 120 characters
- **Target**: Python 3.11+
- **Type hints**: Required on all functions (`mypy` strict mode)
- **Docstrings**: Google-style on all public functions/classes

```python
def calculate_risk(score: float, weight: float = 1.0) -> RiskLevel:
    """Calculate weighted risk level.

    Args:
        score: Raw risk score (0.0–10.0).
        weight: Multiplier for score adjustment.

    Returns:
        The computed RiskLevel enum value.

    Raises:
        ValueError: If score is outside valid range.
    """
```

#### Tools

| Tool | Purpose | Command |
|------|---------|---------|
| `ruff` | Linting (replaces flake8, isort, pyflakes) | `ruff check src/ tests/` |
| `ruff --fix` | Auto-fix lint issues | `ruff check src/ tests/ --fix` |
| `black` | Code formatting | `black src/ tests/` |
| `mypy` | Static type checking | `mypy src/` |
| `pytest` | Test runner | `pytest` |
| `pytest-cov` | Coverage | `pytest --cov=src --cov-report=html` |
| `pip-audit` | Security scanning | `pip-audit` |

#### Architecture Patterns

- **Repository pattern** for data access (`src/data/repositories/`)
- **Service layer** for business logic
- **Pydantic models** for API request/response schemas
- **SQLAlchemy models** for database entities
- **Jinja2 templates** for reports
- **Dependency injection** via FastAPI's `Depends()`

#### Project Setup Pattern

```bash
python -m venv venv
source venv/bin/activate
pip install -e ".[dev]"
cp .env.example .env
```

#### Imports

```python
### 1. Standard library
import os
from pathlib import Path

### 2. Third-party
from fastapi import FastAPI, Depends
from pydantic import BaseModel

### 3. Local
from src.data.models import User
from src.services.auth import AuthService
```


---

## Domain Skills

### Obsidian Vault — Domain Skill

> Activate for projects that use an Obsidian knowledge vault.

#### Vault Structure

Every Obsidian-enabled project opens its **repo root** as the vault. Standard layout:

```
project-root/
├── .obsidian/                    # Vault config (committed)
│   ├── app.json                  # Vault settings
│   ├── appearance.json           # Theme
│   ├── graph.json                # Graph colour groups
│   ├── templates.json            # Template folder config
│   └── templates/                # Note templates
├── docs/obsidian/
│   ├── 000 - Vault Index.md      # Main entry point
│   ├── MOC - *.md                # Maps of Content
│   └── modules/                  # Module/topic notes
```

#### Maps of Content (MOCs)

MOCs are index notes that link to all notes in a category. Standard MOCs:

| MOC | Purpose |
|-----|---------|
| `MOC - Project` | Roadmap, charter, progress |
| `MOC - Architecture` | Tech stack, design patterns |
| `MOC - Modules` | Feature/requirement modules |
| `MOC - Security` | CVE tracking, scanning, security design |
| `MOC - Legal & GDPR` | Legal references (if applicable) |

#### Note Standards

Every note must have:

1. **YAML frontmatter** with `tags`, `aliases`, `created`
2. **Wikilink navigation** — link back to the relevant MOC and Vault Index
3. **Consistent tags** from the project's approved tag list

#### Tags

Use hierarchical tag prefixes:

- `#type/` — note, guide, reference, template
- `#status/` — todo, exploring, draft, done
- `#domain/` — project-specific domains
- `#module` — feature/requirement notes
- `#moc` — Maps of Content
- `#architecture` — tech stack, design
- `#security` — security-related
- `#project-definition` — charter, specs

#### Graph View Colour Groups

Configure in `.obsidian/graph.json`. Standard scheme:

| Tag | Colour | Content |
|-----|--------|---------|
| `#project-definition` | Green | Charter, requirements |
| `#module` | Purple | Feature/module notes |
| `#architecture` | Orange | Tech stack, design |
| `#security` | Red | Security notes |
| `#moc` | Cyan | Maps of Content |

#### Conventions

- **Attachments** go in `docs/attachments/`
- `workspace.json` is **gitignored** (user-specific layout)
- `plugins/` and `themes/` are **gitignored** (user-specific)
- Use **Insert Template** command for new notes (ensures consistent frontmatter)


---

### Belgian Legal & GDPR — Domain Skill

> Activate for projects involving Belgian data protection law, GDPR compliance, or cybersecurity regulation.

#### Key Belgian Regulatory Bodies

| Body | Full Name | Jurisdiction |
|------|-----------|-------------|
| **GBA** | Gegevensbeschermingsautoriteit | Belgian DPA (Dutch) |
| **APD** | Autorité de protection des données | Belgian DPA (French) |
| **CCB** | Centre for Cybersecurity Belgium | National cybersecurity authority |

#### Key Legislation

| Law | Reference | Key Provisions |
|-----|-----------|---------------|
| **GDPR** | Regulation (EU) 2016/679 | Data protection framework |
| **Belgian DPA Act** | Wet van 30 juli 2018 | Belgian GDPR implementation |
| **Camera Act** | Camerawet | Surveillance footage max 1 month retention |
| **NIS2 Directive** | Directive (EU) 2022/2555 | Critical infrastructure cybersecurity |
| **NIS2 Belgian transposition** | (pending/enacted) | Belgian NIS2 implementation |

#### Retention Periods (Belgian Law)

| Category | Period | Legal Basis |
|----------|--------|-------------|
| Surveillance footage | Max 1 month | Camera Act |
| Employment records | 5 years post-contract | Social law |
| Tax/accounting documents | 7 years | Tax code |
| Medical records | 30 years | Patient Rights Act |
| General personal data | Purpose-limited | GDPR Art. 5(1)(e) |

#### Cybersecurity Frameworks

| Framework | Scope |
|-----------|-------|
| **CCB CyberFundamentals** | Belgian framework (Basic / Important / Essential tiers) |
| **NIST CSF** | US-origin, widely adopted |
| **ISO 27001** | International information security |
| **CIS Controls** | Prioritised security actions |
| **NIS2** | EU critical infrastructure |

#### GDPR Key Articles for DPO Work

| Article | Topic |
|---------|-------|
| Art. 5 | Processing principles (lawfulness, purpose limitation, minimisation) |
| Art. 6 | Lawful bases |
| Art. 12–14 | Transparency & information obligations |
| Art. 15–22 | Data subject rights |
| Art. 25 | Data protection by design & by default |
| Art. 28 | Processor obligations (mandatory DPA clauses) |
| Art. 30 | Records of processing activities |
| Art. 33–34 | Breach notification (72h to DPA) |
| Art. 35–36 | DPIA (Data Protection Impact Assessment) |
| Art. 37–39 | DPO designation, position, tasks |

#### Conventions

- Always cite the **source law/article** when referencing Belgian legal requirements
- Reports should follow **McKinsey Pyramid Principle** (situation → complication → resolution)
- When generating agreements, always include **mandatory Art. 28 GDPR clauses**
- This is a **private/local-first** domain — never suggest cloud storage for compliance data
- The tool must **comply with GDPR itself** (data minimisation, purpose limitation)


---

## External Skills

The following external skills from [anthropics/skills](https://github.com/anthropics/skills) are available for this project. Reference them with `@<path>` when needed:

- `@skills-external/anthropic/skills/pdf/SKILL.md`
- `@skills-external/anthropic/skills/docx/SKILL.md`
- `@skills-external/anthropic/skills/pptx/SKILL.md`
- `@skills-external/anthropic/skills/xlsx/SKILL.md`
- `@skills-external/anthropic/skills/webapp-testing/SKILL.md`


---

## Project Context

### DPO-Dashboard

> **Skills**: @skills/* (all), @languages/python.md, @domains/obsidian-vault.md, @domains/belgian-legal.md
>
> **External Skills**: @skills-external/anthropic/skills/pdf/SKILL.md, @skills-external/anthropic/skills/docx/SKILL.md, @skills-external/anthropic/skills/pptx/SKILL.md, @skills-external/anthropic/skills/xlsx/SKILL.md, @skills-external/anthropic/skills/webapp-testing/SKILL.md

#### Project Overview

**DPO/DPA Cybersecurity & Compliance Dashboard** — local-first, open-source dashboard for Data Protection Officers under Belgian and EU data protection law.

- **Repository**: `GielW/DPO-Dashboard` (private)
- **License**: MIT
- **Language**: Python 3.11+
- **Status**: Phase 1 — Core Dashboard (in progress)
- **Version**: 0.5.0

#### Active Skills

This project uses:
- **Python** — Streamlit, SQLAlchemy, Alembic, Pydantic, pytest
- **Obsidian vault** — MOCs for project, architecture, legal, modules, security
- **Belgian legal** — GDPR, GBA/APD, NIS2, CyberFundamentals
- **CI/CD** — GitHub Actions security pipeline (pip-audit, trivy, SBOM)
- **PDF** _(external)_ — report generation (FR-005), form filling, document merging
- **DOCX** _(external)_ — Word document report output
- **PPTX** _(external)_ — presentation report output
- **XLSX** _(external)_ — spreadsheet data import/export
- **Webapp testing** _(external)_ — Playwright-based UI/dashboard testing

#### Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | FastAPI 0.100+ |
| Frontend (Phase 1) | Streamlit 1.30+ |
| Frontend (Phase 2) | React + TypeScript |
| Database (dev) | SQLite |
| Database (prod) | PostgreSQL 15+ |
| ORM | SQLAlchemy 2.0+ (async) |
| Migrations | Alembic 1.12+ |
| Validation | Pydantic 2.0+ |
| Reports | WeasyPrint (PDF), python-docx, python-pptx |
| Templates | Jinja2 3.1+ |
| Charts | Plotly / matplotlib |

#### Module Reference

| ID | Module | Description |
|----|--------|-------------|
| FR-001 | Dashboard | Compliance overview, KPIs, quick actions |
| FR-002 | DPIA Engine | Impact assessment lifecycle |
| FR-003 | Breach Register | Incident logging, 72h tracker, GBA notification |
| FR-004 | Vendor Assessment | Third-party risk scoring |
| FR-005 | Report Generator | McKinsey-style, PDF/DOCX/PPTX |
| FR-006 | GDPR Mapper | Article compliance checker |
| FR-007 | Cybersecurity | NIST/ISO 27001/CIS/NIS2 posture |
| FR-008 | Art. 30 Register | Processing activities management |
| FR-009 | Belgian Regulatory | GBA/APD references, Belgian law |
| FR-010 | Data Management | Storage, backup, encryption, auth |
| FR-011 | Agreements | DPA/JCA/SCC/NDA generator with clause library |
| FR-012 | Data Retention | Retention policies, schedules, deletion workflows |
| FR-013 | Advice Reports | DPO advice documents, recommendations, follow-up tracking |
| FR-014 | CVE Tracker | Vulnerability register, NVD/MITRE feeds, remediation |
| FR-015 | Dependency Scan | Project security scanning (pip-audit, trivy), SBOM, CI/CD |

#### Key Design Principles

1. **Local-first**: No cloud dependency. All data stored locally. No telemetry.
2. **Belgian regulatory focus**: GBA/APD guidelines, Belgian DPA Act, CyberFundamentals, NIS2.
3. **Multi-language**: Dutch (NL), French (FR), English (EN) — all user-facing text.
4. **Modular architecture**: Each module is independent and testable in isolation.
5. **Report quality**: McKinsey Pyramid Principle — lead with the answer, structured arguments.
6. **Security by design**: Encryption at rest (optional SQLCipher), audit trail, no external data.

#### CI/CD Pipeline

GitHub Actions workflow (`.github/workflows/security-scan.yml`): push to `main`, PRs, weekly Monday 06:00 UTC.

| Job | Tools | Output |
|-----|-------|--------|
| Dependency Scan | pip-audit, safety | JSON + readable text |
| Trivy Scan | trivy filesystem | SARIF + JSON + table |
| Security Report | Python aggregator | security-report.txt + security-summary.json |
| SBOM Generation | cyclonedx-bom | CycloneDX JSON (main push only) |

#### Linked Files Checklist

| File | What to update |
|------|---------------|
| `docs/progress/PROGRESS.md` | Task status, commit count, CI status |
| `CHANGELOG.md` | Entry under `[Unreleased]` |
| `docs/project-definition/02-FUNCTIONAL-REQUIREMENTS.md` | FR spec changes |
| `docs/obsidian/modules/FR-0XX *.md` | Module note updates |
| `docs/obsidian/MOC - Modules.md` | Module table |
| `README.md` | Features, structure, version |

#### Current Phase

**Phase 0** — Project Definition ✅
**Phase 1** — Core Dashboard 🟡 In Progress

Completed in Phase 1:
- ✅ 17 SQLAlchemy models + Alembic migration (21 tables)
- ✅ 187 seed records (Futech + web research)
- ✅ Data repositories (CRUD) for all modules
- ✅ Streamlit dashboard with 11 pages + navigation
- ✅ Dashboard overview page with KPIs
- ✅ CRUD forms (add/edit/delete) on all 8 data pages
- ✅ Settings & configuration UI

Remaining Phase 1: user authentication (local)

#### Important Notes

- **Private repository** — do not expose sensitive regulatory interpretations
- Tool must **comply with GDPR itself** (data minimisation, purpose limitation)
- Reports follow **McKinsey Pyramid Principle** (situation → complication → resolution)
- Agreements always include **mandatory Art. 28 GDPR clauses**


---

## ⚠️ Brain Feedback Loop — Self-Learning System

This file is auto-compiled from **brainyMcBrain**. When you discover reusable knowledge during this session, **do not just tell the user** — actively push it back to the brain.

### When to Trigger

| Trigger | Example |
|---------|---------|
| New convention established | "We decided to use X pattern for all services" |
| Recurring mistake fixed | "This is the third time — document the rule" |
| Tool/workflow discovered | "This CLI flag saves time" |
| Legal/regulatory reference | "New GBA guideline" |
| Cross-project pattern | "Multiple projects share this pattern" |

### Do NOT Trigger For

- One-off debugging steps or temporary workarounds
- Project-specific data (serial numbers, API keys, etc.)
- Information already covered in this file

### How to Report Back

When you detect reusable knowledge, **create a GitHub Issue on brainyMcBrain**:

```bash
gh issue create --repo GielW/brainyMcBrain \
  --title "[brain-update] <short description>" \
  --label "brain-update,triage" \
  --body "## Source Project
DPO-Dashboard

## Suggested Target File
<!-- one of: skills/*.md, languages/*.md, domains/*.md, projects/*.md, or 'new file needed' -->
<target>

## Category
<!-- Convention | Pattern fix | Tool/workflow | Legal/regulatory | Cross-project -->
<category>

## Knowledge Content
<the actual rule, convention, or pattern — write it as it should appear in the skill file>

## Context
<what happened that surfaced this knowledge>"
```

### Rules
1. **Always ask the user first**: _"I found reusable knowledge: [summary]. Shall I push this to brainyMcBrain?"_
2. Only create the issue after user confirms
3. One issue per piece of knowledge (don't bundle)
4. Write the knowledge content as you'd want it to appear in the target skill file
