# 1)
- Create a /vendors folder in an alternate location
- set the VENDORS var in the cmake file

- Install cmake

# 2) The first step is compiling glfw from source
- Download GLFW source code
- Unzip and place in /vendors folder

Linux (Ubuntu) for other distros see [Link](https://www.glfw.org/docs/latest/compile.html)
- run `sudo apt install libwayland-dev libxkbcommon-dev xorg-dev` to download dependencies
- run `cmake -S . -B build` from `/vendors/your-glfw-folder`
- run `cd build`
- run `make`

# 3) Setting up glad

Linux
- Go to https://glad.dav1d.de/
- Choose GL version 4.6, Profile: Core
- Scroll to bottom, hit generate and download glad.zip
- Unzip into /glad in your vendors folder

### ADDENDUM 
- If you get a warning about the source being from way in the future thats probably because the server that glad uses to generate the files is ahead of your time zone. When your time zone catches up those warnings will go away but you can also open glad.h and glad.c and save the files.
- That will override the time metadata to your time zone