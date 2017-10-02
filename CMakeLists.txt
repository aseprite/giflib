cmake_minimum_required(VERSION 3.5)
project(giflib)

option(GIFLIB_UTILS "Build giflib utils" on)

if(MSVC)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif()

add_library(giflib
    dgif_lib.c
    egif_lib.c
    gif_err.c
    gif_font.c
    gif_hash.c
    gifalloc.c
    openbsd-reallocarray.c
    quantize.c)

target_include_directories(giflib
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/lib)

if(GIFLIB_UTILS)
  add_library(getarg getarg.c qprintf.c)
  target_link_libraries(getarg giflib)

  function(add_giflib_util name)
    add_executable(${name} ${name}.c)
    target_link_libraries(${name} giflib getarg)
  endfunction()

  add_giflib_util(gif2rgb)
  add_giflib_util(gifbg)
  add_giflib_util(gifbuild)
  add_giflib_util(gifclrmp)
  add_giflib_util(gifcolor)
  add_giflib_util(gifecho)
  add_giflib_util(giffilter)
  add_giflib_util(giffix)
  add_giflib_util(gifhisto)
  add_giflib_util(gifinto)
  add_giflib_util(gifsponge)
  add_giflib_util(giftext)
  if(HAVE_GETOPT_H)
    add_giflib_util(giftool)
  endif()
  add_giflib_util(gifwedge)
endif()
