cmake_minimum_required(VERSION 3.3)
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

set(IMGUI_SOURCES
"code/imgui/imgui.cpp"
"code/imgui/imgui_demo.cpp"
"code/imgui/imgui_draw.cpp"
"code/imgui/imgui_widgets.cpp"
"code/imgui/backends/imgui_impl_dx11.cpp"
"code/imgui/backends/imgui_impl_win32.cpp"
)

#set(IMGUI_HEADERS
#"code/imgui/imconfig.h"
#"code/imgui/imgui.h"
#"code/imgui/imgui_internal.h"
##"code/imgui/stb_rect_pack.h"
##"code/imgui/stb_textedit.h"
##"code/imgui/stb_truetype.h"
#)

#add_library(ImGui ${IMGUI_SOURCES} ${IMGUI_HEADERS})

# add the executable
add_executable(cat-dev code/main.cpp ${IMGUI_SOURCES})

# add subdirectories
list (APPEND EXTRA_INCLUDES "")

include_directories(
	${PROJECT_SOURCE_DIR}
	${PROJECT_SOURCE_DIR}/code/imgui
	${PROJECT_SOURCE_DIR}/code/imgui/backends
#	${PROJECT_SOURCE_DIR}/engine/include
)

# configure a header file to pass some of the CMake setting to the source code
#configure_file (
#	"${PROJECT_SOURCE_DIR}/meConfig.h.in"
#	"${PROJECT_BINARY_DIR}/meConfig.h"
#)

# If you want to link SFML statically
set(SFML_STATIC_LIBRARIES TRUE)

# In most cases better set in the CMake cache
set(SFML_DIR "D:/C++ Projects/SFML-2.5.1/lib/cmake/SFML")

#find_package(imgui REQUIRED)
find_package(SFML 2.5 COMPONENTS graphics audio REQUIRED)
#add_executable(cat-dev main.cpp)
target_link_libraries(cat-dev sfml-graphics sfml-audio d3d11.lib d3dcompiler.lib dxgi.lib XInput.lib)
#target_link_libraries(cat-dev sfml-graphics sfml-audio imgui)