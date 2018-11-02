cmake_minimum_required(VERSION 3.6)
project(dynlib)

cmake_policy(SET CMP0042 NEW)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake)

set(SOURCES
    dynlib.cpp
    TinyXML/tinystr.cpp
    TinyXML/tinyxml.cpp
    TinyXML/tinyxmlerror.cpp
    TinyXML/tinyxmlparser.cpp
)

find_package(IdaSdk REQUIRED)

add_ida_plugin(dynlib NOEA32 ${SOURCES})

target_include_directories(dynlib${_so64}
    PUBLIC ${IdaSdk_INCLUDE_DIRS}
    PRIVATE TinyXML
)

target_include_directories(dynlib${_so64} PUBLIC ${IdaSdk_INCLUDE_DIRS})

target_link_libraries(dynlib${_so64} ${IdaSdk_LIBRARIES})

set_target_properties(dynlib${_so64} PROPERTIES
    CXX_STANDARD 11
)
