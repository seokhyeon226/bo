#******************************************************************************
#
# Makefile - Makefile of semihosting example code
#
# Copyright (c) 2013 Roger Ye.  All rights reserved.
# Software License Agreement
# 
# 
# THIS SOFTWARE IS PROVIDED "AS IS" AND WITH ALL FAULTS.
# NO WARRANTIES, WHETHER EXPRESS, IMPLIED OR STATUTORY, INCLUDING, BUT
# NOT LIMITED TO, IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE APPLY TO THIS SOFTWARE. The AUTHOR SHALL NOT, UNDER
# ANY CIRCUMSTANCES, BE LIABLE FOR SPECIAL, INCIDENTAL, OR CONSEQUENTIAL
# DAMAGES, FOR ANY REASON WHATSOEVER.
#
#******************************************************************************

# This is the makefile for goldfish serial device testing

#
# The base directory.
#
ROOT=../..
PROJECTNAME=c06e2

LD=arm-none-eabi-gcc

#
# Include the common make definitions.
#
include ${ROOT}/makedefs.arm

#
# The default rule, which causes the ${PROJECTNAME} example to be built.
#
all: ${COMPILER}
all: ${COMPILER}/${PROJECTNAME}.axf

#
# The rule to debug the target using Android emulator.
#
debug:
	./setup_sdk.sh
	ddd --debugger arm-none-eabi-gdb ${COMPILER}/${PROJECTNAME}.axf &
	bin/emulator -verbose -show-kernel -avd hd2 -qemu -s -S -semihosting -kernel ${COMPILER}/${PROJECTNAME}.axf

#
# The rule to debug the target using Android emulator.
#
nm:
	@arm-none-eabi-nm -n ${COMPILER}/${PROJECTNAME}.axf

#
# The rule to clean out all the build products.
#
clean:
	@rm -f log.txt
	@rm -rf ${COMPILER} ${wildcard *~}
	@rm -rf ./bin

#
# The rule to create the target directory.
#
${COMPILER}:
	@mkdir -p ${COMPILER}

#
# Rules for building the ${PROJECTNAME} example.
#
${COMPILER}/${PROJECTNAME}.axf: ${COMPILER}/${PROJECTNAME}.o
${COMPILER}/${PROJECTNAME}.axf: ${PROJECTNAME}.ld
SCATTERgcc_${PROJECTNAME}=${PROJECTNAME}.ld
ENTRY_${PROJECTNAME}=__cs3_reset_generic

#
# Include the automatically generated dependency files.
#
ifneq (${MAKECMDGOALS},clean)
-include ${wildcard ${COMPILER}/*.d} __dummy__
endif
