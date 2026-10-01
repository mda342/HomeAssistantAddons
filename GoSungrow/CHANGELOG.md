## [3.0.16] - 2026-10-01
### Fork build (mda342)

- Fix via_device circular reference in MQTT discovery payload.
  ViaDevice was set to swname (software name) for all devices, causing
  a circular reference when swname == parentId (root device). This
  resulted in "A device can not be its own via device" errors when
  Home Assistant tried to register MQTT select entities.
- Fix: Only set ViaDevice when there is an actual parent device
  (swname != parentId). Root devices now have an empty ViaDevice.
- Rebuilt binaries verified by sha256 in `getRelease.sh`.

## [3.0.15] - 2026-08-05
### Fork build (mda342)

- Complete the rebrand of the sensor device discovery: parent devices created by
  `SetDeviceConfig` now advertise `sw_version` as
  `GoSungrow https://github.com/mda342/GoSungrow` and the default vendor is
  `mda342`. The 3.0.14 image only rebranded the "Service" device; the sensor
  devices still showed the MickMake URL/vendor. Rebuilt binaries verified by
  sha256 in `getRelease.sh` (amd64
  `c60116258f0955708e8f32d7c74ef7ba6b36c73a57a9dcaa70e39136b52914ea`).


## [3.0.14] - 2026-08-05
### Fork build (mda342)

- `getRelease.sh` now verifies the downloaded binary's sha256 against the
  expected per-architecture value before installing it. This also busts the
  Docker build cache for the `COPY src/` layer, which the 3.0.13 build reused
  (that layer is unchanged between releases, so the old pre-rebrand binary was
  baked in and the rebranded `sw_version`/`manufacturer` never reached the
  image). The download step now re-runs and must pass both the sha256 check and
  the execution check.


## [3.0.13] - 2026-08-05
### Fork build (mda342)

- Rebrand the fork: user-visible MQTT discovery strings now identify as mda342
  (`sw_version` and `manufacturer`), the add-on repository metadata, maintainer
  emails, and donation links point to mda342 instead of MickMake. Go module
  paths and historical links are unchanged. Requires the rebuilt release
  binaries.

- The `sw_version` shown in the HA device registry is now
  `GoSungrow https://github.com/mda342/GoSungrow` and `manufacturer` is
  `mda342`. Rebuilt release assets are statically-linked
  (`CGO_ENABLED=0`); amd64 tarball sha256
  `20918c070f03ec9cfc652993419a096718de26015e2939ef818f6ca2356b48c2`.


## [3.0.12] - 2026-08-05
### Fork build (mda342)

- `getRelease.sh` now runs the downloaded binary (`GoSungrow help`) at build
  time and aborts the build if it cannot execute. The 3.0.11 image carried the
  cached glibc binary because `config.yaml` (repo root) is not part of the
  `COPY src/` layer, so the download step never re-ran; the execution check
  guarantees a future build ships a working binary or fails loudly.


## [3.0.11] - 2026-08-05
### Fork build (mda342)

- Rebuild the fork release binaries as statically-linked (`CGO_ENABLED=0`).
  The previous build linked against glibc, which cannot exec on the Alpine base
  image (add-on failed at startup: `/usr/local/bin/GoSungrow: No such file or
  directory`). The amd64 binary now has sha256 `4e563b1282c212540f022b144bff
  2829d8e00dcc97993609159bf9ca9d552e34`.


## [3.0.10] - 2026-08-05
### Fork build (mda342)

- Log the downloaded binary's sha256 at build time so the running image can be
  verified against the fork release.


## [3.0.9] - 2026-08-05
### Fork build (mda342)

- Drop `last_reset_value_template` from non-energy total sensors (it errored on
  every state payload, which never carries a `last_reset` key).


## [3.0.8] - 2026-08-05
### Fork build (mda342)

- Add-on now fetches the GoSungrow binary release from the mda342 fork, which
  carries Home Assistant 2026.7 compatibility fixes:
  kWp/Wh/m² device classes, energy `total_increasing` state class without
  `last_reset`, no state_class on string sensors, entity categories, unit
  normalization.


## [3.0.7] - 2023-09-04
### Features

- Alpha support for Modbus, (direct connect to your Sungrow inverter).


### Fixes

- Fixup ResultData.result_data.org_id error.


## [3.0.6] - 2023-05-10
### Features

- Added extra sub-commands:
```
show ps save
show device save
show template save
show point save
show point ps-save
show point device-save
show point template-save
```

### Fixes

- HA binary_sensor not being set correctly.


## [3.0.5] - Not released


## [3.0.4] - 2023-01-05
### Features

### Fixes

- Fixes to the Energy Dashboard of HA.


## [3.0.3] - 2022-12-23
### Features

- Merry Christmas!
- Now supports the Energy Dashboard of HA!

### Fixes

- Fix double virtual.virtual entries.
- Fixup float value determination logic.
- CacheTimeout matches fetch schedule.
- Fixed unit type guessing - "Template error: float got invalid input"
- Fix battery class - correct point used for HA.
- Added more DeviceClass types for HA - will affect long term stats as units will change on some points.


## [3.0.2] - 2022-12-21
### Features

- Control of GoSungrow via MQTT; gosungrow_option_fetchschedule, gosungrow_option_loglevel, gosungrow_option_sleepdelay & gosungrow_option_servicestate
- Updated MQTT message types.

### Fixes

- Incorrect units on points p13119 & p13149.


## [3.0.1] - 2022-12-15
### Changed

- HA install fixups.


## [3.0.0] - 2022-12-14
### Changed

- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/10))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/9))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/8))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/7))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/6))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/5))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/4))
- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/3))


## [2.2.0] - 2022-03-21
### Changed

- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/2))


## [2.1.3] - 2022-03-14
### Changed

- GoSunGrow for HA ([fixes #1](https://github.com/MickMake/GoSunGrow/issues/1))

