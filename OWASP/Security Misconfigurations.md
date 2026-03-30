
It happens when systems, servers or applications are deployed with unsafe defaults, incomplete settings or exposed services. 

There are not code bugs but mistakes in how the environment, software or network is set up.

An example is the Uber. It exposed a backup AWS S3 bucket with sensitive user data, including driver and rider information because the bucket was publicly available.


#### Common Patterns

- Default creds or weak passwords left unchanged.
- Unnecessary services or endpoints exposed to the internet.
- Misconfigured cloud storage or permissions (s3 bucket, Azure Blob, GCP buckets)
- Unrestricted API access or missing authentication/authorisation.
- Verbose error messages exposing stack traces of system details.
- Outdated software, frameworks, or containers with known vulnerabilities.
- Exposed AI/ML endpoints without proper access controls.

**How To Prevent It**

- Harden default configurations and remove unused features or services
- Enforce strong authentication and least privilege across all systems
- Limit network exposure and segment sensitive resources
- Keep software, frameworks, and containers up to date with patches
- Hide stack traces and system information from error messages
- Audit cloud configurations and permissions regularly
- Secure AI endpoints and automation services with proper access controls and monitoring
- Integrate configuration reviews and automated security checks into your deployment pipeline