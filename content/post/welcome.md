+++
date = "2016-07-25T21:44:49-07:00"
next = "/next/path"
prev = "/prev/path"
title = "ProteusISC Intro"
toc = true
weight = 5

+++

**Proteus ISC** is a driver framework for managing In System Configuration Controllers (such as JTAG or SPI adapters).

**Adapt** is a reference implementation for using Proteus ISC to build a useful command line tool without having to worry about drivers for your controlleradapter of choice.


## Motivation

Billions of devices have a form of ISC (In System Configuration) built into their hardware to allow programming and instrumentation. The protocols to communicate with these devices are often well conceived electrical standards sending proprietary messages to the device.

By default, the only tools available to talk to these devices are vendor provided, and often non free or tied up with licenses. Luckily open tools are actively maintained that provide drivers to communicate with these devices.

But for any software to configure a device, the software must send the device bound data through some form of controller or adapter (for example USB to JTAG). Each of these controllers have a unique API which is often undocumented. Developers who wish to write a tool for a new chip type must add support for at least one controller before they are able to build their tools. The result is often subpar controller support.

Furthermore, open drivers for controllers often do not take full advantage of the hardware, which can leave a $200 high end device programmer loading programs as fast as bit banging the data to the device.

Proteus ISC solves this issue by providing a controller support as a library. Any tool developer can spend their time writing drivers for their device with the controller presented as a simple pipe for their commands.

Proteus ISC also supports lazy execution of commands with an aggressive optimization engine that takes full advantage of controller hardware by recomposing your requests into more favorable groupings.

## Download

**Pypi packages**

    #Proteus ISC
    pip3 install proteusisc
    #Adapt
    pip3 install adaptisc

**Firmware, UDEV rules, and firmware loading utilities**

Required to initialize controllers with firmware and set the device access permissions.

    wget -qO - http://apt.proteusisc.org/proteusisc.public.gpg-key | sudo apt-key add -
    echo deb http://apt.proteusisc.org testing main | sudo tee /etc/apt/sources.list.d/proteusisc.list
    sudo apt-get update
    sudo apt-get install proteusisc-controller-firmware

**Github Projects**

* **Proteus ISC** https://github.com/diamondman/proteusisc
* **Adapt Front End** https://github.com/diamondman/Adapt
* **Firmware and tools (deb)** https://github.com/diamondman/proteusisc-firmware-loader
* **Xilinx PC1USB open firmware** https://github.com/diamondman/adapt-xpcusb-firmware

## Documentation

http://diamondman.github.io/Adapt/

