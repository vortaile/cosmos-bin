# Security Policy

COSMOS is a static malware analysis tool used in digital forensics and incident response. We take the security of the tool and the confidentiality of analyzed samples seriously.

## Supported Versions

| Version | Supported |
|---------|-----------|
| Latest release (v1.1.x) | ✅ |
| Older releases | ❌ - upgrade to the latest version |

## Security Properties

- **Offline by default**: COSMOS performs static analysis entirely on the local machine. Sample files are never uploaded to third-party servers unless the analyst explicitly enables the optional VirusTotal integration and provides an API key.
- **No telemetry**: COSMOS does not collect usage statistics, analytics, or personal information.
- **Local data only**: Runtime data (audit logs, VirusTotal cache) is stored under the user profile directory (`~/.cosmos/`) and never transmitted.
- **Chain of custody**: Every analysis writes an immutable JSON Lines audit trail with file hashes before and after analysis, supporting forensic integrity verification.

## Reporting a Vulnerability

If you discover a security vulnerability in COSMOS, please report it privately rather than opening a public issue.

**How to report:**

1. Do not include sample files or other sensitive data in the initial message.
2. Describe the vulnerability, the affected version, and a proof of concept (if available).
3. Send details to the maintainer via the private security channel associated with the project.

**What to include:**

- COSMOS version and operating system
- Type of vulnerability (e.g., arbitrary code execution, path traversal, denial of service)
- Steps to reproduce
- Impact assessment

## Handling Process

1. The report is acknowledged within 5 business days.
2. The issue is investigated and a fix is prepared.
3. A patched release is published, and the vulnerability is disclosed responsibly.

## Safe Handling of Malware Samples

COSMOS is designed to analyze potentially malicious files. Always operate within an isolated analysis environment (dedicated VM or air-gapped machine) when handling live malware. Never open exported report links from untrusted sources without IOC defanging awareness.
