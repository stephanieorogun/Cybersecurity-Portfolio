# Password Security & Cracking Analysis
**Status:** completed | **Source:** TryHackMe — Password Cracking & Hashing Basics
**Tools:** hashid, Hashcat, John the Ripper, rockyou.txt wordlist

## 🎯 What This Project Is
I didn’t just follow tasks — I compared how passwords are protected across different systems, tested how easily they can be cracked, and worked out what actually makes a password strong.

## 🔍 What I Investigated
- How plain-text storage leaves every account exposed instantly
- Why hashing works — and the 4 properties that make it secure
- How salting defeats rainbow table attacks
- MD5 vs SHA-1 vs bcrypt — side-by-side comparison of speed vs security

## 🧪 Hands-On Testing
- Identified unknown hash types using `hashid`
- Ran dictionary attacks with Hashcat against real hashes
- Saw first-hand: fast hashes (MD5) crack in seconds; bcrypt takes far longer — and that’s intentional
- Found that two identical passwords using different algorithms produce completely different hashes

## 📋 Key Findings
- MD5 & SHA-1 → fast to compute, fast to crack → **never use for passwords**
- bcrypt → designed to be slow → best defence against brute-force
- Salting means every password must be cracked individually — no bulk rainbow-table shortcuts
- Length beats complexity alone → 12+ characters > mixing symbols in short passwords

## ✅ Recommendations
- Use bcrypt / Argon2 for password storage
- Enforce minimum 12-character passwords + MFA
- Never store passwords in plain text or unsalted hashes
- Block common breached passwords at input stage

## 🧠 What I Learned
Security isn’t about picking one “best” tool — it’s understanding *why* some methods fail and others hold up. The best protection is slowing attackers down until it’s no longer worth their time.
