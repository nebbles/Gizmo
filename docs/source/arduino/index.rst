=======
Arduino
=======

Welcome to the guide on Arduino. See below for `Why Arduino?`_ and possible `Alternative Microcontrollers`_. 

.. image:: /_static/images/arduino-uno.png
  :align: center

.. toctree::
   :maxdepth: 2
   :numbered:
   :caption: Chapters

   introduction
   practice-basics
   practice-sensors
   practice-actuators
   practice-combined


Why Arduino?
============

The Raspberry Pi and Arduino are complementary platforms and one doesn't exclude the other. If you combine their capabilities you can achieve amazing results. But why would you use Arduino?

- **The community!** Arduino has a lot of materials readily available online, from libraries, to examples. If you have something in mind probably someone has already done it and shared the documentation.
- **Uses very little power** and boots very quickly.
- **Runs at 5V logic level** whereas the Pi digital pins operate at 3.3V.
- **Incredibly cheap hardware** which is useful for powering/controlling prototype electronics which might end up damaging your controller. You have to be more careful with a Pi as they are more easily damaged and more expensive to replace!
- **Real-time capabilities** are more readily accessible whereas there are limitations and constraints to getting the same performance from the Linux-based kernal in Raspbian.

Alternative Microcontrollers
============================

- `ARM mBed <https://os.mbed.com/platforms/mbed-LPC1768/>`_
- `STM32 <http://www.st.com/en/microcontrollers/stm32-32-bit-arm-cortex-mcus.html>`_
- `Teensy <https://www.pjrc.com/teensy/>`_
- `pyBoard <https://store.micropython.org/#/store>`_ runs microPython

Note that microPython is an incredibly useful alternative to the Arduino community and there are a number of new and highly functional boards built specially for microPython.
