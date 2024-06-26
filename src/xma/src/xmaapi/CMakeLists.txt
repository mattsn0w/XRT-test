# SPDX-License-Identifier: Apache-2.0
# Copyright (C) 2019-2021 Xilinx, Inc. All rights reserved.
#
file(GLOB XMA_API_FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/*.h"
  "${CMAKE_CURRENT_SOURCE_DIR}/*.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
  )

set(XMA_API_ALL_SRC
  ${XMA_API_FILES}
  )

add_library(xma2api SHARED ${XMA_API_ALL_SRC})
target_include_directories(xma2api PRIVATE
  "${OPENCL_INCLUDEDIR}")

set_target_properties(xma2api PROPERTIES VERSION ${XMA_VERSION_STRING}
  SOVERSION ${XMA_SOVERSION})

target_link_libraries(xma2api
  PRIVATE
  m
  dl
  gcc_s
  stdc++
  ${Boost_SYSTEM_LIBRARY}
  )

install(TARGETS xma2api
  LIBRARY DESTINATION ${XMA_INSTALL_DIR}/lib ${XRT_NAMELINK_SKIP}
  RUNTIME DESTINATION ${XMA_INSTALL_DIR}/bin
)

install(TARGETS xma2api
  ARCHIVE DESTINATION ${XMA_INSTALL_DIR}/lib COMPONENT ${XRT_DEV_COMPONENT}
  LIBRARY DESTINATION ${XMA_INSTALL_DIR}/lib COMPONENT ${XRT_DEV_COMPONENT} ${XRT_NAMELINK_ONLY}
)
