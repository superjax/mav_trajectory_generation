cmake_minimum_required(VERSION 2.8.3)
project(mav_trajectory_generation)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
add_definitions(-std=c++11)

find_package(yaml-cpp REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(NLopt REQUIRED)
find_package(Glog REQUIRED)

#############
# LIBRARIES #
#############
include_directories(include
  ${EIGEN3_INCLUDE_DIRS}
  ${YAML_CPP_INCLUDE_DIR}
  ${NLOPT_INCLUDE_DIRS})
add_library(${PROJECT_NAME}
  src/motion_defines.cpp
  src/polynomial.cpp
  src/segment.cpp
  src/timing.cpp
  src/trajectory.cpp
  # src/trajectory_sampling.cpp
  src/vertex.cpp
  # src/io.cpp
  src/rpoly/rpoly_ak1.cpp
)

# Link against yaml-cpp.
target_link_libraries(${PROJECT_NAME}
  ${YamlCpp_LIBRARIES}
  ${GLOG_LIBRARIES}
  glog
  ${NLOPT_LIBRARIES}
)
