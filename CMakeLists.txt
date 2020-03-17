cmake_minimum_required(VERSION 2.8)
project(dbow2_ros)

set(CMAKE_BUILD_TYPE Release)
include(ExternalProject)

# Find catkin
find_package(catkin REQUIRED)

# Set directory of the source
set(dbow2_src "${CMAKE_CURRENT_SOURCE_DIR}/DBoW2")

# Add DBoW folder
ExternalProject_Add(DBoW2 #Preserve the name of the original library
  SOURCE_DIR "${dbow2_src}"
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
  BUILD_COMMAND CXXFLAGS=-i${CATKIN_DEVEL_PREFIX}/include make
  INSTALL_COMMAND make install
)

# Catkin dependencies
catkin_package(
  INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/DBoW2/include # Use the original include folder
  LIBRARIES DBoW2
)

#install
install(
  DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/DBoW2/include # Use the original include folder
  DESTINATION ${CMAKE_INSTALL_PREFIX}
)
install(
  FILES ${CATKIN_DEVEL_PREFIX}/lib/libDBoW2${CMAKE_SHARED_LIBRARY_SUFFIX} # Use the name of the library binary
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)















# # Create directory to store the headers
# file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

# message(${CATKIN_DEVEL_PREFIX})

# # Add external project
# ExternalProject_Add(dbow2
#   SOURCE_DIR "${dbow2_src}"
#   CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
#   BUILD_COMMAND CXXFLAGS=-i${CATKIN_DEVEL_PREFIX}/include make
#   INSTALL_COMMAND make install
# )

# # Add library
# add_library(${PROJECT_NAME} SHARED src/dummy.cpp)

# # Add dependencies
# add_dependencies(${PROJECT_NAME} dbow2)
# target_link_libraries(${PROJECT_NAME} 
#   ${CATKIN_DEVEL_PREFIX}/lib/libDBoW2${CMAKE_SHARED_LIBRARY_SUFFIX})

# # Install settings
# install(DIRECTORY include
#   DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
# )
# install(DIRECTORY lib
#   DESTINATION ${CATKIN_GLOBAL_LIB_DESTINATION}
# )
# install(DIRECTORY share
#   DESTINATION ${CATKIN_GLOBAL_SHARE_DESTINATION}
# )