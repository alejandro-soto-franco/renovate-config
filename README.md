# renovate-config

Shared Renovate preset for the repositories under this account.

Consume it from a repository by adding `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>alejandro-soto-franco/renovate-config"]
}
```

## Preset behaviour

- Groups non-major Cargo updates into one pull request, and non-major Python
  updates into another. Routine bumps arrive as two reviews per week, down from
  thirty.
- Isolates major bumps and delays them for seven days. A release that gets
  yanked is therefore never the one under review.
- Keeps `pyo3`, `numpy`, `pyo3-build-config` and `pyo3-ffi` in a single group.
  A split pull request across those never builds.
- Routes GPU and CUDA crates (`cust`, `cudarc`, `ash`, `wgpu`, `cubecl`,
  `cuda-oxide`) through dashboard approval, since those bumps are coupled to
  the hardware and driver on the machine.
- Runs lock file maintenance monthly.
- Schedules everything before 09:00 on Monday, America/New_York.

Commits follow the conventional-commit form already used across these
repositories, `chore(deps): ...`.
