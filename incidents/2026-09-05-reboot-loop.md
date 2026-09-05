# Incident — 2026-09-05 Dish Reboot Loop

## Summary

After the Starlink system had been left powered off for roughly a year, the dish entered a persistent reboot loop during return to service. The router remained substantially more stable than the dish. After many automatic restarts, the dish eventually downloaded/installed newer software, rebooted, and returned to normal Starlink RF/network operation.

## Evidence before recovery

Known-bad debug snapshot:

- Dish hardware: `rev3_proto2`
- Dish firmware: `2026.01.05.mr71198`
- Dish bootcount: `499`
- Dish uptime: `28 s`
- `rf=false`
- `popPingDropRate=1`
- no successful initial network entry recorded
- software update progress `0`
- Ethernet link `1000 Mbps`
- no `noEthernetLink` alert

Router in the same snapshot:

- Firmware: `2026.08.27.mr84914`
- Uptime: `5703 s`
- Bootcount: `192`

This strongly localized the repeated restarting to the dish rather than the router.

## Recovery

The user observed that the system finally downloaded something, installed it, restarted, and then worked. A fresh debug capture confirmed a major dish firmware change:

- old dish firmware: `2026.01.05.mr71198`
- recovered dish firmware: `2026.08.31.cr85832`

Recovered-state telemetry:

- Dish bootcount: `817`
- Dish uptime: `590 s`
- `rf=true`
- `popPingDropRate=0`
- software update progress `1`
- RF ready in `30 s`
- initial network entry in `45 s`
- first POP ping in `55 s`
- stable connection in `171 s`
- Ethernet link remains `1000 Mbps`

Router at this point:

- firmware unchanged: `2026.08.27.mr84914`
- bootcount: `200`
- uptime: `1751 s`

## Interpretation

The evidence is consistent with a dish-side software/firmware recovery problem after an extended offline period. It does not prove the exact internal recovery mechanism. The very large increase in dish bootcount relative to router bootcount supports repeated dish restarts rather than repeated whole-system power loss.

## Cable/power observations

The dish cable was replaced with a new cable and both terminals were physically inspected. Debug telemetry in both failing and working states negotiated 1000 Mbps Ethernet. The recovered router reported no high-cable-ping-drop, poor-WAN-Ethernet, PoE-overcurrent, PoE-undervoltage, or dish-unreachable alerts. This makes the cable a weaker explanation for the September reboot-loop incident.

## Current action

Leave the recovered system powered and stable. Avoid unnecessary factory resets or manual rebooting. Capture new debug data if the fault recurs and compare it against the two baselines.
