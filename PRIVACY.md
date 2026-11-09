# Privacy Policy — Baton

**Team:** JAYTAI  
**Product:** Baton (Atlassian Forge app for Jira and Confluence)  
**Support / contact:** [jayren1121@gmail.com](mailto:jayren1121@gmail.com)  
**Last updated:** 9 November 2026 (UTC+8)

This policy describes how the Baton Forge app (“Baton”, “we”, “us”) handles data when it is installed on an Atlassian Cloud site. It is based on the behaviour of Baton version 5.1.1 as shipped in the app source. It is not legal advice.

---

## 1. Who this applies to

Baton is installed by a site or product administrator on an Atlassian Cloud site. End users who open Baton, enable capture, or use Remember this / Rovo actions are “users”. Site admins configure defaults and exclusions.

---

## 2. What Baton stores (Forge storage)

Baton stores app data in **Atlassian Forge storage** on Atlassian’s platform: the **Custom Entity Store** and **key–value storage (KVS)**. Data is scoped to the app installation on that site.

### Custom entities (per installation)

- **`candidate`** — pending captured items awaiting user review (summary, type, optional due date/time/timezone, source URL/kind/id, status, needs-review flag, owner account id, week key, timestamps).
- **`memory`** — confirmed **Work Memory** items for a user (same kinds of fields, plus state such as done/cancelled and optional linked Jira issue key).
- **`share`** — entity declared in the manifest from an earlier design; **current product code does not use successor sharing**. Successors rely on Confluence handover pages the user creates.

### Settings and indexes (KVS / settings records)

Per-user settings such as: privacy notice accepted, passive capture on/off, language (EN / 中文), calendar open preference, optional Slack member id, custom keywords, weekly-email schedule (weekday/time), optional manual recipient email, optional notify issue key, and weekly-send bookkeeping (ISO week keys). Admin defaults may include default Jira project, Confluence space, and exclusion lists (Jira projects, Confluence spaces, Slack channels, keywords).

Work Memory and candidates are **keyed by the signed-in user’s Atlassian account id**. The product UI is designed so each user sees **their own** items, not other users’ private Work Memory. Baton is **not** intended as a performance-review tool.

---

## 3. What data we collect from Atlassian products

Depending on features you use, Baton may read or write:

| Source | What | When |
|--------|------|------|
| **Jira** | Issue comments (passive capture, if you opt in); issue metadata needed to create issues or notify; your account id; optionally your Atlassian account **email** (`read:email-address:jira`, app identity) for weekly-report addressing | Capture, Send to team board, weekly email, UI |
| **Confluence** | Page/comment content (passive capture, if you opt in); space/page data to create a **handover package** page | Capture, handover |
| **Rovo** | Text you send to the Baton agent; actions read/write **only your** Work Memory | Agent chat |
| **User-entered** | Text from Remember this, manual add, Settings (including optional email / Slack id) | Always under your control |

Passive capture of Jira / Confluence content is **off by default**. You must accept the in-app privacy notice and turn capture on in Settings. Turning capture off can offer deletion of pending (unconfirmed) candidates. “Remember this” and Rovo remember still work when capture is off.

Admins can exclude Jira projects, Confluence spaces, Slack channels, and keywords so matching content is skipped and not sent for classification.

---

## 4. External services (optional / feature-triggered)

Baton declares Forge backend egress to these hosts. Traffic happens only when the related feature runs and is configured.

### Google Gemini (`generativelanguage.googleapis.com`)

- **Purpose:** Optional classification of keyword-matched text (type, summary, due date) and optional handover intro text.
- **What is sent:** Only text that passed the keyword/date pre-filter (not every comment). Secret-like strings are **masked** first (e.g. password/token/api-key patterns, AWS/Google key shapes, Slack tokens, GitHub tokens, JWTs → `[MASKED]`).
- **Required?** No. Without `GEMINI_API_KEY`, capture can still create “needs review” items; manual Remember this works. Baton uses Gemini’s **free tier** when configured; it does not use paid Forge LLMs.

### Slack (`slack.com`) — optional

- **Purpose:** Optional channel message capture via a Forge web trigger (Events API).
- **Limits in product:** Channels the bot is invited to only; **never DMs**; Baton **never posts** to Slack; signatures verified; retries de-duplicated.
- Each user may store their Slack member id in Settings for mapping.

### Jira issue notify (Atlassian API — no separate email vendor)

- **Purpose:** Primary path for the weekly report email to the user’s **Atlassian account email**.
- Uses `POST /rest/api/3/issue/{key}/notify` as the **app** (`asApp`) to a viewable issue. Jira delivers (or drops) mail according to Atlassian/Jira notification settings. “Queued” is not a guarantee of inbox delivery.

### Brevo (`api.brevo.com`) and Resend (`api.resend.com`) — optional

- **Purpose:** Send the weekly report HTML/plaintext **only when** the Settings recipient is a typed address that is **not** the Atlassian account email (or as fallback when notify has no recipients and a key is set).
- The message content is the same weekly report sections shown in the app. API keys are stored as encrypted Forge environment variables by the installer, not in Work Memory entities.

---

## 5. What we do **not** do

- We do **not sell** your personal data or Work Memory.
- We do **not** use Baton data for advertising.
- We do **not** read Slack direct messages.
- We do **not** silently invent an email address; Settings shows the address that will be used, or asks you to enter one.
- We do **not** claim a weekly email was delivered solely because Jira returned a queue success.

---

## 6. Retention, deletion, and uninstall

- Users can **edit or delete** individual candidates and Work Memory items in the UI, including bulk delete of pending candidates.
- Turning **passive capture off** can offer removal of pending items.
- Creating a Confluence handover page copies selected memory content into a **Confluence page** that then follows normal Confluence retention and permissions (outside Forge entity storage).
- **Uninstalling** the Forge app from the site removes the app installation. Forge app storage for that installation is deleted according to **Atlassian Forge / Atlassian Cloud retention for uninstalled apps** (app-stored entity and KVS data for that installation is not kept available to the uninstalled app). Content already written into Jira issues or Confluence pages (for example a handover page or a “Send to team board” issue) remains in those products until site admins or users delete it there.
- Users who want data removed while the app is installed should delete items in Baton and, if needed, delete related Jira/Confluence pages they created.

---

## 7. Children’s data

Baton is a workplace productivity app for Atlassian Cloud teams. It is not directed at children.

---

## 8. Changes

We may update this policy when the product changes. The “Last updated” date at the top will change. Material changes for Marketplace or Sharing distribution will be reflected in the URL provided to admins.

---

## 9. Contact

**Team JAYTAI**  
Email: **jayren1121@gmail.com**

Questions about privacy, data deletion, or this policy: use the address above.
