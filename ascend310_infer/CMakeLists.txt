cmake_minimum_required(VERSION 3.14.1)
project(Ascend310Infer)
find_package(OpenCV 2 REQUIRED)
find_package(gflags REQUIRED)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2 -g  -std=c++17 -Werror -Wall -fPIE -Wl,--allow-shlib-undefined
    -D_GLIBCXX_USE_CXX11_ABI=0")
set(PROJECT_SRC_ROOT ${CMAKE_CURRENT_LIST_DIR}/)
option(MINDSPORE_PATH "mindspore install path" "")
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(${MINDSPORE_PATH})
message(STATUS "mindsporelibs:${MINDSPORE_PATH}")
include_directories(${MINDSPORE_PATH}/include)
include_directories(${PROJECT_SRC_ROOT})
find_library(MS_LIB libmindspore.so ${MINDSPORE_PATH}/lib)
file(GLOB_RECURSE MD_LIB ${MINDSPORE_PATH}/_c_dataengine*)
add_executable(main src/main.cc src/utils.cc)
target_link_libraries(main ${MS_LIB} ${MD_LIB} ${OpenCV_LIBS} gflags)
