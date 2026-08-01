# Contributing to COSMOS

Thank you for your interest in contributing to COSMOS. This repository hosts prebuilt binaries and public documentation; the primary development repository is maintained separately. Contributions that improve the documentation, release process, and downstream user experience are welcome.

## Ways to Contribute

- **Report issues**: Open an issue for bugs, crashes, or unexpected analysis results. Include the COSMOS version, operating system, and a reproducible description.
- **Suggest features**: Propose enhancements with a clear use case and expected behavior.
- **Improve documentation**: Fix typos, clarify instructions, or expand usage examples in the README.
- **Verify releases**: Download new releases, run the integrity checks, and report any packaging problems.

## Reporting Issues

When opening an issue, please provide:

1. COSMOS version (e.g., v1.1.4)
2. Operating system and architecture (e.g., Windows 11 x64, Ubuntu 24.04 x86_64)
3. Steps to reproduce
4. Expected behavior versus actual behavior
5. Relevant error output or crash details

## Development Setup

COSMOS is a Python 3.12 application built with PySide6. A typical development environment:

```bash
git clone <development-repository>
cd cosmos
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cd src
python -m cosmos
```

## Build Process

Release builds are produced with PyInstaller for both platforms:

- Windows: `windows-latest` runner, output `Cosmos_Analyzer.exe`
- Linux: `ubuntu-latest` runner, output `Cosmos_Analyzer`

Build configuration lives in `cosmos.spec`. Binaries are published automatically to this repository's Releases page when a version tag is created.

## Code of Conduct

Be respectful and constructive. All contributions are reviewed with the goal of keeping COSMOS reliable, secure, and useful for the forensic community.
