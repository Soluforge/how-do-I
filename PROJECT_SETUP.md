## New project setup

I begin new projects with a locally hosted git repository, if it goes somewhere I'll push up to github or one of the other git service providers. 

Create a directory for the project and open Visual Studio Code

```PowerShell
PS C:\forge> mkdir helloworld
PS C:\forge> cd helloworld
PS C:\forge> code .
```

Use the git extension in Visual Studio Code to

1. Initialize the git repository
2. Create the README.md file
3. Make the inital commit to the main branch
4. Create a devel branch

The devel branch is where I do all my work. Once a release is ready it gets merged to the main branch and tagged.

I create the .gitignore file I copy the initial contents from:

[github gitignore repo](https://github.com/github/gitignore)

Because of the way I use CMAKE I add entries to .gitignore to exclude the build and install directories.

```.gitignore
# Directories
build/*
install/*

```

Create the initial CMakeLists.txt

```cmake
# Require the first version to include precompiled header support
cmake_minimum_required(VERSION 3.16)

project(projname VERSION 0.1.0
    DESCRIPTION "Project description"
    HOMEPAGE_URL "http://project.name/homepage" )
```

Create an include directory

Create a config.h.in in the include directory

```C
#ifndef __${PROJECT_NAME}_CONFIG_H__

#define PROJECT_NAME "${PROJECT_NAME}"
#define PROJECT_DESCRIPTION "${PROJECT_DESCRIPTION}"
#define PROJECT_HOMEPAGE_URL "${PROJECT_HOMEPAGE_URL}"

#define PROJECT_VERSION_MAJOR ${PROJECT_VERSION_MAJOR}
#define PROJECT_VERSION_MINOR ${PROJECT_VERSION_MINOR}
#define PROJECT_VERSION_PATCH ${PROJECT_VERSION_PATCH}

#endif //__${PROJECT_NAME}_CONFIG_H__
```

Add the the following to CMakeLists.txt

```cmake
...

configure_file(
    ${PROJECT_SOURCE_DIR}/include/config.h.in
    ${PROJECT_BINARY_DIR}/include/config.h)
```

Add a project subdirectory for the first target <target>

Create a CMakeLists.txt in that directory

```cmake
add_executable(target src/main.cpp)

target_include_directories(target PRIVATE
    ${PROJECT_SOURCE_DIR}/include
    ${PROJECT_BINARY_DIR}/include
)
```

Create src/main.cpp

```c++
#include <config.h>

#include<iostream>

int main(int, char**){
    std::cout << std::endl << PROJECT_NAME << " v" << PROJECT_VERSION << std::endl;
    STD::cout << std::endl << "Hello, World!" << std::endl;
}
```
Add this final line to the main CMakeLists.txt

```cmake
...

add_subdirectory(${PROJECT_SOURCE_DIR}/target)
```
