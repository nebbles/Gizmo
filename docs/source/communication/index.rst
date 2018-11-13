Communication
=============

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   serial

- `I2C <https://www.youtube.com/watch?v=DsSBTYbXAKg>`_ is protocol that allows two devices to talk to each other using only two buses: a clock one (SCL bus) and a data on (SDA bus). It can allow up to 127 slaves connected to one master to exchange information. It is a very common protocol for Arduino as it is used to communicate with various sensors. There is a `dedicated library called Wire <https://www.arduino.cc/en/Reference/Wire>`_ in Arduino that you can readily use.
- `SPI <http://radiostud.io/understanding-spi-in-raspberry-pi/>`_ is a synchronous serial communication interface specification used for short distance communication, primarily in embedded systems. It uses four buses: clock (SCK), two data lines (MISO: Master Output Slave Input, MOSI: Master Input Slave Output) and a select line(SS) to choose among the multiple slave devices.
- `Noduino <https://sbstjn.com/noduino/>`_ is a JavaScript and Node.js framework for accessing basic Arduino controls from web applications using HTML5, Socket.IO and Node.js.
- UDP
- MQTT
