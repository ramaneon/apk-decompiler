# APK Bug Bounty Analyzer — In-Browser MobSF & JADX Toolkit

A 100% client-side, zero-install Android security assessment and bug bounty hunting suite that runs directly in your browser on GitHub Pages. Upload any `.apk` file and automatically perform comprehensive static analysis without installing JADX, MobSF, or APKTool.

**Live Application:** https://ramaneon.github.io/apk-decompiler/

---

## Key Capabilities

- ⚡ **Instant Auto-Scan**: File drop or browse selection immediately unpacks and analyzes the APK without manual intervention.
- 🛡️ **MobSF / JADX-Grade Vulnerability Scanner**:
  - **Cryptography**: Detects `AES/ECB` insecure cipher mode, deprecated legacy ciphers (`DES`, `RC4`, `Blowfish`), collision-prone hashes (`MD5`, `SHA-1`), static/predictable `IvParameterSpec` IVs, and hardcoded `SecretKeySpec` keys in bytecode.
  - **Network & TLS**: Flags broken `TrustManager` implementations (`TrustAllCerts`), disabled hostname verification (`NullHostnameVerifier`, `ALLOW_ALL_HOSTNAME_VERIFIER`), and cleartext traffic configurations.
  - **WebView Exploitation**: Identifies exposed JavaScript bridges (`addJavascriptInterface`), cross-origin file access (`setAllowUniversalAccessFromFileURLs`), and SSL error bypasses (`handler.proceed()`).
  - **Storage & Injection**: Detects `MODE_WORLD_READABLE` / `MODE_WORLD_WRITEABLE` files, dynamic SQLite string concatenation, and sensitive logcat emissions (`Log.d(TAG, token)`).
- 🚀 **Exported Components & Deep Link Attack Surface**:
  - Automatically parses manifest components (Activities, Services, Broadcast Receivers) marked `exported="true"`.
  - Extracts URI schemes, hosts, and paths for Deep Links.
  - Generates ready-to-run **ADB PoC commands** (e.g. `adb shell am start -W -a android.intent.action.VIEW -d "..." <package>`) with one-click clipboard copying.
- 🔒 **Dangerous Permissions Audit**:
  - Audits high-risk Android capabilities (`RECORD_AUDIO`, `READ_SMS`, `ACCESS_FINE_LOCATION`, `SYSTEM_ALERT_WINDOW`, `WRITE_EXTERNAL_STORAGE`).
  - Highlights exploitation risks and attack surface expansion.
- 🔑 **API Key & Cloud Secret Discovery**:
  - **Firebase**: Realtime DB URLs, Storage URLs, API keys (`AIza...`), Project IDs, App IDs, Messaging Sender IDs, and VAPID keys with one-click public access test links (`/.json`).
  - **Cloud & SaaS**: AWS Access Keys (`AKIA...`) and Secret Keys, Azure Connection Strings & SAS tokens, Google OAuth Client IDs/Secrets, OpenAI / Anthropic / HuggingFace tokens, Stripe Live & Test keys, Razorpay, Slack OAuth & Webhook URLs, Discord Bot tokens, Twilio SID/tokens, SendGrid, Mailgun, Telegram, GitHub & GitLab PATs, Mapbox, and generic Bearer / Basic auth tokens.
- 🔍 **Instant In-Memory Keyword Search**:
  - Decompressed text files are retained in memory. Type any custom keyword or click presets (`admin`, `debug`, `test`, `token`, `password`) to filter across the entire APK with zero lag.
- 📊 **Security Scorecard & Reporting**:
  - Computes an overall Security Score (0-100) and Letter Grade (A-F) based on CVSS severity weights.
  - One-click export to **Markdown** (formatted for HackerOne / Bugcrowd reports) and **JSON**.

---

## Usage

1. Open https://ramaneon.github.io/apk-decompiler/
2. Drag & drop any `.apk` file onto the drop zone or click **BROWSE APK FILE**.
3. Analysis executes automatically.
4. Switch tabs across **Vulnerabilities**, **Components & PoC**, **Permissions**, **Firebase**, **Secrets & Keys**, **Keywords**, **Endpoints**, **Manifest**, and **File Tree**.
5. Use **EXPORT MARKDOWN** or **EXPORT JSON** to generate vulnerability documentation for bug bounty submissions.

---

## Architecture & Privacy

- **100% Client-Side**: All parsing, regex scanning, and decompilation occur entirely inside your browser sandbox using [JSZip](https://stuk.github.io/jszip/).
- **Zero Telemetry**: No files or extracted secrets are ever transmitted to any remote server or third-party service.
- **Hosted on GitHub Pages**: Deployable to any static web server or CDN with zero backend setup.

---

## Legal Disclaimer

This tool is designed strictly for authorized security research, educational purposes, and approved bug bounty programs. Always obtain explicit written authorization from target asset owners prior to testing.
