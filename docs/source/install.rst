
Installation
------------

You will need to install the libleveldb library. Install `Python 3.6 <https://www.python.org/downloads/release/python-366/>`__ or  `Python 3.7 <https://www.python.org/downloads/release/python-370/>`_ to make sure you don't run into any issues with your version of Python being different than the current maintainer's version. Note that Python 3.5 and below are not supported.

You should install platform specific items before installing ``neo-python``.


Platform Specific Instructions
==============================

Ubuntu/Debian 16.10+
""""""""""""""""""""

Ubuntu starting at 16.10 supports Python 3.6+ in the official repositories.

First, ensure Ubuntu is fully up-to-date with this:

::

   sudo apt-get update && sudo apt-get upgrade
   
You can install Python 3.7 and all the system dependencies like this:

::
   
   sudo apt-get install python3.7 python3.7-dev python3.7-venv python3-pip libleveldb-dev libssl-dev g++
  

Or, you can install Python 3.6 and all the system dependencies like this:

::

    sudo apt-get install python3.6 python3.6-dev python3.6-venv python3-pip libleveldb-dev libssl-dev g++


Older Ubuntu versions (eg. 16.04)
"""""""""""""""""""""""""""""""""

For older Ubuntu versions you'll need to use an external repository like Felix Krull's deadsnakes PPA at https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa (read more `here <https://askubuntu.com/questions/865554/how-do-i-install-python-3-6-using-apt-get>`_):

(The use of the third-party software links in this documentation is done at your own discretion and risk and with agreement that you will be solely responsible for any damage to your computer system or loss of data that results from such activities.)

::

    apt-get install software-properties-common python-software-properties
    add-apt-repository ppa:deadsnakes/ppa
    apt-get update
    apt-get install python3.6 python3.6-dev python3.6-venv python3-pip libleveldb-dev libssl-dev g++


Centos/Redhat/Fedora
""""""""""""""""""""

::

    # Install Python 3.6:
    yum install -y centos-release-scl
    yum install -y rh-python36
    scl enable rh-python36 bash

    # Install dependencies:
    yum install -y epel-release
    yum install -y readline-devel leveldb-devel libffi-devel gcc-c++ redhat-rpm-config gcc python-devel openssl-devel


Windows
"""""""

The installation on the Windows operating system needs a set of unique steps and several common issues that might require troubleshooting, for this reason we dedicated a whole separate page for installing ``neo-python`` on windows.

If this is your operating system please check :doc:`installwindows`


OSX
"""

::

    brew install leveldb

Common issues on OSX
''''''''''''''''''''

If you're having an issue similar to this:

.. code-block:: sh

    from ._plyvel import (  # noqa
    ImportError: dlopen(neo-python/venv/lib/python3.6/site-packages/plyvel/_plyvel.cpython-35m-darwin.so, 2): Symbol not found: __ZN7leveldb2DB4OpenERKNS_7Options
    ERKSsPPS0_
    Referenced from: neo-python/venv/lib/python3.6/site-packages/plyvel/_plyvel.cpython-35m-darwin.so
    Expected in: flat namespace

**Solution**: Update to plyvel 1.0.4: `pip install -r requirements.txt`

-----

You may also encounter issues when installing the pycrypto module on OSX:

.. code-block:: sh

    src/_fastmath.c:36:11: fatal error: 'gmp.h' file not found
    # include <gmp.h>
              ^~~~~~~
    330 warnings and 1 error generated.
    error: command 'clang' failed with exit status 1

This may be fixed by installing the gmp library using homebrew and running pip install with the following commandline:

.. code-block:: sh

    brew install gmp
    CFLAGS='-mmacosx-version-min=10.7 -stdlib=libc++' pip install --no-use-wheel pycrypto --no-cache-dir --global-option=build_ext --global-option="-I/usr/local/Cellar/gmp/6.1.2/include/" --global-option="-L/usr/local/lib"

-----

``import scrypt`` / ``Reason: image not found``

If you encounter an error like this:

.. code-block:: sh

    import scrypt
    File "/project_dir/venv/lib/python3.6/site-packages/scrypt.py", line 11, in
    _scrypt = cdll.LoadLibrary(imp.find_module('_scrypt')[1])
    File "/project_dir/venv/lib/python3.6/ctypes/init.py", line 429, in LoadLibrary
    return self._dlltype(name)
    File "/project_dir/venv/lib/python3.6/ctypes/init.py", line 351, in init
    self._handle = _dlopen(self._name, mode)
    OSError: dlopen(/project_dir/venv/lib/python3.6/site-packages/_scrypt.cpython-36m-darwin.so, 6): Library not loaded: /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib
    Referenced from: /project_dir/venv/lib/python3.6/site-packages/_scrypt.cpython-36m-darwin.so
    Reason: image not found

The solution probably is

.. code-block:: sh

    brew reinstall openssl

-----

If you encounter an issue installing the ``scrypt`` module (possibly after updating OSX) with an error like this:

.. code-block:: sh

    ld: library not found for -lcrypto
    clang: error: linker command failed with exit code 1 (use -v to see invocation)
    error: command 'gcc' failed with exit status 1

The solution probably is

.. code-block:: sh

    $ brew install openssl
    $ export CFLAGS="-I$(brew --prefix openssl)/include $CFLAGS"
    $ export LDFLAGS="-L$(brew --prefix openssl)/lib $LDFLAGS"


Install from PyPi
=================

The easiest way to install ``neo-python`` on your machine is to download it and install from PyPi using ``pip``. First, we recommend you to create a virtual environment in order to isolate this installation from your system directories and then install it as you normally would do:

::

    # create project dir
    mkdir myproject
    cd myproject
    
    # create virtual environment using Python 3.7 and activate or skip to the next step for Python 3.6
    python3.7 -m venv venv
    source venv/bin/activate
    
    # create virtual environment using Python 3.6 and activate
    python3.6 -m venv venv
    source venv/bin/activate

    (venv) pip install neo-python


Install from Git
================

Clone the repository at `https://github.com/CityOfZion/neo-python/ <https://github.com/CityOfZion/neo-python/>`_ and navigate into the project directory.
Make a Python 3 virtual environment and activate it via

::

    git clone https://github.com/CityOfZion/neo-python.git
    cd neo-python
    
    # if you want to use the development branch, switch now
    git checkout development
    
    # create virtual environment using Python 3.7 and activate or skip to the next step for Python 3.6
    python3.7 -m venv venv
    source venv/bin/activate
    
    # create virtual environment using Python 3.6 and activate
    python3.6 -m venv venv
    source venv/bin/activate

    # install the package in an editable form
    (venv) pip install -e .


Updating neo-python from Git
""""""""""""""""""""""""""""

If you are updating neo-python with ``git pull``, make sure you also update the dependencies with ``pip install -r requirements.txt``.


Bootstrapping the Blockchain
============================

If you use neo-python for the first time, you need to synchronize the blockchain, which may take a long time. Included in this project is ``bootstrap.py`` to automatically download a chain directory for you.

To bootstrap for testnet, run ``np-bootstrap``, get a cup of coffee and wait.

To bootstrap for mainnet, use ``np-bootstrap -m`` and get 8 cups of coffee (3.3 GB file).


