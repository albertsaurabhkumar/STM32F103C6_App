#############################################
##  Processor: S32K144
##  Author: Saurabh Kumar
##  GCC Version: 12.3
##  
##  Makefile for S32K144 Application
#############################################

#RootDirectory with the Project paths
ROOT = ./..
SRC_DIR = $(ROOT)/app/src
INC_DIR = $(ROOT)/app/inc $(ROOT)/app/common 
BIN_DIR = $(ROOT)/build/bin
OBJ_DIR = $(ROOT)/build/obj

#Compiler Directories
CC_DIR = $(ROOT)/tools/CC/gcc-10.3
CC_BIN = $(CC_DIR)/bin
CC_INC = $(CC_DIR)/include
CC_LIB = $(CC_DIR)/lib

#Compilar Path
CC = $(CC_BIN)/arm-none-eabi-gcc
OBJSIZE = $(CC_BIN)/arm-none-eabi-size
OBJDUMP = $(CC_BIN)/arm-none-eabi-objdump
OBJCOPY = $(CC_BIN)/arm-none-eabi-objcopy

#Project Name
PROJECT = S32_App

SRC = $(wildcard $(SRC_DIR)/*.c)
INC = $(wildcard $(INC_DIR)/*.h) $(ROOT)/app/common/common.h 
OBJ = $(patsubst $(SRC_DIR)/%.c,$(OBJ_DIR)/%.o,$(SRC))

#Compiler and Linker flags

CFLAGS = -c -mthumb -mcpu=cortex-m4 -Wall -std=gnu11 $(addprefix -I ,$(INC_DIR))
LDFLAGS = -T S32_App.ld -Wl,-Map=$(BIN_DIR)/S32_App.map -nostdlib -mcpu=cortex-m4 -Wall -Werror -Wshadow $(addprefix -L ,$(CC_LIB))
DEBUG_FLAGS = -g3 -ggdb
#Target name with path
TARGET = $(ROOT)/build/bin/$(PROJECT)

#Makefile rules to build the project
all: $(TARGET).elf objcopytobin objsize

$(TARGET).elf:$(OBJ)
	@echo Linking: $@
	@$(CC) $(LDFLAGS) $(DEBUG_FLAGS) $^ -o $@
$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c
	@echo Compiling: $@
	@$(CC) $(CFLAGS) $(DEBUG_FLAGS) $^ -o $@

objsize: 
	@echo Size of output file is:
	@$(OBJSIZE) $(TARGET).elf

objcopytobin:
	@echo Generating .bin file....
	@$(OBJCOPY) -O ihex $(TARGET).elf $(TARGET).hex

clean:
	@echo Removing build files
	@rm -rf $(ROOT)/build/bin/* $(OBJ)
	@echo Done...

.PHONY: all clean