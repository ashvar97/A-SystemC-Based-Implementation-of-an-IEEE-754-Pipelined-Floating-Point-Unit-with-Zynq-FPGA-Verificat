#******************************************************************************
# Copyright (c) 2020, Intel Corporation. All rights reserved.
# 
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception.
# 
# *****************************************************************************
cmake_minimum_required(VERSION 3.12)
enable_testing()
if(NOT DEFINED ENV{ICSC_HOME})
  message("ICSC_HOME is not defined!")
  return()
endif()
# Design template
project(FPU)
## SVC package contains ScTool and SystemC libraries
find_package(SVC REQUIRED)
# C++ standard must be the same as in ScTool, $(SystemC_CXX_STANDARD) contains 17
set(CMAKE_CXX_STANDARD 17)
#include_directories($ENV{ICSC_HOME}/include)
# All synthesizable source files must be listed here (not in libraries)
add_executable(FPU FPU.cpp)
# Add compilation options
# target_compile_definitions(FPU PUBLIC -DMYOPTION)
# target_compile_options(FPU PUBLIC -Wall)
# Add optional library, do not add SystemC library (it added by svc_target)
#target_link_libraries(FPU sometestbenchlibrary)
# svc_target will create @FPU_sctool executable that runs code generation 
# and @FPU that runs general SystemC simulation
# ELAB_TOP parameter accepts hierarchical name of DUT  
# (that is SystemC name, returned by sc_object::name() method)
svc_target(FPU INIT_LOCAL_VARS ELAB_TOP )
