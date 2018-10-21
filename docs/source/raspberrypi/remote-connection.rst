===================
Connecting Remotely
===================

SSH via remot3.it
=================

**remot3.it** services allow you to connect easily and securely to your Pi from a mobile app, browser window and a terminal. It allows you to control remote computers (such as the Pi) using TCP hosts such as SSH. You will be able to connect to your Pi from laptop or desktop at home. The free remot3.it account allows for multiple registered services and 8 hours connections on up to 1 concurrent service(s).

1. To configure weaved in our Pi, first we need to open an account on the `remot3.it website <https://www.remot3.it/web/index.html>`_. You can register from your laptop or desktop.

2. Once you have an account: from your Pi terminal, we need to install weaved (which is the precursor on which remot3.it is based) to be able to connect our Pi. To install it:

  .. code:: bash

    sudo apt-get -y install weavedconnectd

3. Then we will open the weaved installer to link your Pi to your remot3.it account:

  .. code:: bash

    sudo weavedinstaller

4. Enter your remot3.it account username and password. Next, you will see this menu:

  .. image:: /_static/images/pi-remote/remot3-installer-menu-00.png
    :align: center

5. Then enter a name for your Pi (e.g. "pi01"). You can make it up, but remember to make a name easy for you to identify a specific Pi in case you have more than one attached to the weaved service:

  .. image:: /_static/images/pi-remote/remot3-installer-menu-01.png
    :align: center

6. Initially you won’t have any Weaved services installed, so the upper part is empty. Enter **1** to attach Weaved to an existing TCP service (host) on your Raspberry Pi.  You should now see the following screen:

  .. image:: /_static/images/pi-remote/remot3-installer-menu-02.png
    :align: center

7. Enter **1** for SSH.

8. Next, we accept the default port (**y**).

  .. image:: /_static/images/pi-remote/remot3-installer-menu-03.png
    :align: center

9. The installer confirms your choice and asks you to give this connection a name:

  .. image:: /_static/images/pi-remote/remot3-installer-menu-04.png
    :align: center

10. You will now return to the main menu, where you can see your Weaved Service Connection installed, then enter **3** to exit.

  .. image:: /_static/images/pi-remote/remot3-installer-menu-05.png
    :align: center

Your Pi is now ready to run headless (without a direct connection to a screen), we just have to connect with it over SSH on our laptop to control it from the terminal. We have created two access guides, one for Linux and Mac Users and the other for Windows (:ref:`access-from-windows`).

Accessing from Linux or macOS
*****************************

1. We will now see how to access using your laptop to your Pi from the terminal. First, if you login to your remot3.it account,  you will get a list of your devices:

  .. image:: /_static/images/pi-remote/remot3-logged_in.png
    :align: center

2. In your case you will have just one item. When you click on the name of you device, a pop-up will open:

  .. image:: /_static/images/pi-remote/remot3-pop-up-01.png
    :align: center

3. Click on the name of your ssh service and then "Confirm".

4. A second pop-up will appear:

  .. image:: /_static/images/pi-remote/remot3-pop-up-02.png
    :align: center

  We copy the command after *For pi username*, in this example it is: ``ssh -l pi proxy54.yoics.net -p 30015``. For you it will be different.

5. Then, paste the command in your laptop or desktop terminal app. (`Optional alternative app for Mac <https://iterm2.com>`_)

6. The terminal is going to show you this message:

  .. image:: /_static/images/pi-remote/ssh-authenticity-check.png
    :align: center

  Type ``yes``.

7. Then, you will be prompted to enter a password, you should enter the password of the ``pi`` user of your Pi. By default it is ``raspberry`` but you should have changed it in an earlier chapter (:ref:`pi-password`).

You will see on your laptop's terminal that now you are user pi. You are connected from your laptop to your Pi. As long as your Pi is connected to the internet, you can remotely log into it and control it, so you don't need to use the display and mouse anymore.

For some more details on remote connections see :ref:`alternative-ssh`.

.. tip::
  To manage remote terminal sessions we suggest you use *Screen*, check out the guide later in the section :ref:`ssh-screen`.

.. _access-from-windows:

Accessing from Windows
**********************

If your computer operative  system is Windows, to access remotely you will need to install PuTTY, which  is a free implementation of SSH and Telnet for Windows and Unix platforms.

1. To download it click `here <http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html>`_.

  .. image:: /_static/images/pi-remote/windows-putty.jpg
    :align: center

2. Once downloaded, proceed with the standard installation.

3. Once installed double click on the **putty.exe** and you will see a window that looks like the one below:

  .. image:: /_static/images/pi-remote/windows-putty-connect.jpg
    :align: center

4. Then, if you login to your remot3.it account,  you will get a list of the services linked to your devices:

  .. image:: /_static/images/pi-remote/remot3-logged_in.png
    :align: center

5. In your case you will have just one item. When you click on the name of you device, a pop-up will open:

  .. image:: /_static/images/pi-remote/remot3-pop-up-01.png
    :align: center

6. Click on the name of your ssh service and then "Confirm".

7. A second pop-up will appear:

  .. image:: /_static/images/pi-remote/remot3-pop-up-02.png
    :align: center

5. Insert the server address and port obtained from remot3.it into Putty and connect!

  .. note::
    Rather than typing in ``ssh -l pi <server> -p <port>``, you just need to insert the server url and port from remot3.it.

6. When asked for username and password, use your Pi username and password to log-in.

  .. note::
    This is not weaved username and password. The default password is ``raspberry`` but you should have changed it in an earlier chapter (:ref:`pi-password`).

  .. image:: /_static/images/pi-remote/windows-putty-login.png
    :align: center

To exit your putty session, type "exit" and enter.

.. tip::
  To manage remote terminal sessions we suggest you use *Screen*, check out the guide later in the section :ref:`ssh-screen`.

For some more details on remote connections see :ref:`alternative-ssh`.

.. _ssh-screen:

SSH using Screen
================

Remember you can be connected to your Pi for up to 8 hours using **remot3.it**, after that time you have to connect again to your account and do the same access procedure we explained in the previous sections. Therefore we will show you how a *virtual terminal* can help you when you are working remotely on your Pi.

**Screen** is a full-screen software program allows you to use multiple windows (virtual VT100 terminals) in Unix. It offers a user to open several separate terminal instances inside a one single terminal window manager.

The screen application is very useful, if you are dealing with multiple programs from a command line interface and for separating programs from the terminal shell. It also allows you to share your sessions with others users and detach/attach terminal sessions.

When to use Screen?
*******************

One of the advantages of *Screen*, is that you can detach it. Then, you can restore it without losing anything you have done on the *Screen*. One of the typical scenario where *Screen* is of great help is when you are in the middle of SSH session and you want to download a file, update the operative, or transfer a big file to your RPi. The process could be 2 hours long. If you disconnect the SSH session, or suddenly the connection lost by accident, then the download process will stop. You have to start from the beginning again. To avoid that, we can use screen and detach it.

Installing Screen
*****************

Screen allows you to use multiple windows (virtual VT100 terminals) in Unix. If your local computer crashes, or you are connected remotely and lose the connection, the processes or login sessions you establish through screen don't get lost. To install Screen you can enter the following command on the Pi terminal:

.. code:: bash

  sudo apt-get -y install screen

How to use Screen
*****************

- When you are in your terminal, you can create a *screen* or virtual terminal e.g. we will name the screen ``mysession``:

  .. image:: /_static/images/pi-remote/screen-terminal.png
    :align: center

- Then you will be automatically attached to the ``mysession`` screen, that from now on we will call just *"screen"*. You can  now execute commands and work in the terminal without worrying to loose your work:

  .. image:: /_static/images/pi-remote/screen-attached.png
    :align: center

- You can detach from the *"screen"* by pressing ``Ctrl-A`` and then ``d``. Once detached we will be returned to our Pi terminal outside any *screen* session. To check the list of *active screens*: ``screen -ls``

  .. image:: /_static/images/pi-remote/screen-list.png
    :align: center

- We get a list with all the screen IDs. If we want to attach to a particular *screen* we can enter ``screen -r name_of_terminal`` like in the example below:

  .. image:: /_static/images/pi-remote/screen-attaching.png
    :align: center

Basic commands to work with Screen
**********************************

.. list-table::
   :widths: 10 20
   :header-rows: 1

   * - Screen command
     - Description
   * - ``screen -S name_of_terminal``
     - Assigning name to the virtual terminal or screen session
   * - ``screen -ls``
     - List all the virtual sessions or screens opened
   * - ``screen -X -S name_of_terminal quit``
     - Kill an specific virtual terminal.
   * - ``screen -r name_of_terminal``
     - Attach to the virtual terminal or screen
   * - Press ``Ctrl-A`` and ``d``
     - Detach from virtual terminal  or screen
   * - Press ``Ctrl-A`` and ``K``
     - This command will leave and kill the virtual terminal or screen
   * - Press ``Ctrl-A`` and ``n``
     - Switching to the next virtual terminal or screen
   * - Press ``Ctrl-A`` and ``p``
     - Switching to the previous virtual terminal or screen

For additional commands check out the `Screen Cheatsheet <https://github.com/ICL-DE/Gizmo/blob/master/SupplementaryMaterial/Screen_cheatsheet.md>`_

.. _alternative-ssh:

Alternative ways to connect via SSH
===================================

We already know how to connect through remot3.it service, but we know that the connection lasts 8 hours and it allows us to work on one terminal session at a time. Therefore, with the help of remot3.it and another commands we can connect to or Pi for longer and using multiple terminals. In this section we are going to connect to our Pi using its IP address.

If you do not know what is an IP address, please go to the `this video <https://www.youtube.com/watch?v=7_-qWlvQQtY>`_ for a quick explanation. The IPs can be dynamic or static, but what is the difference? When a device is assigned a static IP address, the address does not change. Most devices use dynamic IP addresses, which are assigned by the network when they connect and change over time (which is the case for our Pi on the Imperial-WPA).

Get IP address from remot3.it
***************************************

remot3.it displays the external IP of the devices you have registered. You can get your Pi's one in the *External IP* Tab:

.. image:: /_static/images/pi-remote/remot3-ip.png
  :align: center

.. note::
  If you are connected with your laptop to the same network of your RPi the internal and external IP addresses will be the same like in the example above.

Get IP address from the terminal
********************************

We can use a command to check the different internet connections available on our system: ``ifconfig`` or ``ifconfig -a``.

.. code:: bash

  $ ifconfig

This command allows to know the IP addresses assigned to our Pi. The ``wlan0``, indicates the status of the WiFi, and ``eth0`` shows the status of the Ethernet (wired) connection. In the next screen shoot shows an example of a Pi connected to the internet using the ethernet port. The red oval shows where to find the IP address assigned to the Pi for the Ethernet connection.

.. image:: /_static/images/pi-remote/ifconfig.png
  :align: center

You can find your IP address for the WiFi connection in the corresponding ``wlan0`` ``inet addr`` field.

Connect knowing your IP
***********************

Once you know the IP (e.g. your IP is ``192.31.123.122``), you can access using your laptop terminal to the Pi like this:

.. code:: bash

  $ ssh pi@192.31.123.122

.. tip::
  The syntax for this command is ``ssh username@ipaddress``. You may want to log in using a different username to the default ``pi`` if you created one.

.. note::
  The IP addresses at Imperial are dynamic (most IPs are dynamic), meaning they are constantly changing and being reallocated as needed. It could be that your IP changes in a couple of hours, a day, or a bit longer, so be prepared to have to repeat the steps above to rediscover what your new IP address is.

VNC GUI control
===============

.. todo::
  Using VNC for remote GUI control will be added later.

Transferring files
==================

Using terminal
**************

If are programming on your laptop and you want to transfer your code to test it in your Pi, you can use a number of different methods:

- Secure Copy (scp)
- SSH File Transfer Protocol (`sftp <https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol>`_).
- Secure File Transfer Protocol (ftps)

Secure Copy (scp)
-----------------

``scp`` - Securely copy a file from one location to another.

The general syntax is as follows: ``scp copy_from copy_to``

The locations are written relatively. So if you were to copy a file from one place on your local computer to anther place, you would simply provide the path:

.. code:: bash

  scp /home/pi/Desktop/myprogram.py /home/pi/Desktop/myfolder/

Which would copy the file ``myprogram.py`` to a folder within the same location.

.. note::
  When you use SSH to remotely 'log in' to a computer such as a Pi, then all the commands you then type into your terminal are considered 'local'.

If you wanted to copy something from your computer to the Pi then that would be considered a local-to-remote copy.

For that you would need to :

1. Get the path to the file locally on your computer.
2. Get the path to the location on the Pi you would like to save it.

.. code:: bash

  scp /Users/username/Desktop/program.py pi@192.168.1.10:/home/pi/Desktop

As you can see we copied the file ``/Users/username/Desktop/program.py`` **from** the local computer **to** a remote computer (which is why we need to prefix it with the username and IP address ``pi@192.168.1.10``) in the location specified ``/home/pi/Desktop``.

We can even copy a file back by reversing the order of the commands:

.. code:: bash

  scp pi@192.168.1.10:/home/pi/Desktop/program.py /Users/username/Desktop/

.. hint::
  If you want to copy a folder (not an individual file) then you need to add the *recursive* flag to the command. This tells the terminal that you want to copy the folder and all its sub-contents to the new location. i.e.

  .. code:: bash

    scp /Users/username/Desktop/Gizmo_Folder/ pi@192.168.1.10:/home/pi/Desktop/

SFTP
----

1. First we log into a session with the Pi using the correct username and IP address

.. code:: bash

  sftp pi@192.168.1.1

2. Once establish the connection through SFTP, we can navigate around using ``cd`` (change directory) and ``pwd`` (print working directory) and ``ls`` (to list contents of current directory).

3. Once we have the a file to download from the remote computer (Pi):

  .. code:: bash

    get /path/to/file

  Or for a folder:

  .. code:: bash

    get -r /path/to/directory/

4. To transfer files on our (local) computers to the remote (Pi) we can ``put``:

  .. code:: bash

    put /path/of/local/file

  The same flags that work with ``get`` apply to ``put``. So to copy an entire local directory:

  .. code:: bash

    put -r /path/of/local/directory/

.. note::
  More details and examples of SFTP can be `found here <https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server>`_.

Using Software
**************

Instead a terminal, we can use to transfer files using a software that mounts any remote server storage as a local disk in the Finder.app on Mac and the File Explorer on Windows. We suggest:

- `Cyberduck <https://cyberduck.io/?l=en>`_

  .. image:: /_static/images/pi-remote/cyberduck.png
    :align: center

- For just Windows you can use: `WinSCP <https://winscp.net/eng/index.php>`_

  .. image:: /_static/images/pi-remote/winsc-portable.png
    :align: center
