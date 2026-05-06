# Azure SOC Detection Lab – KQL Workbook Maps

This project demonstrates hands-on SOC analyst capabilities by building and visualizing security detections using KQL in Azure Monitor / Log Analytics.

The focus is on identifying real-world attack patterns across identity, endpoint, network, and cloud activity.

---

## 🚨 Key Outcomes

- Built 5 SOC-relevant detections using real Azure log sources
- Applied geolocation enrichment to identify attack origins
- Visualized security events using Azure Workbook maps
- Simulated real SOC investigation workflows and triage thinking

---

## 🧠 Skills Demonstrated

- KQL (Kusto Query Language)
- SIEM Log Analysis (Azure Monitor / Log Analytics)
- Threat Detection & Investigation
- Identity Security Monitoring (Entra ID)
- Endpoint Monitoring (VM Authentication)
- Network Threat Analysis
- Cloud Activity Monitoring (AzureActivity)
- GeoIP Enrichment & Data Visualization

---

## 📊 Data Sources

- `SigninLogs` – Entra ID authentication events  
- `DeviceLogonEvents` – VM login activity  
- `AzureActivity` – Cloud resource operations  
- `AzureNetworkAnalytics_CL` – Network traffic flows  

---

# 📍 Detection Use Cases

---

## 1. Entra ID Authentication Failures

**Purpose:** Detect brute-force and password spraying attacks

**Detection Logic:**
- Filters failed authentication attempts (`ResultType != 0`)
- Aggregates login attempts by user and geographic location

**SOC Insight:**
- Identifies targeted accounts
- Highlights attack origin locations

![Login Failures](screenshots/login-failures-map.png)

---

## 2. Entra ID Authentication Success

**Purpose:** Identify suspicious successful logins

**Detection Logic:**
- Filters successful authentication (`ResultType == 0`)
- Maps login activity by user and location

**SOC Insight:**
- Detects potential account compromise
- Helps validate attacker success after failed attempts

![Login Success](screenshots/login-success-map.png)

---

## 3. VM Authentication Failures

**Purpose:** Detect brute-force attempts against virtual machines

**Detection Logic:**
- Queries failed logon attempts from `DeviceLogonEvents`
- Maps remote IP activity using geolocation enrichment

**SOC Insight:**
- Identifies exposed systems
- Detects repeated login attempts from external sources

![VM Auth Failures](screenshots/vm-auth-failures-map.png)

---

## 4. Azure Resource Creation Monitoring

**Purpose:** Detect unauthorized or suspicious cloud activity

**Detection Logic:**
- Filters successful `WRITE` operations in `AzureActivity`
- Tracks resource creation by user and source IP

**SOC Insight:**
- Detects potential persistence mechanisms
- Identifies abnormal cloud usage patterns

![Resource Creation](screenshots/resource-creation-map.png)

---

## 5. Malicious Network Traffic Detection

**Purpose:** Identify inbound malicious traffic targeting the environment

**Detection Logic:**
- Filters `MaliciousFlow` traffic from network analytics logs
- Extracts source/destination IP, ports, and protocol

**SOC Insight:**
- Highlights attacker infrastructure
- Reveals targeted services and exposed ports

![Malicious Traffic](screenshots/malicious-traffic-map.png)

---

# 🔍 SOC Analyst Workflow (How I Investigate)

For each detection, I apply the following process:

1. Identify anomaly (failed logins, traffic spikes, resource creation)
2. Analyze source (IP address, geolocation, user identity)
3. Correlate across logs:
   - Login failures → login success
   - Network traffic → VM authentication attempts
4. Determine risk level:
   - Low (noise)
   - Medium (suspicious)
   - High (potential compromise)

---

# 🚀 Why This Project Matters

This project demonstrates the ability to:

- Build real detection logic (not just theory)
- Analyze and interpret security logs
- Think like a SOC analyst during investigations
- Translate raw data into actionable security insights

---

# 📌 Author

**Aaron Welsh**

- LinkedIn: https://www.linkedin.com/in/aaronswelsh/
- GitHub: https://github.com/AaronW-Cipher

---
