# aBaja STM32 Starter

Firmware starter for the **STM32F103C8T6** (Blue Pill): STM32CubeMX-generated
HAL + FreeRTOS, built with CMake and Ninja.

## For developers (Windows + WSL)

### Build

```bash
cmake --preset Debug
cmake --build --preset Debug
```

Result: `build/Debug/aBajaSTMStarter.elf` (plus `.map` and
`compile_commands.json` for clangd).

If you previously built with another toolchain, remove the stale cache first:

```bash
rm -rf build
```

### Flash

A USB ST-Link is not visible inside WSL by default. The easy path is to flash
from **Windows** with [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html):

1. Connect the ST-Link (GND, 3.3V, SWDIO, SWCLK; BOOT0 = 0).
2. Open `build/Debug/aBajaSTMStarter.elf` from
   `\\wsl$\Ubuntu\home\<user>\aBajaSTMStarter\build\Debug\`.
3. Click **Download**.

For flashing/debugging from inside WSL, install `usbipd-win` on Windows
(`winget install usbipd`), `usbipd attach --wsl --busid <id>`, then use OpenOCD:

```bash
openocd -f interface/stlink.cfg -f target/stm32f1x.cfg \
  -c "program build/Debug/aBajaSTMStarter.elf verify reset exit"
```

## Updating the dev container

`docker pull ghcr.io/fx991/abajastmstarter-dev:latest`, then
**Dev Containers: Rebuild Container** in VS Code.
