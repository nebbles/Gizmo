==============
Headless Setup
==============

It can be useful to set up a new Pi even when you *don't have a monitor and keyboard* spare to do a normal set up. Fortunately, there is a way to set up a new Pi without using these peripherals. This is called 'setting the Pi up headless'. The following guide is derived from the `official Pi documentation <https://www.raspberrypi.org/documentation/configuration/wireless/headless.md>`_.

.. note::
  This method is slightly more advanced, so if you are a little unsure of how to do it, ask someone to help you with it.

1. Download the latest Raspbian disk image `from the Pi website <https://www.raspberrypi.org/downloads/raspbian/>`_.
2. Format the SD card using `SDFormatter <https://www.sdcard.org/downloads/formatter_4>`_.
3. Use `Etcher <http://etcher.io/>`_ to flash the Raspbian image (.img) to the SD card.
4. Open the ``boot`` folder on the SD card.
5. Copy the example ``wpa_supplicant.conf`` file (see :doc:`networks`) into the ``boot`` folder.
6. Copy the ``ssh`` file into the ``boot`` folder.
7. Insert the SD into the Pi and power on.
