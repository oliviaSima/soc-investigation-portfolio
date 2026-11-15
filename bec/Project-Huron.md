# 🕵️ BEC Investigation Report

> **Platform:** SOC Simulation Project — WDLabs  
> **Environment:** Microsoft 365 Unified Audit Logs / Microsoft Sentinel

---

## 📋 Case Details

| Field | Value |
|:---|:---:|
| **WDLabs Case Name** | `Project Huron` | 
| **Case Reference** | `003` |
| **Affected Account** | `kenneth.baker@wdlabs.com.au` |
| **Incident Date Range** | `2026-09-19` — `2026-10-03` |
| **Investigation Date** | `2026-10-18` — `2026-11-15` |
| **Analyst** | `Olga Kharitonova` |

---

## 1. Attack Narrative

<div align="justify">
  
An investigation identified that Kenneth Baker's Microsoft 365 account was compromised between 29 September and 3 October 2026. The attacker gained unauthorised access to his work email and SharePoint files and used his account to send suspicious emails to colleagues.

The incident likely began on 29 September, following a suspicious email disguised as a shared marketing file. The attacker may have captured Kenneth's active login session, allowing them to access his account without needing to sign in again or complete additional authentication.

On 30 September, the attacker accessed Kenneth's mailbox, reviewed emails, and explored the company's SharePoint environment. They then downloaded 824 PDF documents from a company SharePoint folder in approximately three minutes, indicating a significant potential data breach.

On 3 October, the attacker returned to the compromised account and sent suspicious emails with the subject "training" to three colleagues. The attacker also created an email rule to hide messages containing words such as "training", "phishing", and "scam", potentially preventing Kenneth from noticing warnings or replies. They also deleted the original suspicious email and Kenneth's response.

The investigation found that the same login session was used from multiple countries, including the Netherlands, Italy, and Spain, providing strong evidence of unauthorised access.

The investigation confirmed a business email compromise involving unauthorised mailbox access, the download of 824 company documents, and suspicious emails sent to three employees. </div> 

---

## 2. Timeline of Events

<!-- Chronological record of all confirmed threat actor activity. UTC throughout. -->

| Time (UTC) | Activity | Detail |
|---|---|---|
| 29 Sep 2026, 12:30 | Initial Access | Suspected phishing-related compromise. The session later used by the attacker was authenticated at 12:30:06. |
| 29 Sep 2026, 12:38 | Phishing Interaction | Kenneth's account sent a reply to the suspicious marketing-file email. |
| 30 Sep 2026, 08:21 | Unauthorised Access | Attacker activity began through a previously authenticated session, using VPN infrastructure in the Netherlands. |
| 30 Sep 2026, 08:26 | Mailbox Access | The attacker accessed email messages in Kenneth's mailbox. |
| 30 Sep 2026, 09:54 | SharePoint Discovery | The attacker explored the WDLabs Operations SharePoint environment. |
| 30 Sep 2026, 09:57–10:00 | Bulk File Download | The attacker downloaded 824 PDF documents from SharePoint. |
| 3 Oct 2026, 03:33 | Evidence Deletion | The original suspicious marketing-file email and Kenneth's reply were moved to Deleted Items. |
| 3 Oct 2026, 04:40 | Inbox Rule Creation | The attacker created a rule named `Delete Spam` to hide emails containing `training`, `phishing`, or `scam`. |
| 3 Oct 2026, 04:51 | Internal Phishing | Suspicious emails titled `training` were sent to three employees. |
| 3 Oct 2026, 05:09 | Inbox Rule Modification | The attacker modified the rule to automatically mark matching emails as read. |
| 3 Oct 2026, 05:17 | Further Email Activity | A reply titled `Re: training` was sent to the same three employees. |

---

## 3. Findings

### 3.1 Initial Access

<div align="justify">

The investigation suggests that Kenneth Baker's Microsoft 365 account was initially compromised on 29 September 2026, potentially through a phishing email disguised as a shared marketing file. The exact method of compromise remains unconfirmed, although the evidence strongly suggests session token theft and replay.

The first identified attacker activity occurred on 30 September 2026 at approximately 08:21 UTC, originating from ExpressVPN infrastructure in the Netherlands (200.162.148.0/24). The attacker used a previously authenticated session associated with an authentication timestamp of 29 September 2026 at 12:30:06 UTC. Subsequent activity involved Outlook on the web and SharePoint Online.

The same session identifier was later observed across multiple IP addresses in the Netherlands, Italy, and Spain without a new interactive sign-in, providing strong evidence that the attacker reused Kenneth's authenticated session to gain unauthorised access.

</div>

---

### 3.2 Unauthorised Activity

<div align="justify">

Following the compromise of Kenneth Baker's Microsoft 365 account, the attacker performed several unauthorised activities across Exchange Online and SharePoint, including mailbox access, email manipulation, and bulk document downloads.

On 30 September 2026, the attacker accessed Kenneth's mailbox, reviewed email conversations, and explored the company's SharePoint environment, downloading 824 PDF documents in approximately three minutes.

On 3 October 2026, the attacker deleted the original suspicious email and Kenneth's response, potentially concealing evidence of the compromise. The attacker also created an inbox rule named Delete Spam to hide messages containing keywords such as training, phishing, and scam, later modifying it to mark matching messages as read.

The compromised account was subsequently used to send suspicious emails to three internal employees, potentially attempting to extend the attack to additional accounts.

Overall, the findings indicate that the attacker used the compromised account to access company information, conceal malicious activity, and target other employees.

</div>

---

### 3.3 Data Access

<div align="justify">

The investigation identified unauthorised access to Kenneth Baker's Exchange Online mailbox and the company's SharePoint environment. Microsoft 365 audit logs were analysed to determine what information the attacker accessed and whether any data was potentially exfiltrated.

In SharePoint, the attacker accessed the WDLabs Operations site and explored its document libraries. On 30 September 2026, between 09:57:22 and 10:00:38 UTC, the attacker downloaded **824 unique PDF documents** from the `Shared Documents/Documents` library. The activity originated from IP address `200.162.148.121`, associated with VPN infrastructure in the Netherlands. The audit records indicate a bulk ZIP download, with individual `FileDownloaded` events recorded for the documents. This provides strong evidence of unauthorised bulk data extraction.

</div>

---

## 4. Lessons Learned
<div align="justify">
  
This investigation highlighted the importance of correlating authentication logs, mailbox activity, and SharePoint events when investigating a business email compromise. One of the key lessons was that a successful authentication event does not necessarily indicate legitimate user activity, as attackers may reuse previously authenticated sessions to access compromised accounts without completing another authentication process.

The investigation also demonstrated the importance of examining inbox rules, deleted messages, and unusual file download activity. These actions can reveal attempts to conceal malicious behaviour and identify additional activity that may not be immediately visible in sign-in logs.

Another important lesson was the value of correlating session identifiers, IP addresses, timestamps, and audit events across multiple Microsoft 365 services to reconstruct the attacker's actions and establish a clear sequence of events.

</div>

---
