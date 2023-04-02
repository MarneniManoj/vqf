
project(ProjectB)
cmake_minimum_required(VERSION 3.15)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fgnu-tm -frename-registers -march=native")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=gnu11 -fgnu-tm -frename-registers -march=native")

set(OPT "-g")

if(P)
   set(OPT "-g -no-pie")
endif()

set(ARCH "-msse4.2")

if(THREAD)
   set(OPT "${OPT} -DENABLE_THREADS")
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

file(GLOB_RECURSE SOURCES "src/vqf_filter.cc")

add_library(ProjectB STATIC ${SOURCES})

target_compile_options(ProjectB PRIVATE ${OPT} ${ARCH})
target_link_libraries(ProjectB PRIVATE pthread ssl crypto m itm)