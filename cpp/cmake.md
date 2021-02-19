# Modern Simple CMake Tutorial

### Simple hello world
* Create a `CMakeLists.txt` file
* Simple hello world program

  ```cmake
  cmake_minimum_required(VERSION 3.10)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)

  project(hello VERSION 1.0)
  add_executable(hello main.cpp)
  ```

### Running CMake
* CMake from the command line.

  ```bash
  cmake . && make && ./hello
  ```

### Adding a header file
* Slightly more involved program with header files. To include a header file directory:

 ```cmake
  target_include_directories(hello PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
  ```

### Multiple source files
* Ok, what if we have a bunch of source files?

  * Now the CMake source explicitly [discourages this](https://cmake.org/cmake/help/latest/command/file.html#filesystem) but the "alternative" of listing every source file or using some other build system that generates your CMakeLists.txt files is perhaps even more cumbersome. So knowing all that, I'd recommend continuing to use glob until some sane alternative shows up:

  ```cmake
  file(GLOB_RECURSE SRC_FILES src/*.cpp CONFIGURE_DEPENDS)
  add_executable(hello ${SRC_FILES})
  ```

### My own lib
* Create a lib from some source files:

  * Replace `add_executable` with `add_library` 
  * E.g:

  ```cmake
  add_library(mylib STATIC lib/blah.cpp)
  ```

* Can then include it in your main executable

  ```cmake
  target_link_libraries(hello PUBLIC mylib)
  ```

### Depending on external library with find_package
* A lot simpler, things are "cmake ready".
* Has two modes: Module mode (uses FindXXX.cmake files) and Config mode(uses XXXConfig.cmake files)
* Install the library in your system: `yay -S sfml`
* Use find_package to find it:
  ```cmake
  find_package(SFML 2 REQUIRED network audio graphics window system)
  ```
* Note that required fails the build if it can't find it.
* This sets certain 'result' variables (`_INCLUDE_DIR(S)`, `_LIBRARIES`, etc) although can differ from library to library.
* then you can simply include and link it:
  ```cmake
  target_include_directories(hello PUBLIC ${SFML_INCLUDE_DIR})
  target_link_libraries(hello PUBLIC ${SFML_LIBRARIES} ${SFML_DEPENDENCIES})
  ```

### Depending on external lib manually

**If the library doesn't have a cmake file**, there are two parts to it:
1. You manually link the library and include files.
2. You figure out that library's dependencies and link those as well.

To manually link a library:

* If it's in a default system lib directory (e.g: /usr/lib), we can simply link it:
  ```cmake
  find_library(MYLIB mylib)
  target_link_libraries(hello PUBLIC ${MYLIB})
  ```
* If it's in a custom path (e.g: /tmp/customPath/mylib.so):
  ```cmake
  find_library(MYLIB mylib PATHS /tmp/customPath)
  target_link_libraries(hello PUBLIC ${MYLIB})
  ```
* Note that you still need include directories for these libraries, you can put these in variables and then link them to the target:
  ```cmake
  set(MYLIB_INCLUDE_DIRS /tmp/customPath/include)
  target_include_directories(hello PUBLIC ${MYLIB_INCLUDE_DIRS})
  ```
* To figure out the library's dependencies, refer to its documentation and then manually link/include those like above.

### Directory structure
* Now, your project might be structured across multiple folders. You can easily create a top level `CMakeLists.txt` that just includes all directories using the `add_subdirectory(subdir)` command and CMake execute those in order.
* One thing to be careful about is setting variables, a subdirectory has its own scope. And in order to make a variable accessible in a higher scope, you need to set it with `PARENT_SCOPE`.

### CPM
https://github.com/TheLartians/CPM.cmake


### Some resources

* https://cliutils.gitlab.io/modern-cmake
* https://github.com/dev-cafe/cmake-cookbook

