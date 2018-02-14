---
layout: post
title:  "Configuring a Nintendo Switch Pro Controller on Linux"
date:   2018-02-14
categories:
---

As of now, I've tested the **Nintendo Switch Pro Controller** on Linux:

- **Wired:** Controller is listed as HID, but **no input is registered**. The same happens on Windows.

- **Bluetooth:** It connects and works, but analog calibration is off. **Both sticks' up and right don't register their full range** (you'd have Mario moving at normal speed backwards but slowly forwards in Super Mario 64, for example).


Then, I tried calibration on jstest-gtk. It just messes everything up: the axis overflows as you move it and goes all around. Won't do.


One solution to this is to use **xboxdrv**.

My configuration is as follows:


{% highlight ruby %}
sudo xboxdrv --evdev /dev/input/eventXX \
--silent --detach-kernel-driver --mimic-xpad --trigger-as-button --force-feedback \
--evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RX=x2,ABS_RY=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
--evdev-keymap BTN_TL=lt,BTN_TR=rt,BTN_SOUTH=a,BTN_EAST=b,BTN_C=x,BTN_NORTH=y,BTN_WEST=lb,BTN_Z=rb,BTN_SELECT=tl,BTN_START=tr,BTN_TL2=back,BTN_TR2=start,BTN_MODE=guide \
--calibration x1=-31320:0:20650,y1=-21743:0:30460,x2=-28945:0:21951,y2=-23636:0:30969 \
--axismap -y1=y1,-y2=y2 \
--deadzone 4000 --device-name "Nintendo Switch Pro Controller"
{% endhighlight %}

The values for **calibration** were obtained using jstest-gtk.

The **/dev/input/eventXX** must be replaced by your device's event path. You can get it by using **sudo evtest** on a terminal.

This maps the buttons for their **physical position** rather than their labels. Games will show Xbox button labels, wich are mirrored from Nintendo's: A=B, B=A, X=Y, Y=X.
