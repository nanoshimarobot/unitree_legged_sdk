cmake_minimum_required(VERSION 3.5)
project(unitree_legged_sdk)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

# check arch and os
message("-- CMAKE_SYSTEM_PROCESSOR: ${CMAKE_SYSTEM_PROCESSOR}")
if("${CMAKE_SYSTEM_PROCESSOR}" MATCHES "x86_64.*")
  set(ARCH amd64)
endif()
if("${CMAKE_SYSTEM_PROCESSOR}" MATCHES "aarch64.*")
  set(ARCH arm64)
endif()

find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

ament_auto_add_library(${PROJECT_NAME} SHARED
  include/${PROJECT_NAME}/a1_const.h
  include/${PROJECT_NAME}/aliengo_const.h
  include/${PROJECT_NAME}/b1_const.h
  include/${PROJECT_NAME}/go1_const.h
  include/${PROJECT_NAME}/comm.h
  include/${PROJECT_NAME}/joystick.h
  include/${PROJECT_NAME}/loop.h
  include/${PROJECT_NAME}/quadruped.h
  include/${PROJECT_NAME}/safety.h
  include/${PROJECT_NAME}/udp.h
  include/${PROJECT_NAME}/unitree_legged_sdk.h
  dummy.cpp
)
target_link_libraries(${PROJECT_NAME} ${PROJECT_SOURCE_DIR}/lib/cpp/${ARCH}/libunitree_legged_sdk.a)

add_compile_options(-O3 -fPIC)
ament_auto_package()