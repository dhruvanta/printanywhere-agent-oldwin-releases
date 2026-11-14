# Parcho Agent (older Windows) — Releases

> Maintained by Dhruvanta Systems Private Limited.

Windows installers for **Parcho Agent (older Windows)**: the print agent for shop PCs that run
**Windows 7, 8 or 8.1** and cannot run the standard Parcho agent. This repository hosts installers
only; the source code is maintained privately.

## Who it is for
- Shops whose print PC runs **Windows 7** (including the original release, build 7600, with no
  Service Pack), **Windows 8** or **Windows 8.1**.
- Older 32-bit PCs (Pentium-class processors with SSE2).

If the PC runs **Windows 10 or 11**, do not use this. Use the standard Parcho agent instead.

## A separate product
This is **not** the standard agent and not an update to it.
- It cannot be installed on a PC that already has the standard agent. The installer checks and
  stops if it finds one.
- It installs into its own folder, `Parcho Agent (older Windows)`.
- It does **not** update itself. To move to a newer version, download the newer installer from
  this page and run it over the old one.

## Download
- Latest installer (stable link):
  **[ParchoAgent-OlderWindows-x86.msi](https://github.com/dhruvanta/printanywhere-agent-oldwin-releases/releases/latest/download/ParchoAgent-OlderWindows-x86.msi)**
- Checksums for the latest release:
  [SHA256SUMS.txt](https://github.com/dhruvanta/printanywhere-agent-oldwin-releases/releases/latest/download/SHA256SUMS.txt)
- All versions: see [Releases](https://github.com/dhruvanta/printanywhere-agent-oldwin-releases/releases)

## Pilot builds are UNSIGNED
Current releases are field-pilot builds and are **not code-signed**. Windows will show
"Unknown publisher" when you run the installer. Check the file before you run it:

1. Download `SHA256SUMS.txt` from the same release.
2. On a PC with PowerShell, run `Get-FileHash .\ParchoAgent-OlderWindows-x86.msi -Algorithm SHA256`.
   On a stock Windows 7 PC without PowerShell 4, run
   `certutil -hashfile ParchoAgent-OlderWindows-x86.msi SHA256` instead.
3. The hash must match the line for that file name in `SHA256SUMS.txt`. If it does not, do not
   run the file.

## What happens at install time
The installer runs a short **self-test** on the PC before it finishes: it checks that the agent's
runtime starts, that it can connect securely to Parcho, that it can store the shop's credentials
safely, and that the PDF printing helper starts. If any check fails, nothing is installed and you
see one plain message saying what to fix (for example, on Windows 7 without Service Pack 1, it may
ask you to install Service Pack 1, update KB976932).

The self-test also looks at whether this PC is exposed to the network in ways an unpatched
Windows 7 is known to be unsafe with (for example, file sharing over SMB1 or open remote-desktop
ports). In the current builds this is a **warning** only: the agent installs, and the warning is
saved and reported so we can follow up with the shop.

## Limits and sunset
This edition runs on **Node.js 18**, the newest version that still works on Windows 7. Node.js 18
reached **end of life in April 2025** and no longer receives security fixes. We accept that only
for these older PCs, and only for a limited time:
- The edition will be **withdrawn on a sunset date that has not been set yet**. When it is set, it
  will be announced here and to the shops that use it.
- It will be withdrawn earlier if a serious security problem is published for Node.js 18 that
  affects how the agent connects to Parcho or its local console.
- The best long-term fix for a shop is to move the print PC to Windows 10 or 11 and use the
  standard agent.

More info: https://www.dhruvantasystems.com/download
