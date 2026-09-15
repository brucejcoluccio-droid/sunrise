# Sunrise

A dawn-simulator alarm that runs as an installed web app on Android.

- gradual light ramp: ember → orange → amber → daylight, squared curve
- deep-red seven-segment clock overnight, with pixel shifting to avoid burn-in
- alarm fires from three independent timers, hold-to-stop, 9-minute snooze
- optional backup alarm handed to the system Clock app
- works fully offline once installed

**Setup: see [SETUP.md](SETUP.md).**

Honest limits: a phone panel puts out roughly 30 lux at half a metre, against
about 500 lux for a purpose-built wake-up light. This is a timing and colour
cue, not a light dose. It travels well; it does not replace a lamp.
