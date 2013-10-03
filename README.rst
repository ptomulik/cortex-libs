cortex-libs
===========

A skeleton used to compile-test libraries for ARM cortex microcontrollers. 

Overview
--------

The actual code that gets compiled is held as separate git-based projects,
which are "attached" to this framework as git submodules. Here we have just a
single ``SConstruct`` script which triggers compilation of all the submodules
by calling their ``SConscripts``. 

Getting Started
---------------

Three steps are necessary to bootstrap complete source tree:

#. Clone this repository::

      git clone git@github.com:ptomulik/cortex-libs.git
      cd cortex-libs

#. Initialize submodules::
      
      git submodule init

#. Update submodules::

      git submodule update

Compiling
---------

Building Libraries
^^^^^^^^^^^^^^^^^^

Just type::

    scons

to generate all libraries. All the stuff goes to ``build`` directory.

What gets built
```````````````

Currently we build the following stuff:

+-----------------------+-----------------------------------------------------+
|      Module           |                       Info                          |
+=======================+=====================================================+
| `ST/StdPeriph`_       | StdPeriph library for STM32 MCUs.                   |
+-----------------------+-----------------------------------------------------+
| `ptomulik/stm32xx`_   | C++ library for STM32 software developers.          |
+-----------------------+-----------------------------------------------------+

The libraries are built for the following target MCUs:

- STM32F10x_CL, STM32F10x_HD, STM32F10x_HD_VL, STM32F10x_LD, STM32F10x_LD_VL,
  STM32F10x_MD, STM32F10x_MD_VL, STM32F10x_XL
- STM32F4xx, STM32F40xx, STM32F427x.

Builing Unit Test Runners
^^^^^^^^^^^^^^^^^^^^^^^^^

Some libraries come with unit tests, to build them type::

    scons unit-test


LICENSE
-------

NOTE
^^^^

The following license applies only to the bare skeleton, which currently
consists of: 

- this ``README.rst``, and 
- the top level ``SConstruct`` file.

Other files, if present, may be subject to separate license terms and may be
copyrighted by other parties.

LICENSE
^^^^^^^

Copyright (c) 2013 by Pawel Tomulik <ptomulik@meil.pw.edu.pl>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE

.. _ST/StdPeriph: https://github.com/ptomulik/stm32-stdperiph
.. _ptomulik/stm32xx: https://github.com/ptomulik/stm32xx

.. <!--- vim: set expandtab tabstop=2 shiftwidth=2 syntax=rst: -->
