# COSMOS - Comprehensive Offline Static Malware Observation System

**Prebuilt binaries for Linux and Windows.**

COSMOS is a desktop application for static forensic analysis of Windows Portable Executable (PE) files. It performs deep analysis entirely offline, ensuring sample confidentiality by never uploading suspicious files to third-party servers. COSMOS is designed for security analysts, malware researchers, and digital forensics investigators performing initial triage during incident response.

## Why COSMOS

| Problem | COSMOS Solution |
|---------|----------------|
| Cloud sandboxes expose samples to third parties | Fully offline analysis, samples never leave the analyst's machine |
| Manual analysis is slow and error-prone | Automated 11-stage pipeline covering hash, PE structure, entropy, strings, IoC, YARA, and more |
| Scattered results are hard to interpret | Unified *Verdict Engine* scoring 0-100 with 4 risk levels |
| Analysts need portable tools on incident sites | Single-file portable executable, no installation, no admin rights |

## Features

- **Multi-algorithm hashing**: MD5, SHA-1, SHA-256, SHA-384, SHA-512, imphash
- **Authenticode signature verification**: certificate chain validation for signed binaries
- **PE structure parsing**: DOS/NT headers, sections, imports, exports, resources, TLS callbacks
- **Entropy analysis**: per-section Shannon entropy to detect packing and obfuscation
- **String extraction**: ASCII and Unicode strings with length filtering
- **IOC detection**: IP addresses, URLs, domains, emails, registry keys, file paths with confidence scoring
- **YARA scanning**: 500+ built-in rules covering APT groups, ransomware, exploit kits, webshells, and packers
- **Threat intelligence integration**: optional VirusTotal lookup with rate limiting and local caching
- **Verdict Engine**: weighted heuristic penalty scoring producing a 0-100 risk score and 4 classification levels (CLEAN, LOW, SUSPICIOUS, MALICIOUS)
- **MITRE ATT&CK mapping**: technique identification and Cyber Kill Chain phase classification
- **Chain of custody audit log**: immutable JSON Lines audit trail (ANALYSIS_START, HASH_BEFORE, HASH_AFTER, VERDICT) with integrity verification
- **Report export**: JSON, HTML, PDF, CSV ZIP, and TXT formats with IOC defanging
- **Modern dark-theme GUI**: 4-tab workflow (File Identity, PE Structure, Content Analysis, Verdict Report) with hex viewer

## System Requirements

| Platform | Requirement |
|----------|-------------|
| **Windows** | Windows 10/11 x64, no Python or dependencies required |
| **Linux** | x86_64 with glibc 2.28+, no Python or dependencies required |

## Quick Start

1. Download the binary matching your operating system from [Releases](https://github.com/vortaile/cosmos-bin/releases)
2. Run it directly (portable, single-file, no installation)
3. Drag and drop a `.exe` or `.dll` file onto the welcome screen, or use **Open PE File**
4. Review the analysis across the 4 tabs and export the report

## Usage Examples

```
# Linux (make executable first)
chmod +x Cosmos_Analyzer
./Cosmos_Analyzer

# Windows
Cosmos_Analyzer.exe
```

## Release Notes

| Version | Date | Highlights |
|---------|------|------------|
| v1.1.4 | 2026-07-31 | Stable GUI on Windows & Linux; fixed windowed-mode crash; dark titlebar theming; automatic CI releases |

## Verify Integrity

Always verify the SHA-256 checksum before running (optional but recommended):

```
# Linux
sha256sum Cosmos_Analyzer

# Windows
certutil -hashfile Cosmos_Analyzer.exe SHA256
```

Checksums are published alongside each release.

## License

See the LICENSE file in this repository.

---

*COSMOS - static analysis you can trust, offline.*
