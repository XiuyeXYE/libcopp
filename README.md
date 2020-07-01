libcopp
================

Cross-platform coroutine library in C++ .

|                   |                                       [Linux+OSX(Clang+GCC)][linux-link]                                       |                                          [Windows(VC+MinGW)][windows-link]                                           | [Coveralls][coverage-link] |
| :---------------: | :------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------: | :------------------------: |
| Build & Unit Test |                                                 ![linux-badge]                                                 |                                                   ![windows-badge]                                                   |     ![coverage-badge]      |
|     Compilers     | linux-gcc-4.7 <br /> linux-gcc-4.8 <br /> linux-gcc-10 <br /> macos-apple-clang-9.0 <br /> | MSVC 14(Visual Studio 2015) <br /> MSVC 15(Visual Studio 2017) <br />MSVC 16(Visual Studio 2019) <br /> MinGW64-gcc |                            |

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/owt5008137/libcopp)](https://github.com/owt5008137/libcopp/releases)


![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/owt5008137/libcopp)
![GitHub repo size](https://img.shields.io/github/repo-size/owt5008137/libcopp)
![GitHub forks](https://img.shields.io/github/forks/owt5008137/libcopp?style=social)
![GitHub stars](https://img.shields.io/github/stars/owt5008137/libcopp?style=social)


[linux-badge]: https://travis-ci.org/owt5008137/libcopp.svg?branch=v2 "Travis build status"
[linux-link]:  https://travis-ci.org/owt5008137/libcopp "Travis build status"
[windows-badge]: https://ci.appveyor.com/api/projects/status/7w6dfnpeahfmgaqj/branch/v2?svg=true "AppVeyor build status"
[windows-link]:  https://ci.appveyor.com/project/owt5008137/libcopp "AppVeyor build status"
[coverage-badge]: https://coveralls.io/repos/github/owt5008137/libcopp/badge.svg?branch=v2 "Coveralls coverage"
[coverage-link]:  https://coveralls.io/github/owt5008137/libcopp?branch=v2 "Coveralls coverage"

LICENSE
----------------

License under the MIT license

Document
----------------

Documents can be found at https://libcopp.atframe.work (Generated by doxygen with *[docs/libcopp.doxyfile](docs/libcopp.doxyfile)*).

INSTALL
----------------

> libcopp use cmake to generate makefile and switch build tools.

### Prerequisites

- **[required]** GCC or Clang or MSVC or clang-cl support ISO C++ 11 and upper
- **[required]** [cmake](www.cmake.org) 3.12.0 and upper
- **[optional]** [gtest](https://code.google.com/p/googletest/) 1.6.0 and upper (Better unit test supported)
- **[optional]** [Boost.Test](http://www.boost.org/doc/libs/release/libs/test/) (Boost.Test supported)

### Unix

- **[required]** ar, as, ld ([binutils](http://www.gnu.org/software/binutils/)) or [llvm](http://llvm.org/)
- **[optional]** if using [gtest](https://code.google.com/p/googletest/), pthread is required.

### Windows

- **[required]** masm (in vc)
- **[optional]** if using [gtest](https://code.google.com/p/googletest/), pthread is required.

### Install with vcpkg

**1. clone and setup vcpkg**(See more detail on https://github.com/Microsoft/vcpkg)

~~~~~~~~~~bash
git clone https://github.com/Microsoft/vcpkg.git
cd vcpkg

PS> .\bootstrap-vcpkg.bat
Linux:~/$ ./bootstrap-vcpkg.sh
~~~~~~~~~~

**2. install libcopp**

~~~~~~~~~~bash
PS> .\vcpkg install libcopp
Linux:~/$ ./vcpkg install libcopp
~~~~~~~~~~


### Custom Build

**1. clone and make a build directory**

~~~~~~~~~~bash
git clone --single-branch --depth=1 -b master https://github.com/owt5008137/libcopp.git 
mkdir libcopp/build && cd libcopp/build
~~~~~~~~~~

**2. run cmake command**

~~~~~~~~~~bash
# cmake <libcopp dir> [options...]
cmake .. -DLIBCOPP_FCONTEXT_USE_TSX=YES -DPROJECT_ENABLE_UNITTEST=YES -DPROJECT_ENABLE_SAMPLE=YES
~~~~~~~~~~

**3. make libcopp**

~~~~~~~~~~bash
cmake --build . --config RelWithDebInfo # or make [options] when using Makefile
~~~~~~~~~~

**4. run test/sample/benchmark** *[optional]*

~~~~~~~~~~bash
# Run test => Required: PROJECT_ENABLE_UNITTEST=YES
cmake --build . --config RelWithDebInfo --target run_test # or make run_test when using Makefile
# Run sample => Required: PROJECT_ENABLE_SAMPLE=YES
cmake --build . --config RelWithDebInfo --target run_sample # or make run_sample when using Makefile
# Run benchmark => Required: PROJECT_ENABLE_SAMPLE=YES
cmake --build . --config RelWithDebInfo --target benchmark # or make benchmark when using Makefile
~~~~~~~~~~

**5. install** *[optional]*

~~~~~~~~~~bash
cmake --build . --config RelWithDebInfo --target install # or make install when using Makefile
~~~~~~~~~~

> Or you can just copy include directory and libcopp.a in lib or lib64 into your project to use it.

#### CMake Options

Options can be cmake options. such as set compile toolchains, source directory or options of libcopp that control build actions. libcopp options are listed below:

| Option                                     | Description                                                                                                               |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| BUILD\_SHARED\_LIBS=YES\|NO                | [default=NO] Build dynamic library.                                                                                       |
| LIBCOPP\_ENABLE\_SEGMENTED\_STACKS=YES\|NO | [default=NO] Enable split stack supported context.(it's only availabe in linux and gcc 4.7.0 or upper)                    |
| LIBCOPP\_ENABLE\_VALGRIND=YES\|NO          | [default=YES] Enable valgrind supported context.                                                                          |
| PROJECT\_ENABLE\_UNITTEST=YES\|NO          | [default=NO] Build unit test.                                                                                             |
| PROJECT\_ENABLE\_SAMPLE=YES\|NO            | [default=NO] Build samples.                                                                                               |
| PROJECT\_DISABLE\_MT=YES\|NO               | [default=NO] Disable multi-thread support.                                                                                |
| LIBCOTASK\_ENABLE=YES\|NO                  | [default=YES] Enable build libcotask.                                                                                     |
| LIBCOPP\_FCONTEXT\_USE\_TSX=YES\|NO        | [default=YES] Enable [Intel Transactional Synchronisation Extensions (TSX)](https://software.intel.com/en-us/node/695149). |
| GTEST\_ROOT=[path]                         | set gtest library install prefix path                                                                                     |
| BOOST\_ROOT=[path]                         | set Boost.Test library install prefix path                                                                                |

USAGE
----------------

### Using with cmake

1. Add ```<WHERE TO INSTALL libcopp>/lib(64)/cmake``` to any of **CMAKE_PREFIX_PATH** 、 **CMAKE_FRAMEWORK_PATH** 、 **CMAKE_SYSTEM_PREFIX_PATH** 、 **CMAKE_SYSTEM_FRAMEWORK_PATH**
2. Just add [```find_package(Libcopp)```](https://cmake.org/cmake/help/latest/command/find_package.html) to use libcopp module.
3. 
~~~~~~~~~~cmake
find_package(Libcopp CONFIG REQUIRED)
target_include_directories(main PRIVATE ${Libcopp_INCLUDE_DIRS})
target_link_libraries(main PRIVATE ${Libcotask_LIBRARIES} ${Libcopp_LIBRARIES})
~~~~~~~~~~

See more detail on https://github.com/Microsoft/vcpkg/tree/master/ports/libcopp .

### Directly use headers and libraries

Just include headers and linking library file of your platform to use libcopp.

~~~~~~~~~~bash
LIBCOPP_PREFIX=<WHERE TO INSTALL libcopp>

# Example command for build sample with gcc 4.9 or upper on Linux
for source in sample_readme_*.cpp; do
    g++ -std=c++14 -O2 -g -ggdb -Wall -Werror -fPIC -rdynamic -fdiagnostics-color=auto -Wno-unused-local-typedefs \
        -I$LIBCOPP_PREFIX/include -L$LIBCOPP_PREFIX/lib64 -lcopp -lcotask $source -o $source.exe;
done

# Example command for build sample with clang 3.9 or upper and libc++ on Linux
for source in sample_readme_*.cpp; do
    clang++ -std=c++17 -stdlib=libc++ -O2 -g -ggdb -Wall -Werror -fPIC -rdynamic        \
        -I$LIBCOPP_PREFIX/include -L$LIBCOPP_PREFIX/lib64 -lcopp -lcotask -lc++ -lc++abi  \
        $source -o $source.exe;
done

# AppleClang on macOS just like those scripts upper.
# If you are using MinGW on Windows, it's better to add -static-libstdc++ -static-libgcc to 
#     use static linking and other scripts are just like those on Linux.

~~~~~~~~~~

~~~~~~~~~~powershell
# Example command for build sample with MSVC 1914 or upper on Windows & powershell(Debug Mode /MDd)
foreach ($source in Get-ChildItem -File -Name .\sample_readme_*.cpp) {
    cl /nologo /MP /W4 /wd"4100" /wd"4125" /EHsc /std:c++17 /Zc:__cplusplus /O2 /MDd /I$LIBCOPP_PREFIX/include $LIBCOPP_PREFIX/lib64/copp.lib $LIBCOPP_PREFIX/lib64/cotask.lib $source
}
~~~~~~~~~~

### Get Start & Example

There serveral samples to use ```copp::coroutine_context``` 、 ```copp::coroutine_context_fiber``` and ```cotask::task``` :

1. Using coroutine context
2. Using coroutine task
3. Using coroutine task manager
4. Using stack pool
5. Using ```task::then``` or ```task::await_task```
6. Using ```copp::future::future_t``` and prepare for c++20 coroutine
7. Using c++20 coroutine
8. Using c++20 coroutine with custom generator
9. Custom error (timeout for example) when polling c++20 coroutine task or generator
10. Let c++20 coroutine work with ```cotask::task```
11. Using Windows fiber and ```SetUnhandledExceptionFilter``` on Windows with ```cotask::task```

All sample codes can be found on [docs/md/EXAMPLES.md]() and [sample](sample).

NOTICE
----------------

Split stack support: if in Linux and user gcc 4.7.0 or upper, add -DLIBCOPP\_ENABLE\_SEGMENTED\_STACKS=YES to use split stack supported context.

It's recommanded to use stack pool instead of gcc splited stack.

BENCHMARK
----------------

Please see CI output for latest benchmark report. the [benchmark on Linux and macOS can be see here](https://travis-ci.org/owt5008137/libcopp) and the [benchmark on Windows can be see here](https://ci.appveyor.com/project/owt5008137/libcopp).

FAQ
----------------

Q: How to enable c++20 coroutine

> ANS: Add ```/std:c++latest /await``` for MSVC or ```-std=c++20 -fcoroutines-ts -stdlib=libc++``` for clang or ```-std=c++20 -fcoroutines``` for gcc.

Q: Will libcopp handle exception?

> ANS: When using c++11 or above, libcopp will catch all unhandled exception and rethrow it after coroutine resumed.

Q: Why ```SetUnhandledExceptionFilter``` can not catch the unhandled exception in a coroutine?

> ANS: ```SetUnhandledExceptionFilter``` only works with **Windows Fiber**, please see [sample/sample_readme_11.cpp](sample/sample_readme_11.cpp) for details.

FEEDBACK
----------------

If you has any question, please create a issue and provide the information of your environments. For example:

+ **OS**: Windows 10 Pro 19041 *(This can be see after running ```msinfo32```)* / Manjaro(Arch) Linux Linux 5.4.39-1-MANJARO
+ **Compiler**: Visual Studio 2019 C++ 16.5.5 with VS 2019 C++ v14.25 or MSVC 1925/ gcc 9.3.0
+ **CMake Commands**: ```cmake .. -G "Visual Studio 16 2019" -A x64 -DLIBCOPP_FCONTEXT_USE_TSX=ON -DPROJECT_ENABLE_UNITTEST=ON -DPROJECT_ENABLE_SAMPLE=ON-DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_INSTALL_PREFIX=%cd%/install-prefix``` / ```cmake .. -G Ninja -DLIBCOPP_FCONTEXT_USE_TSX=ON -DPROJECT_ENABLE_UNITTEST=ON -DPROJECT_ENABLE_SAMPLE=ON -DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_INSTALL_PREFIX=/opt/libcopp```
+ **Compile Commands**: ```cmake --build . -j```
+ **Related Environment Variables**: Please provide all the environment variables which will change the cmake toolchain, ```CC``` 、 ```CXX``` 、 ```AR``` and etc.


DEVELOPER
----------------

Documents can be found at https://libcopp.atframe.work (Generated by doxygen with [```docs/libcopp.doxyfile```](docs/libcopp.doxyfile)).

CONSTRIBUTORS
----------------

+ [owent](https://github.com/owt5008137)

THANKS TO
----------------

+ [mutouyun](https://github.com/mutouyun)
