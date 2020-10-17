cmake_minimum_required(VERSION 2.8.3)
project(cereal_catkin)
find_package(catkin REQUIRED)
catkin_package()
include(ExternalProject)

set(CEREAL_CPP_TAG 3e4d1b84cab4891368d2179a61a7ba06a5693e7f)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(cereal_src
  GIT_REPOSITORY  https://github.com/USCiLab/cereal
  GIT_TAG ${CEREAL_CPP_TAG}
  UPDATE_COMMAND ""
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX} -DBUILD_SHARED_LIBS=ON
)

install(DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/cereal
        DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
        FILES_MATCHING PATTERN "*.h")
install(DIRECTORY ${CATKIN_DEVEL_PREFIX}/lib/
        DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        FILES_MATCHING PATTERN "libcereal*")
