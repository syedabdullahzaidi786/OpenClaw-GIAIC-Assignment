# OpenClaw Setup Guide

This guide explains how to install and configure the **OpenClaw AI Meeting Assistant** on a Windows 11 machine using **OpenRouter**, **Discord**, and **Trello**.

---

# Table of Contents

1. System Requirements
2. Install OpenClaw
3. Verify Installation
4. Configure OpenRouter
5. Configure Discord
6. Configure Trello
7. Install jq
8. Create Your First Agent
9. Test the AI
10. Meeting Summary Workflow
11. Trello Automation
12. Cron Jobs
13. Troubleshooting

---

# System Requirements

- Windows 11
- PowerShell 7 or later
- Node.js (Latest LTS Recommended)
- Internet Connection
- Discord Account
- Trello Account
- OpenRouter Account

---

# Software Used

| Software | Purpose |
|----------|----------|
| OpenClaw | AI Agent Platform |
| OpenRouter | Large Language Models |
| Discord | AI Communication |
| Trello | Task Management |
| jq | JSON Processing |
| PowerShell | Local Configuration |

---

# Step 1 — Install OpenClaw

Install OpenClaw using npm.

```powershell
npm install -g openclaw
```

---

Verify the installation.

```powershell
openclaw --version
```

Expected output:

```text
OpenClaw 2026.7.1-2
```

---

# Step 2 — Initial Configuration

Run the onboarding wizard.

```powershell
openclaw onboard
```

During setup:

- Select Local Mode
- Configure Gateway
- Create the default agent
- Complete the installation wizard

---

# Step 3 — Verify Installation

Run the diagnostic tool.

```powershell
openclaw doctor
```

Check that:

- OpenClaw is installed
- Gateway is running
- Agent is available
- Skills are loaded

---

# Step 4 — Configure OpenRouter

Create an account on OpenRouter.

https://openrouter.ai

Generate an API Key.

Configure OpenClaw to use OpenRouter as the default model provider.

Example configuration:

```json
"model": {
    "primary": "openrouter/auto"
}
```

Restart OpenClaw after saving the configuration.

---

# Step 5 — Configure Discord

Create a Discord Bot.

Enable:

- Message Content Intent
- Server Members Intent

Invite the bot to your server.

Copy the Bot Token.

Update your OpenClaw configuration.

Example:

```json
"channels": {
    "discord": {
        "enabled": true
    }
}
```

Restart OpenClaw.

---

# Step 6 — Configure Trello

Create a Trello board.

Example:

```
AI Meeting Assistant
```

Create the following lists:

- To Do
- Doing
- Done
- Action Items

---

Generate your API Key.

https://trello.com/app-key

Generate a Token.

Set environment variables.

PowerShell:

```powershell
$env:TRELLO_API_KEY="YOUR_API_KEY"
$env:TRELLO_TOKEN="YOUR_TOKEN"
```

Verify:

```powershell
echo $env:TRELLO_API_KEY
echo $env:TRELLO_TOKEN
```

---

# Step 7 — Install jq

Install jq using Winget.

```powershell
winget install jqlang.jq
```

Restart PowerShell.

Verify:

```powershell
jq --version
```

Example:

```text
jq-1.8.2
```

---

# Step 8 — Verify Trello Skill

Run:

```powershell
openclaw skills info trello --agent main
```

Expected:

```text
Ready
```

Requirements should display:

- jq
- curl
- TRELLO_API_KEY
- TRELLO_TOKEN

---

# Step 9 — Test Trello Connection

List your boards.

```powershell
curl.exe "https://api.trello.com/1/members/me/boards?key=$env:TRELLO_API_KEY&token=$env:TRELLO_TOKEN"
```

List board lists.

```powershell
curl.exe "https://api.trello.com/1/boards/BOARD_ID/lists?key=$env:TRELLO_API_KEY&token=$env:TRELLO_TOKEN"
```

If JSON is returned, the integration is working correctly.

---

# Step 10 — Test Discord

Open Discord.

Send a message to the bot.

Example:

```
Hello
```

Expected:

```
Hi! How can I help you today?
```

---

# Step 11 — Meeting Summary Workflow

Example transcript:

```text
Ali will complete the frontend by Friday.

Ahmed will complete the backend by Monday.

Sara will finish improvements before deployment.
```

Ask OpenClaw:

```
Summarize this meeting and extract action items.
```

Expected output:

- Meeting Summary
- Action Items
- Team Members
- Deadlines

---

# Step 12 — Trello Automation

Example request:

```
Create Trello cards for all action items.
```

Expected cards:

| Card | Due |
|------|-----|
| Complete Frontend | Friday |
| Complete Backend | Monday |
| UI Improvements | Before Deployment |

---

# Step 13 — Cron Jobs

Example cron job:

Morning Report

Runs every morning.

Possible tasks:

- Daily summary
- Pending Trello cards
- Meeting reminders
- Motivational message

---

# Troubleshooting

## Trello Skill Not Ready

Check:

```powershell
openclaw skills info trello --agent main
```

Verify:

- jq installed
- curl available
- Environment variables configured

---

## Discord Bot Not Responding

Verify:

- Bot Token
- Bot Permissions
- Gateway Running

Restart:

```powershell
openclaw gateway restart
```

---

## API Rate Limit

Possible causes:

- Free model limits
- Too many requests
- Long prompts

Solutions:

- Wait a few minutes
- Switch to another model
- Upgrade your OpenRouter plan if needed

---

## jq Not Found

Restart PowerShell.

Then run:

```powershell
jq --version
```

---

## OpenClaw Doctor

Useful command:

```powershell
openclaw doctor
```

This checks:

- Gateway
- Skills
- Plugins
- Models
- Security
- Configuration

---

# Project Workflow

```text
Google Meet
      │
      ▼
Meeting Transcript
      │
      ▼
OpenClaw AI
      │
 ┌────┴────┐
 ▼         ▼
Summary  Action Items
 │         │
 ▼         ▼
Discord  Trello
      │
      ▼
Daily Reports
```

---

# Next Steps

After completing this setup, continue with:

- Milestone 1
- Milestone 2
- Milestone 3
- Milestone 4

Documentation for each milestone is available in the `docs` directory.

---

# Author

**Syed Abdullah Zaidi**

GitHub:
https://github.com/syedabdullahzaidi786/OpenClaw-GIAIC-Assignment