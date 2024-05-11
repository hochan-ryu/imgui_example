# Visual Studio Code Configuration for C++ and ImGui with CMake and vcpkg

## Install Visual Studio Code Extensions
- C/C++: Provides features like IntelliSense, debugging, and code browsing.
- CMake Tools: Facilitates CMake integration, including build and debug support.

## Install vcpkg
Follow these steps to install and set up vcpkg:
1. Clone the vcpkg repository:
    ```bash
    git clone --recurse-submodules https://github.com/microsoft/vcpkg.git
    ```
2. Build and prepare the vcpkg tool:
    ```bash
    ./vcpkg/bootstrap-vcpkg.bat
    ```
3. Install necessary libraries using vcpkg:
    ```bash
    ./vcpkg/vcpkg install imgui[glfw-binding,opengl3-binding] glad glfw3 implot curl nlohmann-json
    ```
4. Check the list of installed libraries:
    ```bash
    ./vcpkg/vcpkg list
    ```
5. Integrate vcpkg with your development environment:
    ```bash
    ./vcpkg/vcpkg integrate install
    ```

## Configure Visual Studio Code Settings
Adjust settings in Visual Studio Code to use the vcpkg toolchain file:
- Navigate to the project directory and create a .vscode folder.
- Add a settings.json file with the following configurations to ensure CMake uses the vcpkg toolchain:

    **`settings.json`**
    ```json
    {
        "cmake.cmakePath": "C:\\Program Files\\CMake\\bin\\cmake.exe",
        "cmake.configureSettings": {
            "CMAKE_TOOLCHAIN_FILE": "vcpkg/scripts/buildsystems/vcpkg.cmake"
        }
    }
    ```

## Write the Program
- Add a main.cpp file to project dir/src and implement your application logic there.

## Build and Run Using CMake
To build and run the application, follow these steps:
1. Create a CMakeLists.txt file in the project directory:

    **`CMakeLists.txt`**
    ```cmake
    cmake_minimum_required(VERSION 3.10)
    project(ImGuiExample)

    # Set build type
    set(CMAKE_BUILD_TYPE Debug)

    # Find packages
    find_package(glfw3 CONFIG REQUIRED)
    find_package(glad CONFIG REQUIRED)
    find_package(imgui CONFIG REQUIRED)
    find_package(ImPlot CONFIG REQUIRED)
    find_package(CURL CONFIG REQUIRED)

    # Define executable
    add_executable(${PROJECT_NAME} src/main.cpp)

    # Link libraries
    target_link_libraries(${PROJECT_NAME} PRIVATE glfw glad::glad imgui::imgui implot::implot OpenGL32 CURL::libcurl)
    ```
2. Use the Command Palette to configure the build environment:
    - Press F1, then type and select `CMake: Confiture` to choose MSVC or another suitable compiler.
3. Build and debug the application:
    - Press CTRL + F5 to start building and debugging.
