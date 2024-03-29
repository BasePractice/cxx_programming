cmake_minimum_required(VERSION 3.4.1)
project(cpp_oop C CXX)

set(PROJECT_MAJOR_VERSION 1)
set(PROJECT_MINOR_VERSION 5)
set(PROJECT_BUILD 13)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/.build")
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if (MSVC)
    set(CMAKE_CXX_LINK_FLAGS "${CMAKE_CXX_LINK_FLAGS} /SUBSYSTEM:CONSOLE")
    if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
        set(CMAKE_CFLAGS "${CMAKE_CFLAGS} /MDd")
        add_compile_options(/MDd)
        #add_definitions(-DMEMORY_LEAK_DETECT)
    else ()
        add_compile_options(/MT)
    endif ()
    add_compile_options(/wd4267)
    add_compile_options(/wd4996)
elseif (CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -pedantic -Wp,-w")
    set(CMAKE_CFLAGS "${CMAKE_CFLAGS} -pedantic -Wp,-w")
elseif (CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -pedantic")
    set(CMAKE_CFLAGS "${CMAKE_CFLAGS} -pedantic")
else ()
    message(SEND_ERROR "You are using an unsupported compiler! (not MSVC or GCC)")
endif ()

include_directories(lib/3rdparty/gtest/googletest/include)
include_directories(00_cpp_cur_base)
include_directories(01_c_basic_memories)
include_directories(02_cpp_classes)
include_directories(03_cpp_ref_pointer)
include_directories(04_cpp_dyn_memory)
include_directories(05_cpp_override_operators)
include_directories(06_cpp_stl)

add_subdirectory(lib/3rdparty/gtest/googletest)
add_subdirectory(00_cpp_cur_base)
add_subdirectory(01_c_basic_memories)
add_subdirectory(02_cpp_classes)
add_subdirectory(03_cpp_ref_pointer)
add_subdirectory(04_cpp_dyn_memory)
add_subdirectory(05_cpp_override_operators)
add_subdirectory(06_cpp_stl)
add_subdirectory(tests)


file(COPY
        ${CMAKE_SOURCE_DIR}/data/c_basic_content.txt
        DESTINATION
        ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/data)