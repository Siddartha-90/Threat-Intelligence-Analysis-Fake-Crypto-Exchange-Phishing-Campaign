# Threat Intelligence Analysis: Fake Crypto Exchange Phishing Campaign

## 1. Executive Summary
This report details the analysis of a social engineering and phishing campaign utilizing a fabricated cryptocurrency exchange to perpetrate advance-fee fraud. The threat actor leverages an extreme emotional lure—a fabricated mental health crisis and farewell message—delivered via Facebook Messenger to distribute credentials to a fraudulent platform.

## 2. Incident Artifacts
*   **Vector:** Facebook Messenger (Direct Message)
*   **Sender Profile:** "Dinel Kiba" (Likely a compromised account or cloned identity)
*   **Evidence:** Initial contact screenshot documented as `image_512a34.png`
*   **Lure:** Fake inheritance / final farewell
*   **Target Domain:** `www.jwz.cc`
*   **Provided Credentials:** 
    *   Username: `fgh246`
    *   Password: `hb2364`
*   **Claimed Balance:** 6,303,050.5 USDT($)

## 3. Passive OSINT & Infrastructure Analysis
*Information gathered without directly interacting with the target web server.*

*   **Facebook Profile Reconnaissance:**
    *   *Account Audit:* Review profile creation date, timeline history, and URL string (e.g., `facebook.com/username`) to determine if the account was recently hijacked or created explicitly for spamming.
    *   *Reverse Image Search:* Extract the profile picture visible in `image_512a34.png` and analyze it via Google Lens or TinEye to identify potential identity theft or stock imagery.
*   **Domain & IP Investigation:**
    *   *WHOIS Record:* (Run `whois jwz.cc` and document the registrar, creation date, and expiration date).
    *   *DNS Records:* (Run `dig jwz.cc ANY` to identify the hosting provider and resolved IPs).
    *   *Reputation Check:* (Query VirusTotal, URLhaus, or AbuseIPDB for historical malicious activity).

## 4. Active Analysis & Interception
*Observations from interacting with the domain within an isolated VM environment.*

*   **HTTP/TLS Inspection:** (Run `curl -I https://www.jwz.cc` to map server headers).
*   **Traffic Interception (Burp Suite):** 
    *   *Observation:* Navigating to the site presents a login portal.
    *   *Authentication:* Submitted the provided credentials (`fgh246` / `hb2364`). 
    *   *POST Request Analysis:* (Document payload structure. Assess if data is transmitted securely and identify the backend API endpoint).
*   **Platform Functionality & Exploit Chain:** 
    *   *Observation:* The post-login dashboard artificially displays the 6.3M USDT balance. 
    *   *The Trap:* Attempting a withdrawal triggers a secondary prompt demanding an upfront cryptocurrency deposit (e.g., "account activation fee," "gas fee," or "taxes") to an external, attacker-controlled wallet.

## 5. Indicators of Compromise (IoCs)
*   **Domains:** `jwz.cc`
*   **IP Addresses:** (Insert the resolved IP from DNS records)
*   **Attacker Wallets:** (Document any cryptocurrency address provided by the platform for the fraudulent "fee").

## 6. Conclusion
The domain `jwz.cc` operates as a fraudulent cryptocurrency dashboard designed to execute advance-fee fraud, distributed primarily via compromised or fake Facebook accounts. The site possesses no legitimate trading functionality and relies entirely on social engineering and front-end manipulation to deceive targets into transferring real assets to the threat actor.
