# Vibration Monitor for Corvus GCS

A plugin for [Corvus GCS](https://github.com/M-BSquared/CorvusGCS), the
offline ground control station for PX4 and ArduPilot.

A live graph of gyro coning, gyro high frequency and accelerometer high
frequency vibration, with the cumulative clipping counters beside it. While it
is open it asks the autopilot to send `VIBRATION` more often, and puts the
default rate back when you close it.

Install it in Corvus GCS under Settings, Plugins. The full description is in
the [Corvus guide](https://m-bsquared.github.io/CorvusGCS/guide/plugins.html#vibration).

## What it is

A Rust crate (`corvus_plugin_vibration`) built on `corvus_api`, the plugin API of Corvus GCS, and
published as a shared library from this repository.

- `src/lib.rs`: the plugin, its rules and what is drawn.
- `lang/`: German, French and the dialect file.

## Change it

Corvus GCS carries this repository as a submodule at `plugins/vibration`, and the
crate is a member of its workspace:

```bash
git clone --recurse-submodules https://github.com/M-BSquared/CorvusGCS.git
cd CorvusGCS
./run.sh
```

Settings, Plugins then offers the copy built there. A dependency must be one
that `Cargo.lock` of Corvus GCS already holds.

## Publish it

Commit, then:

```bash
./release.sh
```

It runs the tests and pushes `main`. The workflow builds the plugin for the
newest published Corvus GCS on Linux, macOS and Windows, lets that program load
it, and attaches it to the release `abi-<sum>` of this repository, where every
Corvus GCS with the same plugin interface finds it. A Corvus GCS with a new
interface gets its build within hours. With nothing to push, `./release.sh`
starts that build at once. `--watch` waits for the result, `--help` lists the
rest.

## Tests

From the Corvus checkout:

```bash
cargo test -p corvus_plugin_vibration
```

## Licence

Sustainable Use License, see [LICENSE.md](LICENSE.md). Copyright (c) 2026
Maximilian Böck.
