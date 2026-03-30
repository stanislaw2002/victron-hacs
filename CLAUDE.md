# CLAUDE.md

## Project Overview

This is a **fork** of [keshavdv/victron-hacs](https://github.com/keshavdv/victron-hacs) — a Home Assistant Custom Integration (HACS) that exposes data from Victron devices via Bluetooth Low Energy (BLE) Instant Readout advertisements.

**Fork owner:** [stanislaw2002](https://github.com/stanislaw2002/victron-hacs)

### What this fork changes

The upstream integration only exposes a single set of output sensors for AC Chargers (output 1). This fork adds individual sensors for all 3 AC charger outputs — voltage, current, and power for outputs 1, 2, and 3.

## Repository Structure

- `custom_components/victron_ble/` — the HA integration
  - `manifest.json` — integration metadata, version, and dependencies
  - `device.py` — BLE advertisement parsing; maps parsed data to sensor keys
  - `sensor.py` — sensor entity descriptions and HA sensor platform setup
  - `const.py` — constants (domain name)
  - `config_flow.py` — HA config flow for device setup
  - `__init__.py` — integration setup
- `hacs.json` — HACS repository metadata
- `requirements_test.txt` — test dependencies

## Git Remotes

- `origin` — this fork (`stanislaw2002/victron-hacs`)
- `upstream` — original repo (`keshavdv/victron-hacs`)

To sync with upstream: `git fetch upstream && git merge upstream/main`

## Version Bumping (IMPORTANT)

This is a HACS integration. **Every push that changes integration code must include a version bump.** HACS uses the version field to detect updates for users.

The version lives in one place:
- `custom_components/victron_ble/manifest.json` → `"version"` field

When bumping:
1. Use semver (MAJOR.MINOR.PATCH)
2. Bump PATCH for bug fixes and small changes
3. Bump MINOR for new features (like adding sensors)
4. Bump MAJOR for breaking changes
5. The version in `manifest.json` must be updated **in the same commit or PR** as the code change — do not push code changes without a version bump

## Dependencies

The integration depends on the `victron_ble` Python library (specified in `manifest.json` under `requirements`). If upstream bumps this dependency, we need to match it when syncing.

## Syncing with Upstream

When pulling new changes from `keshavdv/victron-hacs`:
1. `git fetch upstream`
2. `git merge upstream/main`
3. Reapply the 3-sensor AC charger changes if they conflict (modifications are in `device.py` and `sensor.py`)
4. Bump the version in `manifest.json`
5. Commit and push
