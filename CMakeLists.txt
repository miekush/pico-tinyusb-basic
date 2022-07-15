cmake_minimum_required(VERSION 3.12)

include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

project(dev_hid_composite C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_executable(dev_hid_composite)

target_sources(dev_hid_composite PUBLIC
        ${CMAKE_CURRENT_LIST_DIR}/main.c
	${CMAKE_CURRENT_LIST_DIR}/usb_descriptors.c
        )

# Make sure TinyUSB can find tusb_config.h
target_include_directories(dev_hid_composite PUBLIC
        ${CMAKE_CURRENT_LIST_DIR})

pico_enable_stdio_usb(dev_hid_composite 1)
pico_enable_stdio_uart(dev_hid_composite 0)

pico_add_extra_outputs(dev_hid_composite)

target_link_libraries(dev_hid_composite 
    pico_stdlib
    hardware_gpio
    hardware_adc
    tinyusb_device
    tinyusb_board
)
