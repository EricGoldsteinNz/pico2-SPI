# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.0)
set(toolchainVersion 13_3_Rel1)
set(picotoolVersion 2.1.0)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
# Set the target build to pico2 so that its built for RP2350 instead of RP2040
set(PICO_BOARD pico2)
cmake_minimum_required(VERSION 3.13)
# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)
project(pico_serprog)

pico_sdk_init()

add_executable(pico_serprog)

pico_generate_pio_header(pico_serprog ${CMAKE_CURRENT_LIST_DIR}/pio/spi.pio)

target_sources(pico_serprog PRIVATE
        main.c
        # PIO components
        pio/pio_spi.c
        )

target_link_libraries(pico_serprog PRIVATE pico_stdlib hardware_pio)
pico_add_extra_outputs(pico_serprog)

# enable usb output, disable uart output
pico_enable_stdio_usb(pico_serprog 1)
pico_enable_stdio_uart(pico_serprog 0)
