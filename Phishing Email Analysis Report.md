# Phishing Email Analysis Report

## TASK 2 - Analyze a Phishing Email Sample
https://github.com/rf-peixoto/phishing_pot/blob/main/email/sample-1.eml
### 1. Sample Phishing Email
**Subject:** "Important: Verify Your Account Now"


### 2. Sender Email Address Analysis
- The `banco.bradesco@atendimento.com.br` appears legitimate, but is not from `@bradesco.com.br` (Bradesco's official domain)
- The domain `atendimento.com.br` is likely used to impersonate Bradesco
- This is a spoofed sender email address attempting to impersonate Bradesco Bank

### 3. Email Header Analysis
The email headers reveal inconsistencies:
- Sender IP `137.184.34.4` originates from a generic cloud server (`ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06`)
- SPF/DKIM/DMARC failures indicate improper authentication

Key header findings:
1. **X-SID-Result: NONE**
   - No SenderID validation performed (unusual for major banks)
2. **X-MS-Exchange-Organization-SCL: 5**
   - Microsoft's Spam Confidence Level rates this as high spam probability
3. **Return-Path: root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06**
   - Points to non-corporate cloud server, not official Bradesco domain

### 4. Suspicious Links/Attachments
- The email contains a phishing link (https://blog1seguimentmydomaine2bra.me/) disguised as a "Resgatar Agora" (Redeem Now) button, which does not belong to Bradesco’s legitimate domain and is likely a fraudulent site designed to steal login credentials.

### 5. Urgent/Threatening Language
- "Seu cartão tem 92.990 pontos LIVELO expirando hoje!" (Your card has 92,990 points expiring TODAY!)
- Phrases like "evite a perda" (avoid losing) and "resgate agora" (redeem now) create false urgency

### 6. Mismatched URLs
- `<a href="https://blog1seguimentmydomaine2bra.me/">`

### 7. Spelling/Grammar Errors
- While there are no blatant spelling mistakes, the Portuguese phrasing feels unnatural for official bank communications, such as "Pontos Livelo com seu cartão Banco do Bradesco"—a structure rarely used in legitimate financial correspondence. Additionally, while the email correctly names "Banco do Bradesco," its overall styling and branding appear inconsistent with the bank’s official format.

### 8. Summary of Phishing Traits
- This email exhibits classic phishing signs, including a spoofed sender domain, failed authentication checks, deceptive links, urgency-driven language, and an untrustworthy server origin—all confirming it’s a fraudulent attempt to steal sensitive data.

## Interview Questions

### 1. What is Phishing?
Phishing is a cyberattack where attackers impersonate legitimate entities (e.g., banks, companies) via email, SMS, or fake websites to steal sensitive data like login credentials, credit card details, or personal information. These attacks often use social engineering to manipulate victims into clicking malicious links, downloading malware, or entering data on fraudulent pages. Technical methods include domain spoofing, fake SSL certificates, and credential-harvesting forms. Automated phishing kits and bulletproof hosting make these attacks scalable and harder to trace.

### 2. How to Identify a Phishing Email?
- **Sender Address Mismatch:** Check if the domain matches the official organization
- **Suspicious Links:** Hover over URLs to see if they redirect to unknown domains
- **SPF/DKIM/DMARC Failures:** Use email header analyzers to detect authentication failures
- **Urgency/Threats:** Phrases like "Your account will expire today!" pressure victims
- **Unusual Attachments:** Executable files (.exe, .js) or macros in Office docs may deliver malware

### 3. What is Email Spoofing?
Email spoofing forges the "From" field to mimic a trusted sender (e.g., support@paypal.com), even though the email originates from an attacker's server. This exploits lack of strict DMARC enforcement or misconfigured SMTP relays. Attackers may also spoof display names (e.g., "Amazon Support") while using a fake domain. Advanced spoofing can bypass basic filters by compromising legitimate email servers or using homograph attacks (e.g., paypa1.com with a numeral "1").

### 4. Why Are Phishing Emails Dangerous?
- **Credential Theft:** Fake login pages capture usernames/passwords
- **Malware Distribution:** Attachments or links may deploy ransomware, keyloggers, or trojans
- **Financial Fraud:** Stolen data enables unauthorized transactions
- **Business Email Compromise (BEC):** Spoofed executive emails trick employees
- **Data Breaches:** Common entry point for large-scale breaches

### 5. How can you verify the sender's authenticity?
Check email headers for SPF/DKIM/DMARC pass/fail status using tools like MXToolbox. Verify the sender's domain matches the official website. Look for HTTPS and valid SSL certificates on linked sites. Contact the organization via official phone/chat—never use details from the email. Enable multi-factor authentication (MFA).

### 6. What tools can analyze email headers?
- MXToolbox Header Analyzer (checks SPF/DKIM/DMARC)
- Google Admin Toolbox Messageheader (visualizes routing)
- PhishTool (automates threat detection)
- URLScan.io (scans linked domains for malware)
- Wireshark (advanced network analysis for SMTP traffic)

### 7. Actions for Suspected Phishing Emails
Upon identifying a potential phishing email, immediate containment measures should be implemented. First, refrain from any interaction with embedded links or attachments, as these may trigger malware execution or direct users to credential-harvesting pages. The email should be reported through the client's native phishing reporting function (e.g., Microsoft's "Report Message" add-in) or forwarded to relevant abuse desks (e.g., CERT teams) with full headers intact for analysis. Concurrently, initiate endpoint scans using EDR solutions to detect potential IOCs if any interaction occurred. Organizational protocols require notifying the SOC team via designated incident reporting channels, providing the complete MIME content for threat intelligence correlation. This event should be cataloged in security awareness training materials, with observed TTPs integrated into updated blocklists and SIEM detection rules to strengthen defensive posturing against similar campaigns.

### 8. Technical Execution of Social Engineering in Phishing
Modern phishing campaigns employ multi-layered social engineering tactics designed to bypass both technical controls and human vigilance. Authority exploitation manifests through sophisticated display name spoofing combined with Business Email Compromise (BEC) techniques, often leveraging previously compromised email threads for contextual credibility. Scarcity mechanisms are technically enhanced through dynamic HTML elements like JavaScript countdown timers that create false urgency. Fear-based attacks frequently incorporate fake security alerts mimicking enterprise login portals, complete with stolen branding and TLS certificates. Familiarity attacks utilize CRM data leaks to personalize messages with accurate project codes or internal terminology. Curiosity-driven payloads now employ polyglot files (e.g., PDFs with embedded PowerShell scripts) and homograph domains registered via compromised registrar accounts. Defensively, layered email security stacks incorporating NLP analysis, attachment sandboxing, and real-time domain age verification have become essential, complemented by continuous user conditioning through simulated phishing exercises that measure susceptibility to these evolving tactics.
