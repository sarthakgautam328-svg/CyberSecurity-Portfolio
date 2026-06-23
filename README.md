## TryHackMe: FakeBank Web Vulnerability & Defense Write-up

## Objective
To simulate an offensive web attack using directory brute-forcing and parameter tampering, followed by implementing defensive firewall rules to track and block the attacker.

## Tools Used
*   **Dirb:** For directory enumeration.
*   **Web Application Firewall (WAF):** For monitoring and rate-limiting.

## Phase 1: Offensive Reconnaissance
I started by scanning the target web server to find hidden directories that were not linked on the main page. 
*   Executed a directory brute-force attack using `dirb`.
*   Successfully discovered a hidden administrative panel located at `/bank-transfer`.

## Phase 2: Exploitation (IDOR)
Once inside the hidden directory, I identified a logic flaw in how the application handles user input.
*   The application did not properly authenticate my session against the target account.
*   I was able to manipulate the destination account number parameter and force a transfer, successfully exploiting an Insecure Direct Object Reference (IDOR) vulnerability.

## Phase 3: Defensive Incident Response
After the exploitation, I switched to the perspective of the Blue Team (Defenders) to mitigate the attack.
*   Analyzed the server logs and identified a massive spike in HTTP requests coming from a single IP address (the result of my `dirb` scan).
*   Identified the attacker's IP.
*   Implemented a block rule on the firewall, immediately severing the attacker's connection and securing the server.

## Conclusion
This lab demonstrated how easily attackers can find hidden infrastructure if it is not properly secured. It highlights exactly why strict access control checks are required on every web form—especially in fintech and banking applications—to prevent parameter tampering.

