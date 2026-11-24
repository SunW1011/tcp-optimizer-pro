<p align="center"><strong>English</strong> | <a href="https://github.com/SunW1011/tcp-optimizer-pro/blob/main/README.vi.md">Tiếng Việt</a></p>

# TCP Optimizer Pro v2.2.3

TCP Optimizer Pro is a KernelSU module for Android ARM64 (API 26 or later, `versionCode=223`). It applies TCP and Qdisc profiles for Wi-Fi and mobile data, then reads back the values the kernel reports. Available algorithms and queue changes depend on the device kernel and network driver.

## Install

1. Download `TCP-Optimizer-Pro-v2.2.3-KSU.zip` and `SHA256SUMS` from the [v2.2.3 release](https://github.com/SunW1011/tcp-optimizer-pro/releases/tag/v2.2.3).
2. In the download directory, run `sha256sum -c SHA256SUMS` and check that the ZIP reports `OK`.
3. Install the ZIP in KernelSU Manager, reboot the device and open the module WebUI.

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

## Network checks

- Select **Light** in the WebUI to keep a light interface even when Android is set to dark.
- If FQ is waiting on MQ queues, keep **Prime Wi-Fi Qdisc at boot** enabled and reboot to recreate the queues. The WebUI shows a separate message when boot priming is off.
- The kernel dictionary shows 32 live sysctl entries and marks unavailable readings. Bufferbloat uses loaded latency and packet loss for its grade. Compare A/B results from the same network type, test and endpoints.
- To check Private DNS over TCP/853 when automatic DNS uses a local router address, select Cloudflare, Google or AdGuard.

## Backups and diagnostics

In Settings, enter a JSON filename and choose a folder to export or import your settings. The default is `/sdcard/Download`. You can also import a JSON file with the device picker. Review kernel confirmation after an import to see what applied.

Diagnostic reports use the same folder choices and save as TXT files. The WebUI asks before replacing a file and shows the saved path when Android provides it.

## Restore and report issues

Use **Restore originals** to pause tuning and restore values tracked in the current boot. Review the readback for any remaining changes or conflicts.

Include the module version, Android version, device model and steps to reproduce when [reporting an issue](https://github.com/SunW1011/tcp-optimizer-pro/issues). The WebUI can export a diagnostic report.

See the [changelog](https://github.com/SunW1011/tcp-optimizer-pro/blob/main/changelog.md) for release history.
