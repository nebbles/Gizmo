=======================
Backing up your SD card
=======================

It is useful and **always** advisable to backup a working copy of your Pi image. For example, make a backup copy after setting up WiFi. The next time the WiFi is not working, you can reformat the SD card and reinsert this backup copy to revert back to previous version. After this, your Pi will connect to the WiFi right away like before.

.. important::
  Remember that if you SD card becomes corrupted you will likely have to wipe it and lose all your files to reformat it. Despite this being unlikely, always remember to take backups at key milestones throughout a project so that you can restore to a recent state and not lose too much work.

  We also strongly recommend using Git to manage project files. It allows for collaborative working and means you can easily restore your project files onto any new device you might need.

Backup using Windows
====================

1. `Download Win 32 Disk Imager <https://sourceforge.net/projects/win32diskimager/>`_ if none installed on your computer.
2. Insert the SDCard into your computer (e.g. via card reader or SD card slot if your computer has one).
3. Open Win 32 Disk Imager. Select a location and give a file name for the backup image.
4. Select the right drive.
5. Click Read.
6. Once done, keep this backup copy safe. Please note that the size of the backup is the same size of your SD Card. So please be mindful that it will take a considerable amount of disk space.

Backup using macOS
==================

1. Open DiskUtility
2. Select "APPLE SD Card Reader Media"
3. Click on *File → New File → Image from "Untitled"*
4. Leave the selections "CD/DVD" and "no encryption"
5. Insert your password when asked
6. You're done!

Restoring and image to the SD Card
==================================

If you have an image saved somewhere, you can restore it to your SD card at any time to revert back to that version. To do this, check the section on :ref:`flash-sd`.

If you wish to install a fresh Raspbian OS, you should look at the chapter on :doc:`setup-sd`.
