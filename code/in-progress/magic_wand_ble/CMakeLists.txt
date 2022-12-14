
cmake_minimum_required(VERSION 3.12)

project(magic_wand_ble C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)

add_executable(magic_wand_ble "")

target_include_directories(magic_wand_ble
  PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}/.
  )

set_target_properties(
  magic_wand_ble
  PROPERTIES
  COMPILE_FLAGS -fno-rtti
  COMPILE_FLAGS -fno-exceptions
  COMPILE_FLAGS -fno-threadsafe-statics
  COMPILE_FLAGS -nostdlib
)

target_sources(magic_wand_ble
  PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}/imu_provider.h
  ${CMAKE_CURRENT_LIST_DIR}/magic_wand_model_data.cpp
  ${CMAKE_CURRENT_LIST_DIR}/main.cpp
  ${CMAKE_CURRENT_LIST_DIR}/main_functions.cpp
  ${CMAKE_CURRENT_LIST_DIR}/main_functions.h
  ${CMAKE_CURRENT_LIST_DIR}/magic_wand_model_data.h
  ${CMAKE_CURRENT_LIST_DIR}/rasterize_stroke.cpp
  ${CMAKE_CURRENT_LIST_DIR}/rasterize_stroke.h
  ${CMAKE_CURRENT_LIST_DIR}/micro_features_data.cpp
  ${CMAKE_CURRENT_LIST_DIR}/micro_features_data.h
  )

target_link_libraries(
  magic_wand_ble
  pico-tflmicro
  hardware_pwm
  pico_stdlib
  ICM42622
  ICM20948
  LCD_st7735
)

# enable usb output, disable uart output
pico_enable_stdio_usb(magic_wand_ble 1)
pico_enable_stdio_uart(magic_wand_ble 0)

pico_add_extra_outputs(magic_wand_ble)
