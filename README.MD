# gbase

A platform agnostic quick start project for graphics programming with OpenGL and GLFW

For CIMGUI support switch to the `imgui` branch

## Prerequisites

- [cmake version >= 3.20](https://cmake.org/download/)
- [glfw source code](https://www.glfw.org/download.html)
- [glad](https://glad.dav1d.de/)

## Setup
1) Create a `/vendors` folder somewhere on your disk
2) Download the `glfw` and `glad` source. For `glad` choose the OpenGL version of your liking and select `core` mode. Scroll down and click generate. Then download the `glad.zip` file.
3) Unzip both `glfw` and `glad` into your `/vendors` folder. The file structure should look something like this: (For example on WIN64)

```
C:\DEV\VENDORS
├───glad
└───glfw-3.4
```

4) Update the `EXE_NAME` variable in `CMakeLists.txt` to whatever you want to name your exe.
5) Set your `VENDORS` variable in `CMakeLists.txt` to where your vendors folder is. On Linux and Macos you can navigate to your vendors folder and type `pwd` to get the absolute path. Note that this path must be an ***ABSOLUTE PATH***. On WIN64 you can copy the path from the file explorer. Make sure that you use forward slashes in the WIN64 path.
6) Configure whether you want to use `C` or `C++` in `CMakeLists.txt`
7) If you are on MacOS, `CMakeLists.txt` is defaulted to generating a make file for the M series macs. If you want to compile for an Intel machine while on an M series architecture, you should uncomment the line: `set(INTEL_APPLE 1)`

## Build
To generate the make files or the project solution on windows navigate to the project root folder and type the following command in a terminal / command prompt (WIN64). 

```
mkdir build
cd build
cmake ..
```

On Unix based systems you can then run the `make` command to build your project and then `./your-exe-name` to run your exe.

On WIN64 you'll want to open `your-exe-name.sln` in Visual Studio. You an then build the exe by right clicking the project in the solution explorer and hitting build / rebuild.

### ADDENDUM 
If you get a warning about the source being from way in the future thats probably because the server that glad uses to generate the files is ahead of your time zone. When your time zone catches up to the time the file was generated the warnings will go away but you can also open glad.h and glad.c and save the files. That will override the time metadata to your time zone
