================
Protocol: Serial
================

Serial is an important protocol for transferring data between two computational devices. In telecommunication and data transmission, serial communication is the process of sending data one bit at a time, sequentially, over a communication channel or computer bus. This is in contrast to parallel communication, where several bits are sent as a whole, on a link with several parallel channels. Serial communication is used for all long-haul communication and most computer networks. `[1] <https://en.wikipedia.org/wiki/Serial_communication>`_

Combining the Arduino for the Raspberry Pi
==========================================

In this tutorial we will see how to connect your Raspberry Pi to your Arduino. We will start by installing the Arduino IDE that you have already seen and then move to some command line tools. These tools don't need a graphical interface and you can use them without a monitor. The last section will give you some advices on how to install these tools on your laptop.

By combining the strengths of both the Raspberry Pi and an Arduino we get a very useful control system - you can think of the Raspberry Pi as a computer that offers computational power and network capabilities, whereas Arduino communicates with sensors and actuators:

.. image:: /_static/images/comms-serial/rpi-arduino-scheme.png
  :align: center

Talking Over Serial
===================

To communicate between the Raspberry Pi and the Arduino over a serial connection, we’ll use the built-in Serial library on the Arduino side, and the Python serial module on the Pi side.

1. To install the serial module, run the following commands on your Pi terminal:

  .. code-block:: bash

    $ sudo apt-get install python-serial python3-serial

2. Now we want to **upload a new sketch on the Arduino**. Plug into your personal computer and upload the code as follows:

  .. code-block:: arduino

    void setup() {
    Serial.begin(9600);
    }

    void loop() {
       for(byte n=0; n<255; n++){
         Serial.write(n);
         delay(50);
       }
    }

  This code counts upward and sends each number over the serial connection. Note that in Arduino, ``Serial.write()`` sends the actual number in the byte type, the actual 8-bit representation of the number.

3. Now plug the Arduino to the USB of the Raspberry. Then in the Pi terminal let's open the Python shell by typing:

  .. code-block:: bash

    $ python

  This will launch the Python interpreter and the ``>>>`` prompt should appear.

4. Now we type:

  .. code-block:: python

    from serial import Serial

  If successful, when you press enter you should see no errors, and the cursor will return to the ``>>>`` prompt. Now we can use the ``Serial`` class to connect to our Arduino.

5. We create a variable of type Serial that represents the serial connection with our Arduino:

  .. code-block:: python

    serial_from_arduino = Serial('/dev/ttyACM0')

6. We can read one bit at a time what the Arduino has written over serial like this:

  .. code-block:: python

    input = serial_from_arduino.read(1)

7. Then we print it in the console like this:

  .. code-block:: python

    print(ord(input))

  The function ``ord()``, given a string of length one, returns the value of the byte when the argument is an 8-bit string. You should see a ``0`` being printed.

  .. note::
    If you have problems with this step, make sure you have properly done step 2 (uploading the new sketch to Arduino).

.. tip::
  For the next step, you need to use **Ctrl+D** to exit the Python prompt.

8. Now that we have tested that the connection works we want to write a Python script that reads the messages from serial, so we type:

  .. code-block:: bash

    $ cd home/pi/
    $ nano serialEcho.py

  And we paste this code:

  .. code-block:: python

    import serial
    port = "/dev/ttyACM0"
    serial_from_arduino = serial.Serial(port, 9600)
    serial_from_arduino.flushInput()
    while True:
     if (serial_from_arduino.inWaiting() > 0):
       input = serial_from_arduino.read(1)
       print(ord(input))

The meaning of each line is as follows:

- ``import serial``: just like before we import the serial library
- ``port = "/dev/ttyACM0"``: this time we save the port path in a variable
- ``serial_from_arduino = serial.Serial(port, 9600)``: we create an object of the class Serial, this time we specify the baud rate of our serial connection
- ``serial_from_arduino.flushInput()``: we clear out the input buffer
- ``while True:``:we put the reading functions in a loop so we keep on reading the values written by the Arduino constantly
- ``if (serial_from_arduino.in_Waiting() > 0):``: we check that we are receiving bytes (i.e. that the input buffer is not empty)
- ``input = serial_from_arduino.read(1)``: we read the content of the input buffer one byte at a time
- ``print(ord(input))``: we interpret the incoming byte and we print it in the console

The Arduino is sending a number to the Python script, which interprets that number as a string. The input variable will contain whatever character maps to that number in the ASCII table. To get a better idea, try replacing the last line of the Python script with this:

.. code-block:: python

  print(str(ord(input)) + " = the ASCII character " + input + ".")

In Python to check if what you are getting is a string you can use `the method explained here <https://stackoverflow.com/questions/5319922/python-check-if-word-is-in-a-string>`_.

Raspberry Pi to Arduino
***********************

To have the Raspberry Pi write and Arduino read (and turn on the built-in LED) you can use this code:

1. On the Arduino side upload this code:

.. code-block:: arduino

  const int ledPin = 13;

  void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
  }

  void loop() {
    if (Serial.available()) {
      light(Serial.read() - '0');
    }
    delay(500);
  }

  void light(int n) {
    for (int i = 0; i < n; i++) {
      digitalWrite(ledPin, HIGH);
      delay(100);
      digitalWrite(ledPin, LOW);
      delay(100);
    }
  }

2. On the Raspberry Pi run this code:

.. code-block:: python

  import serial
  serialToArduino = serial.Serial('/dev/ttyACM0', 9600)
  serialToArduino.write('3')

Other methods
=============

Sometimes the communication over Serial is not the best option for your project or you might want to make your Pi and Arduino communicate in another way, or maybe communicate to other boards, so see the other Chapters for possible alternatives, but don't limit yourself to the ones listed. They are just brief introductions with plenty of links for a more in-depth knowledge. We leave this exploration to your curiosity!

`Serial over GPIO <https://oscarliang.com/raspberry-pi-and-arduino-connected-serial-gpio/>`_ with this method you can use the same code we have used before, the only difference is the physical connection. **Remember** you need to use the same voltage level between the two digital pins. Since the Pi and Arduino operate at different voltage levels you will need a voltage converter.

.. tip::
  Since you are connecting the Arduino to the Pi using USB, and the Pi is a computer, there's no reason why you couldn't run the Python scripts above using your own computer instead of the Pi.

  This is very easy to set up on a Mac or Linux.

  If you have Mac special attention to the path of the USB port. It is going to look like this ``/dev/tty.usbmodem411`` to find your port name you can enter the command ``ls /dev/tty.usb*``.

  Also on Mac there is no ``apt-get`` command. You have to install another package manager, the most common one which we also recommend using `Homebrew <https://brew.sh/>`_ and to install any package use ``brew install PACKAGE_NAME``.
