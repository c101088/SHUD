cmake_minimum_required(VERSION 3.26)
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"  CACHE STRING "Vcpkg toolchain file")
project(SHUD)
set(CMAKE_CXX_STANDARD 11)


if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    set(VCPKG_TARGET_TRIPLET "x64-linux" CACHE STRING "" FORCE)
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    set(VCPKG_TARGET_TRIPLET "x64-osx" CACHE STRING "" FORCE)
else()
    if (MINGW)
        set(CMAKE_EXE_LINKER_FLAGS -static)
        set(VCPKG_TARGET_TRIPLET "x64-mingw-static" CACHE STRING "" FORCE)
    else ()
        message(FATAL_ERROR "please use mingw environment in windows ")
    endif ()
endif()


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist/bin)

find_package (OpenMP)
find_package(SUNDIALS CONFIG REQUIRED)

add_subdirectory(src)
enable_testing()
add_subdirectory(test)




