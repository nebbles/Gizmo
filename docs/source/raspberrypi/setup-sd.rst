=======================
Setting up your SD Card
=======================

When setting up a new Raspberry Pi, you will need to install an operating system (OS) onto your SD card. There are many operating system options, however the official and most commonly used is `Raspbian OS. <https://www.raspberrypi.org/downloads/raspbian/>`_ For Gizmo you will set up a modified version of Raspian. 

When setting up a new SD card yourself, we recommend using NOOBS (New Out Of Box Software). It is an easy installer to get a Pi up and running quickly (including Raspian OS). For information on how to set up with NOOBS, use `this guide. <https://www.raspberrypi.org/help/noobs-setup/2/>`_


Downloading your Disk Image
===========================

Usually, you would download a zipped image file directly from the `Raspberry Pi website. <https://www.raspberrypi.org/downloads/>`_  

However, for Gizmo we have added drivers for the touchscreen. `Here <https://www.waveshare.com/wiki/5inch_HDMI_LCD>`_ you can see what we did and find additional steps to modify the configuration of the touchscreen.

**Download our Gizmo disk image with touch screen drivers** `here. <https://www.linktobeadded.com/>`_ 


Flashing your Disk Image
========================

1. First you must format (wipe) the SD Card. `Download SDFormatter here <https://www.sdcard.org/downloads/formatter_4/>`_ .
2. Use SDFormatter to format the SD card. Please be careful and make sure you select the correct drive letter.
3.  `Download Etcher <https://www.etcher.io>`_ if not installed.
4. Use Etcher to flash the image to the SD card.

   - Please be careful that the correct drive letter is selected.
   - On Mac: if you backed up the image with the method above you might have to change the file extension from ".cdr" to ".iso"
5. You're done! If all has gone well the Raspberry Pi should boot up correctly with your new SD card.
