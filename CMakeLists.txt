cmake_minimum_required(VERSION 2.8)

project(UP3D_TINKERING)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

#Git init/updates
macro(gitInit)
  execute_process ( COMMAND git submodule init ${CMAKE_CURRENT_SOURCE_DIR}/${argv} )
  execute_process ( COMMAND git submodule update ${CMAKE_CURRENT_SOURCE_DIR}/${argv} )
endmacro()


#option(build_maik "Build based off of maik" ON)
#option(build_kscheff "Builed based off of kscheff" OFF)
#
#if(build_maik)
#  if(build_kscheff)
#    message( FATAL_ERROR "Cannot build both." )
#  endif()

  gitInit(maik)
  add_subdirectory(maik)

#else()
#  gitInit(kscheff)
#  add_subdirectory(kscheff)
#endif()


