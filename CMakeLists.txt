cmake_minimum_required(VERSION 3.10)

message(STATUS "Current Source Dir: ${CMAKE_CURRENT_SOURCE_DIR}")
set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_CURRENT_SOURCE_DIR}/cmake")

set(CMAKE_BUILD_TYPE Debug) 
# Set a default build type if none was specified
set(default_build_type "Debug")

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message(STATUS "Setting build type to '${default_build_type}' as none was specified.")
  set(CMAKE_BUILD_TYPE "${default_build_type}" CACHE
      STRING "Choose the type of build." FORCE)
  # Set the possible values of build type for cmake-gui
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release") 
endif()

message(PROJECT_SOURCE_DIR="${PROJECT_SOURCE_DIR}")

include(toolchain-arm-none-eabi)

set(LINKER_SCRIPT "${CMAKE_CURRENT_SOURCE_DIR}/GCC/STM32F103C8TX_FLASH.ld")
set(STARTUP_ASSEMBLY "${CMAKE_CURRENT_SOURCE_DIR}/GCC/startup_stm32f103c8tx.s")
include(stm32fx)

project(GPIO_InfiniteLedToggling C ASM)

#add_definitions(-Dprintf=iprintf -DDEBUG)
add_definitions(-DSTM32F103xB -DUSE_FULL_LL_DRIVER)

include_directories(
Drivers/BSP/Adafruit_Shield
Drivers/BSP/Components/ak4343
Drivers/BSP/Components/Common
Drivers/BSP/Components/cs43l22
Drivers/BSP/Components/hx8347d
Drivers/BSP/Components/ili9320
Drivers/BSP/Components/ili9325
Drivers/BSP/Components/lis302dl
Drivers/BSP/Components/spfd5408
Drivers/BSP/Components/st7735
Drivers/BSP/Components/stlm75
Drivers/BSP/Components/stmpe811
#Drivers/BSP/STM3210C_EVAL
#Drivers/BSP/STM3210E_EVAL
#Drivers/BSP/STM32F1xx_Nucleo
#Drivers/BSP/STM32VL-Discovery
#Drivers/CMSIS/Core_A/Include
Drivers/CMSIS/Core/Include
Drivers/CMSIS/Device/ST/STM32F1xx/Include
Drivers/CMSIS/DSP/Include
Drivers/CMSIS/Include
Drivers/CMSIS/NN/Include
Drivers/CMSIS/RTOS2/Include
Drivers/CMSIS/RTOS2/Template
Drivers/CMSIS/RTOS/Template
Drivers/STM32F1xx_HAL_Driver/Inc
#Drivers/STM32F1xx_HAL_Driver/Inc/Legacy
)

add_library(STARTUP OBJECT ${STARTUP_ASSEMBLY})

add_library(DRIVERS OBJECT 
	"Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_utils.c" 
	"Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_gpio.c"
)

add_subdirectory(Projects/BluePill)

#FILE(GLOB_RECURSE PROJECT_SRC "Src/*.c")
#set(TARGET ${PROJECT_NAME}.elf)
#add_executable( ${TARGET} ${PROJECT_SRC})
#target_link_libraries(${TARGET} $<TARGET_OBJECTS:STARTUP> $<TARGET_OBJECTS:DRIVERS>)

