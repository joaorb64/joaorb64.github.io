---
published: true
title: "Using Nintendo Switch controllers on Linux"
date: 2020-04-08
comments: true
categories:
---

You can easly setup and use single joycons, L+R merged joycons and Switch Pro controllers on Linux. Rumble and motion inputs are also supported.

Let's go over the instructions:

Steps
---

### 1.If your Kernel does not have the **hid_nintendo** driver, install it as a module from [dkms-hid-nintendo](https://github.com/nicman23/dkms-hid-nintendo)

As of this post's writing, hid-nintendo is in review on the linux-input mailing list. It lets you connect joycons and the Switch Pro Controller via bluetooth and the Pro Controller via USB.

### 2.Install the [joycond](https://github.com/DanielOgorchock/joycond) daemon/userspace driver.

It manages the controllers and exposes their motion inputs. When a controller is connected, the leds will blink waiting for you to press L+R to assign them. You can press SL+SR to use sideways joycons or L+R to merge two joycons as one device. You'll also need to press L+R to assign a Switch Pro Controller when connected.

### And that's it!

Extra use case: Cemuhook UDP compatible applications
---

You can use your controllers with compatible Cemuhook UDP applications for the motion input, such as Dolphin-Emu, Citra, Cemu, Yuzu, ...

### 1.Download [joycond-cemuhook](https://github.com/joaorb64/joycond-cemuhook)
### 2.In a compatible application, enable cemuhook motion input
