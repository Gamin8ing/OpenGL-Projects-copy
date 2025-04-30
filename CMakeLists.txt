cmake_minimum_required(VERSION 3.10)
project(SimpleGame)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find required packages
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(glm REQUIRED)
find_package(GLUT REQUIRED)

# Source files
set(SOURCES
    main.cpp
    functionalities.cpp
    LoadShaders.cpp
    SOIL/src/image_DXT.c
    SOIL/src/image_helper.c
    SOIL/src/SOIL.c
    SOIL/src/stb_image_aug.c
)

# Include directories
include_directories(
    ${OPENGL_INCLUDE_DIRS}
    ${GLEW_INCLUDE_DIRS}
    ${GLM_INCLUDE_DIRS}
    ${GLUT_INCLUDE_DIRS}
    SOIL/src
)

# Create executable
add_executable(SimpleGame ${SOURCES})

# Link libraries
target_link_libraries(SimpleGame
    ${OPENGL_LIBRARIES}
    ${GLEW_LIBRARIES}
    ${GLUT_LIBRARIES}
)

# Copy shader files to build directory
file(GLOB SHADER_FILES
    "*.vert"
    "*.frag"
    "*.vs.glsl"
    "*.fs.glsl"
)

file(GLOB TEXTURE_FILES
    "*.jpg"
    "*.png"
)

foreach(SHADER_FILE ${SHADER_FILES})
    file(COPY ${SHADER_FILE} DESTINATION ${CMAKE_BINARY_DIR})
endforeach()

foreach(TEXTURE_FILE ${TEXTURE_FILES})
    file(COPY ${TEXTURE_FILE} DESTINATION ${CMAKE_BINARY_DIR})
endforeach()
