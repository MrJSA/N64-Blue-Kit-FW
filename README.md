# N64-Blue-Kit-FW

This is the Firmware Repository for the N64-Blue-Kit, a mod Kit to Mod you N64 Controller to be used as a Bluetooth controller.

Should be Compatible with Nintendo Switch and BlueRetro Adapters.

It's also compatible with the original joystick, so there is no need of using an alternative one or doing your own with analogs.

## Installation

The recommended way is to go to the [Online Installer](https://mrjsa.github.io/N64-Blue-Kit-FW/) from a supported browser (like Chrome), connect your ESP32 in Boot/Flash mode, and click in Install. It'll always install the latest version.

The other way is to clone the project and building it yourself, thought this is **not recommended** for new users.

## Using it

After flashing it for the first time, the BluN64 will start in *Switch Mode*, this means that the control will try to connect to an already paired Nintendo Switch, or to a Nintendo Switch in pair mode (i.e. in "**Change Grip/Order**"). If you want to change to *BlueRetro Mode*, you have to press **L, R and Start at the same time** for about five seconds until the Mode LED (**GPIO 16**) turns off. In *BlueRetro Mode*, the controller will be available for every type of device, including any console with a [BlueRetro](https://github.com/darthcloud/BlueRetro) on it, Android Device, Windows, etc. It'll work as a generic controller so everything should be working without any problem. To go back to *Switch Mode*, you have to do the same steps (**L + R + Start** for **5 seconds**)

You can switch between both modes on-the-fly, you don't have to shut down neither the controller nor the console for switching, and every time you turn on the controller it'll start on the latest mode used.

In Nintendo Switch, to press the *Home Button* without a physical button wired to **GPIO 2**, you can press both **Start** and then **L** at the same time. The same thing applies to *ZR* (which can be optionally wired to **GPIO 4**), but this time with **Start** and **R**

## Cloning and building

I'd recommend you to clone this repository using the GitHub Desktop app, otherwise, always remember to add `--recursive` to your `git clone` command. **Don't download this project as a ZIP**

For building, I recommend you to build it using Visual Studio Code with the [Espressif IDF](https://marketplace.visualstudio.com/items?itemName=espressif.esp-idf-extension) extension and with ESP-IDF 5.0 or newer installed. Remember to open the project as a Workplace by going to `File -> Open Workspace from File -> ./.vscode/BluN64-ESP32.code-workspace` on Visual Studio Code. You have to build both the n64-switch and n64-blueretro projects, one at the time, then, you have to flash them manually to your ESP32 using **ESP Flash Tool** with the following parameters

```
n64-switch/build/bootloader/bootloader.bin @ 0x1000
n64-switch/build/partition-table/partition-table.bin @ 0x8000
n64-switch/build/ota_data_initial.bin @ 0xd000
n64-switch/build/n64-control-switch.bin @ 0x10000
n64-blueretro/build/n64-control-blueretro.bin @ 0x110000
```
