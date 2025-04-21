cmake_minimum_required(VERSION 3.13)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(PICO_BOARD pico_w CACHE STRING "Board type")
include(pico_sdk_import.cmake)
project(bit_paint C CXX ASM)

pico_sdk_init()

add_executable(bit_paint bit_paint.c lib/ssd1306.c)

pico_set_program_name(bit_paint "bit_paint")
pico_set_program_version(bit_paint "0.1")

pico_generate_pio_header(bit_paint ${CMAKE_CURRENT_LIST_DIR}/lib/ws2812.pio)

target_link_libraries(bit_paint
        pico_stdlib
        hardware_i2c
        hardware_pwm
        hardware_adc
        hardware_pio)

target_include_directories(bit_paint PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}
)

pico_enable_stdio_uart(bit_paint 1)
pico_enable_stdio_usb(bit_paint 1)

pico_add_extra_outputs(bit_paint)

