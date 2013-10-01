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
  '-Wall', 
  '-Wextra', 
  '-Werror',
  '-Wa,-adhlns=\'${TARGET}.lst\'', 
  '-fmessage-length=0',
  '-funsigned-bitfields'#,
#  '-nostartfiles'
]

#
# FLAGS FOR DEBUG AND RELEASE VARIANTS
#
dbg_flags = {
  True  : [ '-O0', '-g3'   ], # debug flags
  False : [ '-O2', '-flto' ], # release flags
}


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
cxxflags  = ['-std=c++11', '-fno-exceptions', '-fno-rtti']
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


# Compiling StdPeriph for STM32F10x family


for mcu_line in [ 'CL', 'LD', 'MD', 'HD', 'XL', 'LD-VL', 'MD-VL', 'HD-VL']:
    overrides = {
        'MCU_FAMILY'    : 'STM32F10X',
        'MCU_LINE'      : mcu_line,
    }
    lib = SConscript( 'ST/StdPeriph/SConscript', 
                      variant_dir='build/ST/%s' % mcu_line,
                      duplicate=0, exports=['env', 'overrides'])

# Local Variables:
# # tab-width:4
# # indent-tabs-mode:nil
# # End:
# vim: set syntax=scons expandtab tabstop=4 shiftwidth=4:
