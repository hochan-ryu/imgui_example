cmake_minimum_required(VERSION 3.10)
project(ImGuiExample)

# Set the build type
set(CMAKE_BUILD_TYPE Debug)

# Find packages
find_package(glfw3 CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(ImPlot CONFIG REQUIRED)
find_package(CURL CONFIG REQUIRED)

# Define the executable
add_executable(${PROJECT_NAME} src/main.cpp)

# Link libraries
target_link_libraries(${PROJECT_NAME} PRIVATE glfw glad::glad imgui::imgui implot::implot OpenGL32 CURL::libcurl)
