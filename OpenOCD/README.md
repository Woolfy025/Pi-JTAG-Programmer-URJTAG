# Installation

```sh
sudo apt update
sudo apt -y dist-upgrade
sudo apt install openocd
```

# Flash an ATF1504AS

Use the `sysfsgpio.cfg` file in this directory.

```sh
openocd -f sysfsgpio.cfg -c "adapter_khz 400" \
-c "transport select jtag" \
-c "jtag newtap ATF1504AS tap -irlen 3 -expected-id 0x0150403f" \
-c init \
-c "svf myfirmware.svf -quiet" \
-c "sleep 200" \
-c shutdown
```
