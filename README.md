# Sysmon Deployment Suite

**Enterprise-grade endpoint logging in one menu.** Downloads, installs and configures Sysmon with the Olaf Hartong configuration, then tunes it for the two events that actually catch injection and credential theft.

## Why Event ID 7 and 10

| Event | What it reveals |
| --- | --- |
| **7 &mdash; Image Load** | A DLL loading from a temp path, an unsigned module, or a module with no metadata &mdash; the footprint of most injection |
| **10 &mdash; Process Access** | One process opening another with `PROCESS_VM_READ` / `WRITE` &mdash; LSASS access, memory scraping, remote thread setup |

Most default Sysmon configs leave these noisy or disabled. This suite enables them and filters the noise.

## Menu

| Option | Action |
| --- | --- |
| **RUN** | One-click install or update |
| **STATUS** | Service and driver health, current config, event counts |
| **RECONFIGURE** | Hot-reload a new config without reinstalling the driver |
| **UNINSTALL** | Clean removal, including the driver service |

## Install

```powershell
git clone https://github.com/hypersenseindia/Sysmon-Deployment-Suite
cd Sysmon-Deployment-Suite
# run the suite elevated
.\Sysmon-Deployment-Suite.ps1
```

Requires an elevated PowerShell session and internet access on first run.

## Config source

1. [Olaf Hartong's sysmon-modular](https://github.com/olafhartong/sysmon-modular) &mdash; primary
2. [SwiftOnSecurity's sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config) &mdash; fallback if the first is unreachable

The download is verified before it is applied.

## Verify it is working

```powershell
Get-Service Sysmon64
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -MaxEvents 5
```

## Notes

- Windows 10 / 11, PowerShell 5.1+
- Sysmon itself is a Microsoft Sysinternals tool, licensed separately
- Configuration files are downloaded, not vendored &mdash; pin a commit hash if you need reproducibility
---

<p align="center">
  <sub>Built by <b>AG HYDRAXFF</b> &mdash; HYPERSENSEGLOBAL &middot;
  <a href="https://www.instagram.com/hydraxff_yt/">@hydraxff_yt</a></sub>
</p>