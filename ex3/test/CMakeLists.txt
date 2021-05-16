cmake_minimum_required(VERSION 3.2)

include_directories(${CMAKE_SOURCE_DIR})
project(App)

add_executable(app main.cpp)
target_link_libraries(app calc)
