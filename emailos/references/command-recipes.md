# MailOS Command Recipes

Use these recipes when the task is specifically about fetching or rendering email content.

## Quick Command Map

- Find candidate emails: `mailos search ...`
- Read one email by ID/message-id: `mailos read ...`
- Render local message files: `mailos read --file ...`
- Convert email files across formats: `mailos convert ...`
- Preview outbound rendering: `mailos send --preview ...`

## Common Fetch Recipes

```bash
# Latest 20 emails (human-readable)
mailos search --recent -n 20

# Filtered fetch with machine-friendly output
mailos search --from "billing@vendor.com" --days 30 --json

# Read exact message from search output
mailos read --uid 12345 --json

# Read by Message-ID when UID is unknown
mailos read --message-id "<abc123@example.com>" --markdown
```

## Common Rendering Recipes

```bash
# Write one IMAP-backed message to markdown artifact
mailos read --uid 12345 --write-md /output/read/12345.md

# Render one local EML file to markdown
mailos convert ./fixtures/sample.eml --format markdown --output /output/render/sample.md

# Render folder of email files to HTML
mailos convert ./fixtures --format html --output-dir /output/render/html

# Convert local archive to pretty JSON for analysis
mailos convert ./archive --format json --pretty --output-dir /output/render/json
```

## Attachment and Export Recipes

```bash
# Save attachments for a specific message
mailos read --uid 12345 --save-attachments /output/attachments/12345

# Save markdown snapshots of search results
mailos search --subject "invoice" --save-markdown --output-dir /output/search/invoices
```

## Troubleshooting

- `no emails found`: widen filters, increase `--days`, or run `mailos search --resync`.
- `authentication failed`: check configured account and credentials with `mailos configure`.
- `conversion issue on .msg`: convert `.msg` to `.eml` first, then run `mailos read --file` or `mailos convert`.
