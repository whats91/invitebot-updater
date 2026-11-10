# Invite Bot updates

This public repository distributes compiled **Invite Bot** Windows updates. The
application's source code and development history are kept in a separate
private repository and are not published here.

## What is here

| Path | Content |
|---|---|
| `channels/stable.json` | The signed stable channel: the newest Invite Bot version, its packages, sizes and SHA-256 hashes (schema 2). |
| `channels/stable.sig` | The detached ECDSA P-256 signature over the exact bytes of `stable.json`. |
| `schemas/` | The JSON schema of the channel and release manifests. |
| GitHub Releases `v<version>` | Immutable release assets for each version (below). |

Each release `v<version>` carries:

| Asset | Content |
|---|---|
| `InviteBot-<version>-win-x64-full.zip` | Every file of the version, with `InviteBot.Setup.exe`, `manifest.json` (file inventory: path, size, SHA-256) and `SHA256SUMS.txt`. It is also the manual installer. |
| `InviteBot-<base>-to-<version>-win-x64-delta.zip` | Only the files that changed since `<base>`, with setup, the full inventory and `delta.json`. Installed Invite Bot rebuilds the version from it and checks every file; if anything differs it uses the full package. |
| `InviteBot-<version>-manifest.json` / `.sig` | The release-specific signed manifest (identical to the channel file when it was published). |
| `InviteBot-<version>-release-notes.md` | What changed. |
| `InviteBot-<version>-documentation.zip` | The Invite Bot documentation of this version: every guide with its folders and links (start with `README.md`). The same files are installed with Invite Bot (Overview → Documentation). |
| `InviteBot-<version>-AI-BUNDLE.md` | The same documentation in one file, to read or to give to an AI assistant. |
| `InviteBot-<version>-SHA256SUMS.txt` | SHA-256 of every asset of the release. |

The stable channel files first appear when the first release is published. Repository
setup alone does not offer a build to installed PCs.

## How installed Invite Bot uses it

The **Invite Bot Updater** Windows service checks `channels/stable.json` when it
starts and every three hours, verifies the signature with the public key built
into Invite Bot, refuses older, replayed or foreign manifests, downloads the delta
(or the full package), verifies every hash, and installs the update itself.

Public release executables and installers are Authenticode-signed and timestamped
by VELIRDEN TECHNOLOGIES LLP. The separately signed update manifest authorizes
automatic installation; the package hashes bind each download to that manifest.

Do not post secrets, credentials or customer data in a public issue. See
[SECURITY.md](SECURITY.md).
