# Wherever "Configure!" is marked, thats where you have to make changes
# Note: You'll have to create a /src and /include for your .c and .h files respectively
#       Don't worry, I've configured those folders below, but you still have to write your
#       .c files below and run cmake .. from your build dir each time you add a new source file.
cmake_minimum_required(VERSION 3.20)

# Configure! your exe name
set(EXE_NAME quick-start)
# Configure! this as the absolute path to your vendors folder
set(VENDORS "C:/dev/vendors")
# Configure! this if you want to build for the old intel based apple systems
# set(INTEL_APPLE 1)


# Setting up the project name
project(${EXE_NAME})

###################################
# Configure! the language standard
# Enable these for C99
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_FLAGS "-Wall")

# Enable these for C++14
# set(CMAKE_CXX_STANDARD 14)
# set(CMAKE_CXX_FLAGS "-Wall")

# Configuration for Intel based macs
if(APPLE)
    if(DEFINED INTEL_APPLE)
        set(CMAKE_OSX_ARCHITECTURES "x86_64")
    ENDIF()
ENDIF()

set(SOURCE_FILES main.c)

# Setting up cimgui variables
set(cimgui ${VENDORS}/cimgui)
set(imgui_impl ${cimgui}/imgui/backends)

# Add the executable
add_executable(${EXE_NAME} ${SOURCE_FILES})

# Add GLFW subdirectory
add_subdirectory(${VENDORS}/glfw-3.4 glfw-3.4)

# Add the include directory for headers
target_include_directories(${EXE_NAME} PUBLIC include)
target_include_directories(${EXE_NAME} PUBLIC ${VENDORS}/glad/include) # GLAD - OpenGL 4.6 Core
target_include_directories(${EXE_NAME} PUBLIC ${cimgui}) # cimgui
target_include_directories(${EXE_NAME} PUBLIC ${cimgui}/generator/output) # cimgui
target_include_directories(${EXE_NAME} PUBLIC ${cimgui}/imgui) # imgui
target_include_directories(${EXE_NAME} PUBLIC ${imgui_impl}) # imgui_impl

# Link the compile sources
target_link_libraries(${EXE_NAME} PUBLIC glfw)

# Load the GLAD source
target_sources(${EXE_NAME} PUBLIC ${VENDORS}/glad/src/glad.c) 

# Load the cimgui sources
target_sources(${EXE_NAME} PUBLIC
    ${cimgui}/cimgui.cpp
    ${cimgui}/imgui/imgui.cpp
    ${cimgui}/imgui/imgui_demo.cpp
    ${cimgui}/imgui/imgui_draw.cpp
    ${cimgui}/imgui/imgui_tables.cpp
    ${cimgui}/imgui/imgui_widgets.cpp
    ${imgui_impl}/imgui_impl_opengl3.cpp
    ${imgui_impl}/imgui_impl_glfw.cpp)

# cimgui compile definitions
add_compile_definitions(
    IMGUI_IMPL_API=extern\ \"C\"
    IMGUI_IMPL_OPENGL_LOADER_GL3W) 

# Common sources go here
# target_sources(${EXE_NAME} PUBLIC src/your_file.c
    # src/another_file.c
    # src/and_another.c)

# Configure! Set up the platform dependent sources
if(WIN32)
    # target_sources(${EXE_NAME} PUBLIC src/win32_impl.c)
elseif(APPLE)
    # target_sources(${EXE_NAME} PUBLIC src/macos_impl.c)
else() # Linux
    # target_sources(${EXE_NAME} PUBLIC src/linux_impl.c)
endif()

# Add debug mode macro
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_compile_definitions(__DEBUG__)
endif()