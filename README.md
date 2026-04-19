# MailOS Email Ops Skill

Reusable AI agent skill for MailOS email operations.

## Install

```bash
npx skills add email-os/skills -g -y
```

**Compatible with:** Claude Code, OpenCode, Codex, Cursor, Windsurf, Cline, and other skills.sh compatible agents.

## Usage

Once installed, agents will automatically use this skill when working with:
- Searching and reading emails
- Converting email formats (.eml, .mbox, .msg)
- Exporting email content to markdown/JSON/HTML
- Previewing email templates

## Structure

```
mailos-email-ops/
├── SKILL.md                      # Skill definition
└── references/
    └── command-recipes.md        # Command reference
```

## License

MIT
