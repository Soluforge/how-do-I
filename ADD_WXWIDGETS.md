## Adding wxWidgets to a project

The simplest way I've found to use wxWidgets, is to add it as a git submodule and use add_subdirectory in cmake, this imports all wxWidget targets into your project.

In the project directory enter the following git command

```shell
git submodule add https://github.com/wxWidgets/wxWidgets.git 3rdparty/wxWidgets

git submodule update --init --recursive
```

The second command is required to get all of wxWidgets submodules.

Add wxWidgets to you build by add the following to the project CMakeLists.txt file

```cmake
...

add_subdirectory(${PROJECT_SOURCE_DIR}/3rdparty/wxWidgets)
```
