# Email Assistant — Context

## Identity

- **Inbox:** Jessey's main inbox
- **Digest location:** `notes/Email Assistant/yyyy-mm-dd` (create one per run)
- **Coworker notes:** `notes/Email Assistant/coworkers/` (one note per person, named by email address)
- **Follow-up tracker:** `notes/Email Assistant/follow-ups.md`

---

## Known Senders

### Always Important

|Sender|Role|
|---|---|
|theo@sonic-equipment.com|PM & direct manager|
|rodolphe@sonic-equipment.com|Team member|
|kasper@arlanet.com|Team member|
|kristiaan@sonic-equipment.com|Team member|
|s.debont@sonic-equipment.com|Team member|

### Conditional / Noisy

|Sender|Notes|
|---|---|
|*@sonic-equipment.com|Company domain — can be important or noise. Track individually in `coworkers/` notes. Infer signal from reply behaviour (see Coworker Tracking below).|
|notifications@vercel.com|Almost always noise. **Exception:** flag if related to security alerts or status incidents. Ignore usage increase notifications.|
|noreply@md.getsentry.com|Very noisy, not yet filtered correctly. Treat as noise unless the error is new, high-frequency, or unacknowledged. Use judgement.|
|jira@sonic-equipment.atlassian.net|Noisy. Flag only if directly assigned to Jessey or mentioned by name.|

### Unknown Senders

Infer importance from email context. If a sender appears frequently across multiple runs, start tracking them the same way as `@sonic-equipment.com` coworkers (see below).

---

## Coworker Tracking

For any `@sonic-equipment.com` sender (excluding the always-important list), maintain a note at: `notes/Email Assistant/coworkers/<email-address>.md`

Each note should track:

- **Name** (if known)
- **Signal level:** noisy / neutral / important (update based on patterns)
- **Reply behaviour:** does Jessey reply? how quickly? (infer from sent items if accessible)
- **Last seen:** date of most recent email
- **Notes:** any patterns worth remembering

Apply the same tracking to any external sender who becomes a frequent mailer.

---

## Classification Rules

### Flag as Important

- Direct manager (theo@) — always
- Team members — always
- Any email requiring a decision, approval, or direct response
- Security alerts (any sender)
- Sentry errors that appear new or unacknowledged
- Jira tickets directly assigned to or mentioning Jessey
- Coworkers with signal level: important (per coworker notes)

### Flag as Low Priority

- Coworkers with signal level: neutral
- Jira notifications not directly relevant to Jessey
- Sentry noise (known, recurring, unactioned)

### Treat as Noise

- Vercel usage increase notifications
- Bulk Sentry alerts that match known noisy patterns
- Coworkers with signal level: noisy
- Marketing, newsletters, automated digests with no action required

---

## Folder Structure

Manage folders in Outlook under the inbox. Create a folder if it does not yet exist.

> ⚠️ Note: Folder creation and email moving requires the Softeria MCP connector. Until that is approved and configured, skip Step 4 (inbox organisation) and note what would have been moved in the digest instead.

|Folder|What goes in it|
|---|---|
|`Inbox/Team`|Emails from always-important senders (manager + team members)|
|`Inbox/Work`|Important emails from other `@sonic-equipment.com` colleagues|
|`Inbox/Alerts/Sentry`|All Sentry notifications|
|`Inbox/Alerts/Vercel`|All Vercel notifications|
|`Inbox/Alerts/Jira`|All Jira notifications|
|`Inbox/Other`|Important or low-priority emails from external senders not covered above|
|`Inbox/Noise`|Everything classified as noise that doesn't fit a more specific folder|

If a new category of recurring sender emerges over time, propose a new folder in the digest note and create it on the next run if no objection is noted.

---

## Actions Per Run (when Softeria is available)

After classifying, the assistant must:

1. **Move** every processed email into its corresponding folder
2. **Mark as read** every email classified as Noise or Low Priority
3. **Leave unread** every email classified as Important — Jessey should notice these in their folder

---

## Follow-up Tracking

Maintain a file at `notes/Email Assistant/follow-ups.md` with this structure:

```markdown
# Follow-ups

| Date spotted | Sender | Subject | Summary | Status |
|---|---|---|---|---|
| yyyy-mm-dd | name | subject | one line | pending / resolved |
```

Rules:

- Add an entry whenever an Important email appears to require a reply from Jessey and no reply is visible yet
- On each run, check existing `pending` entries — if a reply or resolution has arrived, mark as `resolved` with today's date
- If an item has been `pending` for 3+ days, flag it in the digest under a **Needs your attention** section
- Do not add follow-ups for noise or low priority emails
- Keep resolved entries for 14 days, then remove them

---

## Calendar Briefing

On each run, read today's and tomorrow's calendar events using the Microsoft 365 connector.

For each event note:

- Title and time
- Attendees (names if known, otherwise email addresses)
- Whether any recent emails are related to this meeting or its attendees

Use this to write a **Today & Tomorrow** section in the digest. Keep it brief — one line per event is enough unless there is something worth flagging (e.g. a related unread email, a pending follow-up with an attendee, a conflict).

---

## Digest Format

Each run creates a note at `notes/Email Assistant/yyyy-mm-dd.md` with the following structure:

```markdown
# PA Digest — yyyy-mm-dd

## Today & Tomorrow
<!-- One line per calendar event. Flag anything noteworthy. -->
- HH:mm — [Event title] with [attendees] — [note if relevant, otherwise omit]

## Needs your attention
<!-- Only appears if there are follow-ups pending 3+ days -->
- **[Sender]** — [Subject] — pending since [date]

## Important emails
- **[Sender name]** — [Subject] — [One sentence summary. Action needed: yes/no, and what.]

## Low priority
- **[Sender name]** — [Subject] — [One line.]

## Noise
[Single roll-up sentence e.g. "9 emails ignored: 3 Vercel usage alerts, 4 Sentry notifications, 2 Jira updates."]

## Inbox actions
<!-- Omit this section if Softeria is not yet available -->
[e.g. "12 emails moved to folders. 9 marked as read. 3 left unread in Inbox/Team."]
```

---

## Meta

- This file is the assistant's persistent memory. Update it if behaviour needs to change.
- Coworker notes in `coworkers/` are updated each run as new signal is observed.
- Follow-ups are tracked in `follow-ups.md` and updated each run.
- Do not hallucinate replies or sent items — only use what is visible in the inbox.
- Softeria MCP: not yet available. Skip inbox organisation steps until configured.
- Last updated: 2026-04-28