# Enterprise SIEM Deployment & Endpoint Security Monitoring (Wazuh SIEM Lab)

## Project Overview
Engineered and deployed an on-premises Security Information and Event Management (SIEM) environment to monitor endpoint telemetry, execute baseline configuration audits, and detect adversarial authentication activity in real time.

## Technical Architecture & Tools
* **SIEM Platform:** Wazuh Manager v4.14.7 & Wazuh Indexer / Dashboards
* **Virtualization:** Oracle VM VirtualBox (Bridged Subnet Routing)
* **Monitored Endpoint:** Windows 11 Enterprise / Home (`Windows-Host`, Agent ID `002`)
* **Automation & Scripting:** Windows PowerShell CLI
* **Compliance Standards:** CIS Microsoft Windows 11 Enterprise Benchmark v3.0.0

## Key Milestones & Implementation

### 1. Virtual Infrastructure & Network Engineering
* Deployed the Wazuh virtual appliance within Oracle VM VirtualBox.
* Migrated hypervisor networking from standard NAT to a Bridged Adapter interface (`10.0.0.189`), ensuring bidirectional host-to-manager routing over TCP port 1514 without network address translation conflicts.
* Enrolled the local Windows host via the Wazuh Agent daemon, establishing continuous keep-alive telemetry reporting to `node01`.

### 2. IT Hygiene & Security Configuration Assessment (SCA)
* Conducted an automated configuration audit evaluating the endpoint against 482 system hardening checks defined by the CIS Microsoft Windows 11 Enterprise Benchmark v3.0.0.
* Assessed local security policies (`secedit`), registry baselines, and account lockouts, recording 125 Passed rules, 348 Failed baseline deviations, and 9 Not Applicable checks to prioritize system remediation.

### 3. Threat Hunting & Real-Time Telemetry Ingestion
* Developed PowerShell simulation routines to trigger security event logging on the monitored endpoint.
* Ingested Windows Event ID 4625 (Logon failure: Unknown user name or bad password) mapped to Wazuh Rule 60122 (Level 5).
* Validated live event indexing and query analysis within Wazuh Threat Hunting dashboards, confirming end-to-end detection pipeline integrity.

## Verification Artifacts
* Agent status: `Active (1)`, `Disconnected (0)`
* CIS Benchmark compliance run completed across 482 rule checks
* Real-time event capture logged with user context (`FakeUser`), host IP (`10.0.0.9`), and manager ingestion (`10.0.0.189`)
