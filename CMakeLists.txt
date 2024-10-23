cmake_minimum_required(VERSION 3.28)
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"  CACHE STRING "Vcpkg toolchain file")

project(SHUD)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_EXE_LINKER_FLAGS -static)
option(BUILD_SHARED_LIBS "" OFF)
if (WIN32)
#    set(CMAKE_C_COMPILER gcc)
#    set(CMAKE_CXX_COMPILER g++)
#    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
    set(VCPKG_TARGET_TRIPLET "x64-mingw-static" CACHE STRING "" FORCE)
#    add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>") # msvc 编码问题
else ()
    set(VCPKG_TARGET_TRIPLET "x64-linux" CACHE STRING "" FORCE)
endif ()

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist/bin)

find_package (OpenMP)
find_package(SUNDIALS CONFIG REQUIRED)

add_subdirectory(src)
enable_testing()
add_subdirectory(test)




