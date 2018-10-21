==================
Configuring the Pi
==================

raspi-config
============

.. contents::
  :local:

A lot of the Pi's system settings are configured in ``raspi-config``, a `terminal/shell <https://en.wikipedia.org/wiki/Command-line_interface>`_ based tool. When we run this tool, we will run them as a **root user**, the root has the permission to modify files or default settings as an administrator. By default on Raspbian (the operating system of our Pi) the **root user** is ``pi`` and the **root password** associated to the root user is ``raspberry``. To operate as a root user in the terminal every command is preceded by the ``sudo`` (**s**\ uper **u**\ ser **do**) command.

.. tip::
  Following the new kernal update "Stretched" released in September. Some user has found that their settings get resetted after reboot. If so, please setup your Pi Configuration using within the X-Environment:

  #. Click on Raspbian Icon
  #. Preference
  #. Raspberry Pi Settings

Type the following command and press 'Enter' to open the configuration menu of the Pi:

.. code:: bash

  $ sudo raspi-config

.. note::
  The ``$`` symbol in front of the command signifies when this command should be written in the terminal window. When writing the command you should not write the dollar sign, only the command: ``sudo raspi-config``.

The terminal will show a menu. The options can be navigated with the vertical keys of your keyboard, to accept the options press 'Enter', to finish press the lateral keys of the keyboard.

.. image:: /_static/images/pi-config/raspi-config.png
  :align: center

Keyboard
--------

First we set up the keyboard to prevent any problem when we will change the root password. We access the option: *4 Localisation Options*:

.. image:: /_static/images/pi-config/localisation-options.png
  :align: center

Then *Change Keyboard Layout*:

.. image:: /_static/images/pi-config/keyboard-layout.png
  :align: center

Then we choose *Generic 105 key*:

.. image:: /_static/images/pi-config/keyboard-generic-105.png
  :align: center

And then *English (UK)*:

.. image:: /_static/images/pi-config/keyboard-english-uk.png
  :align: center

Then we can choose the default options that the menu is prompting by pressing enter:

.. image:: /_static/images/pi-config/keyboard-default-layout.png
  :align: center

.. image:: /_static/images/pi-config/keyboard-no-compose.png
  :align: center

.. image:: /_static/images/pi-config/keyboard-terminate-server.png
  :align: center

Timezone
--------

Then we are re-directed to the main menu, now we change the timezone from the *4 Localisation Options* menu.

.. image:: /_static/images/pi-config/localisation-options.png
  :align: center

Then we choose *Change Timezone*:

.. image:: /_static/images/pi-config/timezone-change.png
  :align: center

Then *Europe*:

.. image:: /_static/images/pi-config/timezone-europe.png
  :align: center

Then *London*:

.. image:: /_static/images/pi-config/timezone-london.png
  :align: center

.. _pi-password:

User password
-------------

Now we will change the root user password. This increases the security of the connection we will establish from our laptop to the Pi. Since you are sharing this Pi with your colleagues choose a password together. To change the password we are re-directed to the main menu and here we choose the first option: *1 Change User Password*:

.. image:: /_static/images/pi-config/password-change.png
  :align: center

Then we agree to change the password:

.. image:: /_static/images/pi-config/password-ok.png
  :align: center

Type the new password twice:

.. image:: /_static/images/pi-config/password-typing.png
  :align: center

.. note::
  Nothing will appear on screen when you are typing the password. This is normal - it's still working! If you need to cancel, press ``Ctrl+C`` on the keyboard.

.. image:: /_static/images/pi-config/password-changed-ok.png
  :align: center

We have set the new password. Do not reboot the Pi yet.

Enable SSH
----------

Lastly we will check that the SSH is enabled. We need to enable it to connect with the Pi remotely. From the main menu we access: *5 Interfacing Options*:

.. image:: /_static/images/pi-config/interfacing-options.png
  :align: center

Then we select *SSH*:

.. image:: /_static/images/pi-config/ssh.png
  :align: center

Then we confirm that we want to enable the SSH server:

.. image:: /_static/images/pi-config/ssh-enabling.png
  :align: center

We confirm again:

.. image:: /_static/images/pi-config/ssh-is-enabled.png
  :align: center

Exit the menu by pressing the right arrow twice to select *Finish* and press the Enter key. You will re-enter the terminal.

Now reboot the Pi to ensure all your changes are made:

.. code:: bash

  $ sudo reboot now

Adding users
============

A guide on adding new users to the Pi can be found `here <https://www.raspberrypi.org/documentation/linux/usage/users.md>`_. Generally this is not necessary, and you can continue to use the ``pi`` account. Just remember to change the user password for ``pi`` from ``raspberry`` to something new!

You can create additional users on your Raspbian installation with the ```adduser``` command.
Enter ```sudo adduser bob``` and you will be prompted for a password for the new user *bob*. Leave this blank if you do not want a password. However, we recommend that each user get a password to access remotely in the future, for example:

.. code:: bash

  ssh bob@123.343.1.105

You can delete a user on your system with the command ```userdel```. Apply the ```-r``` flag to remove their home folder too:

.. code:: bash

  sudo userdel -r bob

The default ``pi`` user on Raspbian is a sudoer. This gives the ability to run commands as root when preceded by ``sudo``, and to switch to the root user with ``sudo su``.
