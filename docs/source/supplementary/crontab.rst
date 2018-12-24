=============================
Crontab - scheduling commands
=============================

Crontab (chron tab → time table) is a scheduling assistant built into Unix systems. It is very useful for running commands in a terminal environment at specific times.

Say you have a python3 file called ``script.py`` that posts to the internet, and you need to run it at a regular interval. One option would be to keep the script running and sleep it using ``time.sleep(s)`` to pause it for ``s`` seconds. However if this is running over a long period, this is not ideal. What happens if the script crashes for some reason?

First thing is to make the python3 script an executable. To do this you must first ensure you have included a `shebang line <https://www.in-ulm.de/~mascheck/various/shebang/>`_. In the python file, it must be the first line of the file:

.. code-block:: python

  #!/usr/bin/python3
  import a
  import b
  import c

  # ... rest of file

Then you can change the permissions of the file to make it executable:

.. code-block:: bash

  $ chmod u+x /home/pi/script.py

.. note::
  This assumes that ``script.py`` is saved in the ``/home/pi`` directory.

To check that this worked, you can use the ``ls`` command when in the home directory.

.. code-block:: bash

  $ cd /home/pi
  $ ls

The contents of the directory will be printed, and the ``script.py`` file will be coloured differently (either green or red) instead of white. This means the script can now be executed directly (meaning you don't need to write ``python3`` beforehand):

.. code-block:: bash

  $ /home/pi/script.py

This is important as you can now add it to the crontab configuration file.

.. code-block:: bash

  $ crontab -e

This will open the crontab configuration looks like this:

.. code-block:: text

  # Edit this file to introduce tasks to be run by cron.
  #
  # Each task to run has to be defined through a single line
  # indicating with different fields when the task will be run
  # and what command to run for the task
  #
  # To define the time you can provide concrete values for
  # minute (m), hour (h), day of month (dom), month (mon),
  # and day of week (dow) or use '*' in these fields (for 'any').#
  # Notice that tasks will be started based on the cron's system
  # daemon's notion of time and timezones.
  #
  # Output of the crontab jobs (including errors) is sent through
  # email to the user the crontab file belongs to (unless redirected).
  #
  # For example, you can run a backup of all your user accounts
  # at 5 a.m every week with:
  # 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
  #
  # For more information see the manual pages of crontab(5) and cron(8)
  #
  # m h  dom mon dow   command

  @reboot /home/pi/script.py
  */10 * * * * /home/pi/script.py

As you can see, two lines have been added to the bottom. The first one set runtime to ``@reboot`` which means the ``/home/pi/script.py`` command gets run right away once the Pi is rebooted.

The second line is configured to run the command on *every 10th minute*. You can use sites such as `crontab.guru <https://crontab.guru>`_ to help you configure the exact timings you wish.
