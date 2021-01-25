cmake_minimum_required(VERSION 3.12)

# Name your project
set(NAME test-pico-keypad)

# Symlink this file into the project directory
include(pico_sdk_import.cmake)

project(${NAME} C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialize the SDK
pico_sdk_init()

# Add your sources
add_executable(${NAME}
    main.cpp
)

# Include required libraries
include("../pimoroni-pico/libraries/pico_rgb_keypad/pico_rgb_keypad.cmake")

# Link required libraries
target_link_libraries(${NAME}
    pico_rgb_keypad
)

pico_add_extra_outputs(${NAME})

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${NAME}.uf2
    ${CMAKE_CURRENT_LIST_DIR}/README.md
    DESTINATION .
)

set(CPACK_INCLUDE_TOPLEVEL_DIRECTORY OFF)
set(CPACK_GENERATOR "ZIP" "TGZ")
include(CPack)