cmake_minimum_required(VERSION 3.16)

project(
  example-project
  VERSION 0.0.1
  DESCRIPTION "How to write a CMakeLists.txt that works well with Yocto"
  LANGUAGES CXX C)

add_library(${PROJECT_NAME} SHARED src/hello-world.cpp src/bar.cpp) 

# Don't change global value for minimum CXX version
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17) 

### Bitbake needs the following ###

set_target_properties(${PROJECT_NAME} PROPERTIES 
  VERSION ${PROJECT_VERSION}
  SOVERSION ${PROJECT_VERSION_MAJOR})

# Destination should be inferred from type of TARGETS, still set 
# expliciticly just to be safe and saw it elsewhere
# See: https://cmake.org/cmake/help/latest/command/install.html#targets
install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
