cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(fltk_cmake_fetchcontent_template LANGUAGES CXX)

include(FetchContent)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

message(STATUS "Fetching fltk...")

FetchContent_Declare(
    fltk
    GIT_REPOSITORY https://github.com/fltk/fltk.git
    GIT_TAG release-1.4.4
)
FetchContent_MakeAvailable(fltk)

if(MSVC)
    add_compile_options(/utf-8)
endif()

set(SRCS main.cpp)

if(WIN32)
    # the WIN32 is needed for Windows in order for it to look for WinMain
    # instead of the main function.
    add_executable(main WIN32 ${SRCS})
else()
    add_executable(main ${SRCS})
endif()

target_link_libraries(main PRIVATE fltk::fltk)
