# MailOS Command Recipes

Quick reference for common MailOS operations.

## Search & Read

```bash
# Latest emails
mailos search --recent -n 20

# Filtered search
mailos search --from "billing@vendor.com" --days 30 --json

# Read by ID
mailos read --uid 12345 --json
mailos read --message-id "<abc123@example.com>" --markdown
```

## File Operations

```bash
# Read email file
mailos read --file email.eml

# Convert formats
mailos convert email.eml --format markdown
mailos convert ./emails --format json --output-dir /output/converted
```

## Send & Preview

```bash
# Send email
mailos send --to user@example.com --subject "Hello" --body "Message"

# Preview with template
mailos send --to test@example.com --subject "Preview" --body "Hello" --preview --template
mailos template --open-browser
```

## Drafts

```bash
# Create draft
mailos draft --to user@example.com --subject "Subject" --body "Body"

# List and send drafts
mailos draft --list
mailos send --drafts
```
