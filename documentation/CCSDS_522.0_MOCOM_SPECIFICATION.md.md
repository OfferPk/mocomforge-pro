# CCSDS 522.0-B-1 & ISO 20215 Mission Operations Common Services Specification

## Executive Summary

This document provides the technical architecture and protocol specification for **MOCOMForge Pro**, an industrial workstation implementation of the **Consultative Committee for Space Data Systems (CCSDS) 522.0-B-1** Recommended Standard (Blue Book, Issue 1, May 2020\) and **ISO 20215:2020** *Mission Operations Common Services (MO-CS / MOCOM)*.

CCSDS Common Services define three core foundational service capabilities required by all space mission ground systems, flight software, and payload control centers:

1. **Directory Service (§3)**: Service discovery, provider capability registration, and dynamic Message Abstraction Layer (MAL) URI endpoint resolution.  
2. **Login Service (§4)**: Operator identity management, session token generation, and multi-tier Role-Based Access Control (RBAC).  
3. **Configuration Service (§5)**: Configuration baseline snapshotting, atomic baseline activation, rollback protection, and differential (diff) analysis.

---

## 1\. Architectural Model & Layer Decoupling

\+-------------------------------------------------------------------------+

\|                  Mission Application & Control Layer                    \|

\|       (Payload Operations, Telemetry Displays, Flight Dynamics)         \|

\+-------------------------------------------------------------------------+

                                    \|

\+-----------------------------------+-------------------------------------+

\|        CCSDS 522.0-B-1 Mission Operations Common Services (MO-CS)       \|

\|  \+--------------------+  \+--------------------+  \+--------------------+ \|

\|  \|  Directory Service \|  \|    Login Service   \|  \|Configuration Svc   \| \|

\|  \|  (Dynamic Binding) \|  \|   (RBAC & Auth)    \|  \|  (Baselines/Diff)  \| \|

\|  \+--------------------+  \+--------------------+  \+--------------------+ \|

\+-------------------------------------------------------------------------+

                                    \|

\+-------------------------------------------------------------------------+

\|                Message Abstraction Layer (MAL) CCSDS 521.0              \|

\|        (Request-Response, Submit, Pub-Sub, Progress, Invoke)            \|

\+-------------------------------------------------------------------------+

                                    \|

\+-----------------------------------+-------------------------------------+

\|                 Transport & Data Link Layer Bindings                    \|

\|         MAL-TCP/IP  \|  MAL-SpacePacket  \|  MAL-ZMQ  \|  MAL-WebSockets   \|

\+-------------------------------------------------------------------------+

### 1.1 MAL Decoupling

By decoupling operational services from point-to-point network topology, MOCOM eliminates hardcoded IP addresses and ports across ground stations, Mission Operations Centers (MOC), and Science Operations Centers (SOC).

---

## 2\. Directory Service Specification (CCSDS 522.0 §3)

### 2.1 Service Key and Endpoint Resolution

Every flight and ground service registers its provider capability under an authoritative Service Key:

- Format: `DOM_A.DOM_B.SERVICE_NAME`  
- Target: `mal://<host-or-spacecraft>:<port>/services/<service-id>`

### 2.2 Dynamic Failover & Redundancy

When primary ground equipment experiences degradation, the Directory Service updates the URI endpoint mapping. Clients querying the Directory Service automatically route subsequent MAL operations to the active redundant host without service interruption or software restarts.

---

## 3\. Login Service & Session RBAC Specification (CCSDS 522.0 §4)

### 3.1 Authentication Handshake

- Operator submits credentials over authenticated channel.  
- The Login Service verifies cryptographic hashes and generates a high-entropy session token: `MOC_TOK_<HEX_HASH>`  
- Tokens feature UTC expiration timestamps and explicit revocation boundaries.

### 3.2 Role-Based Access Control (RBAC) Matrix

| Operator Role | Read Telemetry | Acknowledge Alarms | Telecommand Uplink | Configuration Modification | Service Administration |
| :---- | :---: | :---: | :---: | :---: | :---: |
| **FLIGHT\_DIRECTOR** | ✓ | ✓ | ✓ | ✓ | ✓ |
| **SPACECRAFT\_ENGINEER** | ✓ | ✓ | ✓ | ✓ | ✗ |
| **TELECOMMAND\_OPERATOR** | ✓ | ✓ | ✓ | ✗ | ✗ |
| **TELEMETRY\_ANALYST** | ✓ | ✓ | ✗ | ✗ | ✗ |
| **GUEST\_OBSERVER** | ✓ | ✗ | ✗ | ✗ | ✗ |

---

## 4\. Configuration Service Specification (CCSDS 522.0 §5)

### 4.1 Immutable Baselines

A Configuration Baseline is a cryptographically versioned snapshot of flight parameters (e.g., transmitter power levels, heater setpoints, telemetry sampling rates, attitude control gains).

### 4.2 Safe Activation and Atomic Rollback

- **Pre-Activation Validation**: Validates all parameter types and engineering bounds before applying.  
- **Rollback Pointer**: The system preserves the immediate predecessor configuration. If subsystem anomalies occur during re-configuration, the operator triggers an emergency rollback restoring nominal state in \< 50 milliseconds.

### 4.3 Differential (Diff) Analysis

Computes ternary delta sets between any two baselines:

- `ADDED`: New parameters present in target baseline.  
- `MODIFIED`: Changed values with before/after delta tracking.  
- `DELETED`: Deprecated parameters removed from baseline.