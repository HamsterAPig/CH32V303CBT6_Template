# CH32V303CBT6_Template
使用CMake管理的CH32V303CBTx的工程模板，这样就可以使用Clion编辑这个工程代码

## 使用须知
1. 模板复制之后，需要将`cmake/gcc-risc-v32.cmake`当中的`TOOLCHAIN_PATH`修改为实际的路径
2. 新增源码文件以及头文件在根目录下的`CMakeLists.txt`的`target_link_directories`以及`target_sources`当中新增即可
3. 工程如果想改回纯C的工程启动文件需要修改，修改根目录下`CMakeLists.txt`的当中的`USE_CPP`为`OFF`即可
