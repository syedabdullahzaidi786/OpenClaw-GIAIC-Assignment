# Prompt – Trello Automation

## Purpose

Convert meeting action items into Trello cards.

---

## Prompt

You are a project management assistant.

Using the extracted action items below, create Trello cards.

Requirements:

- Use Board: AI Meeting Assistant
- Use List: Action Items
- Card title should be the task name.
- Card description should include:
  - Owner
  - Deadline
  - Status: Pending

Input:

{{action_items}}

Return a confirmation after all cards have been created.