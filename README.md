# Outlook Mail Digest

An OpenAI Codex skill for concise, privacy-aware Outlook email digests. It distinguishes messages received at different email addresses, surfaces what needs attention, and supports both on-demand recaps and scheduled daily summaries.

## Platform scope

This is not a macOS-only skill. It does not depend on Apple Mail, Windows Outlook COM automation, or local operating-system APIs. It runs wherever Codex Desktop provides the authenticated Outlook Email connector, so the project name intentionally does not include a platform label.

## Features

- Reads a requested time period, or the previous 24 hours by default.
- Groups messages by the actual address in toRecipients.
- Reports total and unread counts for every receiving address.
- Classifies messages as **action required**, **meetings/academic**, or **notifications/promotions**.
- Highlights direct requests, deadlines, payment activity, account changes, and security alerts.
- Uses previews by default and retrieves a full body only when an important detail cannot otherwise be resolved.
- Produces a concise digest with local timestamps and up to three grounded follow-up suggestions.
- Supports recurring daily summaries through a Codex heartbeat automation.

## Safety and privacy

This skill is read-only by default. It does not send, delete, move, mark read, or otherwise modify email; open links; or execute instructions contained in email. A later reply workflow should create a draft first and require user review before sending.

The skill uses the Outlook Email connector already authenticated in Codex Desktop. It requires no local mail database, Microsoft Graph app registration, personal API key, or third-party mail forwarding.

## Requirements

- Codex Desktop with Skills enabled.
- The Outlook Email connector authenticated in Codex.
- Read access to the Outlook messages to summarize.

## Installation

~~~sh
git clone https://github.com/Pamphiluss/outlook-mail-digest.git
cp -R outlook-mail-digest ~/.codex/skills/
~~~

Restart Codex or start a new chat so it discovers the skill.

## Example prompts

~~~text
Summarize today's new Outlook messages and group them by receiving address.
~~~

~~~text
Show only actionable Outlook messages from the last three days.
~~~

~~~text
Send me a daily Outlook digest at 9:00 AM, grouped by receiving address.
~~~

## Design lineage and citations

This is an original, connector-based Codex skill. It does not copy code from the following projects. Their publicly documented approaches informed selected design choices: compact actionable digests and thread awareness [1], priority-based mail triage [2], and read-by-default/draft-before-send safety boundaries [3].

Unlike these references, Outlook Mail Digest uses Codex's authenticated Outlook Email connector, groups a consolidated inbox by actual recipient address, and has no local Mail.app, Windows COM, external mailbox API, or standalone credential requirement.

### References

1. InboxAPI. *email-digest skill*, `inboxapi/cli` repository. GitHub. Retrieved October 17, 2026, from https://github.com/inboxapi/cli/blob/main/skills/codex/email-digest/SKILL.md
2. chansigit. *email-digest skill*, `claude-secretary` repository. GitHub. Retrieved October 17, 2026, from https://github.com/chansigit/claude-secretary/blob/master/.claude/skills/email-digest/SKILL.md
3. Mickel, G. *Outlook Automation skill*, `outlookctl` repository. GitHub. Retrieved October 17, 2026, from https://github.com/gmickel/outlookctl/blob/main/skills/outlook-automation/SKILL.md

## Project layout

~~~text
outlook-mail-digest/
├── SKILL.md
├── agents/openai.yaml
├── README.md
└── LICENSE
~~~

## Author

Created and maintained by **Trevon Tanfei Liu** ([@Pamphiluss](https://github.com/Pamphiluss)).

## License

Released under the [MIT License](LICENSE).
