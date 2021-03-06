看到中文readme是一件非常亲切的事情！仔细看完此文档即可完成第一个用例：

1、整体指引：
  1)使用一键式脚本编译、链接并打包压缩，如果编译失败请自行解决编译问题；
  2)如果编译成功会在bin/目录下生成可执行二进制文件"future_net"；
  3)使用如下格式调用并调试程序"./future_net /xxx/topo.csv /xxx/demand.csv /xxx/result.csv"，其中topo.csv和demand.csv是输入文件，result.csv是输出文件;
  4)调试成功后到竞赛官网提交SDK-gcc/目录下的压缩包"future_net.tar.gz"，稍后查询成绩。

2、目录结构：
SDK-gcc/
├── bin/                         可执行二进制文件目录，shell脚本在编译前删除此目录并重新创建此目录，故没有此目录不会影响脚本运行
├── build/                       构建目录，shell脚本在编译前删除此目录并重新创建此目录，故没有此目录不会影响脚本运行
├── future_net/                  代码目录
│     ├── lib/
│     │     ├── lib_io.h         读写文件的头文件
│     │     ├── lib_record.h     将输出结果记录到缓冲区的头文件
│     │     └── lib_time.h       打印时间的头文件
│     ├── CMakeLists.txt         cmake
│     ├── future_net.cpp         main函数源文件
│     ├── route.cpp              你要写代码的源文件
│     └── route.h                你要写代码的头文件
├── batch.sh                     编译、链接、打包批处理脚本
└── readme.txt                   你正在看的文件 -_-" 这不用介绍了吧

3、shell脚本说明：
  执行此脚本可以一键编译、链接、打包。如果编译和链接正确，会在bin/下生成future_net二进制文件，并按照大赛要求生成二进制文件与代码的压缩打包文件存处于SDK/下。
  注意：
    1)shell脚本会删除bin/和build/目录，以及这两个目录下的所有文件和目录。请不要在此保存你的任何文档；
    2)如果想使用shell脚本一键功能，请保持SDK-gcc/目录下所有内容的完整，请不要修改任何目录名和文件名，并保持各目录和文件的位置关系不变。

4、手工操作说明：(非必须。如果选择使用shell脚本构建，可忽略本节内容)
  1)在SDK-gcc/目录下创建build_private/目录，并在build_private/下编写makefile文件；
  2)进入build_private/，执行make完成编译和链接；
  3)将生成的二进制文件和代码目录置于同一级目录下，打包压缩生成"future_net.tar.gz"。
  注意：
  1)不要在build/下保存你的makefile文件，一旦调用batch.sh将会删除你的makefile文件；
  2)生成压缩包时，应确保将future_net二进制文件置于压缩包的最外层，即打开压缩包无需进入任何目录即可看到此二进制文件，否则可能影响判题结果；
  3)生成的二进制文件取名必须为future_net，否则会影响判题结果。

5、SDK代码说明：
  我们已经提供了保姆式的服务，你只需要做：
  1)实现route.cpp文件中的search_route接口；
  2)依次调用record_result将路径结果写入缓冲区;
  3)如果计算结果为没有路径，则不需要调用record_result接口即可直接输出NA。
  SDK已经实现了读取文件、按要求格式写文件以及打印开始和结束时间的功能。
  注意：读取文件功能是指，将图的信息文件和路径信息文件按行读取到内存，其在内存中的存储格式仍是字符串格式。因为这些信息以什么格式存储涉及到算法设计，这样做是为了不禁锢你的思路。

//sll 2016.3.27
在SDK-gcc-1.0下增加案例文件夹case,调试案例语句改为：
在SDK-gcc-1.0路径下打开Terminal，调用下列指令调试单一测试案例
./bin/future_net casemiddle/case1/topo.csv casemiddle/case1/demand.csv casemiddle/case1/result.csv
./bin/future_net casesimple/case0/topo.csv casesimple/case0/demand.csv casesimple/case0/result.csv
./bin/future_net casehard/case1/topo.csv casehard/case1/demand.csv casehard/case1/result.csv
./bin/future_net casehard/case0/topo.csv casehard/case0/demand.csv casehard/case0/result.csv