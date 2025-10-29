cmake_minimum_required(VERSION 3.14.0)
project(common VERSION 1.0.0)

if(NOT TARGET devicetree)
	CPMGetPackage(devicetree.resource)
endif()

add_compile_options(-ffreestanding -nostdlib -nostartfiles -Os -m68040 -fomit-frame-pointer -Wall -Wno-unused-function -Wno-shift-count-overflow -DDEBUG)
file(GLOB_RECURSE common_sources src/*.c include/*.h)
add_library(common STATIC ${common_sources})
target_link_libraries(common PRIVATE devicetree)

target_include_directories(common PUBLIC include)
