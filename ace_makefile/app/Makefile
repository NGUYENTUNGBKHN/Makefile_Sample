# This is a template makefile for building projects with nRF52840
TARGET_NAME:=sample
LINKER_NAME:=sample
BUILD_DIR:=_build
# Makefile library
MAKE_COMMON:=./../Common

# $(info MAKE_COMMON = $(MAKE_COMMON))

# This is the root project directory and the core directory
ROOT_PROJ:=./


# This is the out file rule
$(BUILD_DIR)/$(TARGET_NAME).out: \
	LINKER_SCRIPT := $(ROOT_PROJ)/$(LINKER_NAME).ld

# This is the Flags for the compiler
CPU=
FPU=
OPT=
CCFLAGS+=$(CPU) $(FPU) $(OPT)

ASMFLAG+=$(CPU) $(FPU) $(OPT)

LDFLAGS+=$(CPU) $(FPU) $(OPT)
LDFLAGS+=-T$(LINKER_SCRIPT) -mthumb -mabi=aapcs

SRC_EXCLUDE=\

SRC_INCLUDE+=$(wildcard *.c)

SRC_INCLUDE+=$(wildcard *.s)

SRC_FILES:=$(filter-out $(SRC_EXCLUDE), $(SRC_INCLUDE))

INC_FOLDERS=\

LIBS+=
# LIBS+=-lc -lm


.PHONY:	default help

default: $(TARGET_NAME)

# Include common makefile. File contains TOOLCHAIN directory and rules for building targets
-include $(MAKE_COMMON)/Makefile.common

# Call function to define targets 
$(foreach target, $(TARGET_NAME), $(call define_target, $(target)))

# Help target
help:
	@echo  help

# # # Flash target
# flash: default
# 	Jlink.exe -if swd -device nRF52840_xxAA -speed 4000 -CommanderScript CommanderScript/build_windows.jlink

# # Erase target
# erase:
# 	Jlink.exe -if swd -device nRF52840_xxAA -speed 4000 -CommanderScript CommanderScript/erase_windows.jlink
flash: default
	STM32_Programmer_CLI.exe -c port=SWD -w $(BUILD_DIR)/$(TARGET_NAME).bin 0x08000000 -v -rst

erase: default
	STM32_Programmer_CLI.exe -c port=SWD -e all

