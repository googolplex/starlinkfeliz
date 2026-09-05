# Persistent GPS Failure

## Reported history

GPS stopped functioning after the dish was accidentally driven over by a pickup truck. The external shell did not visibly break.

## Telemetry after firmware recovery

In the known-good Internet/RF state on 2026-09-05:

- `gpsValid=false`
- `gpsSats=0`
- `noSatsAfterTtff=true`
- `rf=true`
- initial network entry succeeded
- POP connectivity succeeded with zero instantaneous packet loss

This demonstrates that the persistent GPS fault is separable from the September firmware boot-loop problem: the main Starlink RF/network path recovered while GPS remained unavailable.

## Working hypothesis

Physical damage to some part of the GPS/GNSS receive path is plausible, for example an antenna element, interconnect, PCB trace/solder joint, low-noise amplifier, or related front-end circuitry. The available debug telemetry cannot identify the damaged component, so this remains a hypothesis rather than a confirmed component-level diagnosis.

## Diagnostic policy

If GPS is investigated again:

1. Place the dish outdoors with a clear sky and away from nearby metal structures/vehicles.
2. Allow sufficient uninterrupted operating time.
3. Capture fresh debug data while normal Internet service remains active.
4. Compare `gpsValid`, `gpsSats`, `noSatsAfterTtff`, RF state, initialization timings, and any GPS-related alerts against the known-good baseline.
5. Do not open the sealed dish merely to inspect it while otherwise functional.
