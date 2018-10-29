========
Software
========

Now that you have your Pi connected to the internet, you should make sure it is completely up-to-date.

Removing packages
=================

When you install a standard build of Raspbian, a lot of packages get installed for you. To make sure some of the larger packages aren't wasting space on you SD card, you can remove them. We recommend you remove some of these. This can be done by running each of the following lines one-by-one on the command line.

.. code:: bash

  sudo apt-get purge libreoffice wolfram-engine sonic-pi scratch
  sudo apt-get clean
  sudo apt-get autoremove

You can reinstall any of these again later if you need them.

Operating System
================

Run the following line in the terminal to update your Pi. Note: this might take some time.

.. code:: bash

  sudo apt-get update && sudo apt-get upgrade

Installing packages
===================

Now the OS is updated, we need to install Python. To install Linux packages onto our Pi we use the command: ``sudo apt-get install <name_of_package>`` in the terminal. Each installation could take a few minutes.

1. Run each of the following two lines to install C lib, needed by Python

  .. code:: bash

    sudo apt-get -y install libffi-dev
    sudo apt-get -y install libssl-dev

2. Installing Python, run each line one-by-one ensuring they complete

  .. code:: bash

    sudo apt-get -y install build-essential python-dev python-openssl
    sudo apt-get -y install python-setuptools
    sudo apt-get -y remove --purge python-pip
    sudo apt-get -y install python-pip
    sudo pip install --upgrade pip

Next, we're going to take you through how to connect remotely to your Pi over a network (without needing to use a monitor keyboard and mouse with the Pi). However we strongly recommend you remember to take a backup of your SD card later. You can find a guide on how to do this later on: :doc:`backing-up`.
