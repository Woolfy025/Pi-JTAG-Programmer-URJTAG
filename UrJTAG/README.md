# Introduction

[UrJTAG](http://urjtag.org/) is another tool that can be used to talk to many different devices over JTAG.

# Installation

Unfortunately the version in the Pi OS repository has a bug which means that GPIO 4 cannot be used for any of the GPIO pins. This has been fixes in the UrJTAG source back in 2017, so we have to compile from source. This can be done as follows:

```sh
sudo apt install autoconf automake autopoint libtool libusb-1.0-0-dev
git clone https://git.code.sf.net/p/urjtag/git urjtag-git
cd urjtag-git/urjtag
./autogen.sh
./configure --prefix=/usr
make
sudo make install
```

# Running UrJTAG

UrJTAG has its own command line user interface which you can execute using:

```sh
sudo jtag
```

You then have to supply details for the connection cable which is the GPIO. This can be done as follows at the `jtag>` prompt:

```
cable gpio tdi=22 tdo=27 tck=17 tms=4
```

Once initialize you can detect what is on the JTAG chain by running the following command at the `jtag>` prompt:

```
detect
```

For more commands and information please see the [UrJTAG Documentation](http://urjtag.org/book/index.html).