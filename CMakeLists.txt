cmake_minimum_required(VERSION 3.0)
project(sqlite.hpp)

set(CMAKE_CXX_FLAGS "-O3 -g -std=c++11 -stdlib=libc++ -Weverything -Wno-c++98-compat -Wno-c++98-compat-pedantic -Wno-missing-prototypes -Wno-padded -Wno-switch-enum -Wno-weak-vtables")

add_subdirectory(src)
add_subdirectory(test)
