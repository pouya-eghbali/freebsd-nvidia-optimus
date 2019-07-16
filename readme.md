# FreeBSD Nvidia Optimus Driver

This is a modified version of the x11/nvidia-driver that works with Nvidia
optimus (muxless) laptops. This package also provides utilities to make it
easier to run programs on the Nvidia GPU.

## Install

You can install this in 2 ways, one way is to grab the binaries from
[releases](https://github.com/pouya-eghbali/freebsd-nvidia-optimus/releases).
and then install using pkg:

	pkg install nvidia-optimus-driver-430.34.txz

or

	pkg install nvidia-optimus-driver-390-390.116.txz

Please note these binaries are built on FreeBSD 12.

To build this on your system, you should clone this repo (or download the source)
then do:

	make install

or

	make package

and then install using pkg.

## Using

To use Nvidia optimus driver, you need to start the optimus service.
To do that, you can add
	
	optimus_enable="YES"

to /etc/rc.conf

Alternatively you can do

	service optimus onestart

The optimus service provides a few configurable options:

	optimus_manage_kld: allow optimus to manage kldload/unload of
											the Nvidia kernel modules (default="YES")
	optimus_modeset: 		load Nvidia modeset kernel driver
											(default="YES")
	optimus_screen:			Screen number for running the optimus X
											server (default="8")
	optimus_x_conf:			Config file to use for X. If this doesn't
											exist it will be generated automatically.
											You should probably check the PCI address
											specified in the generated config file as
											it is extracted from pciconf automatically.
											(default="/usr/local/etc/X11/optimus.x.conf")
  optimus_x_flags:		optimus X server flags
											(default="-sharevts -noreset")

If you don't want optimus manage your kldload/unloads, you must
load nvidia.ko and/or nvidia-modeset.ko yourself.
Refer to x11/nvidia-driver for more info about this.

After you have the service running, you can use the provided
optirun command to run your programs on the Nvidia GPU:

	optirun glxgears
