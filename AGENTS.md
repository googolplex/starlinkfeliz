# AGENTS.md — Starlink Dishy Recovery

## Scope and isolation

This repository concerns only the Starlink system documented here. It is completely separate from vessel telemetry work. Never modify, reference as configuration, or place Starlink artifacts inside `googolplex/telemetria-barcos`.

## Diagnostic method

1. Read `README.md`, the relevant incident note, hardware history, GPS note, and available debug baselines before proposing actions.
2. Treat the router and dish as separate devices. Compare their firmware, uptime, boot counters, update states, RF state, network state, and alerts independently.
3. When new debug data arrives, compare it against both:
   - `debug/2026-09-05-failing-redacted.json`
   - `debug/2026-09-05-working-redacted.json`
4. Prefer evidence from telemetry over assumptions about cables, power, firmware, or RF hardware.
5. Do not infer that generic telemetry fields imply installed hardware. Example: battery-related fields may exist with zero values even when there is no user-serviceable battery.
6. Do not recommend factory reset, repeated power cycling, cable replacement, or hardware replacement casually. Explain the evidence and expected diagnostic value first.
7. Preserve chronology. Boot counters are cumulative; uptime is per boot. Do not confuse a high boot count with current uptime.
8. Preserve uncertainty. Distinguish confirmed observations from likely explanations.

## Known baselines

### Failing state — 2026-09-05

- Dish firmware: `2026.01.05.mr71198`
- Dish bootcount: `499`
- Dish uptime at capture: `28 s`
- Dish RF ready: `false`
- Dish POP ping drop rate: `1`
- Dish software update progress: `0`
- Dish Ethernet: `1000 Mbps`
- Router firmware: `2026.08.27.mr84914`
- Router uptime at capture: `5703 s`
- Router bootcount: `192`

### Working state — 2026-09-05

- Dish firmware: `2026.08.31.cr85832`
- Dish bootcount: `817`
- Dish uptime at capture: `590 s`
- Dish RF ready: `true`
- Dish POP ping drop rate: `0`
- Dish software update progress: `1`
- Dish Ethernet: `1000 Mbps`
- Initialization: RF ready `30 s`, initial network entry `45 s`, first POP ping `55 s`, stable connection `171 s`
- Router firmware: `2026.08.27.mr84914`
- Router uptime at capture: `1751 s`
- Router bootcount: `200`

## Persistent GPS condition

The GPS fault predates the September 2026 firmware recovery and reportedly began after the dish was accidentally driven over by a pickup truck. External housing did not visibly break. In the recovered working state, the main RF/network path works while GPS reports no satellites. Treat physical GPS/front-end/interconnect damage as a plausible hypothesis, not a proven component-level diagnosis.

## Safety and preservation

- Do not advise opening the sealed dish merely for exploratory inspection while service is working.
- Do not commit unredacted debug exports.
- Keep original evidence unchanged outside the repository if the user chooses to retain it privately.
