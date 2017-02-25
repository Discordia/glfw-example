cmake_minimum_required(VERSION 3.6)
project(glfw_example)

set(CMAKE_CXX_STANDARD 14)

set(SOURCE_FILES main.cpp glad.c)


if(APPLE)
    # GLFW
    find_package(glfw3 REQUIRED)
    include_directories(${GLFW_INCLUDE_DIRS})

    find_package(GLEW REQUIRED)
    include_directories(${GLEW_INCLUDE_DIRS})

    # app_framework executable
    add_executable(glfw_example ${SOURCE_FILES})
    target_link_libraries(glfw_example ${GLEW_LIBRARY} glfw3)
    target_link_libraries(glfw_example "-framework Cocoa -framework OpenGL -framework IOKit -framework CoreVideo")
else()
    # GLFW
    find_package(PkgConfig REQUIRED)
    pkg_search_module(GLFW REQUIRED glfw3)
    include_directories(${GLFW_INCLUDE_DIRS})

    # GLEW
    find_path(GLEW_INCLUDE_DIR GL/glew.h)
    find_library(GLEW_LIBRARY NAMES GLEW glew32 glew glew32s PATH_SUFFIXES lib64)

    # app_framework executable
    add_executable(glfw_example ${SOURCE_FILES})
    target_link_libraries(glfw_example ${GLEW_LIBRARY} ${GLFW_STATIC_LIBRARIES})
endif()