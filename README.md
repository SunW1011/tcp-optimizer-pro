<p align="center"><strong>English</strong> | <a href="https://github.com/SunW1011/tcp-optimizer-pro/blob/main/README.vi.md">Tiếng Việt</a></p>

# TCP Optimizer Pro v2.4.0

TCP Optimizer Pro is a KernelSU module for Android ARM64 (API 26 or later, `versionCode=240`). It applies TCP and Qdisc profiles for Wi-Fi and mobile data, then reads back the values the kernel reports. Available algorithms and queue changes depend on the device kernel and network driver.

## WebUI

Home shows the active connection, both network profiles, four TCP metrics and four temperature readings. Open the route summary for IPv4 and IPv6 diagnostics and device information. Tap a temperature to see its sensor and the protection threshold for the battery.

In **Settings → Advanced**, the temperature bar shows the battery reading and both protection thresholds. Use the step buttons, presets or the four-column picker to change the base threshold. The picker covers 35.0°C to 50.0°C in 0.5°C steps. Charging raises the threshold by 2°C. In **Settings → Network**, a Driver MQ warning indicates that the driver retains its queue tree. Auto and `fq` remain selectable.

The Apps tab displays the installed app label and icon when the manager provides them. Hosts with an APK inspection tool can read labels from APK metadata. Other hosts show a shortened package name or an initial when the corresponding app metadata is unavailable.

## Install

1. Download `TCP-Optimizer-Pro-v2.4.0-KSU.zip` and `SHA256SUMS` from the [v2.4.0 release](https://github.com/SunW1011/tcp-optimizer-pro/releases/tag/v2.4.0).
2. In the download directory, run `sha256sum --ignore-missing -c SHA256SUMS` and check that the ZIP reports `OK`.
3. Install the ZIP in KernelSU Manager, reboot the device and open the module WebUI.

### Companion app

Download `TCP-Optimizer-Pro-v2.4.0-Companion.apk` from the same release, run the checksum command above and check that the APK reports `OK`. Install the APK after installing the module. Open the app and grant it root access in the manager so it can read live module state and apply settings. Configuration exports and diagnostic reports use the Android system document picker. If prompted, update Android System WebView and reopen the app.

## Quick profiles

Settings offers three profiles for Wi-Fi and mobile data. Each selects Auto for TCP and Qdisc and enables boot-time Qdisc priming. Auto tries `bbr3 → bbr2 → bbr → cubic → westwood → htcp → reno`. It prefers FQ with BBR and FQ-CoDel with other TCP algorithms.

| Profile | Changes |
| --- | --- |
| Maximum speed | Enables balanced initial TCP windows and keeps the send window after idle in eligible modes. |
| Gaming / Low latency | Enables temporary low-latency settings while the screen is active and the battery stays below the limit. |
| Balanced & battery saving | Keeps ROM defaults, enables background Auto and the TSQ/Lowat guard, and turns off low-latency leases. |

The profiles keep ROM defaults and leave your selected operating mode in place. Measured throughput remains subject to the link and its upstream capacity. The TCP low-latency settings can take effect in Gaming or Fast Download, including when Auto selects either scene in the background. Gaming can temporarily turn off Wi-Fi power saving on supported hardware. Open the WebUI to start that lease. The daemon ends leases when the screen turns off, the link becomes weak, or the battery gets too hot.

## Dual Wi-Fi

When two Wi-Fi interfaces are routing, the module restores the initial TCP windows it changed on Wi-Fi and releases the Gaming Wi-Fi power-save lease. It reapplies the configured windows after 15 seconds on a single Wi-Fi interface, even with the WebUI closed. Mobile data and the TCP-only leases follow their usual rules.

The WebUI shows **Paused (Dual Wi-Fi)** while the initial windows are deferred. Wi-Fi stability also depends on the ROM, driver and access points.

## VPN and tunnels

A routed VPN pauses initial TCP window tuning on Wi-Fi and mobile. The daemon restores the IPv4 and IPv6 route metrics it changed and leaves the tunnel routes alone. It waits five seconds after the tunnel disconnects before reapplying eligible settings. The home screen and diagnostic report show the pause.

## Network checks

- Select **Light** in the WebUI to keep a light interface even when Android is set to dark.
- If FQ is waiting on MQ queues, keep **Prime Wi-Fi Qdisc at boot** enabled and reboot to recreate the queues. The WebUI shows a separate message when boot priming is off.
- The kernel dictionary shows 32 live sysctl entries and marks unavailable readings. Bufferbloat uses loaded latency and packet loss for its grade. Compare A/B results from the same network type, test and endpoints.
- To check Private DNS over TCP/853 when automatic DNS uses a local router address, select Cloudflare, Google or AdGuard.

## Backups and diagnostics

Settings opens on **Network**. Use **Advanced** for daemon controls, route tuning and ROM overrides. **System** contains kernel confirmation, backups, diagnostics, the collapsed kernel reference, and community links.

Under **System**, use **Export config** to save a JSON backup. **Import config** asks for confirmation before opening the Android file picker. Review kernel confirmation after importing.

**Export config** and **Save file** in the diagnostic preview open the same folder browser. It starts at `/sdcard/Download` and opens `/sdcard` if Download is missing. Tap a folder to open it, **←** to go up, or **+** to create a folder. Use **×** beside the filename to clear it. The WebUI asks before replacing a file and shows the full path after saving.

The Apps page shows installed app icons where the manager provides them and uses initials as a fallback. In **System**, open **Community & Support** for GitHub, Telegram or voluntary support. The project includes offline bank and USDT QR codes.

## Restore and report issues

Use **Restore originals** to pause tuning and restore values tracked in the current boot. Review the readback for any remaining changes or conflicts.

Include the module version, Android version, device model and steps to reproduce when [reporting an issue](https://github.com/SunW1011/tcp-optimizer-pro/issues). The WebUI can export a diagnostic report.

See the [changelog](https://github.com/SunW1011/tcp-optimizer-pro/blob/main/changelog.md) for release history.
