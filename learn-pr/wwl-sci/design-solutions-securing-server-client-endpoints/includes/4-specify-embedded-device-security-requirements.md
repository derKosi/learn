IoT devices and embedded systems present unique security challenges that differ significantly from traditional endpoints. These devices often run specialized firmware, operate in physically exposed environments, and connect networks that were historically isolated. Security architects must specify requirements that address the constraints of resource-limited devices while protecting critical infrastructure.

## Establish a threat model foundation

Security requirements for IoT and embedded systems should begin with threat modeling. Understanding how attackers target these devices helps you specify appropriate controls. The STRIDE framework—spoofing, tampering, repudiation, information disclosure, denial of service, and elevation of privilege—provides a structured approach for identifying threats across IoT architecture zones.

Divide your IoT architecture into security zones:

- **Device zone**: Physical devices and their immediate environment
- **Gateway zone**: Edge devices that aggregate and process data locally
- **Cloud zone**: Cloud-based services for data processing and management
- **Operations zone**: User interfaces and management systems

Each zone requires specific authentication, authorization, and data protection requirements. Use zones to isolate damage and restrict the impact of compromised components.

## Specify device identity requirements

Strong device identity forms the foundation of IoT security. Unlike user authentication, device identity must operate autonomously without human interaction.

**Hardware root of trust**: Require devices to include hardware security modules (HSM) or trusted platform modules (TPM) that:

- Store cryptographic credentials in tamper-resistant hardware
- Provide immutable onboarding identity tied to the physical device
- Support unique per-device renewable operational credentials

**Authentication mechanisms**: Specify passwordless authentication using X.509 certificates as the primary method:

- Provision operational certificates from a trusted public key infrastructure (PKI)
- Configure automatic certificate renewal to prevent service disruption
- Support certificate revocation lists (CRL) to immediately disable compromised devices
- Require TLS 1.2 or higher for all device-to-cloud communications

**Device registry**: Require a centralized organizational IoT device registry to:

- Manage device lifecycle from provisioning through decommissioning
- Track device health, patch status, and security state
- Enable query-based grouping for scaled operations and access control

For legacy devices that cannot support strong identity, require IoT gateways to act as guardians. The gateway authenticates to cloud services on behalf of less-capable devices while enforcing security policies locally.

## Define network security requirements

Network design for IoT environments must assume devices can be compromised. Specify requirements that limit lateral movement and contain potential breaches.

**Network segmentation**: Require micro-segmentation that isolates IoT devices based on:

- Risk exposure and criticality of connected systems
- Traffic patterns and communication requirements
- Trust level and security capabilities of devices

For operational technology (OT) environments, require alignment with the Purdue model (ISA-95) to separate process control networks from enterprise IT networks. This provides layers of defense between physical processes and external threats.

**Firewall requirements**: Specify next-generation firewall rules that:

- Allow only required device-to-cloud communications
- Block unauthorized lateral traffic between devices
- Monitor for anomalous traffic patterns that indicate compromise

**Air-gapped considerations**: For environments requiring complete network isolation, specify:

- Physical separation from enterprise and internet networks
- Local sensor deployment for threat detection
- Secure processes for applying updates without network connectivity

## Specify threat detection and monitoring

Continuous monitoring is essential for detecting threats in IoT environments, particularly for legacy devices that cannot run security agents.

**Network-based detection**: Require agentless network sensors that:

- Perform continuous asset discovery to identify all connected devices
- Detect deviations from baseline behavior using machine learning
- Monitor industrial protocols (Modbus, OPC-UA, BACnet) for anomalies
- Generate alerts for unauthorized configuration changes

Microsoft Defender for IoT provides these capabilities through OT network sensors that connect to SPAN ports or network TAPs. The sensors use deep packet inspection to detect threats without installing agents on devices.

**Device health evaluation**: Specify ongoing assessment that includes:

- Security configuration verification
- Vulnerability scanning for known exploits
- Credential strength evaluation (certificate validity, TLS versions)
- Behavioral anomaly detection

**Integration requirements**: Require threat data to integrate with:

- Security information and event management (SIEM) systems
- Security orchestration and automated response (SOAR) platforms
- Conditional access policies for automated response

## Define update management requirements

Devices that cannot receive security updates become permanent vulnerabilities. Specify update mechanisms that support the full device lifecycle.

**Update capabilities**: Require devices to support:

- Over-the-air (OTA) firmware updates with cryptographic verification
- Rollback capability to recover from failed updates
- Staged rollout with validation before broad deployment

**Update policies**: Specify requirements for:

- Maximum time from vulnerability disclosure to patch deployment
- Automatic flagging of devices that fail to update
- Compliance gates that restrict access for unpatched devices

**End-of-life planning**: Require documentation of:

- Supported device lifetime with committed security updates
- Decommissioning procedures for devices reaching end of support
- Replacement timelines for devices that cannot be updated

## Apply zero-trust principles

Zero-trust architecture assumes breach and requires verification for every access request. Adapt these principles for IoT constraints.

**Zero-trust device requirements**:

| Requirement | Purpose |
| --- | --- |
| Hardware root of trust | Provides verifiable device identity |
| Renewable credentials | Enables revocation of compromised devices |
| Least-privileged access | Limits device permissions to required functions |
| Device health signals | Enables conditional access decisions |
| Update mechanisms | Maintains device security posture |
| Security telemetry | Supports threat detection and response |

**Conditional access**: Require policies that evaluate device context before granting access:

- Device compliance status from management systems
- Risk signals from threat detection sensors
- Location and network context
- Time-based access restrictions

**Least-privileged access**: Specify controls that:

- Limit device access to only required cloud endpoints
- Restrict local device capabilities (disable unused ports, disable unnecessary services)
- Enforce just-in-time access for administrative operations

## Design considerations for architects

When specifying IoT and embedded security requirements, consider:

**Device constraints**: Many IoT devices have limited processing power, memory, and storage. Requirements must account for devices that cannot run full security agents or support complex cryptographic operations.

**Operational continuity**: Industrial and OT environments prioritize availability. Security controls must not disrupt critical processes. Plan for maintenance windows and gradual rollouts.

**Legacy equipment**: Many organizations have brownfield deployments with devices designed before current security standards. Compensating controls through network monitoring and gateway-based protection may be necessary.

**Supply chain security**: Require verification of device integrity from manufacturing through deployment. Specify secure boot requirements and tamper-evident packaging for physical security.

**Compliance alignment**: Map requirements to relevant standards like IEC 62443 for industrial automation, NIST guidelines for IoT security, and industry-specific frameworks like NERC CIP for energy sector OT systems.
