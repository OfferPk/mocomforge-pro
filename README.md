# MOCOMForge Pro (v1.0.0)

### CCSDS 522.0-B-1 & ISO 20215 Mission Operations Common Services Workstation

MOCOMForge Pro is an industrial mission operations workstation and software suite conforming to the **CCSDS 522.0-B-1** Recommended Standard (*Mission Operations Common Services*, Issue 1, May 2020\) and **ISO 20215:2020**. It delivers the three indispensable common services required by space mission ground systems, flight software, and payload control centers: **Directory Service**, **Login Service**, and **Configuration Service**, fully decoupled across the **CCSDS 521.0-B-2 Message Abstraction Layer (MAL)**.

---

## Key Capabilities

1. **Dynamic Service Directory & MAL URI Resolver (§3)**:  
     
   - Dynamic service provider registration and lookup across multi-domain ground networks.  
   - Dynamic MAL URI endpoint resolution (`mal://<host>:<port>/services/<service-id>`), removing hardcoded network configs from flight and ground segments.  
   - Built-in failover rerouting for redundant MOC ground station antennas.

   

2. **Operator Login & Role-Based Access Control (RBAC) (§4)**:  
     
   - High-entropy cryptographic session token generation with configurable expiration windows.  
   - Multi-tier role permissions (`FLIGHT_DIRECTOR`, `SPACECRAFT_ENGINEER`, `TELECOMMAND_OPERATOR`, `TELEMETRY_ANALYST`, `GUEST_OBSERVER`).  
   - Granular authorization enforcement gating telecommand uplink and configuration modifications.

   

3. **Configuration Baseline Manager & Instant Rollback (§5)**:  
     
   - Cryptographically hashed, immutable configuration baselines with author metadata and UTC timestamps.  
   - Atomic baseline switching and single-command emergency rollback to previous nominal flight states in \< 50ms.  
   - Automated ternary differential (diff) analysis calculating parameter additions, modifications, and deletions.

   

4. **10-Point Normative Aerospace Compliance Auditor**:  
     
   - Automated audit engine verifying adherence to CCSDS 522.0-B-1 and ISO 20215 clauses (`MOCOM-001` through `MOCOM-010`).  
   - 100% pass rate with instant compliance report generation for flight readiness reviews (FRR).

   

5. **Multi-Interface Workstation Delivery**:  
     
   - **Interactive Web Console (`index.html`)**: Real-time Glass-Cockpit dark UI with interactive directory resolution, login/RBAC manager, and configuration differential viewer.  
   - **Aerospace Python 3 CLI (`mocom_cli.py`)**: Multi-subcommand CLI (`directory`, `login`, `config`, `audit`, `run`) with zero external dependencies.  
   - **Cross-Platform Core Engine (`mocom-engine.js`)**: Pure JavaScript implementation for browser, Node.js, and embedded ground controllers.

---

## Verification & Test Results

- Automated Unit Tests: 10/10 Passed (100.0%)  
- Normative Aerospace Audit: 10/10 Passed (100.0%) \- CCSDS\_522\_0\_MOCOM\_CERTIFIED

---

## Commercial Licensing & Distribution

- **Product Category**: Aerospace Ground Segment / Mission Operations Software  
- **Target Audience**: Satellite operators, defense ground stations, commercial space constellations, MOC software architects (US, UK, UAE, ESA, NASA, ISRO).  
- **Pricing Model**: Commercial Site License (\$18,500/MOC instance) or Enterprise Constellation Subscription (\$4,200/month/constellation).