cmake_minimum_required(VERSION 3.5)

project(map_tnode_project)

set(CMAKE_CXX_STANDARD 20)

include_directories(${PROJECT_SOURCE_DIR}/ytsaurus)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/ytsaurus/cmake/)

add_subdirectory(ytsaurus)

find_package(Python3 3.7 EXACT COMPONENTS Interpreter)

# set(EXTERNAL_LIB_HEADERS ytsaurus)

# add_executable(map_tnode main.cpp)
add_executable(map_tnode)

# target_include_directories(
#   map_tnode PRIVATE
#   ${EXTERNAL_LIB_HEADERS}
# )

target_compile_options(map_tnode PRIVATE
  -Wdeprecated-this-capture
)

target_link_libraries(map_tnode PUBLIC
 contrib-libs-linux-headers
  contrib-libs-cxxsupp
  yutil
  cpp-malloc-tcmalloc
 libs-tcmalloc-no_percpu_cache
  library-cpp-cpuid_check 
  cpp-mapreduce-interface
 cpp-mapreduce-client
  )

target_link_options(map_tnode PRIVATE
  -ldl
  -lrt
  -Wl,--no-as-needed
  -fPIC
  -fPIC
  -lpthread
  -lrt
  -ldl
  -lutil
)

target_sources(map_tnode PRIVATE
  ${CMAKE_SOURCE_DIR}/main.cpp
)

vcs_info(map_tnode)
