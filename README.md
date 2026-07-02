# maniflow

A CS:GO/Source-engine-style **surf** game set inside a living math diagram. Ramps are
glowing graph-paper planes labeled with their actual plane equations; the HUD is a
vector readout; the finish line is a limit.

## Play

Any static file server works:

```sh
python3 -m http.server 8742
# then open http://localhost:8742
```

(Three.js loads from a CDN, so you need to be online.)

## Controls

| Key | Action |
| --- | --- |
| Mouse | look / steer |
| A / D | strafe (your main tool on ramps and in air) |
| W / S | ground movement only — release W on ramps |
| Space | jump (hold to auto bunny-hop) |
| R | reset the run |

## How to surf

The physics is real Source-style movement: Quake air-accelerate plus velocity
clipping against convex plane sets. Surfing *is* the clip:

> v′ = v − (v·n̂)n̂

Gravity pulls you into the ramp; the clip resolves it along the plane, so steep
faces accelerate you. Hold the strafe key that presses you **into** the face
(A on a right-hand face), keep W released, and steer with smooth mouse turns.
In the air, sync strafe keys with mouse turns to gain speed (airstrafing).

## The course

Start platform → the great ridge Π₁/Π₂ (peak prism, surf either face) → gap →
the valley (two inward-sloped planes) → launch to the finish platform through
the `lim t→∞` rings. Timer starts when you leave the platform; best time is
kept in localStorage. Fall into the abyss and you respawn at the last
checkpoint with the clock still running.

## Tech

Single self-contained `index.html`: Three.js, custom anti-aliased tri-planar
graph-paper shader, convex-prism colliders generated from 2D cross-sections,
fixed 120 Hz physics tick.
