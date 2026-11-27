<p align="center"><strong>English</strong> | <a href="https://github.com/SunW1011/tcp-optimizer-pro/blob/main/README.vi.md">Tiếng Việt</a></p>

# TCP Optimizer Pro v2.6.2

TCP Optimizer Pro is a module for KernelSU, APatch and Magisk for Android ARM64 (API 26 or later, `versionCode=262`). It applies TCP and Qdisc profiles for Wi-Fi and mobile data, then reads back the values the kernel reports. Available algorithms and queue changes depend on the device kernel and network driver.

Expiring IPv6 router-advertised routes keep their original lifetime. On cellular, IPv4 probes can use the CLAT interface paired with the active IPv6 route.

## WebUI

Home shows the active connection, both network profiles, four TCP metrics and four temperature readings. Open the route summary for IPv4 and IPv6 diagnostics and device information. Tap a temperature to see its sensor and the protection threshold for the battery.

In **Settings → Advanced**, the temperature bar shows the battery reading and both protection thresholds. Use the step buttons, presets or the four-column picker to change the base threshold. The picker covers 35.0°C to 50.0°C in 0.5°C steps. Charging raises the threshold by 2°C. In **Settings → Network**, a Driver MQ warning indicates that the driver retains its queue tree. Auto and compatible leaf schedulers are available according to the kernel.

The Apps tab displays the installed app label and icon when the manager provides them. Hosts with an APK inspection tool can read labels from APK metadata. Other hosts show a shortened package name or an initial when the corresponding app metadata is unavailable.

## Install

1. Download `TCP-Optimizer-Pro-v2.6.2-KSU.zip` and `SHA256SUMS` from the [v2.6.2 release](https://github.com/SunW1011/tcp-optimizer-pro/releases/tag/v2.6.2).
2. In the download directory, run `sha256sum --ignore-missing -c SHA256SUMS` and check that the ZIP reports `OK`.
3. Flash the ZIP in your root manager and reboot. In KernelSU or APatch, **WebUI** opens the manager’s built-in module interface. In Magisk, tap **Action** to launch the Companion. **Action** also launches the Companion in KernelSU and APatch.

### Companion app

The module ZIP includes the Companion. Reboot after flashing, then tap **Action** in the manager. The app connects while it is in the foreground. If the connection is unavailable, open the module WebUI in the manager. A reboot with the same module version respects manual removal. Tap **Action** to install or update for the device owner, or use the verified standalone APK. Imports and exports use the Android document picker. The Companion requests no Android system permissions and opens no Internet connection. Its only manifest permission is an app-private, signature-level receiver guard. It sends commands to the daemon over a local Unix socket. The daemon checks the app’s UID, process mapping and pinned APK signing certificate.

## Quick profiles

Settings offers three profiles for Wi-Fi and mobile data. Each selects Auto for TCP and Qdisc and turns on **Set default Qdisc at boot**. Auto tries `bbr3 → bbr2 → bbr → cubic → westwood → htcp → reno`. It prefers FQ with BBR and FQ-CoDel with other TCP algorithms.

| Profile | Changes |
| --- | --- |
| Maximum speed | Enables balanced initial TCP windows and keeps the send window after idle in eligible modes. |
| Gaming / Low latency | Enables temporary low-latency settings while the screen is active and the battery stays below the limit. |
| Balanced & battery saving | Keeps ROM defaults, enables background Auto and the TSQ/Lowat guard, and turns off low-latency leases. |

The profiles keep ROM defaults and leave your selected operating mode in place. Measured throughput remains subject to the link and its upstream capacity. With the WebUI closed and the screen on, background Auto samples every 2 seconds after a change. It backs off to 5 seconds after three stable samples and 15 seconds after at least 30 seconds of stability. Background sampling stops when the screen is off or in AOD. The TCP low-latency settings can take effect in Gaming or Fast Download, including when Auto selects either scene in the background. Gaming can temporarily turn off Wi-Fi power saving on supported hardware. Open the WebUI to start that lease. The daemon ends leases when the screen turns off, the link becomes weak, or the battery gets too hot.

## Dual Wi-Fi

When two Wi-Fi interfaces are routing, the module restores the initial TCP windows it changed on Wi-Fi and releases the Gaming Wi-Fi power-save lease. It reapplies the configured windows after 15 seconds on a single Wi-Fi interface, even with the WebUI closed. Mobile data and the TCP-only leases follow their usual rules.

The WebUI shows **Paused (Dual Wi-Fi)** while the initial windows are deferred. Wi-Fi stability also depends on the ROM, driver and access points.

## VPN and tunnels

A routed VPN pauses initial TCP window tuning on Wi-Fi and mobile. The daemon restores the IPv4 and IPv6 route metrics it changed and leaves the tunnel routes alone. It waits five seconds after the tunnel disconnects before reapplying eligible settings. The home screen and diagnostic report show the pause.

## Network checks

- Select **System** to follow Android’s light or dark theme. Select **Light**, **Dark** or **AMOLED** to use a fixed theme.
- For driver MQ, the picker offers **Auto** and up to six compatible leaves supported by the kernel: `fq`, `fq_codel`, `cake`, `codel`, `pie` and `sfq`. The module preserves the driver’s `mq 0:` tree. Enable **Set default Qdisc at boot** and reboot to let the kernel build fresh leaves from the selected default.
- `net.core.default_qdisc` is one system-wide value. If Wi-Fi and mobile both use driver MQ with different choices, new queues can inherit only the currently selected global default. Check each link’s leaf readback.
- The kernel dictionary shows 32 live sysctl entries and marks unavailable readings. Bufferbloat uses loaded latency and packet loss for its grade. Compare A/B results from the same network type, test and endpoints.
- To check Private DNS over TCP/853 when automatic DNS uses a local router address, select Cloudflare, Google or AdGuard.

## Backups and diagnostics

Settings opens on **Network**. Use **Advanced** for daemon controls, route tuning and ROM overrides. **System** contains kernel confirmation, backups, diagnostics, the collapsed kernel reference, and community links.

Under **System**, use **Export config** to save a JSON backup. **Import config** asks for confirmation before opening the Android file picker. Review kernel confirmation after importing.

**Export config** and **Save file** in the diagnostic preview open the same folder browser. It starts at `/sdcard/Download` and opens `/sdcard` if Download is missing. Tap a folder to open it, **←** to go up, or **+** to create a folder. Use **×** beside the filename to clear it. The WebUI asks before replacing a file and shows the full path after saving.

The Apps page shows installed app icons where the manager provides them and uses initials as a fallback. In **System**, open **Links & support** for GitHub, Telegram or voluntary support. The project includes offline bank and USDT QR codes.

## Restore and report issues

Use **Restore originals** to pause tuning and restore values tracked in the current boot. Review the readback for any remaining changes or conflicts.

Include the module version, Android version, device model and steps to reproduce when [reporting an issue](https://github.com/SunW1011/tcp-optimizer-pro/issues). The WebUI can export a diagnostic report.

See the [changelog](https://github.com/SunW1011/tcp-optimizer-pro/blob/main/changelog.md) for release history.
