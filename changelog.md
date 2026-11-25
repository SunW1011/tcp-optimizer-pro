# Changelog

## v2.3.0

- Added VPN protection for initial TCP windows. Physical routes return to their prior IPv4 and IPv6 metrics while a routed tunnel is active. Tuning resumes after five seconds without the tunnel.
- Added VPN pause status to the home screen, the TCP window details and the diagnostic report.
- Fixed app icons on the first visit to the Apps tab with a cached app list.
- Kept the compact TSQ readout on one line on narrow screens.

## v2.2.6

- Added installed app icons on KernelSU managers that serve them, with initials as a fallback. Shortened the default app profile label.
- Clarified the initial TCP window preset and separated daemon controls from routing and queue controls.
- Aligned the System action buttons and added GitHub, Telegram and voluntary support below the collapsed kernel reference. Both support QR codes are stored in the module.
- Made the Bufferbloat button full width and explained why the log can show only the daemon startup entry.

## v2.2.5

- Split Settings into pinned Network, Advanced and System tabs.
- Reduced the backup card to Export config and Import config. Moved import confirmation before the Android file picker.
- Added a shared folder browser for JSON backups and diagnostic text files, including folder creation in shared storage.
- Simplified the diagnostic preview to Save file, Copy and Close.

## v2.2.4

- Replaced the folder shortcuts with a picker for JSON backups and diagnostic reports.
- Shortened suggested filenames and added a clear button.
- Opened the Android file picker from the main import button and kept import from the selected folder available.
- Tightened the diagnostic dialog and placed Save file first.

## v2.2.3

- Added custom filenames and folders for configuration backups and diagnostic reports, with overwrite confirmation.
- Added JSON import through the Android file picker and kept import by path available.
- Fixed initial TCP window status during restore and when optimization is paused.
- Added Dual Wi-Fi deferral to the initial TCP window details.
- Fixed keyboard dismissal and focus restoration for app profiles, and clarified when a saved profile is waiting for optimization to resume.
- Rechecked pending apply requests after the WebUI returns from the background.

## v2.2.2

- Restored Wi-Fi initial TCP windows when two Wi-Fi interfaces began routing and resumed tuning after 15 seconds on single Wi-Fi.
- Released the Gaming Wi-Fi power-save lease during Dual Wi-Fi and deferred station queries for 2.5 seconds after link events.
- Added a Dual Wi-Fi pause message to the initial TCP window card and settings.

## v2.2.1

### Fixed

- Kept Light selected in the WebUI when the host WebView prefers dark colors.
- Enabled TCP low-latency leases when Auto selects Gaming or Fast Download. Kept screen, temperature, route and signal checks in force. A new Wi-Fi power-saving lease still requires the WebUI to be open.
- Continued sampling after Signal Guard releases a lease and read TCP retransmit counters from the kernel so a strong link can recover.
- Included restore, resume and reapply events in the Apply log filter.
- Wrapped long RTT ranges within the latency card. Saved a temperature slider change on release and combined repeated step-button taps into one save.
- Cleared quick-profile highlights while optimization is paused or the original settings are restored.

### Changed

- Grouped mobile radio readings in one row, omitted missing Wi-Fi region codes and added a hint when Wi-Fi diagnostics can be opened.
- Put preferred TCP and Qdisc entries first in the kernel dictionary and clarified the Lowat and initial TCP window descriptions.
- Shortened app hints and used consistent mode names across the WebUI.

## v2.2.0

### Added

- Added Maximum speed, Gaming / Low latency, and Balanced & battery saving quick profiles with confirmation and active-profile indicators.
- Exposed TCP autocorking, compressed SACK delay, the established TCP retry limit, and ECN fallback in the live sysctl list.

### Changed

- Ordered Auto TCP selection as BBRv3, BBRv2, BBR, CUBIC, Westwood, H-TCP and Reno. Auto Qdisc continues to prefer FQ for BBR and FQ-CoDel for other TCP algorithms.
- Grouped related settings and collapsed the advanced settings and kernel dictionary by default.
- Rewrote the kernel dictionary with parameter-specific descriptions, roles and readable units. Added Escape dismissal and focus restoration to the detail sheet.
- Moved Private DNS into its own card, showed Bufferbloat grade and loss with status colors, and added a prompt for the second A/B measurement.
- Simplified app mode choices and compacted the activity log.

### Fixed

- Handled IPv6 zone identifiers in local DNS addresses without throwing an error.
- Showed fixed TSQ and Lowat limits for apps with a manual mode.
- Showed the kernel-reported retry value next to the default option and rendered disabled CAKE choices in neutral colors.
- Reported the reboot needed to recreate FQ MQ queues only when boot priming is enabled.
- Reported TSQ ownership backoff as an informational state and kept subsequent settings reads on the same WebUI module instance.

## v2.1.2

### Fixed

- Reported driver-managed MQ with existing pfifo_fast queues as waiting for a reboot when FQ is already the kernel default. Suppressed the partial-apply toast for that state and reported unsupported manual queue changes separately.
- Refreshed missing mobile radio data when Home first opens on mobile or switches to mobile through an offline state, with a 15-second cooldown.
- Capped the Bufferbloat grade based on packet loss during load.
- Labeled each A/B measurement with its network type and limited deltas to measurements on the same network type.
- Skipped the DoT probe on TCP/853 when automatic DNS uses a local resolver address.
- Omitted unknown Wi-Fi generations from the connection title and synchronized the title with the primary route during handover.
- Kept all six Bufferbloat cells visible during a repeat test and set a 44 px minimum touch target for the TCP retries picker.

## v2.1.1

### Changed

- Moved all WebUI select menus to the shared bottom sheet, including ping targets, Private DNS, TCP retries and route windows.
- Matched option descriptions, selected labels and disabled states across themes in English and Vietnamese.

### Fixed

- Restored page scrolling after closing the picker with the close button, the backdrop or Escape.

## v2.1.0

### Added

- Added an eight-layer compatibility report and a read-only diagnostic export that omits subscriber, address, Wi-Fi and app identifiers. The report includes available root backend and page-size information.
- Added detection for Unisoc and Exynos mobile interfaces, additional battery and skin sensors, and OLED panel states.

### Changed

- Detected TCP congestion control and policy sysctls at startup, reported kernel capabilities and used FQ-CoDel as the fallback for FQ. Unsupported sysctl settings were left alone.
- Excluded CLAT and VPN interfaces from physical-interface tuning and omitted local addresses from mobile gateway readback.
- Read legacy and current Android subscription records, including single-SIM live registry output, and added a scoped Wi-Fi framework fallback.
- Required a complete TLS handshake, system CA trust and provider identity verification before switching to a named Private DNS provider. The system choice restored Android opportunistic mode. An unavailable TLS ABI left the current settings in place.

## v2.0.2

### Fixed

- Read the associated access point from the kernel BSS cache and preserved valid RSSI when a driver returned its own MAC in a station dump.
- Preserved in-flight apply and resume requests during concurrent control events and expired abandoned requests with a one-shot deadline.
- Corrected paused profile labels, advanced Qdisc availability, verification age and feedback for recommended profiles.

## v2.0.1

### Fixed

- Read the connected access point BSSID from station replies and kept the Wi-Fi identity when telemetry expired on the same association.
- Calculated the displayed Bufferbloat delta from the rounded RTT values and retained the measured grade.
- Showed one thermal status dot next to the battery temperature and reused Home kernel readback for standby mobile routes in Settings.

## v2.0.0

### Changed

- Left Wi-Fi power saving with Android and migrated legacy ownership once. Made the F16 gaming lease opt-in, required driver readback and stopped trying the lease on that interface after a failure.
- Isolated secondary Wi-Fi events and used a one-shot handover timer. Applied the route window once per settled route and preset. Used 10/20 on detected 2.4 GHz Wi-Fi and kept the configured preset for other or unknown bands.
- Resolved concurrent foreground apps by rule priority and kept Gaming active for up to five seconds through an overlay without a rule.
- Suspended low-latency leases on persistent weak signal or kernel loss while the WebUI or a lease was active. Required four seconds of clean samples before resuming. Counted link drops per interface and TCP retransmits per network namespace.
- Used the median of five idle ICMP probes for Bufferbloat and withheld the grade when loaded RTT was more than 15 ms below idle RTT.

### Added

- Added thermal, TSQ, link and lease readback to the WebUI and showed the Bufferbloat grade in the result grid.
- Added a separate switch for boot-time Qdisc priming.

## v1.9.4

### Fixed

- Fixed mobile radio cache field splitting on Android mksh and added support for non-negative eSIM slot indices.
- Warmed up ICMP before idle measurements. Kept live HTTP streams across ICMP windows, timestamped echoes first, retained qualifying samples at EOF or the byte cap, and aggregated samples across fallback downloads.
- Used Cloudflare HTTP load endpoints with a 64 MiB cap, a 4.8-second load limit and a 7.5-second total limit. Required enough bytes and valid replies before grading.
- Preserved idle ping tiles during Bufferbloat tests and displayed the correct jitter and loss units for missing values.

## v1.9.3

### Added

- Added an on-demand Bufferbloat measurement that compares idle ICMP RTT with ICMP during a bounded HTTP download. It reported loaded jitter and packet loss and withheld the grade when the download was insufficient.
- Kept the last two measurements on Home for an A/B comparison with their TCP algorithm, Qdisc and operating mode.
- Read the active data SIM, LTE/5G display state and RSRP from the matching live phone block during on-demand mobile refresh. Mobile labels omitted missing signal values and latency units stayed attached to their numbers.

## v1.9.2

### Added

- Exported settings and app rules to a timestamped JSON backup in `/sdcard/Download`. Import replaced saved settings and rules after daemon schema validation, using the existing atomic commit and kernel readback paths.
- Probed DoT with a bounded TLS ClientHello on TCP/853. Included SNI for DNS names and reported ServerHello, HelloRetryRequest or TLS Alert. The probe stopped before certificate verification.
- Supported callback and legacy synchronous WebUI bridges. Honored disable and removal markers at startup and preserved the recovery journal if uninstall could not verify restoration.

## v1.9.1

### Fixed

- Calculated jitter, packet loss, and first and min–max RTT directly from the gateway-only ICMP batch.
- Replaced `Unknown + Unknown` readback labels on inactive network paths with `Inactive (Wi-Fi active)` or `Inactive (Mobile active)`.
- Updated the Home Wi-Fi and Mobile cards to show the confirmed driver-managed MQ state in place of a pending warning.
- Fixed the detail dialog to show the device RAM reported in `status.json`.

### Removed

- Removed generated Python cache files from the repository archive.

## v1.9.0

### Added

- Opened Wi-Fi diagnostics by tapping the Home Wi-Fi card.
- Added selectable and custom ping targets bound to the active egress interface. Choices included `1.1.1.1`, `8.8.8.8`, `9.9.9.9`, Gateway only and a custom hostname or IP address.
- Added read-only Private DNS status and an on-demand DoT connectivity check on TCP/853.

### Changed

- Redesigned Network Route Diagnostics with collapsible secondary interfaces and restyled the Kernel Verification card in Bento style. Fixed label wrapping in Settings and Apps.
- Synchronized daemon and WebUI versions and removed legacy fallback version strings.

## v1.8.1

### Fixed

- Displayed the running daemon version in the WebUI header.

### Changed

- Explained the selected TCP algorithm and queue discipline in the TCP + Qdisc dialog when set to Auto.
- Replaced the CAKE Diffserv dropdown with a Bento-style segmented button group.

## v1.8.0

### Added

- Added an optional Wi-Fi Power Save lease for Gaming and optional TCP leases for autocorking and slow start after idle in Gaming and Max Speed. Screen state and battery temperature gated the leases, and the journal restored the original values.
- Extended optional `initcwnd` and `initrwnd` tuning to verify and apply independently to IPv4 and IPv6 default routes on the active egress interface, skipping cross-interface CLAT and ambiguous routes.
- Added PIE and FQ-PIE detection where supported. Manual configurations could use MTU-based quantum for FQ and FQ-CoDel or Diffserv modes for CAKE.
- Expanded Wi-Fi diagnostics with live Power Save state, lease status, channel width, frequency, band and driver-reported country code.
- Added KernelSU Next OTA metadata and an automated GitHub release workflow for verified tags.

### Changed

- Disabled leases, route windows and advanced Qdisc options by default for new installations. Upgrades preserved saved settings.

## v1.7.0

### Changed

- Replaced hardcoded device profiles with runtime detection of hardware and kernel TCP and Qdisc capabilities. Preferred FQ for BBR and FQ-CoDel for other congestion-control algorithms.

### Added

- Added cellular and VPN interface detection across platforms, handover debounce, first and min–max RTT metrics, and a copy-logs button in the WebUI.

## v1.6.1

### Changed

- Shipped the C11 Netlink daemon with 16 KiB ELF alignment on ARM64 and refined the English and Vietnamese WebUI.

### Fixed

- Fixed TSO handling for `errno=16` and diagnostic export in WebView.
