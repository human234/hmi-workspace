# hmi-workspace

West workspace manifest for the **HMI** Zephyr module
(https://github.com/human234/simple_ui). Pins Zephyr **v4.4.2** (stable) and
installs the HMI module at `modules/hmi`.

## One-time setup

1. [Install Docker Desktop](https://docs.docker.com/desktop/setup/install/windows-install/)
   on Windows (WSL2 backend), or Docker on Linux/macOS. No Zephyr toolchain
   is needed anywhere else.
2. Bootstrap the workspace:
   `west init -m https://github.com/human234/hmi-workspace hmi-workspace`
3. `cd hmi-workspace`
4. `west update`  — fetches Zephyr + all default modules + the HMI module

> `west` (and Python) are only required for the two bootstrap steps. To avoid
> installing anything, run them inside the Zephyr Docker image first, as
> described in `modules/hmi/README-WINDOWS.md`.

## Build / flash the bundled demo

From inside `hmi-workspace`:

| Platform | Build | Flash |
|----------|-------|-------|
| Windows | `modules\hmi\build.ps1` | `modules\hmi\flash.ps1` |
| Linux / WSL | `make -C modules/hmi build` | `make -C modules/hmi flash` |

Default board is `nucleo_g474re`; override with `-Board <name>` / `BOARD=<name>`.

## Releasing

Pin `revision` in `west.yml` to a released tag of `simple_ui` (e.g. v0.1.0)
so consumers always get a reproducible module.