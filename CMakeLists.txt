cmake_minimum_required(VERSION 3.0.2)
project(giflib)

option(GIFLIB_UTILS "Build giflib utils" on)

if(MSVC)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif()

add_library(giflib
    lib/dgif_lib.c
    lib/egif_lib.c
    lib/gif_err.c
    lib/gif_font.c
    lib/gif_hash.c
    lib/gifalloc.c
    lib/openbsd-reallocarray.c
    lib/quantize.c)

target_include_directories(giflib
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/lib)

if(GIFLIB_UTILS)
    add_subdirectory(util)
endif()
