cmake_minimum_required(VERSION 3.1)
project(cat-dev VERSION 0.0.1)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# enable warning for GNU
if ("${CMAKE_CXX_COMPLIER_ID}" STREQUAL "GNU")
	set (warnings "-Wall -Wextra -Werror")
	if (NOT CONFIGURED_ONCE)
		set (CMAKE_CXX_FLAGS "${warnings}"
			CACHE STRING "Flags used by the compiler during all build types." FORCE)
		set (CMAKE_C_FLAGS "${warnings}"
			CACHE STRING "Flags used by the compiler during all build types." FORCE)
	endif()
endif()

# Link standard c++ library staticly to the programm
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static-libstdc++")

# add the executable
add_executable(cat-dev code/main.cpp)

# add subdirectories
list (APPEND EXTRA_INCLUDES "")

include_directories(
	${PROJECT_SOURCE_DIR}
	${PROJECT_SOURCE_DIR}/engine/include
)

# configure a header file to pass some of the CMake setting to the source code
#configure_file (
#	"${PROJECT_SOURCE_DIR}/meConfig.h.in"
#	"${PROJECT_BINARY_DIR}/meConfig.h"
#)

# If you want to link SFML statically
# set(SFML_STATIC_LIBRARIES TRUE)

# In most cases better set in the CMake cache
#set(SFML_DIR "D:/C++ Projects/SFML-2.5.1/lib/cmake/SFML")

#find_package(SFML 2.5 COMPONENTS graphics audio REQUIRED)
#add_executable(cat-dev main.cpp)
#target_link_libraries(cat-dev sfml-graphics sfml-audio)