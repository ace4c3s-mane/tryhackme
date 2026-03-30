
Happen when applications rely on components, libraries, services or models that are compromised, outdated or improperly verified.

These weaknesses are not inherent in my code,, but rather in the software and tools you depend on. 

Attackers exploit these weak links to inject malicious code, bypass security or steal sensitive data.

### Why this matters

Modern applications are built from many third-party packages, APIs and AI models. One compromised dependency can compromise your entire system.

Supply chain attacks can be automated and distributed making them hard to detect and very damaging.

SolarWinds is an example.

**Common Patterns**
- Using unverified or unmaintained libraries and dependencies
- Automatically installing updates without verification
- Over-reliance on third-party AI models without monitoring or auditing
- Insecure build pipelines or CI/CD processes that allow tampering
- Poor license or provenance tracking for components
- Lack of monitoring for vulnerabilities in dependencies after deployment

**How To Protect The Supply Chain**

- Verify all third-party components, libraries, and AI models before use
- Monitor and patch dependencies regularly
- Sign, verify, and audit software updates and packages
- Lock down CI/CD pipelines and build processes to prevent tampering
- Track provenance and licensing for all dependencies
- Implement runtime monitoring for unusual behaviour from dependencies or AI components
- Integrate supply chain threat modelling into the SDLC, including testing, deployment, and update workflows