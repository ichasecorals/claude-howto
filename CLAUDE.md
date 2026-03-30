# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is **Claude How To** — a structured educational guide for learning Claude Code features, organized as 10 progressive tutorial modules. Content is primarily Markdown with templates and example configurations. The only code is a Python-based EPUB builder in `scripts/`.

## Development Commands

All Python tooling lives in `scripts/` and uses `uv`:

```bash
# Set up environment
cd scripts
python3 -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"

# Run tests
pytest

# Lint Python code
ruff check scripts/
ruff format scripts/

# Security scan
bandit -c pyproject.toml -r scripts/

# Build EPUB
python scripts/build_epub.py

# Pre-commit checks
pre-commit run --all-files
```

Tests live in `scripts/tests/` and follow `test_*.py` / `test_*` naming.

## Architecture

### Module Structure

10 numbered lesson folders, each self-contained:

| Folder | Topic |
|--------|-------|
| `01-slash-commands/` | Custom slash command templates |
| `02-memory/` | CLAUDE.md memory file examples |
| `03-skills/` | Reusable skill definitions (auto-invoked) |
| `04-subagents/` | Specialized agent definitions |
| `05-mcp/` | Model Context Protocol configs |
| `06-hooks/` | Event-driven automation scripts |
| `07-plugins/` | Bundled multi-feature solutions |
| `08-checkpoints/` | Session snapshot/rewind examples |
| `09-advanced-features/` | Planning mode, permissions, thinking |
| `10-cli/` | CLI reference |

### Key File Patterns

- **Slash commands**: `.md` files with optional YAML frontmatter — placed in `01-slash-commands/`
- **Skills**: directories in `03-skills/<name>/` containing `SKILL.md`, optional `scripts/`, `templates/`
- **Hooks**: `.sh` scripts in `06-hooks/`
- **MCP configs**: `.json` files in `05-mcp/`
- **Memory templates**: `project-CLAUDE.md`, `personal-CLAUDE.md`, `directory-*.md` in `02-memory/`

Built-in skills are in `.claude/skills/` (lesson-quiz, self-assessment).

## Content Conventions (from STYLE_GUIDE.md)

### File Naming
- Lesson folders: `NN-kebab-case/` (two-digit prefix)
- Feature files: `kebab-case.md`
- Shell scripts: `kebab-case.sh`
- Top-level docs: `UPPER_CASE.md`
- Memory files: scope-prefixed (`project-CLAUDE.md`, `personal-CLAUDE.md`)
- Use hyphens, never underscores or spaces

### Lesson README Structure
Each `NN-*/README.md` follows this order:
1. H1 title → brief overview → optional quick-reference table
2. Architecture diagram (Mermaid)
3. Detailed H2 sections with numbered practical examples (4–6)
4. Best practices (Do's and Don'ts tables)
5. Troubleshooting → Related guides / Official docs → metadata footer

### Markdown Rules
- One H1 per document; never skip heading levels
- Sentence case headings (capitalize first word + proper nouns only)
- Callouts use blockquotes: `> **Note**:`, `> **Tip**:`, `> **Warning**:`, `> **Important**:`
- Unordered lists use `-` with 2-space indentation; max 3 nesting levels
- All code blocks must specify a language

### When Adding New Content
- **Slash command**: create `.md` in `01-slash-commands/`, update that folder's `README.md`
- **Skill**: create `03-skills/<name>/SKILL.md` (plus `scripts/`/`templates/` as needed), update `03-skills/README.md`
- **Hook**: create `.sh` in `06-hooks/` with shebang, description comment, and error handling; update `06-hooks/README.md`
- **MCP config**: create `.json` in `05-mcp/` with setup instructions; update `05-mcp/README.md`
- After adding content, also update `CATALOG.md`, `INDEX.md`, and root `README.md` as appropriate

## Git Branch Naming
- `add/feature-name`
- `fix/issue-description`
- `docs/improvement-area`
