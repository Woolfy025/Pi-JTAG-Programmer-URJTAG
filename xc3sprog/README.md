# Installation

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

# List JTAG chain

```sh
sudo xc3sprog -c sysfsgpio_creator -j
```

# Read target IC into file

```sh
sudo xc3sprog -c sysfsgpio_creator -v -p 0 myxilinx.jed:r
```

# Write a file to the target IC

```sh
sudo xc3sprog -c sysfsgpio_creator -v -p 0 myfirmware.jed
```

# Program via SSH from Linux or macOS

```sh
ssh pi@raspberrypi.local 'cat > /tmp/FK.jed && sudo xc3sprog -c sysfsgpio_creator -v -p0 /tmp/FK.jed && rm -f /tmp/FK.jed' < myfirmware.jed
```


