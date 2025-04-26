# Compiler and flags
CC = gcc
CFLAGS = -Wall -Wextra -O2

# Define the project root directory based on relative paths
ROOT_DIR = ../..

# Directories relative to where the Makefile is located
OBJ_DIR = ./obj
BIN_DIR = ./bin
INJECT_SRC_DIR = ./
SO_SRC_DIR = $(ROOT_DIR)/so/src

# Source files using relative paths
INJECT_SRC_FILES = $(INJECT_SRC_DIR)/inject.c $(INJECT_SRC_DIR)/ptrace.c $(INJECT_SRC_DIR)/utils.c
SO_SRC_FILES = $(SO_SRC_DIR)/ReflectiveLoader.c

# Object files (corresponding to the source files)
INJECT_OBJ_FILES = $(patsubst $(INJECT_SRC_DIR)/%.c,$(OBJ_DIR)/%.o,$(INJECT_SRC_FILES))
SO_OBJ_FILES = $(patsubst $(SO_SRC_DIR)/%.c,$(OBJ_DIR)/%.o,$(SO_SRC_FILES))

# Final executable
TARGET = $(BIN_DIR)/injector

# Default target
all: $(TARGET)

# Rule for linking the object files into the final executable
$(TARGET): $(INJECT_OBJ_FILES) $(OBJ_DIR)/ReflectiveLoader.o
	@mkdir -p $(BIN_DIR)  # Ensure the bin directory exists
	$(CC) $(CFLAGS) $^ -o $@

# Rule for compiling inject source files into object files
$(OBJ_DIR)/%.o: $(INJECT_SRC_DIR)/%.c
	@mkdir -p $(OBJ_DIR)  # Ensure the obj directory exists
	$(CC) $(CFLAGS) -c $< -o $@

# Special rule for ReflectiveLoader.c
$(OBJ_DIR)/ReflectiveLoader.o: $(SO_SRC_DIR)/ReflectiveLoader.c
	@mkdir -p $(OBJ_DIR)  # Ensure the obj directory exists
	$(CC) $(CFLAGS) -c $< -o $@

# Clean the project (remove bin and obj directories)
clean:
	rm -rf $(OBJ_DIR) $(BIN_DIR)

.PHONY: all clean
