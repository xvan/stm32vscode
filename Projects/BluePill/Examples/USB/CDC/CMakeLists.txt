include_directories(
    ${CMAKE_SOURCE_DIR}/Middlewares/ST/STM32_USB_Device_Library/Core/Inc
    ${CMAKE_SOURCE_DIR}/Middlewares/ST/STM32_USB_Device_Library/Class/CDC/Inc
    Inc
    )

FILE(GLOB_RECURSE HAL_SRC "${CMAKE_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/*.c")
list(FILTER HAL_SRC EXCLUDE REGEX ".*template\\.c$")
add_library(DRIVERS_HAL OBJECT ${HAL_SRC})
#target_link_libraries(DRIVERS_HAL DRIVERS)


add_library(USB_DEVICE OBJECT
    ${CMAKE_SOURCE_DIR}/Middlewares/ST/STM32_USB_Device_Library/Core/Src/usbd_core.c
    ${CMAKE_SOURCE_DIR}/Middlewares/ST/STM32_USB_Device_Library/Core/Src/usbd_ctlreq.c
    ${CMAKE_SOURCE_DIR}/Middlewares/ST/STM32_USB_Device_Library/Core/Src/usbd_ioreq.c
)

add_library(USB_CDC OBJECT ${CMAKE_SOURCE_DIR}/Middlewares/ST/STM32_USB_Device_Library/Class/CDC/Src/usbd_cdc.c )


get_filename_component(ProjectId ${CMAKE_CURRENT_LIST_DIR} NAME)
string(REPLACE " " "_" ProjectId ${ProjectId}.elf)

FILE(GLOB_RECURSE PROJECT_SRC "Src/*.c")
set(TARGET ${ProjectId})
add_executable( ${ProjectId} ${PROJECT_SRC})
target_link_libraries(${ProjectId} STARTUP DRIVERS_HAL USB_DEVICE USB_CDC)

