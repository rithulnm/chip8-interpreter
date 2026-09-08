cmake_minimum_required(VERSION 3.16)
project(chip8_interpreter)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(chip8 src/main.cpp src/chip8.cpp)