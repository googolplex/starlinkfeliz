# Starlink Dishy Recovery

Technical incident log and diagnostic baseline for one Starlink Gen-2 system with a rectangular `rev3_proto2` dish.

This repository is intentionally **separate** from all vessel/telemetry projects. Nothing here should be copied into `googolplex/telemetria-barcos`.

## Current status

- Service recovered on 2026-09-05 after a prolonged dish reboot loop.
- Known failing dish firmware: `2026.01.05.mr71198`.
- Known working dish firmware after recovery: `2026.08.31.cr85832`.
- Router firmware during the incident: `2026.08.27.mr84914`.
- Dish Ethernet link: 1000 Mbps in both failing and working captures.
- GPS remains nonfunctional (`gpsValid=false`, `gpsSats=0`, `noSatsAfterTtff=true`) after prior physical compression by a pickup truck.
- Main Starlink RF/network operation is currently functional despite the GPS fault.

## Repository layout

- `AGENTS.md` — rules for future ChatGPT/Codex diagnostic work.
- `incidents/2026-09-05-reboot-loop.md` — reboot-loop incident and recovery.
- `notes/hardware-history.md` — physical/system history relevant to diagnosis.
- `notes/gps-damage.md` — persistent GPS fault and evidence.
- `debug/` — redacted known-bad and known-good debug snapshots.

## Privacy

Do **not** commit unredacted Starlink debug exports. They may contain account identifiers, push tokens, device identifiers, MAC addresses, IP addresses, Wi-Fi details, and client information. The snapshots in `debug/` are curated redacted diagnostic extracts intended for comparison.

## Resume prompt

In a new chat, use:

> Continue `googolplex/starlinkfeliz`. Read `AGENTS.md`, `README.md`, the latest incident note, and the available debug baselines before diagnosing anything.
