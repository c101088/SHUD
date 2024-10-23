cmake_minimum_required(VERSION 3.28)
project(SHUDTest)
add_definitions(-DTestDataPath="${CMAKE_SOURCE_DIR}/")

FIND_PACKAGE(OpenMP REQUIRED)
find_package(GTest)


aux_source_directory(. SRC_LIST)

add_executable(${PROJECT_NAME}
        ${SRC_LIST}
)
target_link_libraries(${PROJECT_NAME}
        GTest::gtest
        SUNDIALS::cvode_static
        SHUD_lib
)

add_test(${PROJECT_NAME} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${PROJECT_NAME} -maxwarnings 10000)
