---
name: emailos
description: Use MailOS to fetch, inspect, render, and export email content from IMAP or local email files. Trigger this skill when a task involves searching inbox data, reading specific messages, converting .eml/.mbox/.emlx/.msg files to markdown/json/html/text, previewing template-rendered output, or saving email artifacts for analysis.
compatibility: universal
metadata:
  author: mailos
  category: email
  tools: Read, Bash, Glob
---

# Emailos

Use this skill to run reliable MailOS CLI workflows for email retrieval and rendering without inventing ad hoc parsers.

## Start Procedure

1. Resolve binary path in this order:
   - `./mailos` if present and executable in the repo.
   - `mailos` from `PATH` otherwise.
2. Verify CLI availability before workflows:
   - `<mailos-bin> --help`
3. Keep fetch operations read-only unless user explicitly requests write/send/delete actions.
4. Write generated artifacts to `/output/...` instead of home or arbitrary repo folders.
5. Test email system behavior through MailOS commands directly, not Python or other external readers.

## Workflow Selection

- Use `search` + `read` for fetching inbox/server messages.
- Use `read --file` for one local email file.
- Use `convert` for batch rendering/conversion of email files.
- Use `send --preview` and `template` for outbound HTML rendering checks.

## Fetch Workflow (IMAP or account-backed)

1. Search first to identify candidate message IDs:
   - `<mailos-bin> search --recent -n 20`
   - Add filters (`--from`, `--subject`, `--days`, `--has-attachments`) as needed.
   - Use `--json` if downstream processing is required.
2. Read one message using stable identifiers:
   - `<mailos-bin> read <uid>`
   - `<mailos-bin> read --uid <uid>`
   - `<mailos-bin> read --message-id "<id@domain>"`
3. Export renderings when needed:
   - Markdown: `<mailos-bin> read <uid> --write-md /output/read/<uid>.md`
   - JSON: `<mailos-bin> read <uid> --json`
   - Attachments: `<mailos-bin> read <uid> --save-attachments /output/attachments`

## Render Workflow (file-backed or format transforms)

1. Render one local file:
   - `<mailos-bin> read --file email.eml`
2. Convert file/folder to explicit output formats:
   - `<mailos-bin> convert email.eml --format markdown`
   - `<mailos-bin> convert email.eml --format html`
   - `<mailos-bin> convert ./emails --format json --output-dir /output/converted`
3. For outbound HTML preview:
   - `<mailos-bin> send --to test@example.com --subject "Preview" --body "Hello" --preview --template`
   - `<mailos-bin> template --open-browser` for template-only visual checks.

## Safety and Reliability Rules

- Prefer `--dry-run` when command intent may change mailbox state.
- Use `search --resync` if results are stale or missing.
- Keep recipient examples synthetic unless user provides real addresses.
- Avoid logging sensitive message bodies unless explicitly requested.

## Additional Recipes

For compact command recipes and handoff patterns, read [references/command-recipes.md](references/command-recipes.md).
