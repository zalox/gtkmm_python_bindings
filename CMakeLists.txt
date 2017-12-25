cmake_minimum_required(VERSION 3.0)

project(gtkmm_python_bindings)

set(EXTRA_MAKE_MODULES
  ${CMAKE_SOURCE_DIR}/lib/libclangmm/cmake_modules
)
set(CMAKE_MODULE_PATH
  ${CMAKE_MODULE_PATH}
  ${EXTRA_MAKE_MODULES}
)
set(CMAKE_CXX_FLAGS "\
  ${CMAKE_CXX_FLAGS} \
  -std=c++14 \
  -Wall \
  -Wextra \
")

include(FindPkgConfig)
find_package(LibClang REQUIRED)
find_package(PythonLibs 3 REQUIRED)

set(global_libraries
  ${LIBCLANG_LIBRARIES}
  ${PYTHON_LIBRARIES}
)

set(global_includes
  ${PROJECT_SOURCE_DIR}/lib/pybind11/include
  ${PROJECT_SOURCE_DIR}/lib/libclangmm/src
  ${LIBCLANG_INCLUDE_DIRS}
  ${PYTHON_INCLUDE_DIRS}
)

include_directories(${global_includes})
file(GLOB source_files "./src/*.cpp")

add_executable(${CMAKE_PROJECT_NAME}
  ${source_files}
  ./src/main.cxx
)
target_link_libraries(${CMAKE_PROJECT_NAME} ${global_libraries})
