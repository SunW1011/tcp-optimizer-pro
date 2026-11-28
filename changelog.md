# Changelog

## v2.7.1

### Changed
- Made checked switch thumbs actually visible on Dark/AMOLED and added focus outlines to every switch and App search.
- Bumped tight controls to 40 px, padded Quick Profiles so corners stop getting clipped, and separated thermal buttons from their background.
- Unified Kernel Reference and Support tabs; toned down the second primary button in DoT.
- Reused interface counter FDs and stopped rescanning thermal zones for GPU/Wi-Fi sensors your phone doesn't have.
- Action now prints the real Companion install error code instead of silently shrugging.

### Fixed
- Stopped Bufferbloat from rage-quitting slow downloads right after HTTP headers.
- Taught the 60s Companion watchdog to reset its timer while live pushes are flowing.
- Bumped log dedup to 1,024 bytes and rolled back half-written debug lines instead of gluing timestamps together.
- Restored Quick Profile takeover over custom Auto settings, plus a direct fallback when `timeout` is missing.

### Removed
- Evicted 4 unused nav SVGs and 9 dead localization strings.

## v2.7.0

### Added
- Compact temperature bars on Home, a Bufferbloat A+ to D scale, a cancel button, and a second HTTP load provider.

### Changed
- Folded route details into the connection card and grouped Ping, Bufferbloat, and DoT into one tabbed panel.
- Better keyboard access for app profiles, settings info buttons, and the USDT address (no more lone character falling onto line two).
- Batched debug writes, cut redundant kernel readbacks, and split route observation and Companion peer discovery out on their own.

## v2.6.2

### Changed
- Background Auto now backs off from 2s to 5s to 15s when idle instead of poking the CPU every 2 seconds all day.
- Moved config and installer locks off flash onto runtime tmpfs, with retries for brief startup lock contention.
- Fixed theme contrast, widened touch targets, and cleaned up the shared Wi-Fi/mobile recommendation control.

### Fixed
- Kept fresh interface flags and MTU on merge; restored Android API and conflict details in diagnostic exports.
- Fixed recommended-profile takeover when CWND was already on, and stopped pointless thermal rescans without a skin sensor.

## v2.6.1

### Added
- Boot-time Qdisc priming for compatible MQ leaves, naming the chosen Qdisc in reboot notices.

### Changed
- Clarified quantum, CAKE Diffserv, and low-latency descriptions.

## v2.6.0

### Added
- Live event-driven status pushes in Companion and mid-test Bufferbloat latency/throughput readouts.

### Fixed
- Wi-Fi diagnostics after roaming and repeated Qdisc refreshes while waiting for VPN to disconnect.

## v2.5.6

### Changed
- Routed public probes over active VPNs and blocked strict Private DNS changes while tunneled.
- Kept pending applies across handovers and surfaced TCP ownership conflicts after kernel readback.
- Synced Companion theme/system bars, added launcher-visible system apps, and polished WebUI accessibility.

### Fixed
- Transient Wi-Fi power-save failures, escaped Unicode, and exclusive shared-storage saves.

## v2.5.5

### Fixed
- Persistent TCP/Qdisc conflicts after external edits — changing a network setting or hitting Reapply reclaims ownership while preserving the original value for Restore.

## v2.5.4

### Changed
- Clarified why hardware MQ limits choices to Auto and fq.
- Hid half-loaded Home cards at startup and gave Companion a short wake window for a fresh snapshot.

### Fixed
- Companion System theme on launch and live Android light/dark switches.
- Battery badge during cooldown; kept the TSQ cap until the battery actually cools.

### Removed
- Internal IPA control interfaces from the secondary network list.

## v2.5.3

### Added
- Matched cellular CLAT support for IPv4 probes and longer Bufferbloat/Private DNS timeouts.

### Changed
- Broader backlight, thermal, and radio checks; more system apps and extra HyperOS overlay filters.
- Clarified advanced Qdisc behavior in Auto and showed driver MQ as informational.

### Fixed
- Initial TCP windows after Wi-Fi roaming/band steering while keeping expiring IPv6 RAs intact.
- Repeated event logging after log clears and safe interface names in diagnostic exports.

## v2.5.2

### Changed
- Filtered repeated secondary Wi-Fi events, read channel frequency before applying windows, and filtered 3 more HyperOS overlays.
- Bounded Companion worker shutdown, aligned import limits, and capped Wi-Fi radio probes at 2s.
- Better narrow-screen contrast/truncation and Wi-Fi Direct names in diagnostics.

### Fixed
- Dual Wi-Fi restore now ignores self-echo Netlink events and keeps live gateway/MTU.
- Cleared stale Signal Guard status when sampling stops and kept thermal recovery alive across screen changes.

## v2.5.1

### Added
- Worker restart backoff and a bounded app icon cache.

### Changed
- Served fast reads inside the IPC worker, cut redundant telemetry updates, and synced public metadata before draft releases.

### Fixed
- Companion config picker, full imports, Android Back navigation, and upgrades via Action.

### Removed
- Periodic Companion polling while idle.

## v2.5.0

### Added
- App-owned Unix socket for Companion with daemon-side peer authentication.

### Changed
- Bundled Companion APK in the module ZIP and launched it from Action.

### Fixed
- Back navigation and saving to document providers that omit display names.

## v2.4.0

### Added
- Standalone Companion app running the same WebUI, Android document picker for exports/reports, and real app labels/icons.

### Changed
- Release packaging now ships the module ZIP and signed APK with one shared checksum file.

## v2.3.2

### Added
- HTTP load throughput readout in Bufferbloat results.

### Changed
- Icon-only Home mode buttons with accessible labels, single-row 320 px temps, side-by-side A/B results, and collapsible route details.
- Opaque top/bottom bars, unified segmented controls, consistent radii/fonts, and a 4-column 0.5°C thermal picker.
- Regrouped System cards with side-by-side Reapply/Restore, single-line app metadata, log actions in the header, and sharper AMOLED delete contrast.

## v2.3.1

### Added
- Read-only battery thermal bar, 0.5°C steps, 3 presets, exact picker, and a Companion-ready save adapter.

### Changed
- Moved profiles/routes into the Home header, TCP metrics into a 2×2 grid, and temps into one strip.
- Ranked TCP/Qdisc pickers, disabled incompatible MQ queues, added real app labels with bounded icon loading, and synced probes with active language.

## v2.3.0

### Added
- VPN protection for initial TCP windows (restores physical IPv4/IPv6 routes and resumes 5s after disconnect) plus VPN pause status in UI/reports.

### Changed
- Kept compact TSQ readouts on one line on narrow screens.

### Fixed
- Missing app icons on first visit when opening from cache.

## v2.2.6

### Added
- Installed app icons (with initial fallback) plus GitHub, Telegram, and offline bank/USDT QR codes.

### Changed
- Split daemon vs routing controls, aligned System buttons, full-width Bufferbloat button, and added a startup-only log note.

## v2.2.5

### Added
- Shared folder browser for backups and diagnostic exports, including creating folders.

### Changed
- Pinned Network/Advanced/System tabs, streamlined Export/Import flow, and simplified diagnostic preview actions.

## v2.2.4

### Added
- Clear button for suggested backup/report filenames.

### Changed
- Unified folder picker, shorter default filenames, Android file picker on main Import, and Save file first in diagnostics.

## v2.2.3

### Added
- Custom filenames/folders with overwrite confirmation, Android file picker JSON import, and Dual Wi-Fi deferral details.

### Changed
- Rechecked pending applies after backgrounding and clarified paused app-rule notices.

### Fixed
- CWND status on restore/pause, plus keyboard dismissal and focus restoration on app sheets.

## v2.2.2

### Added
- Dual Wi-Fi pause notice in Home and Settings.

### Changed
- Restored Wi-Fi CWND on Dual Wi-Fi (15s resume on single Wi-Fi), released Gaming Wi-Fi lease, and deferred station queries 2.5s after link events.

## v2.2.1

### Changed
- Single-row mobile radio readouts, preferred Kernel Reference ordering, clearer Lowat/CWND text, and shorter app hints.

### Fixed
- Kept Light theme when host WebView prefers dark; enabled TCP low-latency leases under Auto with guards intact.
- Kept Signal Guard sampling via kernel retransmits, included restore/resume/reapply in Apply filter, wrapped RTT ranges, debounced thermal saves, and cleared Quick Profile highlights when paused.

## v2.2.0

### Added
- Quick Profiles (*Maximum speed*, *Gaming / Low latency*, *Balanced & battery saving*) and live autocork/SACK/retry/ECN sysctls.

### Changed
- Auto TCP order `BBRv3 → BBRv2 → BBR → CUBIC → Westwood → H-TCP → Reno`; grouped/collapsed settings, rewritten Kernel Reference, dedicated Private DNS card, colored Bufferbloat, and compact logs.

### Fixed
- IPv6 zone IDs in local DNS, fixed manual app TSQ/Lowat limits, kernel retry labels, neutral disabled CAKE options, scoped MQ reboot notice, and informational TSQ backoff.

## v2.1.2

### Fixed
- Driver MQ reboot-wait notice, 15s mobile radio refresh, loss-capped Bufferbloat grades, same-network A/B deltas, and skipping DoT on local DNS.
- Omitted unknown Wi-Fi generations, synced handover titles, kept all 6 bloat cells on repeats, and set a 44 px touch target on TCP retries.

## v2.1.1

### Changed
- Moved all select menus to the shared bottom sheet with matched EN/VI descriptions and theme contrast.

### Fixed
- Restored page scroll after closing pickers.

## v2.1.0

### Added
- Eight-layer compatibility report, privacy-filtered diagnostic export, Unisoc/Exynos interfaces, extra thermal sensors, and OLED panel states.

### Changed
- Runtime TCP/sysctl detection (`fq_codel` fallback), excluded CLAT/VPN from physical tuning, stripped local mobile gateways, and required full TLS/CA verification before switching Private DNS.

## v2.0.2

### Fixed
- Associated AP from BSS cache, valid RSSI preservation, concurrent apply/resume deadlines, and paused/Qdisc/recommended labels.

## v2.0.1

### Fixed
- AP BSSID from station replies, rounded Bufferbloat delta, single battery thermal dot, and reused standby mobile readback.

## v2.0.0

### Added
- Thermal, TSQ, link, and lease readback, Bufferbloat grade in grid, and a separate boot Qdisc switch.

### Changed
- Left Wi-Fi power saving with Android (opt-in F16 Gaming lease), isolated secondary Wi-Fi, `10/20` on 2.4 GHz, 5s Gaming overlay hold, Signal Guard 4s recovery, and median of 5 idle ICMP probes.

## v1.9.4

### Fixed
- Mobile radio field splitting on `mksh`, eSIM slot indices, ICMP warmup, 64 MiB/4.8s/7.5s Cloudflare streaming, preserved idle ping tiles, and missing units.

## v1.9.3

### Added
- On-demand Bufferbloat test, Home A/B latency comparison, and active SIM LTE/5G/RSRP refresh.

## v1.9.2

### Added
- Timestamped JSON backup export/import, bounded `TCP/853` DoT ClientHello probe, legacy bridge support, disable/remove markers, and journal retention on failed uninstall.

## v1.9.1

### Fixed
- Gateway-only ping metrics, `Inactive` standby link labels, confirmed Driver MQ on Home, and device RAM in details.

### Removed
- Stray Python cache files from the archive.

## v1.9.0

### Added
- Tappable Wi-Fi diagnostics, selectable/custom egress-bound ping targets, and read-only Private DNS + DoT check.

### Changed
- Collapsible route diagnostics, Bento kernel verification card, and synced daemon/WebUI versions.

### Fixed
- Label wrapping in Settings and Apps.

## v1.8.1

### Changed
- Explained Auto TCP/Qdisc picks in details and moved CAKE Diffserv to segmented buttons.

### Fixed
- Displayed the running daemon version in the header.

## v1.8.0

### Added
- Optional Gaming Wi-Fi and TCP leases, independent IPv4/IPv6 `initcwnd`/`initrwnd`, PIE/FQ-PIE, MTU quantum, CAKE Diffserv, expanded Wi-Fi diagnostics, and KSU Next OTA + release workflow.

### Changed
- Leases, route windows, and advanced Qdisc options default off on fresh installs.

## v1.7.0

### Added
- Cellular/VPN detection, handover debounce, first/min–max RTT metrics, and a copy-logs button.

### Changed
- Replaced hardcoded device profiles with runtime TCP/Qdisc capability detection.

## v1.6.1

### Changed
- Shipped the C11 Netlink daemon with 16 KiB ARM64 ELF alignment and refined EN/VI WebUI.

### Fixed
- TSO `errno=16` handling and WebView diagnostic export.