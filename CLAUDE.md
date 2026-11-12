# bowling-ball-taps

Classroom animation for Richard Wright's Advanced Physics class, built for the circular motion exploration's first observation (Bowling Ball, Whole Class): a bowling ball rolls in a straight line and students work out where to tap it with a rubber mallet so it makes a smooth circular turn to the right, beginning at point A. It revisits malletball.

Live at **https://wrightphysics.org/bowling-ball-taps/** (repo `WrightPhysics/bowling-ball-taps`, GitHub Pages from `main`, root). The homepage card is in `WrightPhysics/wrightphysics.github.io`.

## How the project works

- Everything is in **one file: `index.html`**, with inline CSS and JS and no build step. The only outside dependency is Google Fonts.
- **Deploying = pushing to `main`** (GitHub Pages). Test with a cache-busting query string (`?v=2`).
- Commit and push only when Richard asks.

## The four scenarios

1. **No taps:** constant velocity.
2. **One tap to the right at A:** one change in velocity, then a new straight line.
3. **Repeated taps to the right:** a tap at every dot from A on; the path bends but the speed grows.
4. **Repeated taps toward the center:** a tap at every dot from A on, each aimed at the center of the circle; the ball follows the arc at constant speed and keeps circling.

**Stop tapping** (scenarios 3 and 4) ends the taps mid-run so the ball leaves in a straight line.

## Physics model

- Top view, canvas 760 x 640, math coordinates with y up (`Y()` flips for drawing). Ball starts below A moving up at `V0`.
- Motion is straight lines between events. An event happens every `T = edge / V0`; each event drops a position dot and, depending on the scenario, applies a tap (an instant change in velocity of size `dv`).
- `n` = taps per quarter turn (slider, 3 to 18). `th = 90 deg / n`, `edge = 2 R sin(th/2)`, `dv = 2 V0 sin(th/2)`. The same `dv` is used in scenarios 2, 3 and 4.
- Scenario 4 traces a regular polygon inscribed in the circle of radius `R`. The center `C` sits `R sin(th/2)` below A's level (not directly to its right) so that every tap is equal, points at `C`, and the speed stays exactly `V0`.
- After one full lap in scenario 4 the dots, arrows and path stop recording (`S.recording`); Stop tapping starts a new path segment from the last tap.
- Colors come from the CSS tokens in `:root` (light and dark); the canvas reads them each draw.

Keys: 1-4 scenario, Space play/pause, R reset, S stop tapping.
