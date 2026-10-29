# Ole AI Buddy — downloads

Installable builds of **Ole AI Buddy**, a desktop app for local AI models: it inspects
GGUF/ONNX files, tells you whether a model fits your hardware, benchmarks it (TTFT,
tokens/s, latency percentiles, regressions) and lets you chat with it while showing how
every token was chosen. Everything runs on your computer; nothing is uploaded.

Part of the **Ole** product line (see also [Ole Disk Buddy](https://github.com/cear12/olediskbuddy-releases)).
The source code is private; this repository only hosts the packages and the build workflow.

## Download

Latest release: **[Releases → Latest](https://github.com/cear12/oleaibuddy-releases/releases/latest)**

| Platform | Package | Direct link (always the newest build) |
|---|---|---|
| Windows 10/11 x64 | Installer (per-user, no admin rights) | [OleAIBuddy-windows-x64-Setup.exe](https://github.com/cear12/oleaibuddy-releases/releases/latest/download/OleAIBuddy-windows-x64-Setup.exe) |
| Windows 10/11 x64 | Portable ZIP (unpack and run `bin\OleAIBuddy.exe`) | [OleAIBuddy-windows-x64-portable.zip](https://github.com/cear12/oleaibuddy-releases/releases/latest/download/OleAIBuddy-windows-x64-portable.zip) |
| Linux x86_64 | AppImage (`chmod +x`, run) | [OleAIBuddy-linux-x86_64.AppImage](https://github.com/cear12/oleaibuddy-releases/releases/latest/download/OleAIBuddy-linux-x86_64.AppImage) |
| Linux x86_64 | tar.gz (unpack, run `./OleAIBuddy`) | [OleAIBuddy-linux-x86_64.tar.gz](https://github.com/cear12/oleaibuddy-releases/releases/latest/download/OleAIBuddy-linux-x86_64.tar.gz) |
| macOS 13.3+ (Apple Silicon) | DMG | [OleAIBuddy-macos-arm64.dmg](https://github.com/cear12/oleaibuddy-releases/releases/latest/download/OleAIBuddy-macos-arm64.dmg) |

Each release also carries `SHA256SUMS.txt` (verify with `sha256sum -c SHA256SUMS.txt`) and
`latest.json` (the update feed the app reads).

### First start
- **Windows:** the builds are not code-signed yet, so SmartScreen may say "Windows protected
  your PC" — choose *More info → Run anyway*.
- **macOS:** the app is not notarized yet: right-click the app → *Open* → *Open*.
- **Linux:** built on Ubuntu 24.04, so it needs glibc 2.39+ (Ubuntu 24.04, Debian 13, Fedora 40
  or newer) and FUSE (`libfuse2`); without FUSE run it with `--appimage-extract-and-run`.

## Building (maintainers)

`Actions → Build → Run workflow` builds the private source (`cear12/oleaibuddy-git`) on this
public repository's runners. Inputs: version `X.Y.Z`, source ref, *publish* (creates the
GitHub Release here), optional Android/MSI/ONNX Runtime and extra CMake arguments.

Required settings of this repository:
- secret **`SOURCE_TOKEN`** — fine-grained personal access token, *Repository access:*
  `cear12/oleaibuddy-git` only, *Permissions → Contents: Read-only*;
- variable **`OLEAI_LICENSE_PUBKEY`** — the production licence public key (hex), needed to
  publish (see `docs/RELEASE.md` in the source repository).

Optional signing secrets (Azure Trusted Signing, Apple Developer ID + notarization, Android
keystore) are listed in the source repository's `docs/RELEASE.md`. The workflow file is
maintained in the source repository (`packaging/releases-repo/`) and copied here by
`scripts/sync_releases_repo.ps1`.
