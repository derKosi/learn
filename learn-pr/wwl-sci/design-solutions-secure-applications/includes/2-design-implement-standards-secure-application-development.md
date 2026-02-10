As a cybersecurity architect, one of your most impactful responsibilities is defining the standards and practices that development teams follow to build secure software. Without clear standards, security becomes inconsistent across projects, vulnerabilities accumulate as technical debt, and remediation costs increase dramatically when issues are discovered late in the development process.

This unit covers two complementary frameworks: the Microsoft Security Development Lifecycle (SDL), which provides 10 key security practices for integrating security into development, and the Microsoft Cloud Security Benchmark (MCSB) DevOps Security controls, which provide specific technical guidance for securing the development pipeline.

## Microsoft Security Development Lifecycle (SDL) practices

The Microsoft SDL is a set of practices and tools that help organizations build more secure software. It has evolved over 20 years at Microsoft and continues to adapt as the threat landscape changes. The SDL integrates security into each stage of the development process, following a continuous improvement model rather than a one-time assessment.

Security risks can occur at any point in the development lifecycle. During design, insecure architecture can give attackers easy access. During coding, vulnerabilities can allow unauthorized control of applications. During build and deployment, compromised continuous integration and continuous delivery (CI/CD) processes can alter code. During runtime, misconfigured environments expose workloads. The SDL addresses all of these stages through 10 key practices.

### The 10 SDL practices

1. **Establish security standards, metrics, and governance.** Define clear security requirements and measure compliance across the organization. As an architect, you set the bar for what "secure enough" means and create the accountability structures to enforce it.
2. **Require use of proven security features, languages, and frameworks.** Mandate the use of approved, security-validated libraries and frameworks. Maintain an approved and prohibited list, and enforce it through pipeline guardrails.
3. **Perform security design review and threat modeling.** Require threat modeling during the design phase using the STRIDE methodology and data flow diagrams. Identify threats before development begins when remediation is cheapest.
4. **Define and use cryptography standards.** Establish organizational standards for encryption algorithms, key lengths, and key management processes. Prohibit deprecated algorithms such as DES and MD5.
5. **Secure the software supply chain.** Verify provenance and integrity of all third-party components. Generate Software Bill of Materials (SBOM) documents and continuously scan dependencies for known vulnerabilities.
6. **Secure the engineering environment.** Protect developer workstations, build agents, and source code repositories with the same rigor as production systems. Enforce network segmentation, identity controls, and vulnerability scanning on these systems.
7. **Perform security testing.** Integrate both Static Application Security Testing (SAST) and Dynamic Application Security Testing (DAST) into CI/CD pipelines. Combine automated scanning with manual penetration testing for high-risk applications.
8. **Ensure operational platform security.** Apply security baselines and hardening configurations to environments where applications run. Follow the principle of least privilege for all runtime identities.
9. **Implement security monitoring and response.** Enable comprehensive logging and monitoring across development and production environments. Forward security events to a centralized Security Information and Event Management (SIEM) platform for correlation and alerting.
10. **Provide security training.** Require developers to complete formal training on secure coding practices. Establish a Security Champions program with designated, trained security facilitators in each development team.

As an architect, your role is to determine which of these practices are mandatory for your organization, define how they're enforced, and establish the governance structure that sustains them over time.

## MCSB DevOps Security controls

The Microsoft Cloud Security Benchmark (MCSB) DevOps Security family provides seven specific controls that map to the SDL practices and offer detailed implementation guidance for Azure and GitHub environments.

### DS-1: Conduct threat modeling

Implement STRIDE-based threat modeling as a mandatory design-phase activity. Create data flow diagrams (DFDs) that map system components, data flows, trust boundaries, and external dependencies. For each component and data flow, systematically evaluate threats across all six STRIDE categories: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege. Use the Microsoft Threat Modeling Tool for consistency and integrate threat model outputs into Azure DevOps work items with clear ownership and acceptance criteria.

### DS-2: Secure the software supply chain

Implement dependency scanning and management that covers both direct and transitive dependencies. Generate SBOM documents in industry-standard formats (SPDX, CycloneDX). Use tools like GitHub Advanced Security with Dependabot for automated vulnerability detection and pull request-based remediation. Configure Azure Artifacts with signature verification and dependency pinning to prevent confusion attacks and unauthorized package substitution. Extend visibility to deployed environments using Microsoft Defender for Cloud DevOps Security for code-to-cloud traceability.

### DS-3: Secure the DevOps infrastructure

Centralize secrets management using Azure Key Vault. Configure pipelines to retrieve secrets dynamically at runtime through managed identities or workload identity federation, eliminating hardcoded credentials. Enforce just-in-time access with approval gates for production deployments. Harden self-hosted build agents with network isolation. Integrate infrastructure-as-code (IaC) security scanning to prevent deployment of misconfigured resources.

### DS-4: Integrate Static Application Security Testing (SAST)

Deploy multiple specialized SAST scanners because no single tool detects all vulnerability classes. Use GitHub CodeQL for semantic code analysis that identifies complex vulnerabilities like SQL injection through multiple function calls. Configure secret scanning with push protection to block credential exposure at commit time. Establish severity-based quality gates that prevent merge of critical findings. The Microsoft Security DevOps Extension can orchestrate scanners including Bandit, BinSkim, Checkov, ESLint, Template Analyzer, Terrascan, and Trivy through a single pipeline task.

### DS-5: Integrate Dynamic Application Security Testing (DAST)

Complement SAST with runtime testing in pre-production staging environments that mirror production architecture. Focus on high-risk attack surfaces: API authentication bypasses, authorization failures, session management vulnerabilities, and business logic flaws. For containerized workloads, implement continuous runtime monitoring with Microsoft Defender for Containers, combining pre-deployment image scanning with post-deployment behavioral analysis.

### DS-6: Secure the workload lifecycle

Treat container and VM images as critical artifacts requiring immutable infrastructure practices. Use minimal base images with multi-stage builds. Integrate automated vulnerability scanning with quarantine policies that prevent deployment of images with critical CVEs. Enforce cryptographic signing and verification to prevent image substitution attacks. Use Azure Container Registry with Microsoft Defender for Containers for integrated scanning and content trust.

### DS-7: Implement DevOps logging and monitoring

Capture all security-relevant DevOps activities: authentication events, code commits, pipeline modifications, deployment executions, secret access, and permission changes. Forward audit logs in real-time to Microsoft Sentinel for long-term forensic analysis and correlation with security events from other systems. Implement behavioral analytics to detect suspicious patterns such as after-hours pipeline modifications, unusual secret access, and privilege escalations.

## Architect design considerations

When implementing these standards, consider these architectural decisions:

- **Enforcement vs. guidance.** Determine which controls block pipeline execution versus which generate alerts. Critical and high-severity findings typically warrant blocking gates, while medium and low findings are advisory.
- **Centralized vs. federated scanning.** Decide whether security scanning uses organizational-level pipeline templates (ensuring consistency) or team-managed configurations (allowing flexibility). Centralized templates require governance processes for exceptions.
- **Risk-based tiering.** Classify applications by data sensitivity, external exposure, and regulatory scope. Align the depth and rigor of security controls to each tier.
- **Developer experience.** Security controls that significantly slow development velocity get bypassed. Optimize scan times, provide clear remediation guidance, and integrate findings directly into pull request comments.


