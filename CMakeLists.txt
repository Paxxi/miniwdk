cmake_minimum_required(VERSION 3.16)
project(miniwdk VERSION 10.0.18362 LANGUAGES CXX)

set(um "C:/Program Files (x86)/Windows Kits/10/Include/${PROJECT_VERSION}.0/um")
set(km "C:/Program Files (x86)/Windows Kits/10/Include/${PROJECT_VERSION}.0/km")
set(shared "C:/Program Files (x86)/Windows Kits/10/Include/${PROJECT_VERSION}.0/shared")
set(SOURCES
  ${um}/d3d10TokenizedProgramFormat.hpp
  ${um}/d3d10umddi.h
  ${um}/d3d11TokenizedProgramFormat.hpp
  ${um}/d3d12TokenizedProgramFormat.hpp
  ${um}/d3d12umddi.h
  ${shared}/d3dkmddi.h
  ${shared}/d3dkmdt.h
  ${km}/d3dkmthk.h
  ${shared}/d3dukmdt.h
  ${um}/d3dumddi.h
)
add_library(miniwdk INTERFACE
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)

install(TARGETS miniwdk EXPORT miniwdk
  INCLUDES DESTINATION include
)

install(FILES
  ${SOURCES}
  DESTINATION include
)

install(EXPORT miniwdk
  NAMESPACE
    ${PROJECT_NAME}::
  DESTINATION
    lib/cmake/${PROJECT_NAME}
)

install(FILES
  cmake/${PROJECT_NAME}-config.cmake
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
  DESTINATION
    lib/cmake/${PROJECT_NAME}
)


