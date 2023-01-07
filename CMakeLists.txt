cmake_minimum_required(VERSION 3.13)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake CACHE STRING "Vcpkg toolchain file")

set(RELEASE_PATH "${PROJECT_SOURCE_DIR}/release")
set(DEBUG_PATH "${PROJECT_SOURCE_DIR}/debug")
project(3DGameOpenGL)

add_subdirectory(src)

install(DIRECTORY  ${CMAKE_SOURCE_DIR}/resources DESTINATION ${RELEASE_PATH}/resources)
install(DIRECTORY  ${CMAKE_SOURCE_DIR}/resources DESTINATION ${DEBUG_PATH}/resources)

if (MSVC) 
    set_target_properties(3DSnake PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY ${DEBUG_PATH}) 
    set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT 3DSnake)
endif()