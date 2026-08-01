<div align="center">

<img src="assets/COSMOS.png" alt="COSMOS Logo" width="120">

# COSMOS

**Static Malware Analysis for Windows PE Files**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform: Windows](https://img.shields.io/badge/Platform-Windows_10/11-blue.svg)](https://github.com/vortaile/cosmos-bin/releases)
[![Platform: Linux](https://img.shields.io/badge/Platform-Linux_x64-blue.svg)](https://github.com/vortaile/cosmos-bin/releases)
[![Release: v1.1.4](https://img.shields.io/badge/Release-v1.1.4-brightgreen.svg)](https://github.com/vortaile/cosmos-bin/releases/tag/v1.1.4)
[![Release Date](https://img.shields.io/badge/Release_Date-2026--07--31-lightgrey.svg)](https://github.com/vortaile/cosmos-bin/releases/tag/v1.1.4)

</div>

COSMOS is a desktop application for static forensic analysis of Windows Portable Executable (PE) files. It runs fully offline, so samples are never uploaded to third-party servers. Built for security analysts, malware researchers, and digital forensics investigators performing initial triage.

## Features

- **Hash computation**: MD5, SHA-1, SHA-256, SHA-384, SHA-512, and imphash
- **Signature verification**: magic byte validation and Authenticode certificate chain checks
- **PE structure parsing**: DOS/NT headers, sections, imports, exports, resources, and TLS callbacks
- **Entropy analysis**: per-section Shannon entropy to detect packing and obfuscation
- **String extraction**: ASCII and Unicode strings with length filtering
- **Indicator of Compromise detection**: IPs, URLs, domains, emails, registry keys, and file paths with confidence levels
- **YARA scanning**: 500+ bundled rules covering APT groups, ransomware, exploit kits, webshells, packers, crypto miners, and maldocs
- **Threat intelligence integration**: optional VirusTotal lookup with rate limiting and local caching
- **Verdict engine**: weighted heuristic scoring from 0 to 100 with four risk levels (CLEAN, LOW, SUSPICIOUS, MALICIOUS)
- **MITRE ATT&CK mapping**: technique identification and Cyber Kill Chain phase classification
- **Audit trail**: immutable JSON Lines chain-of-custody log with before and after file hashes
- **Report export**: JSON, HTML, PDF, CSV ZIP, and TXT with IOC defanging
- **Dark GUI**: four-tab workflow with hex viewer and live progress feedback

## Architecture

COSMOS follows a modular pipeline design. Each analysis stage is an independent module that feeds results into the next, ending with a unified verdict:

```
File Load -> Hash -> Signature -> PE Parse -> Entropy -> Strings -> IoC -> YARA -> Metadata
    -> Threat Intel (optional) -> Verdict Engine -> Report
```

Key design decisions:

- **Modular analyzers**: every analysis stage is a standalone module, easy to extend or replace
- **Offline-first**: all analysis runs locally; VirusTotal is opt-in per analysis
- **Chain of custody**: hashes are computed before and after analysis to verify sample integrity
- **Portable**: single-file executable, no installation, no system modification

## Technology Stack

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| Language | Python | 3.12 | Core application logic |
| GUI framework | PySide6 (Qt 6) | 6.7.2 | Desktop interface, dark theme, tabs |
| Web engine | QtWebEngine | bundled | Hex viewer rendering and PDF export |
| PE parsing | pefile | 2024.8.26 | DOS/NT header, section, import, export parsing |
| YARA engine | yara-python | 4.5.1 | Signature-based malware rule scanning |
| Crypto | cryptography | 44.0.0 | Authenticode certificate chain verification |
| HTTP client | httpx | 0.27.2 | VirusTotal API v3 integration |
| HTTP client | requests | 2.32.3 | Legacy HTTP support |
| File typing | python-magic | 0.4.27 | Magic byte and MIME detection |
| Secret storage | keyring | latest | Secure API key storage in OS keychain |
| Packaging | PyInstaller | latest | Single-file executable bundling |
| Build automation | GitHub Actions | N/A | Cross-platform build, test, release pipeline |
| Distribution | GitHub Releases | N/A | Binary distribution with SHA-256 verification |

## Python Standard Library Usage

| Module | Purpose |
|--------|---------|
| `hashlib` | MD5, SHA-1, SHA-256, SHA-384, SHA-512 hashing |
| `mmap` | Memory-mapped file loading for large binaries |
| `struct` | Binary structure parsing |
| `json` | Structured report and audit log serialization |
| `logging` | Rotating file and console logging |
| `multiprocessing` | Parallel YARA scanning worker |
| `threading` | Background analysis tasks |
| `socket`, `getpass` | Audit log host and user metadata |
| `pathlib` | Cross-platform path handling |
| `datetime`, `timezone` | UTC timestamp for audit trail |

## YARA Rule Categories

COSMOS bundles 500+ YARA rules organized into 22 categories:

| Category | Focus |
|----------|-------|
| Antidebug / Antivm | Anti-analysis and VM-detection techniques |
| Capabilities | Malware capability detection |
| Crypto | Cryptographic algorithm and library detection |
| CVE rules | Known vulnerability exploitation patterns |
| Exploit kits | Exploit kit families |
| Maldocs | Malicious documents (Office, PDF) |
| Email | Phishing and malicious email artifacts |
| Deprecated | Retired rules kept for reference |

Plus coverage for ransomware families, webshells, packers, loaders, and infostealers.

## Module Breakdown

| Module | Responsibility |
|--------|---------------|
| Analysis Engine | Orchestrates the full analysis pipeline |
| File Loader | Memory-mapped loading with size limits |
| Hash Analyzer | Computes MD5, SHA-1, SHA-256, SHA-384, SHA-512, imphash |
| Signature Checker | Validates magic bytes and Authenticode chains |
| PE Analyzer | Parses PE structure and flags anomalies |
| Entropy Analyzer | Computes per-section Shannon entropy |
| String Extractor | Extracts ASCII and Unicode strings |
| IoC Detector | Detects IPs, URLs, domains, emails, registry keys, file paths |
| YARA Scanner | Scans against 500+ rules in 22 categories |
| VirusTotal Client | Optional cloud lookup with rate limiting |
| Verdict Engine | Combines signals into a 0-100 risk score |
| Audit Logger | Writes immutable chain-of-custody JSON Lines log |
| Report Exporter | Exports to JSON, HTML, PDF, CSV ZIP, TXT |
| Config Manager | Persists user preferences and API key settings |

## Requirements

| Platform | Notes |
|----------|-------|
| Windows 10/11 x64 | No Python or dependencies required |
| Linux x86_64 | glibc 2.28 or newer, no Python or dependencies required |

## Quick Start

1. Download the binary for your operating system from the Releases page.
2. Run it directly. No installation needed.
3. Drag and drop any Windows PE file (.exe, .dll, .sys, .scr, .ocx, etc.) onto the welcome screen, or use Open PE File.
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

COSMOS is released under the [MIT License](LICENSE).

Copyright (c) 2026 Arizha Praja Wirakusuma

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
