# Waifu2x-Vulkan-Library

Dynamic Link Library for Waifu2x implemented with NCNN and Vulkan  
Ready-to-Use：https://github.com/Aloento/YourWaifu2x/blob/master/README-Eng.md

## About

This library is part of **ArknightsAssetStudio**  

For an introduction to Waifu2x, see  
https://github.com/nagadomi/waifu2x  
For an introduction to Waifu2x_NCNN_Vulkan, see  
https://github.com/nihui/waifu2x-ncnn-vulkan

## Usage

Using this library is very easy  
Let's say our target is Windows 10

### Download

[**Released**](https://github.com/Aloento/Waifu2x-Vulkan-Library/releases/latest)  
[**OpenMP(non-essential)**](https://github.com/Aloento/Waifu2x-Vulkan-CSharp/raw/master/vcomp140.dll)  
[**Models**](https://github.com/Aloento/Waifu2x-Vulkan-CSharp/tree/master/models)

### Build from Source

#### Dependencies

* Visual Studio and **C++ Tool Chains**  
  https://visualstudio.microsoft.com/downloads/


* CMake  
  `scoop install cmake`  
  Or from Official https://cmake.org/download/


* Vulkan SDK  
  `scoop install vulkan`  
  Or from Official https://vulkan.lunarg.com/

#### Clone with all Submodules

```shell
git clone git@github.com:Aloento/Waifu2x-Vulkan-Library.git
cd Waifu2x-Vulkan-Library
git submodule update --init --recursive
```

#### Modify Code

##### Generate Normal DLL

* Comment out line 12 of `wrapper.h`, and uncomment line 11
* Delete `wrapper_wrap.cxx` from `CMakeLists.txt` on line 229
* Build with CMake

```shell
mkdir build
cd build
cmake ../src
cmake --build . -j 4
```

You will then get the file named `libWaifu2x.dll`  
It can be loaded by any Native method, such as JNA and P/Invoke

##### Generate Target Code

* No changes to the file are required
* Install swig  
  `scoop install swig`  
  Or from Official http://www.swig.org/download.html

Suppose we want to generate code for use in C# under Windows

```shell
cd src
swig -c++ -csharp wrapper_win.i
mkdir build
cd build
cmake ../
cmake --build . -j 4
```

Then, the generated `*.cs` files are ready for use by the C# project  
Don't forget to copy the `libWaifu2x.dll`

### Invoke

For details and usage examples, see  
https://github.com/Aloento/Waifu2x-Vulkan-CSharp/blob/master/README-Eng.md
