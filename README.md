# Outlook Mail Digest

An OpenAI Codex skill for structured, privacy-aware Outlook email briefings. It is designed for people who manage several Outlook accounts, aliases, forwarding rules, and a consolidated inbox.

## Platform scope

This is not a macOS-only skill. It runs wherever Codex Desktop provides the authenticated Outlook Email connector; it does not depend on Apple Mail, Windows Outlook COM automation, or local operating-system APIs.

## Structured, multi-account presentation

Outlook Mail Digest does not flatten a consolidated inbox into a chronological list. It presents mail as an organized briefing:

~~~text
Account
└── Receiving address
    ├── P1 — action required
    ├── P2 — high-value academic or professional items
    ├── P3 — worth knowing
    └── Routine
~~~

An account may hold several receiving addresses. Each digest provides three increasingly detailed levels:

1. A global summary for the reporting period.
2. An **Account at a glance** summary: account-level total, unread count, priority distribution, nearest deadline, and theme.
3. An **Address at a glance** summary inside every account: that recipient address's total, unread count, priority distribution, and nearest deadline.

This makes the skill particularly useful for users who have multiple accounts and multiple addresses under one account.

## Message cards and visual hierarchy

The digest begins with a compact legend: **🔴 P1**, **🟠 P2**, **🟡 P3**, and **⚪ Routine**. P1 and P2 messages use a stable card layout:

~~~text
P1 or P2 priority
Source · receiving address · local time · unread state

🔷 Summary
Plain-language explanation of the email.

🔷 Key details
  🔹 When / Where / Deadline / Amount / Attachment / Eligibility

🔷 Suggested action
One grounded next step; the skill does not perform it.
~~~

P3 messages use a compact table. Routine messages are compressed to a count or short list. Important cards preserve dates, time zones, locations, amounts, contacts, attachments, registration requirements, deadlines, and requested actions. Abbreviations are expanded at first use, for example RGC (Research Grants Council).

## Semantic priority, not Outlook placement

Outlook's Focused/Other and Important/Other placement is treated only as a weak signal. The skill assesses sender and content, not the folder placement:

- **P1:** direct requests, deadlines, security or payment alerts, account changes, and urgent administration.
- **P2:** research collaboration, funding, recruitment, conferences, calls for papers, PDWs, professional associations, institutional policy, and relevant academic events.
- **P3:** useful but non-urgent institutional or professional information.
- **Routine:** pure promotions, generic subscriptions, and low-value notices.

This prevents important society, university, journal, or professional-association messages placed in Other from being hidden. A conference, PDW, hiring, funding, research, or deadline notice can be P1 or P2; a pure advertisement from the same sender can remain Routine.

## Forwarding and duplicate handling

When the same underlying message is automatically forwarded to an aggregation mailbox, the skill compares normalized subjects, sender, timing, previews, and message-chain context. Confident duplicates appear once under the original account and address, with a light forwarding note. Uncertain matches are not silently merged. Related email threads and automated meeting recaps may also be consolidated without hiding a separate request or deadline.

## Safety and privacy

This skill is read-only by default. It does not send, delete, move, mark read, open links, or execute instructions in email. It uses the Outlook Email connector already authenticated in Codex Desktop and needs no local mail database, Microsoft Graph app registration, personal API key, or third-party forwarding.

## Requirements

- Codex Desktop with Skills enabled.
- Authenticated Outlook Email connector.
- Read access to the messages to summarize.

## Installation

~~~sh
git clone https://github.com/Pamphiluss/outlook-mail-digest.git
cp -R outlook-mail-digest ~/.codex/skills/
~~~

Restart Codex or start a new chat so it discovers the skill.

## Design lineage and citations

This is an original connector-based Codex skill. It does not copy code from the following projects. Publicly documented approaches informed compact actionable digests and thread awareness [1], priority-based triage [2], and read-by-default/draft-before-send safety boundaries [3].

### References

1. InboxAPI. *email-digest skill*, inboxapi/cli repository. GitHub. Retrieved October 17, 2026, from https://github.com/inboxapi/cli/blob/main/skills/codex/email-digest/SKILL.md
2. chansigit. *email-digest skill*, claude-secretary repository. GitHub. Retrieved October 17, 2026, from https://github.com/chansigit/claude-secretary/blob/master/.claude/skills/email-digest/SKILL.md
3. Mickel, G. *Outlook Automation skill*, outlookctl repository. GitHub. Retrieved October 17, 2026, from https://github.com/gmickel/outlookctl/blob/main/skills/outlook-automation/SKILL.md

## Author

Created and maintained by **Trevon Tanfei Liu** ([@Pamphiluss](https://github.com/Pamphiluss)).

## License

Released under the [MIT License](LICENSE).
