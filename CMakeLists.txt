cmake_minimum_required(VERSION 3.6)

project(LEPCC CXX C)
string(TOLOWER ${PROJECT_NAME} PROJECT_NAME_LOWER)

set(ROOT_DIR "${PROJECT_SOURCE_DIR}")

file(GLOB BASE_SRCS
    src/*.cpp
    )
set (CMAKE_CXX_STANDARD 11)
message(INFO "files ${BASE_SRCS}")

set(LEPCC_INCLUDE_DIR "${PROJECT_SOURCE_DIR}/src/include")
message(INFO "LEPCC_INCLUDE_DIR ${LEPCC_INCLUDE_DIR}")

file(GLOB TEST_SRCS
    ${PROJECT_SOURCE_DIR}/src/Test_C_Api.cpp)
message(INFO "TEST_SRCS ${TEST_SRCS}")

list(REMOVE_ITEM BASE_SRCS ${TEST_SRCS})

message(INFO "files ${BASE_SRCS}")
add_library(lepcc STATIC "${BASE_SRCS}")

target_include_directories(lepcc PRIVATE
        ${LEPCC_INCLUDE_DIR})


add_executable(lepcctest ${TEST_SRCS})
target_include_directories(lepcctest PRIVATE
        ${LEPCC_INCLUDE_DIR})
target_link_libraries(lepcctest lepcc)
