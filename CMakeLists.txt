cmake_minimum_required(VERSION 3.0)

project(gtkmm_python_bindings)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall -Wextra")

include(FindPkgConfig)

set(global_libraries

)

set(global_includes
)

include_directories(${global_includes})
file(GLOB source_files "./src/*.cpp")

add_executable(${CMAKE_PROJECT_NAME} ${source_files} ./src/main.cxx)
target_link_libraries(${CMAKE_PROJECT_NAME} ${global_libraries})
