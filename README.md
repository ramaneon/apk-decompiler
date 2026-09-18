# APK Bug Bounty Analyzer — Firebase & Secret Hunter

A free, 100% client-side web tool for Android bug bounty hunters.  
Upload any .apk file and scan it for Firebase URLs, API keys, hardcoded secrets, and more — all in the browser with zero server-side processing.

**Live Tool:** https://ramaneon.github.io/apk-decompiler/

---

## Features

- **Firebase Detection**: Realtime DB URLs, RTDB default URLs, Storage URLs, API keys, Project IDs, App IDs, Messaging Sender IDs, Storage Buckets
- **Secret Scanning**: Google API Keys (AIza...), AWS Access Keys, JWT Tokens, Private Keys, Stripe/Slack tokens, OAuth Client IDs
- **Generic Secrets**: Hardcoded passwords, auth tokens, bearer tokens, client secrets
- **URL Enumeration**: All HTTP/HTTPS endpoints per file, deduplicated
- **Custom Keyword Search**: Comma-separated, search any string across the entire APK
- **Quick Presets**: One-click add of common bug bounty keywords
- **Manifest Viewer**: AndroidManifest.xml (for debug/re-signed APKs)
- **File Tree**: Browse all APK contents with filter
- **Copy to Clipboard**: One-click copy for all findings
- **Open Read Test Links**: Generates Firebase RTDB /.json URLs for quick public-access testing

## How to Use

1. Go to https://ramaneon.github.io/apk-decompiler/
2. Drag & drop an .apk file (or click Browse)
3. Optionally add custom keywords in the search box
4. Click **Analyze APK**
5. Review findings across the tabs: Firebase, Secrets, Keywords, URLs, Manifest, File Tree

## Deploy to GitHub Pages

1. Fork or clone this repository
2. Go to **Settings > Pages** in your GitHub repo
3. Set **Source** to main branch, root folder (/)
4. Your tool will be live at https://<username>.github.io/<repo>/

## Technical Details

- **No server**: Pure static HTML/JS, works on any static host
- **APK extraction**: Uses [JSZip](https://stuk.github.io/jszip/) to parse APK (ZIP format) in-browser
- **Scanning**: Regex-based pattern matching across all text-readable files (.xml, .json, .java, .kt, .smali, .js, .properties, .gradle, etc.)
- **Manifest**: Shows AndroidManifest.xml only if it is text-encoded (debug APKs / re-signed). Binary-compiled manifests need decompilation tools like jadx.

## Limitations

- Binary-compiled AndroidManifest.xml (standard release APKs) shows as unreadable — use jadx for full decompilation
- .dex, .so files are skipped (binary); use jadx/apktool for smali decompilation
- Pattern-based scanning, not AST-based — may have false positives

## Legal

This tool is for **authorized security research and bug bounty programs only**.  
Always get permission before testing. Use responsibly.
