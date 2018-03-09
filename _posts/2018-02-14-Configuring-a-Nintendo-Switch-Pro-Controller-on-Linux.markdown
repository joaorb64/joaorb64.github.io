---
layout: post
title:  "Configuring a Nintendo Switch Pro Controller on Linux"
date:   2018-02-14
comments: true
categories:
---

Short version
===

There are two main ways of using a Nintendo Switch Pro Controller on Linux while there's no proper driver for it. We'll solve the issue that **the analog sticks don't register full range going right or up** (still no rumble or proper player led indicator until there's a driver specific for it).

It only works via bluetooth until there are drivers for wired mode.

If you wish to change the calibration values, I recommend **Dolphin Emulator** for checking your calibration for **Method 1** (while configuring a Game Cube controller, the red dot should reach the outer square borders and neutral position should be centralized) and **jstest-gtk** for **Method 2** (use the numbers on the axis bars).

Method 1 is more direct and fixes the evdev device, used for SDL, Steam and recent emulators. Method 2 (xboxdrv) creates virtual joystick, evdev and udev devices, so it works with pretty much anything.

Steps
---

1. Connect it to your pc via bluetooth. I use blueman and Gnome Bluetooth. LEDs still blink left-right even when connected.
2. Find your device id via "sudo evtest"

**Method 1: Calibrate the evdev device**

3. Configure the calibration as follows, changing from eventX to your device's id:

{% highlight ruby %}

# We're defining a temporary variable only for convenivence
device=/dev/input/eventX

# Left stick X, Y then right stick X, Y. You can copy/paste this whole block to your terminal
sudo evdev-joystick --e $device --a 0 --minimum 5000 --maximum 52000 & \
sudo evdev-joystick --e $device --a 1 --minimum 10000 --maximum 60000 & \
sudo evdev-joystick --e $device --a 3 --minimum 8000 --maximum 52000 & \
sudo evdev-joystick --e $device --a 4 --minimum 10000 --maximum 60000

# You can check the current calibration with this command
sudo evdev-joystick --s $device

{% endhighlight %}

And you're good to go!

**Method 2: xboxdrv**

3. Install xboxdrv

4. Run the following command:

{% highlight ruby %}
sudo xboxdrv --evdev /dev/input/eventX \
--silent --detach-kernel-driver --mimic-xpad --trigger-as-button --force-feedback \
--evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RX=x2,ABS_RY=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
--evdev-keymap BTN_TL=lt,BTN_TR=rt,BTN_SOUTH=a,BTN_EAST=b,BTN_C=x,BTN_NORTH=y,BTN_WEST=lb,BTN_Z=rb,BTN_SELECT=tl,BTN_START=tr,BTN_TL2=back,BTN_TR2=start,BTN_MODE=guide \
--calibration x1=-31320:0:20650,y1=-21743:0:30460,x2=-28945:0:21951,y2=-23636:0:30969 \
--axismap -y1=y1,-y2=y2 \
--deadzone 4000 --device-name "Nintendo Switch Pro Controller"
{% endhighlight %}

This maps the buttons for their **physical position** rather than their labels. Games will show Xbox button labels, wich are mirrored from Nintendo's: A=B, B=A, X=Y, Y=X.

---------------------------------------

Some notes
===

As of now, I've tested the **Nintendo Switch Pro Controller** on Linux:

- **Wired:** Controller is listed as HID, but **no input is registered**. The same happens on Windows.

- **Bluetooth:** It connects and works, but analog calibration is off. **Both sticks' up and right don't register their full range** (you'd have Mario moving at normal speed backwards but slowly forwards in Super Mario 64, for example). The same happens on Android.


And calibration on jstest-gtk just messes everything up: the axis overflows as you move it and goes all around. Won't do.

---------------------------------------

If you know of any driver for this controller on Linux please share with us on the comments below, as this tutorial is only a workaround.

Last edited: 03/09/2018 - some clean-up and improvements to text.
