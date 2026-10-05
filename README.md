# AIBHound

Azure Image Builder log viewer for Windows. Follow builds live, read
multi-GB customization logs, and see phases, health, cost estimates and known
issues with their fixes.

This repository hosts **releases only**.
**[Download the latest release](https://github.com/AdmiralTolwyn/aibhound_public/releases/latest)**

## Install

Requires Windows 10 or 11 (x64).

1. Download `AIBHound-<version>-windows-x64.zip` from the latest release.
2. Optional: check the download against the published checksum:
   ```powershell
   Get-FileHash .\AIBHound-<version>-windows-x64.zip -Algorithm SHA256
   ```
3. Extract it anywhere and run `AIBHound\aibhound.exe`.

The app is not code-signed yet, so Windows SmartScreen may warn on first run:
choose **More info** › **Run anyway**.

There is no installer. To remove AIBHound, delete its folder and
`%APPDATA%\AIBHound`.

## Features

- **Live builds:** discover running Image Builder builds across your
  subscriptions, stream the customization log as it is written, follow the
  pipeline with ETAs, pause, cancel, download `customization.log`.
- **Past runs:** runs you watched, plus the logs still kept in the staging
  storage accounts.
- **Log reader:** handles multi-GB logs; filter or highlight search, regex,
  severity filter, minimap, go-to-line.
- **Analytics:** phases, A–F health, cost estimate at Azure's pay-as-you-go
  price, known issues with fixes, error groups, script profiler, flame chart.
- **Customizers:** each template customizer matched to its step, with status,
  duration and errors.
- **Notifications** when a build finishes, fails or logs its first error.
- In-app manual (**?** button) and a scrubbed diagnostics log for bug reports.

## Sign-in and permissions

AIBHound signs in as you with Microsoft Entra ID in your browser (OAuth 2.0
with PKCE) and acts with your own Azure permissions. It uses the Azure
PowerShell public client by default; you can enter your own app registration
on the sign-in screen.

| Feature | Role you need |
|---|---|
| Discover builds, live logs, template status | Reader on the subscriptions or resource groups |
| Download `customization.log`, past runs | Storage Blob Data Reader on the `IT_*` staging storage account |
| Cancel a run | Contributor on the image template |

Access tokens stay in memory. Only the refresh token is kept, in Windows
Credential Manager, and sign-out removes it. The app talks only to
`login.microsoftonline.com`, `management.azure.com`,
`<account>.blob.core.windows.net` and the public Azure Retail Prices API
(`prices.azure.com`, which never receives a token).

## Your data

Settings, saved runs and cached logs stay on your PC in
`%APPDATA%\AIBHound\aibhound`. Build logs can contain secrets a script
printed; cached logs are deleted after 7 days by default (Settings › Data &
storage). Debug logging is off by default.

## Feedback

Open an [issue](https://github.com/AdmiralTolwyn/aibhound_public/issues) with
the version (Settings › About › Copy diagnostics) and steps to reproduce. Do
not paste tokens or logs that contain secrets.

## License

Free to use under the [license](LICENSE). Third-party components are listed
in the app under Settings › About › Open-source licenses.

AIBHound is an independent tool and is not affiliated with or endorsed by
Microsoft. Azure is a trademark of the Microsoft group of companies.
