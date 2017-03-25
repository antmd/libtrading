cmake_minimum_required( VERSION 3.2 )

project(tradinglib VERSION 0.1.0)

set(LIBTRADING_BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_CURRENT_SOURCE_DIR}/cmake-scripts")
set(INCLUDE_FILES_DIR ${LIBTRADING_BASE_DIR}/include)

add_subdirectory(lib)
add_subdirectory(tools)


