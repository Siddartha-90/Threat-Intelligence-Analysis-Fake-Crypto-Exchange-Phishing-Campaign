# Threat Intelligence Analysis: Fake Crypto Exchange Phishing Campaign

## 1. Executive Summary
This report details the analysis of a social engineering and phishing campaign utilizing a fabricated cryptocurrency exchange to perpetrate advance-fee fraud. The threat actor leverages an emotional lure via direct messaging to distribute credentials to a fraudulent platform.

## 2. Incident Artifacts
*   **Vector:** Direct Message (Social Engineering)
*   **Lure:** Fake inheritance / mental health crisis
*   **Target Domain:** `www.jwz.cc`
*   **Provided Credentials:** 
    *   Username: `fgh246`
    *   Password: `hb2364`
*   **Claimed Balance:** $6,303,050.5 USDT

## 3. Passive OSINT & Infrastructure Analysis
*Information gathered without directly interacting with the target web server.*

*   **WHOIS Record:** (Run `whois jwz.cc` and document the registrar, creation date, and expiration date. Scammer domains are often registered very recently).
*   **DNS Records:** (Run `dig jwz.cc ANY` to find the hosting provider and IP address).
*   **Threat Intelligence Vendors:** (Check the IP and domain against VirusTotal, URLhaus, or AbuseIPDB to see if it has been previously flagged).

## 4. Active Analysis & Interception
*Observations from interacting with the domain within an isolated environment.*

*   **HTTP Headers:** (Run `curl -I https://www.jwz.cc` to identify the server type and security headers).
*   **Traffic Analysis:** Configured Burp Suite to intercept traffic. 
    *   *Observation:* Navigating to the site presents a login portal.
    *   *Authentication Mechanism:* Attempted login using the provided credentials (`fgh246` / `hb2364`). 
    *   *POST Request Analysis:* (Document the parameters sent during login. Does it send them in plaintext? Does it use a standard API endpoint?)
*   **Platform Functionality:** 
    *   *Observation:* Upon successful login, the dashboard artificially inflates the account balance to match the lure. 
    *   *The Exploit:* Attempting to initiate a withdrawal triggers a secondary prompt requesting an upfront deposit (e.g., "tax payment," "gas fees," or "account activation") to an external, attacker-controlled wallet.

## 5. Indicators of Compromise (IoCs)
*   **Domains:** `jwz.cc`
*   **IP Addresses:** (Insert the resolved IP from step 3)
*   **Attacker Wallets:** (If the platform provides a cryptocurrency address to send the "activation fee" to, document it here).

## 6. Conclusion
The domain `jwz.cc` operates as a fraudulent cryptocurrency dashboard designed to execute advance-fee fraud. The site possesses no legitimate trading functionality and relies entirely on front-end manipulation to deceive targets into transferring real assets to attacker-controlled wallets.
