cmake_minimum_required (VERSION 3.9.5)

project(app)

set(RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_CXX_STANDARD 17)

include_directories("${PROJECT_SOURCE_DIR}/include")

find_package(PkgConfig REQUIRED)
pkg_check_modules(SDL2 REQUIRED sdl2)
pkg_check_modules(SDL2_image REQUIRED SDL2_image)

file(GLOB_RECURSE ${PROJECT_NAME}_SRCFILES
    "${PROJECT_SOURCE_DIR}/include/*.h"
    "${PROJECT_SOURCE_DIR}/src/*.cpp"
)
list(FILTER ${PROJECT_NAME}_SRCFILES EXCLUDE REGEX "/build/")

add_executable(${PROJECT_NAME} ${${PROJECT_NAME}_SRCFILES})
target_include_directories(${PROJECT_NAME} PRIVATE ${SDL2_INCLUDE_DIRS} ${SDL2_image_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES} ${SDL2_image_LIBRARIES})
target_compile_features(${PROJECT_NAME} PRIVATE cxx_range_for)
