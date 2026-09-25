# Phishing Email Analysis
**Status:** ⏳ completed 
**Source:** [TryHackMe — Phishing Emails in Action](https://tryhackme.com/room/phishingemailsinaction)
**Skills:** Email header analysis, impersonation detection, link manipulation, attachment forensics, tracking pixel identification

---

## 🎯 Project Overview
I examined **four real-world phishing scenarios** to identify exactly how attackers craft deceptive messages — from spoofed addresses and hidden links to malicious attachments. This isn't theory — I analysed actual samples and documented the red flags step by step.

---

## 📧 Scenario 1: Fake PayPal Receipt — "Cancel Your Order"
**Techniques used:** Spoofed address, URL shortening, brand impersonation

| Observation | Detail | Why It's a Red Flag |
|---|---|---|
| **Display vs From** | Shows `service@paypal.com` → actual sender: `gibberish@sultanbogor.com` | Display names are easy to fake — always check the real address |
| **Reply-To mismatch** | Different address entirely from the sender | Classic trick to send replies straight to attackers |
| **False urgency** | "You sent a payment of $120.00" — fear of unauthorised transaction | Pressures you to click *now* without thinking |
| **Hidden destination** | Button links obscured — true URL masked | Hover text doesn't match where it actually goes |

**Key lesson:** A familiar name means nothing — verify the full sending domain.

---

## 📦 Scenario 2: Fake Shipping Notification — "Track Your Package"
**Techniques used:** Spoofed brand, link manipulation, tracking pixels

| Observation | Detail | Why It's a Red Flag |
|---|---|---|
| **Display vs Domain** | Shows `Distribution Center` → actual: `contact@begmpro.club` | `.club` is not a legitimate logistics domain |
| **Link mismatch** | Text says `Track your package: #LZ8942...` → goes to `devret.xyz` | Looks convincing — the text matches the pattern, but the domain is fake |
| **Tracking pixel** | Hidden 1×1 image: `Tracking.png` → `devret.xyz/Creatives/Tracking.png` | Lets attacker know *you opened the email* — confirms active address |
| **Email provider block** | Yahoo automatically blocked images → exposed the trick | Missing/blocked images = common sign of hidden tracking |

**Key lesson:** Inspect the raw HTML source — what you see is rarely the full story.

---

## 🚚 Scenario 3: DHL Brand Impersonation — "Scheduled Shipment"
**Techniques used:** Brand impersonation, conflicting geography, malicious attachment

| Observation | Detail | Why It's a Red Flag |
|---|---|---|
| **Name mismatch** | Shows `DHL Express` → from: `info@glamcargocompany.de` | Not DHL's official domain |
| **Geography conflict** | Addresses India; language mix; German domain | Legitimate DHL emails match your actual location/language |
| **Suspicious attachment** | `Invoice.xlsx` — `.xlsx` is technically valid, but... | File type alone isn't safe — must check what's *inside* |
| **Single link only** | Entire document is just one clickable link | No real invoice details — pure lure |

**Key lesson:** Brand logos don't prove authenticity — domains and verified authentication results do.

---

## ⚠️ Scenario 4: Malicious Excel Attachment — Hidden Payload
**Techniques used:** Macro-enabled file, disguised executable, multi-stage infection

| Observation | Detail | Why It's a Red Flag |
|---|---|---|
| **File behaviour** | Opens → shows error message → `regasm.exe` executes in background | Error is distraction — payload runs unseen |
| **What it does** | Tries to download + run further code → establishes persistence → exfiltrates data | Full malware chain: execute → connect → steal → spread |
| **Excel as delivery** | `.xlsx` with hidden macros/payloads — looks harmless | Documents should *never* need to run code |
| **Persistence = danger** | Installs itself to survive reboots → attacker has ongoing access | Single click = long-term compromise |

**Key lesson:** Even "safe" file types can be weaponised — if you didn't expect it, don't open it.

---

## 🔍 Universal Red Flag Checklist
I now apply this to *every* suspicious email:

✅ **Check the FROM address** — not just the display name  
✅ **Check REPLY-TO** — should match the FROM domain  
✅ **Hover ALL links** — does the real URL match the text?  
✅ **Inspect attachments** — were you expecting it? Is it a document *or* code?  
✅ **Check for urgency/fear** — "Act now", "Suspend", "Verify" = pressure = danger  
✅ **Look for geography/language oddities** — do they know who you are?  
✅ **Review email auth** — SPF/DKIM/DMARC pass?

---

## 🛡️ How to Respond
1. **Don't click, reply, or download**
2. **Don't forward to anyone** — risk spreading it
3. **Report it** — use your organisation's button + `report@phish-reply.service.gov.uk`
4. **Delete** — if you clicked: change passwords, enable MFA, review account activity

---

## 🧠 Key Takeaways
- **Impersonation is about trust** — they use brands you know to lower your guard
- **Link manipulation is easy** — text can say one thing, link goes somewhere completely different
- **Tracking pixels confirm you're real** → leads to *more* targeted attacks
- **Attachments are the next step** — once you trust the email, they deliver the payload
- **One red flag = investigate; multiple = phishing** — always verify independently via official channels

---

## 🔗 Resources
- [TryHackMe — Phishing Emails in Action](https://tryhackme.com/room/phishingemailsinaction)
- [NCSC — How to Spot Phishing](https://www.ncsc.gov.uk/guidance/phishing)
- [VirusTotal — Scan Links & Files](https://www.virustotal.com/)
