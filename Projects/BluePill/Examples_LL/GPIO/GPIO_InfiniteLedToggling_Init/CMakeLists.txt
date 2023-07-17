get_filename_component(ProjectId ${CMAKE_CURRENT_LIST_DIR} NAME)
string(REPLACE " " "_" ProjectId ${ProjectId}.elf)

FILE(GLOB_RECURSE PROJECT_SRC "Src/*.c")
set(TARGET ${ProjectId})
add_executable( ${ProjectId} ${PROJECT_SRC})
target_link_libraries(${ProjectId} STARTUP DRIVERS)
target_include_directories(${ProjectId} PRIVATE Inc)