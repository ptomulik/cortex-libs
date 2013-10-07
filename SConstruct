#
# Copyright (c) 2013 by Pawel Tomulik
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE

import os

tools = {
  'ADDR2LINE'   : 'arm-none-eabi-addr2line',
  'AR'          : 'arm-none-eabi-ar',
  'AS'          : 'arm-none-eabi-gcc',
  'CXXFILT'     : 'arm-none-eabi-c++filt',
  'CPP'         : 'arm-none-eabi-cpp',
  'CS'          : 'arm-none-eabi-cs',
  'ELFEDIT'     : 'arm-none-eabi-elfedit',
  'CXX'         : 'arm-none-eabi-g++',
  'CC'          : 'arm-none-eabi-gcc',
  'GCC_AR'      : 'arm-none-eabi-gcc-ar',
  'GCC_NM'      : 'arm-none-eabi-gcc-nm',
  'GCC_RANLIB'  : 'arm-none-eabi-gcc-ranlib',
  'GCOV'        : 'arm-none-eabi-gcov',
  'GDB'         : 'arm-none-eabi-gdb',
  'GPROF'       : 'arm-none-eabi-gprof',
  'LINK'        : 'arm-none-eabi-ld',
  'NM'          : 'arm-none-eabi-nm',
  'OBJCOPY'     : 'arm-none-eabi-objcopy',
  'OBJDUMP'     : 'arm-none-eabi-objdump',
  'RANLIB'      : 'arm-none-eabi-ranlib',
  'READELF'     : 'arm-none-eabi-readelf',
  'SIZE'        : 'arm-none-eabi-size',
  'STRINGS'     : 'arm-none-eabi-strings',
  'STRIP'       : 'arm-none-eabi-strip',
}

#
# COMMON COMPILATION FLAGS
#
common_flags = [
    '-g',
    '-Wall', 
    '-Wextra', 
    '-Werror',
    '-fmessage-length=0',
    '-funsigned-bitfields'
]

#
# ASFLAGS
#
asflags   = ['-x', 'assembler-with-cpp']
#
# CFLAGS
#
cflags    = []
#
# CXXFLAGS
#
cxxflags  = ['-fno-exceptions', '-fno-rtti']
#
# LINKFLAGS
#
linkflags = []

#
# ALL THE FLAGS TOGETHER
#
kwargs = tools.copy()
kwargs.update( ASFLAGS   = common_flags + asflags,
               CFLAGS    = common_flags + cflags,
               CXXFLAGS  = common_flags + cxxflags,
               LINKFLAGS = common_flags + linkflags )

env = Environment(ENV = os.environ, **kwargs)

mcu_targets = [

    # STM32F10x
    'STM32F10X_CL',
    'STM32F10X_LD',
    'STM32F10X_MD',
    'STM32F10X_HD',
    'STM32F10X_XL',
    'STM32F10X_LD_VL',
    'STM32F10X_MD_VL',
    'STM32F10X_HD_VL',

    # STM32F4xx
#    'STM32F4XX',
#    'STM32F40XX',
#    'STM32F427X',
]

#
# Compile StdPeriph for each STM32Fxxx target
#
for mcu_target in mcu_targets:
    options = { 
      'MCU_TARGET'        : mcu_target,
      'CMSIS_BASEDIR'     : env.Dir('.'),
    }
    lib = env.SConscript( 'ST/StdPeriph/SConscript', 
        variant_dir='build/ST/%s' % mcu_target,
        duplicate=0, exports=['env', 'options'] )

#
# Compile stm32++ for each STM32Fxxx target
#
for mcu_target in mcu_targets:
    options = { 
      'MCU_TARGET'        : mcu_target,
      'CMSIS_BASEDIR'     : env.Dir('.'),
      'STDPERIPH_BASEDIR' : env.Dir('ST/StdPeriph'),
    }
    lib = env.SConscript( 'ptomulik/stm32xx/SConscript', 
        variant_dir='build/stm32xx/%s' % mcu_target,
        duplicate=0, exports=['env', 'options'] )

#
# Compile unit tests for stm32++
#
for mcu_target in mcu_targets:
    options = { 
      'MCU_TARGET'        : mcu_target,
      'CMSIS_BASEDIR'     : env.Dir('.'),
      'STDPERIPH_BASEDIR' : env.Dir('ST/StdPeriph'),
      'SCONSCRIPT_TARGET' : 'unit-test'
    }
    target = env.SConscript( 'ptomulik/stm32xx/SConscript', 
        variant_dir='build/test/unit/stm32xx/%s' % mcu_target,
        duplicate=0, exports=['env', 'options'] )
env.Ignore('build/test', 'build/test/unit')
env.Clean('build/test', 'build/test/unit')
env.Alias('unit-test', 'build/test/unit')

# Local Variables:
# # tab-width:4
# # indent-tabs-mode:nil
# # End:
# vim: set syntax=scons expandtab tabstop=4 shiftwidth=4:
