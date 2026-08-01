# COSMOS

**Static Malware Analysis for Windows PE Files**

COSMOS is a desktop application for static forensic analysis of Windows Portable Executable (PE) files. It runs fully offline, so samples are never uploaded to third-party servers. Built for security analysts, malware researchers, and digital forensics investigators performing initial triage.

## Features

- **Hash computation**: MD5, SHA-1, SHA-256, SHA-384, SHA-512, and imphash
- **Signature verification**: magic byte validation and Authenticode certificate chain checks
- **PE structure parsing**: DOS/NT headers, sections, imports, exports, resources, and TLS callbacks
- **Entropy analysis**: per-section Shannon entropy to detect packing and obfuscation
- **String extraction**: ASCII and Unicode strings with length filtering
- **Indicator of Compromise detection**: IPs, URLs, domains, emails, registry keys, and file paths with confidence levels
- **YARA scanning**: 500+ bundled rules covering APT groups, ransomware, exploit kits, webshells, and packers
- **Threat intelligence integration**: optional VirusTotal lookup with rate limiting and local caching
- **Verdict engine**: weighted heuristic scoring from 0 to 100 with four risk levels (CLEAN, LOW, SUSPICIOUS, MALICIOUS)
- **MITRE ATT&CK mapping**: technique identification and Cyber Kill Chain phase classification
- **Audit trail**: immutable JSON Lines chain-of-custody log with before and after file hashes
- **Report export**: JSON, HTML, PDF, CSV ZIP, and TXT with IOC defanging
- **Dark GUI**: four-tab workflow with hex viewer and live progress feedback

## Requirements

| Platform | Notes |
|----------|-------|
| Windows 10/11 x64 | No Python or dependencies required |
| Linux x86_64 | glibc 2.28 or newer, no Python or dependencies required |

## Quick Start

1. Download the binary for your operating system from the Releases page.
2. Run it directly. No installation needed.
3. Drag and drop a `.exe` or `.dll` file onto the welcome screen, or use Open PE File.
4. Review results across the tabs and export the report.

## Usage

```
# Linux
chmod +x Cosmos_Analyzer
./Cosmos_Analyzer

# Windows
Cosmos_Analyzer.exe
```

## Releases

| Version | Linux | Windows |
|---------|-------|---------|
| v1.1.4 | `Cosmos_Analyzer` | `Cosmos_Analyzer.exe` |

## Integrity Verification

Verify the SHA-256 checksum before running, especially when handling untrusted downloads.

```
sha256sum Cosmos_Analyzer          # Linux
certutil -hashfile Cosmos_Analyzer.exe SHA256   # Windows
```

Checksums are published with each release.

## License

MIT License. See the LICENSE file.
