cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 11)

# 指定生成的动态库和可执行文件所在目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

# 把src下的cpp文件全部拿出来，放到SRC_LISTS变量中
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)

# 生成动态库common
add_library(common SHARED ${SRC_LISTS})

# 因为动态库要依赖头文件，所以还要包含以下头文件目录
target_include_directories(common PUBLIC ${PROJECT_SOURCE_DIR}/include)

# 生成可执行文件planning_main
add_executable(planning_main planning_main.cpp)

# 将可执行文件与动态库链接
target_link_libraries(planning_main common)

# 生成的可执行文件也需要链接头文件所在目录
target_include_directories(planning_main PUBLIC ${PROJECT_SOURCE_DIR}/include)
