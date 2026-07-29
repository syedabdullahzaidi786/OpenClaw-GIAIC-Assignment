# Troubleshooting Guide

This document provides solutions to common issues encountered while setting up and using the **OpenClaw AI Meeting Assistant**.

---

# Table of Contents

1. OpenClaw Installation Issues
2. Gateway Issues
3. OpenRouter Issues
4. Discord Issues
5. Trello Issues
6. jq Issues
7. Cron Job Issues
8. Skills Issues
9. OpenClaw Doctor
10. Useful Commands

---

# OpenClaw Installation Issues

## Problem

```text
'openclaw' is not recognized as an internal or external command.
```

### Cause

- OpenClaw is not installed.
- npm global directory is not added to the system PATH.

### Solution

Verify Node.js installation.

```powershell
node --version
```

Verify npm installation.

```powershell
npm --version
```

Install OpenClaw.

```powershell
npm install -g openclaw
```

Restart PowerShell and verify.

```powershell
openclaw --version
```

---

# Gateway Issues

## Problem

Dashboard is not opening.

### Solution

Start the gateway.

```powershell
openclaw gateway start
```

Restart the gateway.

```powershell
openclaw gateway restart
```

Stop the gateway.

```powershell
openclaw gateway stop
```

---

## Problem

Unable to connect to Gateway.

### Solution

Run:

```powershell
openclaw doctor
```

Ensure:

- Gateway is running
- Port is available
- Authentication token is valid

---

# OpenRouter Issues

## Problem

```text
API rate limit reached
```

### Cause

The selected model has exceeded its usage limit.

### Solution

- Wait a few minutes before retrying.
- Use another available model.
- Upgrade your OpenRouter plan if higher usage is required.

---

## Problem

```text
LLM request timed out
```

### Cause

- Slow model response
- Network issues
- Temporary provider delay

### Solution

- Retry the request.
- Use a faster model.
- Shorten very large prompts.

---

## Problem

```text
Model rejected by allowlist
```

Example:

```text
google/gemini-2.5-flash is not in [openrouter/auto]
```

### Solution

Use an allowed model or update the OpenClaw configuration to include the desired model.

---

# Discord Issues

## Problem

Bot is offline.

### Solution

Verify:

- Bot Token
- Internet connection
- Gateway status

Restart OpenClaw.

```powershell
openclaw gateway restart
```

---

## Problem

Bot does not reply.

### Verify

- Bot has been invited to the server.
- Message Content Intent is enabled.
- Required permissions have been granted.
- OpenClaw gateway is running.

---

## Problem

```text
Discord recipient is required.
```

### Cause

A cron job or automation attempted to send a message without specifying a destination.

### Solution

Specify a valid Discord recipient.

Examples:

```text
channel:123456789012345678
```

or

```text
user:123456789012345678
```

---

# Trello Issues

## Problem

Trello skill is blocked.

### Solution

Install jq.

```powershell
winget install jqlang.jq
```

Restart PowerShell.

Verify installation.

```powershell
jq --version
```

---

## Problem

```text
Missing TRELLO_API_KEY
```

### Solution

Set environment variables.

```powershell
$env:TRELLO_API_KEY="YOUR_API_KEY"
$env:TRELLO_TOKEN="YOUR_TOKEN"
```

Verify.

```powershell
echo $env:TRELLO_API_KEY
echo $env:TRELLO_TOKEN
```

---

## Problem

Cards are not appearing on the board.

### Verify

- Correct Board ID
- Correct List ID
- Valid API Key
- Valid Token

List boards.

```powershell
curl.exe "https://api.trello.com/1/members/me/boards?key=$env:TRELLO_API_KEY&token=$env:TRELLO_TOKEN"
```

List lists.

```powershell
curl.exe "https://api.trello.com/1/boards/BOARD_ID/lists?key=$env:TRELLO_API_KEY&token=$env:TRELLO_TOKEN"
```

---

## Problem

Unable to assign members automatically.

### Cause

The member ID is required.

### Solution

Retrieve the member ID through the Trello API before assigning users to cards.

---

# jq Issues

## Problem

```text
jq is not recognized
```

### Solution

Restart PowerShell.

Verify installation.

```powershell
jq --version
```

If needed, reinstall.

```powershell
winget install jqlang.jq
```

---

# Cron Job Issues

## Problem

Morning Report fails.

### Possible Causes

- API rate limit
- Timeout
- Missing Discord recipient
- Invalid model configuration

---

## Problem

```text
Cron job failed: API rate limit reached
```

### Solution

- Wait before retrying.
- Switch to another model.
- Reduce execution frequency.

---

## Problem

```text
LLM request timed out
```

### Solution

Retry later or use a faster model.

---

## Problem

Cron executes but no Discord message appears.

### Verify

- Discord recipient
- Bot permissions
- Gateway status

---

# Skills Issues

## Problem

Skill shows **Blocked**.

### Solution

Run:

```powershell
openclaw skills info trello --agent main
```

Review missing requirements.

Install missing tools or configure required environment variables.

---

## Problem

Skill shows **Eligible** but does not work.

### Solution

Reload the configuration.

```powershell
openclaw doctor
```

Then restart the gateway.

```powershell
openclaw gateway restart
```

---

# OpenClaw Doctor

Run:

```powershell
openclaw doctor
```

The diagnostic tool checks:

- Gateway
- Plugins
- Skills
- Models
- Security
- Environment
- Configuration

Resolve any warnings before continuing.

---

# Useful Commands

## Version

```powershell
openclaw --version
```

---

## Doctor

```powershell
openclaw doctor
```

---

## Restart Gateway

```powershell
openclaw gateway restart
```

---

## Stop Gateway

```powershell
openclaw gateway stop
```

---

## Start Gateway

```powershell
openclaw gateway start
```

---

## View Skill Information

```powershell
openclaw skills info trello --agent main
```

---

## List Trello Boards

```powershell
curl.exe "https://api.trello.com/1/members/me/boards?key=$env:TRELLO_API_KEY&token=$env:TRELLO_TOKEN"
```

---

## List Trello Lists

```powershell
curl.exe "https://api.trello.com/1/boards/BOARD_ID/lists?key=$env:TRELLO_API_KEY&token=$env:TRELLO_TOKEN"
```

---

## Verify jq

```powershell
jq --version
```

---

# Best Practices

- Keep OpenClaw updated.
- Store secrets in environment variables.
- Never commit API keys or tokens to GitHub.
- Test integrations individually before combining them.
- Run `openclaw doctor` after configuration changes.
- Restart the gateway after updating environment variables or configuration.

---

# Additional Resources

- OpenClaw Documentation
- OpenRouter Documentation
- Discord Developer Portal
- Trello REST API Documentation

---

# Author

**Syed Abdullah Zaidi**

GitHub:
https://github.com/syedabdullahzaidi786/OpenClaw-GIAIC-Assignment