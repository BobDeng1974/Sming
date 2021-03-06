Windows Installation
====================

.. highlight:: powershell

Install Chocolatey
------------------

This is a package manager, like apt-get but for Windows. Official
website: https://chocolatey.org

.. note::

   You may prefer a :doc:`windows-manual`.

Open an *administrative* **cmd.exe** command prompt and paste the text
from the box below and press enter::

   # Install Latest Chocolatey
   @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin

Upgrade .NET
------------

Choco requires recent version of .NET in order to be able to access
successfully HTTPS links. To check if you need upgrade type the
following command::

   choco --v

If you see a warning similar to the one below then make sure to upgrade your .NET version:

.. code-block:: text

   Choco prefers to use TLS v1.2 if it is available, but this client is running on .NET 4.3,
   which uses an older SSL. It's using TLS 1.0 or earlier, which makes it susceptible to BEAST
   and also doesn't implement the 1/n-1 record splitting mitigation for Cipher-Block Chaining.
   Upgrade to at least .NET 4.5 at your earliest convenience.

You can upgrade the .NET version from this
`direct link <https://www.microsoft.com/en-us/download/details.aspx?id=55170>`__
or search in internet for “.NET upgrade”.

Add package repository
----------------------

::

   choco sources add -name smingrepo -source 'https://www.myget.org/F/sming/'

Install Sming
-------------

::

   # Powershell - run as Administrator
   choco install -y sming

This will install:

-  Unofficial Espressif Development Kit for Windows
   (`source <https://github.com/slaff/chocolatey-packages/blob/master/manual/esp8266-udk/tools/chocolateyInstall.ps1>`__)
-  Mingw & required packages
   (`source <https://github.com/slaff/chocolatey-packages/blob/master/manual/sming/tools/chocolateyInstall.ps1>`__)
-  Python
-  Latest stable version of Sming
   (`source <https://github.com/slaff/chocolatey-packages/blob/master/manual/sming.core/tools/chocolateyInstall.ps1>`__)

If for some reason you don’t want UDK, MinGW and Environment configured just run::

   choco install sming.core -y -source 'https://www.myget.org/f/sming/'

Configure git for Windows environment
-------------------------------------

Configure your git client to leave line-endings intact or else patching will fail::

   git config --global core.autocrlf input

Install Sming Examples (optional)
---------------------------------

This will install:

-  Java Runtime 8
-  Eclipse C/C++ (`source <https://github.com/kireevco/chocolatey-packages/blob/master/manual/eclipse-cpp/tools/chocolateyInstall.ps1>`__)
-  ``sming`` package

and will create desktop shortcut *Sming Examples*::

   # Run as Administrator
   choco install sming.examples -y

Configuration
~~~~~~~~~~~~~

You might want to configure your project before building. :ref:`Edit component.mk <component>` to the proper values.

Confirm Environment
~~~~~~~~~~~~~~~~~~~

Make sure the MinGW make.exe is the only one in the path.
This will correct most “make: \*\* No rule to make target” problems.*::

   # should only show one make
   where make.exe
   "C:\Tools\mingw64\msys\1.0\bin\make.exe"

Build Basic_Blink
-----------------

1. Open Eclipse via “Sming Examples” Desktop link
2. Find *Basic_Blink* project
3. Build

Update Sming
------------

Sming is very dynamic and updates are usually announced in gitter. The
command below will get for you the latest ``stable`` release::

   choco upgrade sming -y

Force Reinstall Sming
---------------------

In case something is broken, this will overwrite the current Sming installation::

   choco install sming -y -force -source 'https://www.myget.org/F/sming/'

Next steps
----------

Proceed to :doc:`config`.
