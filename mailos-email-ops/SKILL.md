---
name: mailos-email-ops
description: Use MailOS CLI for email management. Trigger this skill when working with email retrieval, reading, searching, converting email files, or managing emails via command line.
compatibility: universal
metadata:
  author: mailos
  category: email
  tools: Read, Bash, Glob
---

# MailOS CLI - Email Operations

Use the MailOS CLI for email management tasks.

MailOS is a powerful CLI for email operations with IMAP support, file conversion, and AI integration.

## Command Format

Always use the following format:

```bash
mailos [command]
```

**Do NOT use:**
- `./mailos [command]`
- Any path variations or prefixes

## Explanation

The `mailos` command should be invoked directly as a system command, not as a relative or absolute path. This format assumes `mailos` is properly installed and available in the system PATH.

## Common Commands

```bash
# Search and read emails
mailos search --recent -n 20
mailos read 12345
mailos read --uid 12345 --json

# Read from email files
mailos read --file email.eml
mailos read --file message.mbox --write-md output.md

# Convert email formats
mailos convert email.eml --format markdown
mailos convert ./emails --format json --output-dir /output/converted

# Send emails
mailos send --to user@example.com --subject "Hello" --body "Message"
mailos send --preview --template

# Draft management
mailos draft
mailos draft --to user@example.com --subject "Subject" --body "Body"

# Search with filters
mailos search --from "billing@vendor.com" --days 30
mailos search --subject "invoice" --has-attachments --json
```

## Key Workflows

### Fetch Emails (IMAP)
1. Search: `mailos search --recent -n 20`
2. Read by ID: `mailos read <uid>`
3. Export: `mailos read <uid> --write-md /output/read/<uid>.md`

### Convert Email Files
- Single file: `mailos read --file email.eml`
- Batch convert: `mailos convert ./emails --format json --output-dir /output/converted`

### Send/Preview
- Preview: `mailos send --to test@example.com --subject "Preview" --body "Hello" --preview --template`
- Template check: `mailos template --open-browser`

## Safety Guidelines

- Prefer `--dry-run` for operations that may change mailbox state
- Use `--resync` if search results are stale
- Keep recipient examples synthetic unless real addresses provided
- Avoid logging sensitive message bodies

## Additional Reference

For detailed command recipes, see [references/command-recipes.md](references/command-recipes.md).
