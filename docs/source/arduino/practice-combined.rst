==========================
Combined Sense & Actuation
==========================

**Material Covered**

- DC motor control (speed and direction)
- Capacitive touch

Motor
=====

Intro to Motor Driver
*********************

.. image:: /_static/images/arduino-practise/motor-driver.png
  :align: center

A motor driver is a current amplifier; the function of motor drivers is to take a low-current control signal and transform it into a higher-current signal that can drive a motor.

The Adafruit DRV8833 Motor Driver contains two full H-bridges (four half H-bridges). That means you can spin two DC motors bi-directionally or step one bi-polar or uni-polar stepper with up to 1.2A per channel. This motor driver chip is a nice alternative to the TB6612 driver.

The DRV8833 chip is better for low voltage uses (it can run from 2.7V up to 10.8V motor power) and has built in current limiting capability. The driver is set it up for 1A current limiting so you don't get more than 2A per chip, but you can also disable the current limiting, or change it to a different limit!

.. image:: /_static/images/arduino-practise/motor-driver-size.png
  :align: center

The DRV8833 chip is soldered to a breakout board, with a polarity protection FET on the motor voltage input. Only use with motors that draw 1.2 Amp or less. This is the limit of the chip. They can handle a peak of 2A but only for a short amount of time.

The Driver comes with built in kick-back diodes internally so you do not have to worry about the inductive kick damaging your project or driver! You also don't have to worry as much about burning out the chip with overdriving since there is current limiting.

.. image:: /_static/images/arduino-practise/motor-driver-setup.png
  :align: center

There's two digital inputs per H-bridge (one for each half of the bridge), you can PWM one of the inputs to control motor speed. Runs at 2.7V-10.8V logic/motor power. The motor voltage is the same as the logic voltage, but logic voltage from 2.7V or greater will work so no need to worry if you are powering the motors from 9V and using 3.3V logic. `For higher voltages, check out the TB6612 <https://adafru.it/sdc>`_. `For much higher voltages and currents check out the DRV8871 <http://adafru.it/3190>`_!

The Motor Driver Comes as one assembled and tested breakout board plus a small strip of header. We've done the soldering to attach the header onto the breakout PCB.

.. image:: /_static/images/arduino-practise/motor-driver-parts.png
  :align: center

Pinouts
*******

Power Pins
----------

- **Vmotor** - This is the voltage for the motors, not for the logic level. Keep this voltage between 2.7V and 10.8V. This power supply will get noisy so if you have a system with analog readings or RF other noise-sensitive parts, you may need to keep the power supplies separate (or filtered!). The terminal block has a simple polarity protection on the + pin that feeds into VM. The VM pin is not protected, but VMotor is!
- **GND** - This is the shared logic and motor ground. All grounds are connected.

Signal in Pins
--------------

These are all "2.7V or higher logic level" inputs:

- **AIN1, AIN2** - these are the two inputs to the Motor A H-bridges. If you want to use speed control, PWM the pin that is normally high. If you dont need PWM control, connect them to logic high/low.
- **BIN1, BIN2** - these are the two inputs to the Motor B H-bridges. If you want to use speed control, PWM the pin that is normally high. If you dont need PWM control, connect them to logic high/low.
- **FLT** - This is the **Fault** output, which will drive low if there's a thermal shutdown or overcurrent. Note it is open drain so connect a pull-up resistor to your desired logic voltage!
- **SLP** - this is the sleep pin for quickly disabling the driver. **By default it is pulled low with an internal 500K resistor, so the chip is not active!** Connect to a logic high pin (or 5V supply) either directly or via a pull-up resistor to enable the motor control!

Current Limit Pins
------------------

The DRV8833 can perform current limiting for each motor H-bridge. Basically a resistor is connected between Asen and ground to set the Motor A limit (ditto for Bsen and Motor B)

The current limiting rule is:

.. math::

  LimitCurrent (amps) = \frac{0.2 V}{RSENSE}

By default, there are two 1206-sized 0.2 Ω resistors on the board for both motors.

If you'd like to raise the limit, you can put a 0.2 Ω from Asen to ground, which will then make the RSENSE equal to 0.1 Ω (2 parallel 0.2Ω resistors) for a limit of 2A.

You can also *disable* current limiting by soldering *closed* the two jumpers on the back.

.. image:: /_static/images/arduino-practise/motor-driver-focus.png
  :align: center

If you want a lower current limit, remove/destroy the 0.2Ω resistor on the board and add your own resistor value between Asen or Bsen and ground.

Motor Out Pins
--------------

These are motor power outputs

- **Motor A** - these are the two outputs for motor A, controlled by AIN1 and AIN2
- **Motor B** - these are the two outputs for motor B, controlled by BIN1 and BIN2

DC Motor
********

A `DC motor <https://www.wikiwand.com/en/DC_motor>`_ is any of a class of rotary electrical machines that converts direct current electrical energy into mechanical energy. The most common types rely on the forces produced by magnetic fields. Nearly all types of DC motors have some internal mechanism, either electromechanical or electronic, to periodically change the direction of current flow in part of the motor.

Assembly
********

.. image:: /_static/images/arduino-practise/motor-driver-wiring.png
  :align: center

- AIN1 to pin 9
- AIN2 to pin 10
- SLP to 5V
- GND to Arduino GND
- Vm to 5V
- motorA to DC motor

Code
****

For this sketch copy and paste the following code. You should see the motor speed up in one direction, slow down and then rotate in the opposite direction:

.. code-block:: arduino

  #define MOTOR_AIN1 9
  #define MOTOR_AIN2 10

  int MAX_PWM = 255;
  int MIN_PWM = 50;

  void setup() {
    Serial.begin(9600);
    pinMode(MOTOR_AIN1, OUTPUT);
    pinMode(MOTOR_AIN2, OUTPUT);
  }

  void loop() {
    // ramp up forward
    digitalWrite(MOTOR_AIN1, LOW);

    for (int i=MIN_PWM; i<MAX_PWM; i++) {
      analogWrite(MOTOR_AIN2, i);
      delay(10);
    }

    // forward full speed for one second
    delay(1000);

    // ramp down forward
    for (int i=MAX_PWM; i>=MIN_PWM; i--) {
      analogWrite(MOTOR_AIN2, i);
      delay(10);
    }

    // ramp up backward

    digitalWrite(MOTOR_AIN2, LOW);

    for (int i=MIN_PWM; i<MAX_PWM; i++) {
      analogWrite(MOTOR_AIN1, i);
      delay(10);
    }

    // backward full speed for one second
    delay(1000);

    // ramp down backward
    for (int i=MAX_PWM; i>=MIN_PWM; i--) {
      analogWrite(MOTOR_AIN1, i);
      delay(10);
    }
  }

Challenge 1
===========

.. important::
  **You must demonstrate your build & code to the tutor team**

We challenge you to combine the previous sketch with the potentiometer (Pot) sketch from the previous Chapters such that the Pot controls the speed of the motor. No need to reverse it!

Challenge 2
===========

.. important::
  **You must demonstrate your build & code to the tutor team**

We challenge you to combine the first motor sketch, with your sketch from Challenge 1 and the photocell sketches from previous Chapters:

- Use two photocells to control the direction and speed of two brushed DC motors
- Assume that you want to use this circuit and software, in order to cause a robot to move toward a light source

Capacitive Touch Sensor
=======================

.. image:: /_static/images/arduino-practise/capacitive-board.png
  :align: center

Add lots of touch sensors to your next microcontroller project with this easy-to-use 12-channel capacitive touch sensor breakout board, starring the MPR121. This chip can handle up to 12 individual touch pads.

.. image:: /_static/images/arduino-practise/capacitive-board-size.png
  :align: center

The MPR121 has support for only I2C, which can be implemented with nearly any microcontroller. You can select one of 4 addresses with the ADDR pin, for a total of 48 capacitive touch pads on one I2C 2-wire bus. Using this chip is a lot easier than doing the capacitive sensing with analog inputs: it handles all the filtering for you and can be configured for more or less sensitivity.

.. image:: /_static/images/arduino-practise/capacitive-board-parts.png
  :align: center

The breakout board provides a 3V regulator and I2C level shifting so its safe to use with any 3V or 5V microcontroller/ processor like Arduino. There is an LED onto the IRQ line so it will blink when touches are detected, making debugging by sight a bit easier on you. For contacts, we suggest using copper foil or pyralux, then solder a wire that connects from the foil pad to the breakout.

Pinouts
*******

.. image:: /_static/images/arduino-practise/capacitive-board-pinouts.png
  :align: center

The little chip in the middle of the PCB is the actual MPR121 sensor that does all the capacitive sensing and filtering. The breakout board comes with all the extra components you need to get started, and 'break out' all the other pins you may want to connect to onto the PCB.

Power Pins
----------

The sensor on the breakout requires 3V power. Since many customers have 5V microcontrollers like Arduino, we tossed a 3.3V regulator on the board. Its ultra-low dropout so you can power it from 3.3V-5V

- **Vin** - this is the power pin. Since the chip uses 3 VDC, we have included a voltage regulator on board that will take 3-5VDC and safely convert it down. To power the board, give it the same power as the logic level of your microcontroller - e.g. for a 5V micro like Arduino, use 5V
- **3Vo** - this is the 3.3V output from the voltage regulator, you can grab up to 100mA from this if you like
- **GND** - common ground for power and logic

I2C Pins
--------

Don't worry too much about how these work - it will be covered in a later Chapter!

- **SCL** - I2C clock pin, connect to your microcontrollers I2C clock line.
- **SDA** - I2C data pin, connect to your microcontrollers I2C data line.

IRQ and ADDR Pins
-----------------

- **ADDR** is the I2C address select pin. By default this is pulled down to ground with a 100K resistor, for an I2C address of 0x5A. You can also connect it to the 3Vo pin for an address of 0x5B, the SDA pin for 0x5C or SCL for address 0x5D
- **IRQ** is the Interrupt Request signal pin. It is pulled up to 3.3V on the breakout and when the sensor chip detects a change in the touch sense switches, the pin goes to 0V until the data is read over i2c

Wiring
******

You can easily wire this breakout to any microcontroller, we'll be using an Arduino. For another kind of microcontroller, just make sure it has I2C, then port the code - its pretty simple stuff!

.. image:: /_static/images/arduino-practise/capacitive-board-wiring.png
  :align: center

- Connect **Vin** to the power supply, 3-5V is fine. Use the same voltage that the microcontroller logic is based off of. For most Arduinos, that is 5V
- Connect **GND** to common power/data ground
- Connect the **SCL** pin to the I2C clock **SCL** pin on your Arduino. On an UNO & '328 based Arduino, this is also known as **A5**, on a Mega it is also known as **digital 21** and on a Leonardo/Micro, **digital 3**
- Connect the **SDA** pin to the I2C data **SDA** pin on your Arduino. On an UNO & '328 based Arduino, this is also known as **A4**, on a Mega it is also known as **digital 20** and on a Leonardo/Micro, **digital 2**

The MPR121 **ADDR** pin is pulled to ground and has a default I2C address of 0x5A You can adjust the I2C address by connecting **ADDR** to other pins:

- ADDR not connected: 0x5A
- ADDR tied to 3V: 0x5B
- ADDR tied to SDA: 0x5C
- ADDR tied to SCL: 0x5D

We suggest sticking with the default for the test demo, you can always change it later.

Download Adafruit_MPR121
************************

To begin reading sensor data, you will need to `download Adafruit_MPR121_Library from our github repository <https://adafru.it/dKE>`_. You can do that by visiting the GitHub repo and manually downloading or, easier, just click this button to download the zip:

.. raw:: html

  <div style="text-align:center">
  <a class="btn btn-info btn-custom" href="https://adafru.it/dKF" role="button" style="margin-bottom:20px;" style="margin-bottom:20px;">Download Adafruit_MPR121</a></div>

Rename the uncompressed folder **Adafruit_MPR121** and check that the **Adafruit_MPR121** folder contains **Adafruit_MPR121.cpp** and **Adafruit_MPR121.h**

Place the **Adafruit_MPR121** library folder your ``arduinosketchfolder/libraries/`` folder. You may need to create the ``libraries/`` subfolder if its your first library. Restart the IDE.

`There is a great tutorial on Arduino library installations. <https://adafru.it/aYM>`_

Load Demo
*********

Open up **File → Examples → Adafruit_MPR121 → MPR121test** and upload to your Arduino wired up to the sensor.

.. image:: /_static/images/arduino-practise/capacitive-board-example.png
  :align: center

Thats it! Now open up the serial terminal window at 9600 speed to begin the test.

.. image:: /_static/images/arduino-practise/capacitive-board-serial.png
  :align: center

Make sure you see the "MPR121 found!" text which lets you know that the sensor is wired correctly. Now touch the 12 pads with your fingertip to activate the touch-detection:

.. image:: /_static/images/arduino-practise/capacitive-board-touch.png
  :width: 49%

.. image:: /_static/images/arduino-practise/capacitive-board-output.png
  :width: 49%

For most people, that's all you'll need! Our code keeps track of the 12 'bits' for each touch and has logic to let you know when a contect is touched or released.

If you're feeling more advanced, you can see the 'raw' data from the chip. Basically, what it does it keep track of the capacitance it sees with "counts". There's some baseline count number that depends on the temperature, humidity, PCB, wire length etc. Where's a dramatic change in number, its considered that a person touched or released the wire.

Comment this "return" line to activate that mode:

.. code-block:: arduino

  // comment out this line for detailed data from the sensor! return;

Then reupload. Open up the serial console again - you'll see way more text.

Each reading has 12 columns. One for each sensor, #0 to #11. There's two rows, one for the 'baseline' and one for the current filtered data reading. When the current reading is within about 12 counts of the baseline, that's considered untouched. When the reading is more than 12 counts smaller than the baseline, the chip reports a touch.

.. image:: /_static/images/arduino-practise/capacitive-board-output-advanced.png
  :align: center

Most people don't need raw data too much, but it can be handy if doing intense debugging. It can be helpful if you are tweaking your sensors to get good responsivity.

Library Reference
*****************

Since the sensors use I2C, there's no pins to be defined during instantiation. You can just use:

.. code-block:: arduino

  Adafruit_MPR121 cap = Adafruit_MPR121();

When you initialise the sensor, pass in the I2C address. It can range from 0x5A (default) to 0x5D

.. code-block:: arduino

  cap.begin(0x5A)

``begin()`` returns true if the sensor was found on the I2C bus, and false if not.

Touch detection
---------------

99% of users will be perfectly happy just querying what sensors are currently touched. You can read all at once with ``cap.touched()`` which returns a 16 bit value. Each of the bottom 12 bits refers to one sensor. So if you want to test if the #4 is touched, you can use

.. code-block:: arduino

  if (cap.touched() && (1 << 4)) {
    // do something
  }

You can check its not touched with:

.. code-block:: arduino

  if ( !(cap.touched() && (1 << 4)) ) {
    // do something
  }

Raw Data
--------

You can grab the current baseline and filtered data for each sensor with:

.. code-block:: arduino

  filteredData(sensornumber);
  baselineData(sensornumber);

It returns a 16-bit number which is the number of counts, there's no unit like "mg" or "capacitance". The baseline is initialized to the current ambient readings when the sensor ``begin()`` is called - you can always reinitialize by re-calling ``begin()``! The baseline will drift a bit, that's normal! It is trying to compensate for humidity and other environmental changes.

If you need to change the threshholds for touch detection, you can do that with:

.. code-block:: arduino

  setThreshholds(uint8_t touch, uint8_t release)

By default, the touch threshhold is 12 counts, and the release is 6 counts. It's reset to these values whenever you call ``begin()`` by the way.

Challenge 3
===========

.. important::
  **You must demonstrate your build & code to the tutor team**

We challenge you to combine the touch sensor sketch with a simple analog output. Either a sound output using the ``tone()`` command to create a touch sensitive electric organ... or a RGB LED that changes colour when a touch pad is activated.

.. admonition:: Acknowledgements
   :class: refbox

   Adapted from these guides [`1`_, `2`_]

.. _1: https://learn.adafruit.com/adafruit-drv8833-dc-stepper-motor-driver-breakout-board

.. _2: https://learn.adafruit.com/adafruit-mpr121-12-key-capacitive-touch-sensor-breakout-tutorial
