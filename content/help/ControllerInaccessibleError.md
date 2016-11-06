+++
Categories = []
Description = "how to fix a Controller Inaccessible Error"
Tags = ["faq", "error"]
date = "2016-07-26T16:14:01-07:00"
title = "Controller Inaccessible Error"

+++

## Symptom

When initializing a controller's scan chain in Adapt, the following error is reported:

    **********************************************************
    *    Controller Inaccessible: Permission Denied Error    *
    * http://proteusisc.org/help/ControllerInaccessibleError *
    **********************************************************

## Cause

In linux, usb devices appear as files. These files by default have very restrictive permissions that require root access to read and write to. Rules files can be installed that instruct the UDEV subsystem to give more reasonable permissions to devices that match a filter.

Attempting to access a device with default permissions will produce a Permission Error.

If you are encountering this error it is likely that you either have not installed the provided proteusisc-controller-firmware debian package, are unable to install the package due to being on an incompatable system, or are a developer creating a new driver for one of your controllers and have not added the appropriate UDEV rules to your system.

## Solution

### General Users with a supported controller:

A debian package is available that adds sane device permission defaults for supported devices. It can be installed with by running te following:

    wget -qO - http://apt.proteusisc.org/proteusisc.public.gpg-key | sudo apt-key add -
    echo deb http://apt.proteusisc.org testing main | sudo tee /etc/apt/sources.list.d/proteusisc.list
    sudo apt-get update
    sudo apt-get install proteusisc-controller-firmware

Then detach and raattach your controller/dev board.

### Non Debian Users:

If you are on a **non Debian based system** (such as RedHat) and want the package to be available to you, please goto https://github.com/diamondman/proteusisc-firmware-loader and open an issue. Pull requests are welcome.

Until a package is available for you, the .rules fules in the repository above can be installed into your /etc/udev/rules.d folder, or your distribution's equivalent.

### ProteusISC Controller Driver Developer:

If you are a **developer adding a controller driver to proteusisc**, your new controller will not have udev rules to set the permissions to a useful default.

Create a new file /etc/udev/rules.d/{controller}.rules containing something like this

    ATTR{idVendor}=="0000", ATTR{idProduct}=="0000", MODE:="666", RUN+="command_to_run"

Each clause in this line is optional. Commands run from rules can be provided details about the new device. Look at rules files in the proteusisc-controller-firmware for samples, or consult

    man udev

for details on rule syntax, uses, and variables.

## Related Exception:

DevicePermissionDeniedError