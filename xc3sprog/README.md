# Introduction

[xc3sprog](http://xc3sprog.sourceforge.net/) is a utility to Xilinx CPLDs and FPGAs via JTAG. The default Raspberry Pi repositories have xc3sprog in them, but this version does not support GPIO usage. You instead need to install from source using the instructions below.

The default GPIO pinout configuration for xc3sprog is compatible with Pi JTAG.

# Installation

Unfortunately the version in the Pi OS repostiories does not support GPIO communication, so this needs compiling as below:

```sh
sudo apt update
sudo apt -y dist-upgrade
sudo apt install build-essential libusb-dev \ libftdi-dev libgpiod-dev git cmake
git clone https://github.com/matrix-io/xc3sprog
mkdir xc3sprog/build
cd xc3sprog/build
cmake .. -DUSE_WIRINGPI=OFF
make
sudo make install
```

# GPIO cable option

It is recommended you use the "sysfsgpio_creator" option. "matrix_creator" also works and is typically a little faster, but this is not compatible with the latest Pi OS releases or with the Raspberry Pi 4 series.

# List JTAG chain

JTAGs can have multiple ICs in a chain, the following command lists all the devices in the chain with their chain position numbers:

```sh
sudo xc3sprog -c sysfsgpio_creator -j
```

# Read target IC into file

The following reads the firmware from the IC in JTAG position 0 and saves it to the file "myxilinx.jed":

```sh
sudo xc3sprog -c sysfsgpio_creator -v -p 0 myxilinx.jed:r
```

# Write a file to the target IC

This command flashes the IC in position 0 with the firmware in "myfirmware.jed":

```sh
sudo xc3sprog -c sysfsgpio_creator -v -p 0 myfirmware.jed
```

# Program via SSH from Linux or macOS

The following assumes you want to flash "myfirmware.jed" using a Pi with the SSH username "pi" with the hostname "raspberrypi.local".

It essentially writes the firmware to a temporary file called "FK.jed" on the Pi and flashes that. Then finally it removes the temporary file.

```sh
ssh pi@raspberrypi.local 'cat > /tmp/FK.jed && sudo xc3sprog -c sysfsgpio_creator -v -p0 /tmp/FK.jed && rm -f /tmp/FK.jed' < myfirmware.jed
```


