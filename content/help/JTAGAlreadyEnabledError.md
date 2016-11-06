+++
Categories = []
Description = "How to fix a JTAG Already Enabled Error"
Tags = ["faq", "error"]
date = "2016-07-27T02:32:35-07:00"
title = "JTAG Already Enabled Error"

+++

## Symptom

When enabling a controller's JTAG output in Adapt, the following error is reported:

    **********************************************************
    *       Error: JTAG Already Enabled on Controller!       *
    *  Controller is either in use or left in invalid state. *
    *   Use -noerr flag to ignore this error or powercycle   *
    *         your controller. Use at your own fish.         *
    *   http://proteusisc.org/help/JTAGAlreadyEnabledError   *
    **********************************************************

## Cause

Many JTAG controllers have commands to enable and disable jtag output. Some of these controllers will fail if their JTAG Enable command is sent when they already have JTAG output enabled. This is intended to prevent multiple people from using the controller at the same time.

If a controller fails to enable JTA output multiple times in a row, its driver should raise the JTAGAlreadyEnabledError exception, which will stop the current action and report the above error.

Often this happens because a program shut down improperly, leaving the controller in an improper state. The controller may work perfectly well, but the driver believes it is in use and will not take control.

## Solution

If another program is using the controller, then close that program.

If no program is using the controller and you believe the controller is in an invalid state, simply power cycle the controller.

If this is happening often (for example you are developing a driver), you can provide the -noerr flag to adapt to silence this error and have proteus try to continue using this controller.

## Related Exception:

JTAGAlreadyEnabledError