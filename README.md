# VSCode Template for RP2 Project with Debugging

This template is meant to be used in the development of application utilizing the Raspberry Pi Pico microcontroller board.  

The debugging capabilities are provided by using a seperate RP2 loaded with the **picoprobe** firmware.

The following instructions pertain to Linux (Ubuntu 22.04.1).

1. Create a directory used to contain all need dependancies. `pico-dev` is used in these instructions.
2. Using the [RP2 Getting Started Guide](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) clone the following repositories.
    - pico-sdk
    - openocd
    - picobrobe
3. Build OpenOCD.
4. Build picobrobe and upload uf2 to RP2 to be used for debugging.
5. In you project's `CMakeLists.txt`, disable usb and enable uart for stdio binding.
```
# enable/disable usb and uart output
pico_enable_stdio_usb(${PROJECT_NAME} 0)
pico_enable_stdio_uart(${PROJECT_NAME} 1)
```
6. Create a `.vscode` directory and files: `launcch.json` and `settings.json`.
7. Fill in the following JSON field that correspond to your installation locations.
8. Add RP2 Picoprobe to udev rules.
```
echo 'SUBSYSTEMS=="usb", ATTRS{idVendor}=="2e8a", ATTRS{idProduct}=="0004", GROUP="users", MODE="0666"' | sudo tee -a /etc/udev/rules.d/98-PicoProbe.rules

sudo udevadm control --reload
```
9. Reboot
10. Your done, happy developing!