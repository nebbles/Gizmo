=========================
Assembling Pi workstation
=========================

The goal of this section is to set up the physical components to the Raspberry Pi. Later on we will look at how we might run a Pi 'headless'. This means we can control the Pi remotely without the need for a screen, keyboard, mouse, or any other peripherals directly connected to the Pi itself.

To do this, we will be using `SSH <https://en.wikipedia.org/wiki/Secure_Shell>`_ protocol. SSH will remotely connect you to a Pi over a local or global network. For this, you need to complete the Networks section before you can move onto the Connecting Remotely section.

When using the Pi in this advanced format, we will be using the 'Terminal' a lot. If you are new to the terminal can be a bit overwhelming at first, don't panic and just follow the steps carefully! There are many great resources on the internet to help you understand how to use a terminal, including this website.

Getting going
=============

At first we will setup the Pi using peripherals. Each team should get the following equipment:

- 1 Touchscreen
- 1 Raspberry to touchscreen HDMI-HDMI plug
- 1 Touchscreen pen
- 1 Raspberry Pi Power Supply
- 1 Raspberry Pi
- 1 Keyboard
- 1 SD Card
- 1 Wooden plate
- 8 M2.5 Bolts
- 4 M2.5 Standoffs
- 3 M3 Bolts
- 4 M3 Spacers
- 4 M3 Nuts
- 1 Breadboard
- 1 Arduino
- 1 USB A to USB B Cable
- 1 Screwdriver
- 1 Pair of Pliers

.. image:: /_static/images/pi-hardware/provided-material.jpg

1. Attach the Raspberry Pi to the wooden plate, first bolt the 4 M2.5 Standoffs to the plate and then attach the RPi to the plate with 4 more bolts (don't tighten them too much):

  .. image:: /_static/images/pi-hardware/assembly-pi.jpg
    :align: center

2. Repeat the same operation with the Arduino using the M3 spacers, nuts and bolts. You will be able only to secure it with three bolts, remember not to tighten them too much:

  .. image:: /_static/images/pi-hardware/assembly-arduino.jpg
    :align: center

3. To attach the breadboard to the wooden plate, peel off the back of it to expose the adhesive strip and glue it to the wooden plate:

  .. image:: /_static/images/pi-hardware/assembly-sticky_back.jpg
    :align: center

  .. image:: /_static/images/pi-hardware/assembly-final.jpg
    :align: center

4. Insert the micro-SD card in the back of the Pi, like so:

  .. image:: /_static/images/pi-hardware/assembly-rpi_sd.jpg
    :align: center

5. Connect the touchscreen to the Pi, connecting it to the pins and with the HDMI plug, like so:

  .. image:: /_static/images/pi-hardware/assembly-screen.jpg
    :align: center

6. Connect the keyboard with the USB.

  .. image:: /_static/images/pi-hardware/assembly-keyboard.jpg
    :align: center

7. Using the power cable, power up the Pi and the screen:

  .. image:: /_static/images/pi-hardware/assembly-power.jpg
    :align: center

8. The Pi will start the setup, if the screen doesn't illuminate check that it is on.

.. note::
  Go to the next section to find out more about the SD card we have provided.
