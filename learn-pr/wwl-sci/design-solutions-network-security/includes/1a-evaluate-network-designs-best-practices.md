As a security architect, you evaluate whether network designs meet your organization's security requirements and align with industry best practices. Rather than building networks from scratch, you assess existing or proposed architectures to identify gaps, recommend improvements, and ensure alignment with frameworks like Zero Trust.

## Evaluate network designs against Zero Trust principles

Zero Trust is the foundational framework for evaluating modern network security designs. Traditional perimeter-based networks assume that all systems inside the boundary can be trusted. This assumption fails when employees access resources from anywhere and attackers who breach the perimeter can move laterally across the network.

When you evaluate a network design, assess whether it enforces these three Zero Trust principles:

- **Verify explicitly** — Does the design authenticate and authorize every access request based on all available signals, including user identity, device health, location, and workload context?
- **Use least privilege access** — Does the design limit access to only necessary resources, using just-in-time and just-enough-access approaches?
- **Assume breach** — Does the design minimize blast radius through segmentation and verify end-to-end encryption, with analytics for visibility and threat detection?

A network design that relies solely on perimeter firewalls and VPN access doesn't align with these principles. Instead, look for designs that incorporate identity-aware controls, microsegmentation, and continuous verification at every network boundary.

## Use Microsoft cloud security benchmark v2 as evaluation criteria

The [Microsoft cloud security benchmark (MCSB) v2](/security/benchmark/azure/overview) provides a structured set of controls you can use as evaluation criteria for network designs. The Network Security (NS) control family maps directly to the areas a security architect should assess:

| Control | Evaluation focus |
|---|---|
| **NS-1**: Establish network segmentation boundaries | VNet segmentation, NSGs, ASGs, subnet isolation |
| **NS-2**: Secure cloud native services with network controls | Private endpoints, disabled public access, VNet integration, Network Security Perimeter |
| **NS-3**: Deploy firewall at the edge of enterprise network | Azure Firewall, edge filtering, user-defined routes |
| **NS-4**: Deploy intrusion detection/intrusion prevention systems (IDS/IPS) | Azure Firewall Premium IDPS, host-based EDR |
| **NS-5**: Deploy DDoS protection | Azure DDoS Protection tiers on internet-facing VNets |
| **NS-6**: Deploy web application firewall | Azure WAF on Application Gateway or Front Door |
| **NS-7**: Manage network security centrally and effectively | Azure Virtual Network Manager Security Admin Rules, Firewall Manager, flow logs v2, Traffic Analytics |
| **NS-8**: Detect and disable insecure services and protocols | Microsoft Sentinel insecure protocol detection |
| **NS-9**: Connect on-premises or cloud network privately | ExpressRoute, VPN, VNet peering |
| **NS-10**: Ensure Domain Name System (DNS) security | Azure Private DNS, Defender for DNS (included in Defender for Servers Plan) |

Each MCSB v2 control also maps to industry frameworks such as CIS Controls v8.1, NIST SP 800-53 r5, PCI-DSS v4, NIST CSF v2.0, ISO 27001:2022, and SOC 2, helping you align your evaluation to regulatory and compliance requirements. When you evaluate a network design, use these controls as a checklist to identify gaps and prioritize remediation.

## Evaluate segmentation and traffic control

Effective network segmentation is a core security requirement and aligns to MCSB v2 control NS-1. When evaluating a network design, determine whether it isolates workloads appropriately and controls traffic flow between segments.

### Network segmentation layers

Azure provides multiple segmentation options that create layers of isolation. Evaluate whether the design uses them effectively:

- **Subscriptions** separate organizational units and provide platform-level isolation between environments such as production, development, and testing.
- **Virtual networks (VNets)** provide network-level containment, with no traffic allowed between VNets by default — communication must be explicitly provisioned.
- **Subnets** with **network security groups (NSGs)** create granular perimeters within a VNet. Evaluate whether NSG rules follow the principle of least privilege, with only required traffic allowed between subnets.
- **Application security groups (ASGs)** simplify rule management by grouping VMs by application role, reducing rule complexity and the risk of misconfiguration.

### Hub-and-spoke topology

For most enterprise environments, evaluate whether the design uses a hub-and-spoke model. In this pattern, a central hub VNet hosts shared security services like Azure Firewall, and spoke VNets contain workloads. All traffic between spokes and to the internet routes through the hub. This design provides:

- Centralized security policy enforcement
- Consistent logging and monitoring at the hub
- Reduced security posture management overhead as the network grows

When the hub-and-spoke model is in place, verify that traffic between spokes is denied by default and only permitted paths are configured through the firewall.

## Evaluate defense-in-depth controls

A strong network design applies defense-in-depth by layering multiple security controls. MCSB v2 controls NS-3 through NS-6 define the specific controls to evaluate at each layer.

### Azure Firewall

[Azure Firewall](/azure/firewall/overview) is a cloud-native, stateful firewall as a service. It provides centralized network and application rule enforcement across VNets and subscriptions. When evaluating, check whether the design:

- Uses Azure Firewall as the central egress and east-west filtering point in a hub VNet
- Leverages Azure Firewall Premium features such as TLS inspection and intrusion detection and prevention system (IDPS) for environments that require deep packet inspection
- Integrates with Azure Firewall Manager to centrally manage policies across multiple firewalls

### Azure Web Application Firewall

For designs that include web-facing applications, evaluate whether [Azure Web Application Firewall (WAF)](/azure/web-application-firewall/overview) protects against Layer 7 attacks. WAF is available through Azure Application Gateway for regional workloads and through Azure Front Door for global workloads. Verify that the design uses managed rule sets aligned with OWASP top threats, rate limiting, and bot protection.

### Azure DDoS Protection

Evaluate whether the design enables Azure DDoS Protection on perimeter virtual networks that have internet-facing endpoints. Azure DDoS Protection automatically tunes to help protect your specific Azure resources and provides layer 3 and layer 4 mitigation. For web application protection at layer 7, WAF provides complementary defense.

There are two tiers to consider:

- **DDoS IP Protection** — Protects specific public IP addresses; suited for smaller or targeted deployments.
- **DDoS Network Protection** — Covers entire virtual networks with advanced mitigation, analytics, and integration for larger enterprise environments.

## Evaluate private connectivity and reduced exposure

MCSB v2 controls NS-2 and NS-9 address private connectivity. A key evaluation criterion is whether the design minimizes the attack surface by reducing exposure to the public internet.

### Azure Private Link and private endpoints

Evaluate whether the design uses [Azure Private Link](/azure/private-link/private-link-overview) to access Azure PaaS services like Azure Storage and Azure SQL Database over private endpoints within the virtual network. This approach:

- Removes public internet access to service resources
- Keeps traffic on the Microsoft Azure backbone network
- Protects against data exfiltration by mapping a private endpoint to a specific resource instance rather than the entire service

For a security architect, the presence of private endpoints in a design is a strong indicator of least-exposure principles.

### Azure Bastion for secure remote access

Evaluate how the design handles administrative access to virtual machines. Designs that expose RDP or SSH ports directly to the internet present significant risk. Azure Bastion provides secure RDP/SSH connectivity through the Azure portal over TLS, without requiring public IP addresses on VMs. Check that the design uses Azure Bastion and combines it with just-in-time VM access in Microsoft Defender for Cloud to limit when ports are open.

### Hybrid connectivity

For hybrid environments, evaluate whether the design avoids sending sensitive traffic over the public internet. Azure ExpressRoute provides dedicated, private WAN connectivity between on-premises networks and Azure. Verify that the design uses ExpressRoute for sensitive or high-bandwidth workloads and that it terminates at the appropriate point relative to the perimeter firewall.

## Evaluate identity-aware network security with Global Secure Access

Microsoft's Security Service Edge (SSE) solution — comprising Microsoft Entra Internet Access and Microsoft Entra Private Access under the unified [Global Secure Access](/entra/global-secure-access/overview-what-is-global-secure-access) platform — extends security controls beyond the traditional network perimeter with identity-centric network security.

Global Secure Access integrates with Microsoft Entra Conditional Access to enforce policies based on user identity, device compliance, location, and risk level at the network layer. This approach aligns with Zero Trust by verifying explicitly at the point of access.

When evaluating a design that includes Global Secure Access, assess whether:

- **Traffic forwarding profiles** are configured to route Microsoft 365 traffic, internet traffic, and private application traffic through the appropriate security controls
- **Web content filtering** policies restrict access to risky or inappropriate web categories
- **Conditional Access policies** are linked to security profiles to enforce identity-aware access decisions on network traffic

## Evaluate network monitoring and posture management

A network design is incomplete without continuous visibility and monitoring. MCSB v2 controls NS-7 and NS-8 emphasize centralized network security management and detecting insecure protocols. Evaluate whether the design includes:

- **Microsoft Defender for Cloud** networking recommendations and the interactive network map for visualizing topology, identifying unprotected resources, and surfacing risk-based recommendations.
- **Azure Network Watcher** tools such as NSG flow logs, packet capture, and Traffic Analytics for real-time and historical analysis of traffic patterns.
- **Centralized logging** that sends firewall, NSG flow, and DDoS diagnostic logs to Azure Monitor or Microsoft Sentinel.

Without monitoring, security gaps in the network design go undetected, reducing the effectiveness of the security controls in place.

## Learn more

- [Zero Trust security overview](/security/zero-trust/zero-trust-overview)
- [Microsoft cloud security benchmark v2 — Network Security controls](/security/benchmark/azure/mcsb-v2-network-security)
- [Azure network security best practices](/azure/security/fundamentals/network-best-practices)
- [Azure Firewall Premium features](/azure/firewall/premium-features)
- [Azure DDoS Protection overview](/azure/ddos-protection/ddos-protection-overview)
- [Azure Web Application Firewall overview](/azure/web-application-firewall/overview)
- [Azure Private Link overview](/azure/private-link/private-link-overview)
- [Azure Bastion overview](/azure/bastion/bastion-overview)
- [Global Secure Access overview](/entra/global-secure-access/overview-what-is-global-secure-access)
- [Secure networks with Zero Trust](/security/zero-trust/deploy/networks)
