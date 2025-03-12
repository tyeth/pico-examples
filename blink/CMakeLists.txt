cmake_minimum_required(VERSION 3.13...3.27)
set("PICO_SDK_PATH" "/root/dev-proj/cmake/adafruit_pico-sdk")

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)

project(my_project)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

# get current folder name and log to console
get_filename_component(PROJECT_FOLDER_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)
message(STATUS "Building from: ${PROJECT_FOLDER_NAME}")


# Create target name with board type
set(TARGET_NAME "blink_${PICO_BOARD}")

add_executable(${TARGET_NAME}
    blink.c
    )

# pull in common dependencies
target_link_libraries(${TARGET_NAME} pico_stdlib)

if (PICO_CYW43_SUPPORTED)
    target_link_libraries(${TARGET_NAME} pico_cyw43_arch_none)
endif()

# create map/bin/hex file etc.
pico_add_extra_outputs(${TARGET_NAME})

# add url via pico_set_program_url
# example_auto_set_url(blink)
