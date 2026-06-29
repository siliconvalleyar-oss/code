###############################################################################

cmake_minimum_required (VERSION 3.9.5)

project(app)

# app binary output folders
set(RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_CXX_STANDARD 17)

# Add include directories
include_directories("${PROJECT_SOURCE_DIR}")

# Find SDL2
find_package(PkgConfig REQUIRED)
pkg_check_modules(SDL2 REQUIRED sdl2)

# Include all source files into the project
file(GLOB_RECURSE ${PROJECT_NAME}_SRCFILES
	"${PROJECT_SOURCE_DIR}/*.h"
	"${PROJECT_SOURCE_DIR}/*.cpp"
)
list(FILTER ${PROJECT_NAME}_SRCFILES EXCLUDE REGEX "/build/")

# Executable to be produced with required libraries
add_executable(${PROJECT_NAME} ${${PROJECT_NAME}_SRCFILES})
target_include_directories(${PROJECT_NAME} PRIVATE ${SDL2_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES})
# Requiered compiler features
target_compile_features(${PROJECT_NAME} PRIVATE cxx_range_for)
