# KyberCheck GitHub Action 🛡️

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-KyberCheck--Action-blue?logo=github)](https://github.com/marketplace/actions/kybercheck-scanner)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

**Prepare for the Post-Quantum era.** KyberCheck scans your codebase for quantum-vulnerable cryptography, identifying legacy algorithms (like RSA and ECC) that are at risk from future quantum computer attacks.

## 🚀 Quick Start

Add the following workflow to your repository at `.github/workflows/kybercheck.yml`:

```yaml
name: KyberCheck Scan
on:
  push:
    branches: [main, master]
  pull_request:

jobs:
  scan:
    name: Quantum Vulnerability Scan
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Run KyberCheck Scan
        uses: KyberCheck/kybercheck-action@main
        with:
          api-key: ${{ secrets.KYBERCHECK_API_KEY }}
```

## ⚙️ Configuration

| Input | Description | Required | Default |
| :--- | :--- | :--- | :--- |
| `api-key` | Your KyberCheck API Key. Get one at [kybercheck.com](https://kybercheck.com). | **Yes** | N/A |
| `path` | The directory to scan. | No | `.` (Root) |
| `exclude` | Patterns to exclude (glob). E.g., `**/test/**,**/*.spec.js`. | No | None |
| `languages` | Specific languages to scan. E.g., `python,rust`. | No | All |
| `fail-on-critical` | Fail the workflow if critical vulnerabilities are found. | No | `false` |

## 🔑 Setup
1. **Get an API Key:** Sign up at [kybercheck.com](https://kybercheck.com) to receive your API key.
2. **Add Secret:** In your GitHub repository, go to **Settings > Secrets and variables > Actions** and add a new secret named `KYBERCHECK_API_KEY`.

## 🛠️ How it works
This action downloads the high-performance **KyberCheck CLI** (written in Rust) and executes a scan against your source code. It identifies:
*   Asymmetric algorithms vulnerable to Shor's Algorithm.
*   Insufficient symmetric key lengths.
*   Hardcoded cryptographic parameters.

Results are automatically uploaded to your KyberCheck dashboard for detailed analysis and remediation tracking.

## ⚡ Performance
This action uses pre-compiled binaries for **instant execution**. Unlike other security actions that require long build steps or heavy Docker pulls, KyberCheck typically installs and starts scanning in under 2 seconds.

## 📄 License
This GitHub Action is licensed under the [Apache 2.0 License](LICENSE). The KyberCheck scanner binary is subject to the KyberCheck Terms of Service.

---
© 2026 KyberCheck. All rights reserved.
```
