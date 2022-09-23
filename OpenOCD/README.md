#Introduction

[OpenOCD](https://openocd.org/) is an open source JTAG debugger, this can also be used to flash firmware using the SVF format. It can be used with numerous types of ICs that talk via JTAG, including microcontrollers and CPLDs.

This needs a configuration file to be compatible with Pi JTAG which can be found in this directory. 

# Installation

OpenOCD is in the default Pi OS repository.

```sh
sudo apt update
sudo apt -y dist-upgrade
sudo apt install openocd
```

# Flash an ATF1504AS

Use the [`sysfsgpio.cfg`](sysfsgpio.cfg) file in this directory. This configures the Pi GPIO as the cable type and the GPIO pinout.

The following will flash an ATF1504AS CPLD with the firmware called "myfirmare.svf". The expected ID section can be dropped if you do not know the JTAG model ID for your IC and the "ATF1504AS" is more of a label so this can be anything. These changes makes the command a little more universal.

```sh
openocd -f sysfsgpio.cfg -c "adapter_khz 400" \
-c "transport select jtag" \
-c "jtag newtap ATF1504AS tap -irlen 3 -expected-id 0x0150403f" \
-c init \
-c "svf myfirmware.svf -quiet" \
-c "sleep 200" \
-c shutdown
```

For more information please see the [OpenOCD user guide](https://openocd.org/doc/html/index.html).