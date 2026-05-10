# LOCAL

Track intentional fork drift for the default fork layout.

## Current Drift

- `main` is based on `upstream/main`.
- The fork carries only Brian's fork metadata and local install wiring:
  - version suffix `3.1.0-0xble.0.1.0`
  - `bin/upgrade`
  - `bin/smoke`

## Sync Notes

- Do not keep separate local feature branches in this checkout.
- Future upstream base bumps should reset the fork suffix to `0xble.0.1.0`
  unless the same upstream base has already shipped with a higher suffix.
