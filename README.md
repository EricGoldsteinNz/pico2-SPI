# PICO2 Notes

This fork explicitly sets the board type to pico to stop default building for the original pico.

I've also tested the pico2 running at 18MHz instead of 12 and it seems to work fine.

# pico-serprog

This is a basic flashrom/serprog compatible SPI flash reader/writer for the Raspberry Pi Pico.

It does not require a custom version of flashrom, just drag the compiled uf2 onto your Pico and you're ready to go.

The default pin-out is:

| GPIO | Pico Pin | Function |
|------|----------|----------|
| 1    |    2     | CS       |
| 2    |    4     | SCK      |
| 3    |    5     | MOSI     |
| 4    |    6     | MISO     |

## Usage

Dump a flashchip:

```
flashrom -p serprog:dev=/dev/ttyACM0:115200,spispeed=18M -r foo.bin
```

## Installation

1. Install VS Code
2. In VS Code,  open 'Extensions' from the left hand menu (Ctrl + Shift + X)
3. Install 'Raspberry Pi Pico'
4. Download this project. 
5. In VS Code, Open 'Raspberry Pi Pico Project' in the left hand menu.
6. Click 'Import Project' and import the downloaded project folder.
7. On your Pico2 hold the 'Bootsel' button and connect the USB cable.
8. In 'Raspberry Pi Pico Project' Click 'Run Project (USB)'. This will upload the code to your Pico.
9. You should now be able to used the flashrom command in Usage.

## License

The project is based on the spi_flash example by Raspberry Pi (Trading) Ltd. which is licensed under BSD-3-Clause.

As a lot of the code itself was heavily inspired/influenced by `stm32-vserprog` this code is licensed under GPLv3.
