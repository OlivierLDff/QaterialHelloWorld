# MIT License
#
# Copyright (c) 2020 Olivier Le Doeuff
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

cmake_minimum_required(VERSION 3.14.0 FATAL_ERROR)

project(QaterialHelloWorld VERSION 1.0.0 LANGUAGES CXX)

find_package(Qt5 COMPONENTS Core Quick)
include(FetchQaterial.cmake)

set(QATERIAL_HELLOWORLD QaterialHelloWorld)

# Precompile ressources
qtquick_compiler_add_resources(QATERIAL_HELLOWORLD_QML_RES HelloWorld.qrc)

# Trick to force cmake to run each time qrc is modified
configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/HelloWorld.qrc
  ${CMAKE_CURRENT_BINARY_DIR}/HelloWorld.qrc.junk
)

# Create our app
add_executable(${QATERIAL_HELLOWORLD}
  HelloWorld.cpp
  ${QATERIAL_HELLOWORLD_QML_RES}
)

# We assume that Qaterial is available somewhere. You should have a look at 'cmake/FetchQaterial.cmake'
target_link_libraries(${QATERIAL_HELLOWORLD} PRIVATE Qaterial)

# AUTORCC is to compile the .qrc files
set_target_properties(${QATERIAL_HELLOWORLD} PROPERTIES AUTORCC TRUE)

# Support Static Qt (this will be no longer necessary with qt6)
get_target_property(QT_TARGET_TYPE Qt::Core TYPE)
if(${QT_TARGET_TYPE} STREQUAL "STATIC_LIBRARY")
  qt_generate_qml_plugin_import(${QATERIAL_HELLOWORLD} QML_SRC ${CMAKE_CURRENT_SOURCE_DIR} VERBOSE)
  qt_generate_plugin_import(${QATERIAL_HELLOWORLD} VERBOSE)
endif()
