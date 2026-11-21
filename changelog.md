## TCP Optimizer Pro v1.9.2

- Export settings and app rules to a timestamped JSON backup in `/sdcard/Download`. Import replaces the saved settings and rules after daemon schema validation, using the existing atomic commit and kernel readback paths.
- Probe DoT with a bounded TLS ClientHello on TCP/853. Include SNI for DNS names and report ServerHello, HelloRetryRequest, or TLS Alert. The probe stops before certificate verification.
- Support callback and legacy synchronous WebUI bridges. Honor disable and removal markers at startup, and preserve the recovery journal if uninstall cannot verify restoration.

## TCP Optimizer Pro v1.9.1

- Gateway-only latency probe now computes Jitter, Packet Loss, and first/min-max RTT directly from the Gateway ICMP batch.
- Replaced `Unknown + Unknown` readback labels on inactive network paths with clear status text (`Inactive (Wi-Fi active)` / `Inactive (Mobile active)`).
- Updated the Home Wi-Fi and Mobile cards to display a clear confirmed driver-managed MQ state instead of a pending warning.
- Fixed the detail modal usage note to display the real device RAM from `status.json`.
- Cleaned Python `__pycache__` artifacts from the source repository package.

## TCP Optimizer Pro v1.9.0

- Enabled tapping the Home Wi-Fi card directly to open the Wi-Fi diagnostics popup.
- Added selectable and custom public Ping targets (`1.1.1.1`, `8.8.8.8`, `9.9.9.9`, `Gateway only`, or custom host/IP) bound to the active egress interface.
- Added read-only Private DNS status display and an on-demand DoT (TCP/853) connectivity check.
- Redesigned Network Route Diagnostics (collapsible secondary interfaces) and the Kernel Verification card in Bento style; fixed label wrapping in Settings and Apps tabs.
- Synchronized version metadata across daemon and WebUI, removing legacy fallback version strings.

## TCP Optimizer Pro v1.8.1

- WebUI header now displays the live version read from daemon status.
- TCP + Qdisc modal explains the resolved algorithm and queue discipline when set to Auto.
- Replaced the CAKE Diffserv dropdown with a Bento-styled segmented button group.

## TCP Optimizer Pro v1.8.0

- Added optional Wi-Fi Power Save lease for Gaming mode and two optional TCP leases (autocorking and slow-start-after-idle) for Gaming and Max Speed modes, guarded by screen state and battery temperature with automatic journal restore.
- Extended optional `initcwnd`/`initrwnd` route tuning to verify and apply independently to both IPv4 and IPv6 default routes on the active egress interface while skipping cross-interface CLAT and ambiguous routes.
- Added PIE and FQ-PIE detection when supported by the kernel, plus optional MTU-based quantum for FQ/FQ-CoDel and Diffserv modes for CAKE in manual configurations.
- Expanded Wi-Fi diagnostics popup with live Power Save state, active lease status, channel width, frequency, band, and driver-reported country code.
- Added KernelSU Next OTA metadata and automated GitHub Release workflow for verified tags.
- New installations disable leases, route windows, and advanced Qdisc options by default; upgrades preserve existing user settings.

## TCP Optimizer Pro v1.7.0

- Universal Zero-Hardcode upgrade: dynamically probes 100% of hardware, TCP, and Qdisc capabilities from the kernel with automatic CC-aware priority chains (`BBR -> fq`, non-BBR `-> fq_codel`).
- Added multi-platform cellular and VPN interface detection, handover debounce protection, first/min-max RTT metrics, and a copy-logs button in WebUI.

## TCP Optimizer Pro v1.6.1

- Stable v1.6.1 release featuring ARM64 16 KiB ELF alignment, pure C11 Netlink daemon, TSO `errno=16` fix, WebView diagnostics export fix, and VI/EN UI refinements.
