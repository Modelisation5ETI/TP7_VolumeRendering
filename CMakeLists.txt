cmake_minimum_required(VERSION 2.6)

project( VolumeRendering )

# Configure Project
set(CMAKE_BUILD_TYPE Debug)
set( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR} )

set( SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src" )
set( DATA_DIR "${CMAKE_CURRENT_SOURCE_DIR}/data" )
set( CMAKE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/CMake" )
set( SCRIPT_DIR "${CMAKE_CURRENT_SOURCE_DIR}/scripts" )


configure_file( ${CMAKE_DIR}/Project_Config.h.in
  ${CMAKE_CURRENT_BINARY_DIR}/Project_Config.h @ONLY )

# Include directories
include_directories( ${SRC_DIR} ${CMAKE_CURRENT_BINARY_DIR} )

# Copy scripts to CMAKE_CURRENT_BINARY_DIR
file( GLOB scripts ${SCRIPT_DIR}/* )
file( COPY ${scripts} DESTINATION ${CMAKE_CURRENT_BINARY_DIR} )
# Create output directories
file( MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/output )
file( MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/output_png )
file( MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/output_anim )

# add_executable sources
file( GLOB_RECURSE
  source_files
  ${SRC_DIR}/*.[cht]pp
  )

add_executable( ${PROJECT_NAME} ${source_files} )

add_definitions( -O2 -Wall -Wextra -std=c++11 -Wno-comment -Wno-unused-parameter -Wno-unused-function -DCORRECTION )

target_link_libraries( ${PROJECT_NAME} -lm -ldl -fopenmp )


