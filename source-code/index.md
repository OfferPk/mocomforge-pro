  
MO  
MOCOMForge Pro v1.0.0  
CCSDS 522.0-B-1 & ISO 20215 Mission Operations Common Services Workstation  
MAL v2 Compliant MOC Connected

UTC: \--:--:--

🌐 Dashboard 📁 Directory & Resolver 🔐 Login & RBAC ⚙️ Configuration Baselines 🛡️ 10-Point Normative Auditor

📁  
3  
Registered MO Services

🔐  
1 Active  
Authorized Operators

⚙️  
NOMINAL\_v1.0  
Active Baseline

🚀 Mission Overview: Lunar Gateway MOC  
CCSDS 522.0-B-1

---

MOCOMForge Pro provides the mission operations ground architecture with service discovery, secure operator authentication, role-based telecommand gating, and baseline configuration archiving.

| Service Layer | Standard | Status |
| :---- | :---- | :---- |
| Message Abstraction Layer (MAL) | CCSDS 521.0-B-2 | ACTIVE |
| Directory Service | CCSDS 522.0-B-1 §3 | ONLINE |
| Login Service (RBAC) | CCSDS 522.0-B-1 §4 | AUTHENTICATED |
| Configuration Service | CCSDS 522.0-B-1 §5 | NOMINAL |

📜 Real-Time Security & MOCOM Event Stream  
Clear

---

🔍 Dynamic MAL URI Endpoint Resolver  
---

Service Key / Identity MONITOR\_CONTROL (CCSDS 522.1 M\&C Service) TIME\_CORRELATION (CCSDS 524.2 Time Service) PAYLOAD\_DATA (Science & Telemetry Service)

Resolve MAL URI

RESOLVED ROUTING ENDPOINT:

📋 Registered MO Directory Entries  
---

| Service Key | Domain | Protocol | Status   |
| :---- | :---- | :---- | :---- |

🔑 Operator Login & Authentication  
---

Operator Call-Sign

Authentication Token / Key

Role Classification Flight Director (Full Authorization) Telecommand Operator (Execution & Telemetry) Telemetry Analyst (Read-Only Telemetry) Guest Observer (Restricted)

Authenticate Session

🛡️ Active Operator Sessions & RBAC  
---

| Operator | Role | Token | Expires | Action   |
| :---- | :---- | :---- | :---- | :---- |

⚙️ Configuration Baseline Manager  
Active: NOMINAL\_v1.0

---

Select Baseline to Inspect or Activate NOMINAL\_v1.0 (Flight Baseline) HIGH\_POWER\_PAYLOAD\_v1.1 (Payload Science Burst) SAFE\_HOLD\_v1.0 (Emergency Power Saving)

Activate Selected Baseline Emergency Rollback

BASELINE PARAMETER MAP:

📊 Baseline Differential (Diff) Analysis  
---

Baseline A (Source) NOMINAL\_v1.0 HIGH\_POWER\_PAYLOAD\_v1.1 SAFE\_HOLD\_v1.0  
Baseline B (Target) HIGH\_POWER\_PAYLOAD\_v1.1 NOMINAL\_v1.0 SAFE\_HOLD\_v1.0

Compute Differential

Click 'Compute Differential' to inspect configuration deltas.

🛡️ CCSDS 522.0-B-1 / ISO 20215 10-Point Normative Auditor  
Run Comprehensive Audit

---

| ID | Requirement Description | Normative Focus | Status   |
| :---- | :---- | :---- | :---- |

