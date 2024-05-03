#
# SPDX-FileCopyrightText: Copyright 2010-2023 Arm Limited and/or its affiliates <open-source-office@arm.com>
#
# SPDX-License-Identifier: Apache-2.0
#
# Licensed under the Apache License, Version 2.0 (the License); you may
# not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an AS IS BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

cmake_minimum_required(VERSION 3.15.6)
set(CMSIS_OPTIMIZATION_LEVEL "-Ofast" CACHE STRING "Compiler optimization level.")

project(CMSISNN)

# add_library(cmsis-nn STATIC)

# @Note: We should not use add_library() directly, as it will not work with the zephyr build system.
# Instead, we should use zephyr_library_named() to create a library that can be used with the zephyr build system.
# 
# Here's the definition of zephyr_library_named() for reference defined in ~/ncs/v2.6.0/zephyr/cmake/modules/extensions.cmake:
#       macro(zephyr_library_named name)
#            # This is a macro because we need add_library() to be executed
#            # within the scope of the caller.
#            set(ZEPHYR_CURRENT_LIBRARY ${name})
#            add_library(${name} STATIC "")
#
#            zephyr_append_cmake_library(${name})
#
#            target_link_libraries(${name} PUBLIC zephyr_interface)
#        endmacro()
zephyr_library_named(cmsis-nn)

target_compile_options(cmsis-nn PRIVATE ${CMSIS_OPTIMIZATION_LEVEL})

target_include_directories(cmsis-nn PUBLIC "Include")

add_subdirectory(Source)
