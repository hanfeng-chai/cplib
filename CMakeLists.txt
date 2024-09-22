cmake_minimum_required(VERSION 3.10)

# Project name
project(cplib)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Generate compile_commands.json
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Adds include directories
include_directories("inc")

# Find all source files recursively
file(GLOB_RECURSE SOURCES "src/*.cpp")

foreach(SOURCE_FILE ${SOURCES})
    # Get the relative path of SOURCE_FILE from the src directory
    file(RELATIVE_PATH SOURCE_REL_PATH "${CMAKE_CURRENT_SOURCE_DIR}/src" "${SOURCE_FILE}")

    # Replace all forward slashes in the relative path with dot
    string(REPLACE "/" "." UNIQUE_NAME "${SOURCE_REL_PATH}")

    # Remove the file extension to get a valid target name
    string(REGEX REPLACE "(.main)?(.test)?.cpp" "" TARGET_NAME "${UNIQUE_NAME}")

    # Create an executable for each source file
    add_executable(${TARGET_NAME} ${SOURCE_FILE})

endforeach()
