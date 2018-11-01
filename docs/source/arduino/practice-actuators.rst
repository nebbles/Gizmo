=========
Actuators
=========

In this section we are going to learn about actuators and how to control them.

1. Piezo Buzzer
2. Servo Motor

At the beginning of this session you should have collected a kit that is made of:

- `Buzzer <http://uk.rs-online.com/web/p/piezo-buzzer-components/0457011/>`_
- `Servo Motor <https://www.rapidonline.com/feetech-fs90-mini-servo-120-9g-37-1339>`_


Piezo Buzzer
============

A `piezoelectric speaker <https://www.wikiwand.com/en/Piezoelectric_speaker>`_ (sometimes colloquially called a "piezo") or buzzer is a loudspeaker that uses the piezoelectric effect for generating sound. The initial mechanical motion is created by applying a voltage to a piezoelectric material, and this motion is typically converted into audible sound using diaphragms and resonators.

.. image:: /_static/images/arduino-practise/piezo-bending.png
  :align: center

When fixed to a metallic diaphragm and excited with an alternating voltage, the diameter of the disc varies by a small amount, this causes dishing of the diaphragm which gives a much louder sound.

Example Circuit
***************

From the kit you are going to need:

- Buzzer
- Jumper Wires
- Arduino

.. image:: /_static/images/arduino-practise/piezo-buzzer-wiring.png
  :align: center

Code
****

For the code you can use the **Example → 2.Digital → toneMelody**. Play around with the sketch and ``tone()`` command. You may find it useful for whenever you want to make musical notes. More information on the pitches Arduino library and tone command `here <https://www.arduino.cc/en/Tutorial/ToneMelody?from=Tutorial.Tone>`_. Try also **Example → 10.StarterKit_BasicKit → p06 LightTheremin**.

Servo Motor
===========

`A servo motor <https://www.wikiwand.com/en/Servomotor#/RC_servos>`_ is a rotary actuator or linear actuator that allows for precise control of angular or linear position, velocity and acceleration. It consists of a suitable motor coupled to a sensor for position feedback. It also requires a relatively sophisticated controller, often a dedicated module designed specifically for use with servomotors.

Example Circuit
***************

From the kit you are going to need:

- Servo Motor
- Jumper Wires
- Arduino

.. image:: /_static/images/arduino-practise/servo-sweep-wiring.png
  :align: center

Code
****

For this example you are going to use the built-in `servo library <https://www.arduino.cc/en/Reference/Servo>`_ by Arduino and we are going to use the built-in sketch **Example → Servo → Sweep**.

.. image:: /_static/images/arduino-practise/arduino-servo-choice.png
  :align: center

.. code-block:: arduino

  /* Sweep
   by BARRAGAN <http://barraganstudio.com>
   This example code is in the public domain.

   modified 8 Nov 2013
   by Scott Fitzgerald
   http://www.arduino.cc/en/Tutorial/Sweep
  */

  #include <Servo.h>

  Servo myservo;  // create servo object to control a servo
  // twelve servo objects can be created on most boards

  int pos = 0;    // variable to store the servo position

  void setup() {
    myservo.attach(9);  // attaches the servo on pin 9 to the servo object
  }

  void loop() {
    for (pos = 0; pos <= 180; pos += 1) { // goes from 0 degrees to 180 degrees
      // in steps of 1 degree
      myservo.write(pos);              // tell servo to go to position in variable 'pos'
      delay(15);                       // waits 15ms for the servo to reach the position
    }
    for (pos = 180; pos >= 0; pos -= 1) { // goes from 180 degrees to 0 degrees
      myservo.write(pos);              // tell servo to go to position in variable 'pos'
      delay(15);                       // waits 15ms for the servo to reach the position
    }
  }

Challenge
=========

.. important::
  **You must demonstrate your build & code to the tutor team**

We challenge you to combine previous sketches (Button, Sweep, tone) to create one that:

- With the press of a button, sweeps a servo in one direction
- With the press of a second button, sweeps the same servo in the opposite direction
- When the servo has swept its maximum travel, the buzzer should sound (beep).

.. admonition:: Acknowledgements
   :class: refbox

   - `Adafruit Learn <https://learn.adafruit.com/>`_
   - `Wikiwand Piezoelectric Speaker <https://www.wikiwand.com/en/Piezoelectric_speaker>`_
