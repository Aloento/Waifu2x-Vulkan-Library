# Waifu2x-Vulkan-Library

用NCNN和Vulkan实现的Waifu2x的**动态链接库**版本

## 关于

本库是**ArknightsAssetStudio**的一部分  
Wrapper相关代码大多由 **@zuoziqi** 编写

对Waifu2x的介绍请参阅  
https://github.com/nagadomi/waifu2x  
对Waifu2x_NCNN_Vulkan的介绍请参阅  
https://github.com/nihui/waifu2x-ncnn-vulkan

## 使用方法

使用本库非常简单  
假设我们的目标运行环境是Windows10

### 获取

[**发布的库稳定版本**](https://github.com/Aloento/Waifu2x-Vulkan-Library/releases/latest)  
[**OpenMP依赖库(非必要)**](https://github.com/Aloento/Waifu2x-Vulkan-CSharp/raw/master/vcomp140.dll)  
[**模型**](https://github.com/Aloento/Waifu2x-Vulkan-CSharp/tree/master/models)

### 自行编译

#### 安装依赖

* 安装最新的Visual Studio和 **C++工具链**  
  https://visualstudio.microsoft.com/zh-hans/downloads/


* 安装CMake  
  `scoop install cmake`  
  或者从官网获取 https://cmake.org/download/


* 获取Vulkan SDK  
  `scoop install vulkan`  
  或者从官网获取 https://vulkan.lunarg.com/

#### 拉取源码

```shell
git clone git@github.com:Aloento/Waifu2x-Vulkan-Library.git
cd Waifu2x-Vulkan-Library
git submodule update --init --recursive
```

#### 修改代码以符合需求

##### 生成传统DLL

* 注释掉 wrapper.h 中的第12行，并将第11行解除注释
* 删除 CMakeLists.txt 中第229行的 wrapper_wrap.cxx
* 进行编译

```shell
mkdir build
cd build
cmake ../src
cmake --build . -j 4
```

随后你将得到名为 libWaifu2x.dll 的文件  
它可以通过任何Native方式加载，如JNA和P/Invoke

##### 生成目标语言代码

* 不需要对文件做任何更改
* 安装swig  
  `scoop install swig`  
  或者从官网获取 http://www.swig.org/download.html

假设我们要生成给在Windows下C#使用的代码

```shell
cd src
swig -c++ -csharp wrapper_win.i
mkdir build
cd build
cmake ../
cmake --build . -j 4
```

随后，生成的*.cs文件即可给C#项目使用  
不要忘记复制生成的 libWaifu2x.dll

### 调用

具体调用和使用范例请参阅  
https://github.com/Aloento/Waifu2x-Vulkan-CSharp  
