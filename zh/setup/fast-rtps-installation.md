# FastRTPS 安装

<img src="../../assets/fastrtps/eprosima_logo.png" style="float:left;" /> [eProsima Fast RTPS](http://eprosima-fast-rtps.readthedocs.io/en/latest/) 是 RTPS（实时发布订阅者）协议的 C++ 实现，它在不可靠的传输（如 UDP）上提供发布者-订阅者通信，由对象管理组（OMG）定义和维护社区。 RTPS 也是为数据分发服务（DDS）标准定义的有线互操作性协议，也是由 OMG 定义的。

PX4 使用 FastRTPS，使 RTPS 接口能够与板外组件（包括机器人和模拟器工具）共享 PX4 uORB 主题。 RTPS 是 DDS 的基本协议，是 OMG（对象管理组）提供实时发布/订阅中间件的标准，广泛应用于航空航天、国防和物联网应用。 它也被用作 ROS2 机器人工具包的中间件。 有关详细信息，请参阅：[RTPS/ROS2 接口：PX4-FastRTPS Bridge](../middleware/micrortps.md)。

<span></span>

> **Note** 本主题来源于官方的 [*eProsima Fast RTPS* 文件](http://eprosima-fast-rtps.readthedocs.io/en/latest/)。 有关详细信息，请参阅︰

* [要求](http://eprosima-fast-rtps.readthedocs.io/en/latest/requirements.html#requirements)
* [源码安装](http://eprosima-fast-rtps.readthedocs.io/en/latest/sources.html#installation-from-sources)
* [二进制安装](http://eprosima-fast-rtps.readthedocs.io/en/latest/binaries.html#installation-from-binaries)

## 标准安装

在某些平台上，RTPS 作为 PX4 开发环境的一部分安装：

* [Mac 的开发环境（FastRTPS中包括常用工具）](../setup/dev_env_mac.md)
* [Development Environment on Windows > Bash on Windows](../setup/dev_env_windows_bash_on_win.md) (FastRTPS included in install script)

下面的说明对于在其他环境中添加 FastRTPS 支持非常有用。

## 要求

*eProsima Fast RTPS* 需要以下软件包才能正常工作。

### 依赖

#### Java

Java 需要使用我们内置的代码生成工具-*fastrtpsgen*。 建议使用 [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。

### Windows 7 32位和64位

#### Visual C++ 2013 or 2015 Redistributable Package

*eProsima Fast RTPS</0 > 需要在安装或编译过程中选择的 Visual Studio 版本的 Visual C++ 可再发行包。 安装程序为您提供下载和安装它们的选项。</p> 

## 源码安装

在 Github 上下载项目：

```sh
$ git clone -b v1.8.1 https://github.com/eProsima/Fast-RTPS
$ mkdir Fast-RTPS/build && cd Fast-RTPS/build
```

> **Note** 您可能需要 [install Gradle](https://gradle.org/install/) 来构建源代码（例如，在vanilla Fedora Linux 上确实如此）。 如果是这种情况，将显示生成警告。

如果您在 Linux 上，请执行：

```sh
$ cmake -DTHIRDPARTY=ON -DBUILD_JAVA=ON ..
$ make
$ sudo make install
```

这会将 FastRTPS 安装在 `/usr/local`。 You can use `-DCMAKE_INSTALL_PREFIX=<path>` to install to a custom location. Afterwards make sure the `fastrtpsgen` application is in your `PATH`. You can check with `which fastrtpsgen`.

如果你是在 Windows，选择 *Visual Studio* 的版本：

```sh
> cmake -G "Visual Studio 14 2015 Win64" -DTHIRDPARTY=ON -DBUILD_JAVA=ON ..
> cmake --build . --target install
```

如果你想编译例程，那么请在调用 *CMake* 时，添加参数 `-DCOMPILE_EXAMPLES=ON`。

如果你想编译性能测试程序，那么请在调用 *CMake* 时，添加参数 `-DPERFORMANCE_TESTS=ON`。

## 二进制安装

你可以从 [官网](http://www.eprosima.com/) 下载最新发布的 *eProsima Fast RTPS* 的可执行文件。

操作文档请参见： [二进制安装](http://eprosima-fast-rtps.readthedocs.io/en/latest/binaries.html#installation-from-binaries)（*eProsima Fast RTPS* 官方文档）

### Windows 7 32位和64位

执行说明的 installer，收到提示后选择 *Visual Studio*版本。

#### 环境变量

*eProsima Fast RTPS* 功能配置完善，需要如下的环境变量配置生效。

* `FASTRTPSHOME`： *eProsima Fast RTPS* 根目录已安装。
* 添加到 `PATH`：所选 Visual Studio 版本的 **/bin** 文件夹和子文件夹应追加到 PATH 中。

这些变量是通过在安装过程中选中相应的框自动设置的。

### Linux

提取包的内容。 它将包含 *eProsima Fast RTPS*及其所需的软件包 *eProsima Fast CDR*。 对于这两个包，您将遵循相同的过程，从 *Fast CDR* 开始。

配置编译：

```sh
$ ./configure --libdir=/usr/lib
```

如果要使用调试符号进行编译（这也启用了verbose模式）：

```sh
$ ./configure CXXFLAGS="-g -D__DEBUG"  --libdir=/usr/lib
```

配置项目后，编译并安装库：

```sh
$ sudo make install
```