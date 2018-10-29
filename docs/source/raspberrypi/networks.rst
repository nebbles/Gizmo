==================
Accessing Networks
==================

WiFi via GUI
============

When running the Pi in desktop mode, you can join new Wifi Networks in a similar way to how you would do it on a Macintosh. In the menu bar at the top, on the right-hand side click on the wireless icon. Then from their you can select from the list of discovered networks to join them.

.. note::
  If they have a padlock next to them then they require a password to join.

WPA Supplicant
==============

.. contents::
  :local:

Since the College has a more complex form of authentication (username *and* password required). We will setup the Pi to connect to the IC network a slightly different way. We are going to modify a modify a configuration file called  *wpa_supplicant.conf*.

Backup
******

First we back up the configuration file ``wpa_supplicant.conf``. We create the backup file ``wpa_supplicant.conf_backup`` in case we need to restore it later. *It's important that you don't edit this backup after creating it*. To do so we enter the command:

.. code:: bash

  $ sudo cp /etc/wpa_supplicant/wpa_supplicant.conf /etc/wpa_supplicant/wpa_supplicant.conf_backup

Edit
****

Then we edit the ``wpa_supplicant.conf``. The default text editor installed in the Pi is *nano*. To edit a file with the nano editor is sufficient to enter the command ``nano /path/to/file``. Therefore to edit ``wpa_supplicant.conf`` we enter the following command with admin user permission:

.. code:: bash

  $ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf


This file should just have this at the beginning:

.. code:: bash

  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  update_config=1


So we add to the content of *wpa_supplicant.conf* so that is looks like this:

 .. code:: bash

  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  update_config=1

  network={
         ssid="Imperial-WPA"
         proto=RSN
         key_mgmt=WPA-EAP
         pairwise=CCMP
         auth_alg=OPEN
         eap=PEAP
         identity="ic\COLLEGE_USERNAME"
         password="YOUR_PASSWORD"
         priority=7
  }

Where ``COLLEGE_USERNAME`` has to be replaced with your college username and ``YOUR_PASSWORD`` with the password associated to it.

.. important::
   The configuration is case sensitive, so make sure you do not have typos. **Even the slightest error in this file can cause the networking to fail** so make sure it exactly like this.

.. note::
  If you want to connect your Pi to the **eduroam** network, then set ``identity="COLLEGE_USERNAME@ic.ac.uk"``. Apply the same procedure for setting the password as seen below.

In the nano editor, to exit, press ``Ctrl + x``. The editor will then present you with different options such as save the file or exit without modifying the file: ``y``/``n``. We press ``y`` and then press ``enter``. The editor now asks us for the name of the file we are saving, but as it already fills out the previous name for us, we press ``enter`` again.

Now we can check if the connection works by rebooting your RPi. Reboot it by entering:

.. code:: bash

  $ sudo reboot now

One the system starts again the Pi should connect automatically to the WiFi.

Encrypting Your Password
************************

1. In order not to store the password in a plain text we substitute our password with an **encrypted** one using a **MD4 hash generator**. You can generate the hash with the following Linux command:

  .. code:: bash

    $ echo -n 'YOUR_PASSWORD' | iconv -t utf16le | openssl md4


  You will have to substitute ``YOUR_PASSWORD`` with the password related to the account in the *wpa_supplicant.conf*. This will be the only time you'll have to type it in plain text. Ask your colleagues to look away from the screen if you are not comfortable in them seeing your password.

2. The previous command will display the encrypted password on your terminal like this:

  .. code:: bash

    $ (stdin)= a6c71eedc2eacbca84003336a4a62a1c

  We **copy the string** that was generated in your terminal screen (i.e. ``'a6c71eedc2eacbca84003336a4a62a1c'``).

  .. tip::
    You can save the hash from your password in a file and then read its content:

    .. code:: bash

      $ echo -n 'YOUR_PASSWORD' | iconv -t utf16le | openssl md4 > hash.txt
      $ cat hash.txt

    The first command creates the encrypted password and stores it in the __hash.txt__ file.
    The second command reads the content of the __hash.txt__ file.
    In general we use the `cat` command to read and concatenate files.

3. Then we open the *wpa_supplicant.conf* file again:

  .. code::

    $ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

4. In the password field replace ``"YOUR_PASSWORD"`` with the string you generated as hexadecimal characters, adding the 'hash:' prefix as shown in the example bellow:

  .. code:: bash

    network={
      ssid="Imperial-WPA"
      proto=RSN
      key_mgmt=WPA-EAP
      pairwise=CCMP
      auth_alg=OPEN
      eap=PEAP
      identity="ic\COLLEGE_USERNAME"
      password=hash:a6c71eedc2eacbca84003336a4a62a1c
    }

5. The last security step to perform is to remove the bash history (the one that stores all the commands we had typed on the terminal). Therefore, we enter the following commands:

  .. code:: bash

    $ history -w
    $ history -c

6. Then we reboot the Pi to check that the password was properly set up:

  .. code:: bash

    $ sudo reboot now

7. And you are done!

Pi as a hotspot
===============

The Raspberry Pi can act as a standalone network. This can be useful in some situations where you do not want to rely on a separate wireless network, or when you might be going to a new location that cannot provide you with a network to use. Remember though that a standalone network made by the Pi will not be connected to the internet. You can find the `guide to set up a standalone network here <https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md>`_.
