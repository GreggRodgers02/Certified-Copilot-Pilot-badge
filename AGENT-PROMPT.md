# Recognition Agent — design notes

The instructions themselves live in [`agent-instructions.md`](agent-instructions.md),
ready to paste into Agent Builder. This file explains why they are written that way.

## Why the prompt no longer describes the badge

An earlier version spent about 1,100 words describing how to draw the badge — ring
gradients, feather counts, aircraft geometry — then asked the agent to render it and
self-check the result against a 13-point visual list. That cannot be consistent.
Image generation samples a new image every run, so the badge differs each time, and
a model cannot reliably audit fine visual detail in its own output, so the pass/fail
gate did not gate anything.

The current version supplies the badge as an uploaded file and has the agent
**composite** it in code. Badge pixels are copied, not redrawn. Every run is
identical.

That original prompt was 7,951 characters against an 8,000 limit. Deleting the
drawing spec freed roughly 4,600, which went to the things that actually reduce
variance: a working reference implementation, input handling, batch support, and
explicit failure wording.

## Geometry

Measured from the PNG's alpha channel. The transparent center has a radius of 295px
on a 750×750 canvas; clipping at 298 tucks the photo just under the ring with no
visible seam. The photo is scaled by a single factor derived from its shorter side,
which fills the circle without distortion.

Verified against portrait (600×900) and landscape (1600×700) sources: 750×750 RGBA
output, badge pixels unmodified in both.

## Why files are identified by pixels, not by order

The agent cannot count on being told which upload is which — the normal interaction
is two images and no text. Filenames are unreliable and upload order is not
guaranteed, so the badge is detected by its transparent center, sampled at five
points rather than one to avoid a false positive on a stray transparent pixel.

Tested against six inputs: the real badge, a portrait photo, a landscape photo, a
square opaque RGBA image, a single-transparent-pixel file, and a finished
recognition image being re-uploaded. All six classify correctly.

`is_badge` swallows exceptions deliberately. A simulated batch containing one
corrupt file showed it raising during partitioning, which killed every headshot in
the message before compositing began — the opposite of the failure isolation the
instructions promise. Unreadable files now sort to headshots and fail individually.

## Why there is no step-by-step wizard

A "type start, then send the badge, then send the headshot" flow costs three
round-trips for a one-message job, and it still needs the silent two-image path
underneath, since users drop files without being asked. It also infers file roles
from turn position, which is less reliable than checking the pixels. The one real
gap it addressed — a greeting with no attachments — is handled by asking for both
files at once.

## Open items

- The instructions and the badge PNG in this repo describe different designs, and
  the boundaries section forbids the Copilot mark that the PNG contains. Resolve
  before rollout.
- Copilot's per-message file limit and whether the code sandbox persists uploads
  across turns are both untested. The badge-reuse rule depends on the second.

## Fallback

If the agent's code tool cannot accept image uploads, no prompt will fix it — that
is a capability ceiling, not a wording problem. Use [`overlay.html`](overlay.html),
which performs the same composite in the browser with the same geometry.
