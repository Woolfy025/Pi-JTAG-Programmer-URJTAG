# Flash an ATF1504AS

```sh
openocd -f sysfsgpio.cfg -c "adapter_khz 400" \
-c "transport select jtag" \
-c "jtag newtap ATF1504AS tap -irlen 3 -expected-id 0x0150403f" \
-c init \
-c "svf myfirmware.svf -quiet" \
-c "sleep 200" \
-c shutdown
```
