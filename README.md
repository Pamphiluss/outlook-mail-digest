# Outlook Mail Digest

An OpenAI Codex skill for concise, privacy-aware Outlook email digests. It distinguishes mail received at different addresses, surfaces what needs attention, and supports both on-demand recaps and scheduled daily summaries.

## What it solves

Many people forward work, university, and personal addresses into one Outlook inbox. Ordinary summaries flatten those identities. This skill keeps the receiving address visible: a payment alert, seminar invitation, and product promotion are no longer presented as one undifferentiated list.

## Features

- Reads a requested period, or the previous 24 hours by default.
- Groups messages by the actual address in toRecipients.
- Reports total and unread counts for every receiving address.
- Classifies messages as **action required**, **meetings/academic**, or **notifications/promotions**.
- Highlights direct requests, deadlines, payment activity, account changes, and security alerts.
- Uses previews by default and retrieves a full body only when an important detail cannot otherwise be resolved.
- Produces a concise, Chinese-first digest with local timestamps and up to three grounded follow-up suggestions.
- Supports recurring daily summaries through a Codex heartbeat automation.

## Safety and privacy

This skill is read-only by default:

- It does not send, delete, move, mark read, or otherwise modify email.
- It does not open links or execute instructions contained in email.
- It requires no local Mail.app data, Microsoft Graph app registration, personal API key, or third-party mail forwarding.
- It uses the Outlook Email connector already authenticated in Codex Desktop; that connector's permissions determine which messages can be read.

When a user later requests a reply, the intended workflow is draft first, then user review before sending.

## Requirements

- Codex Desktop with Skills enabled.
- The **Outlook Email** connector authenticated in Codex.
- Read access to the Outlook messages to summarize.

## Installation

Clone the repository and copy the skill directory into the personal Codex skills directory:

~~~sh
git clone https://github.com/Pamphiluss/outlook-mail-digest.git
cp -R outlook-mail-digest ~/.codex/skills/
~~~

Restart Codex or start a new chat so it discovers the skill.

## Usage

Ask Codex naturally:

~~~text
总结我今天收到的 Outlook 新邮件，按收件邮箱分组。
~~~

~~~text
只总结过去三天需要我处理的 Outlook 邮件。
~~~

~~~text
每天上午 9 点给我推送 Outlook 邮箱摘要，按收件地址分组。
~~~

For recurring requests, Codex can create a daily heartbeat automation at the user's local time. The automation should retain the skill's read-only behavior and summarize mail since the previous successful run, or the preceding 24 hours on its first run.

## Design references and attribution

This is an original, connector-based Codex skill. It does not copy code from the following projects; their public documentation informed selected product and safety decisions:

- [InboxAPI CLI — email-digest skill](https://github.com/inboxapi/cli/blob/main/skills/codex/email-digest/SKILL.md): concise digest structure, thread-aware recaps, and actionable follow-ups.
- [claude-secretary — email-digest skill](https://github.com/chansigit/claude-secretary/blob/master/.claude/skills/email-digest/SKILL.md): practical priority categories and deadline-oriented triage.
- [outlookctl — Outlook Automation skill](https://github.com/gmickel/outlookctl/blob/main/skills/outlook-automation/SKILL.md): read-by-default and draft-before-send safety boundary.

Unlike those references, this project uses Codex's authenticated Outlook Email connector, groups consolidated mail by actual recipient address, and has no local Mail.app, Windows COM, external mailbox API, or standalone credential requirement.

## Project layout

~~~text
outlook-mail-digest/
├── SKILL.md            # Operational guidance used by Codex
├── agents/openai.yaml  # Codex skill metadata
├── README.md
└── LICENSE
~~~

## Author

Created and maintained by **Trevon Tanfei Liu** ([@Pamphiluss](https://github.com/Pamphiluss)).

## License

Released under the [MIT License](LICENSE).
