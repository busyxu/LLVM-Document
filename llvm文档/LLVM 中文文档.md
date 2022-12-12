# The LLVM Compiler Infrastructure

> https://llvm.org/

***

## LLVM Overview

LLVM项目是模块化和可重用的编译器和工具链技术的集合。尽管它的名字叫LLVM，但LLVM与传统的虚拟机没有什么关系。“LLVM”这个名字本身并不是一个缩写词;这是项目的全称。

LLVM最初是伊利诺伊大学的一个研究项目，其目标是提供一种现代的、基于ssa的编译策略，能够同时支持任意编程语言的静态和动态编译。从那时起，LLVM已经发展成为一个由许多子项目组成的伞形项目，其中许多子项目被广泛用于各种商业和开源项目的生产中，并被广泛用于学术研究。LLVM项目中的代码在“Apache 2.0许可与LLVM例外”下获得许可。

LLVM的主要子项目有:

- LLVM core
- Clang
- LLDB
- libc++ & libc++ ABI
- compiler-rt
- MLIR
- OpenMP
- polly
- libclc
- klee
- LLD
- BOLT

除了LLVM的官方子项目之外，还有各种各样的其他项目使用LLVM的组件来完成各种任务。通过这些外部项目，你可以使用LLVM来编译Ruby、Python、Haskell、Rust、D、PHP、Pure、Lua、Julia和其他一些语言。LLVM的一个主要优点是它的多功能性、灵活性和可重用性，这就是为什么它被用于如此广泛的不同任务:从对Lua这样的嵌入式语言进行轻量级JIT编译，到为大型超级计算机编译Fortran代码。

## LLVM Features

用于C和c++的LLVM编译器系统包括以下内容:

- C, c++， Objective-C, Fortran等的前端。它们支持ansi标准的C和c++语言。此外，还支持许多GCC扩展。
- LLVM指令集的稳定实现，它同时作为在线和脱机代码表示，以及汇编(ASCII)和字节码(二进制)读取器和写入器，以及验证器。
- 一个强大的传递管理系统，它根据传递的依赖关系自动对传递(包括分析、转换和代码生成传递)进行排序，并将它们串联起来以提高效率。
- 广泛的全局标量优化。
- 一个链接时过程间优化框架，具有丰富的分析和转换集，包括复杂的全程序指针分析，调用图构造，以及对配置文件引导优化的支持。
- 一个容易重定向的代码生成器，目前支持X86, X86-64, PowerPC, PowerPC-64, ARM, Thumb, SPARC, Alpha, CellSPU, MIPS, MSP430, SystemZ, WebAssembly和XCore。
- JIT代码生成系统，目前支持X86、X86-64、ARM、AArch64、Mips、SystemZ、PowerPC和PowerPC-64。
- 支持生成DWARF调试信息。
- 类似于gprof的分析系统。
- 带有大量基准代码和应用程序的测试框架。
- api和调试工具，简化LLVM组件的快速开发。

## **Strengths of the LLVM System**

- LLVM使用具有严格语义定义的简单低级语言。
- 它包括C和c++的前端。Java、Scheme和其他语言的前端正在开发中。
- 它包括一个积极的优化器，包括标量优化、过程间优化、配置文件驱动优化和一些简单的循环优化。
- 它支持终身编译模型，包括链接时、安装时、运行时和脱机优化。
- LLVM完全支持精确的垃圾收集。
- LLVM代码生成器相对容易重定向，并使用了强大的目标描述语言。
- LLVM有大量的文档，并托管了许多不同类型的项目。
- 许多第三方用户声称LLVM易于使用和开发。例如，Stacker前端是由一个对LLVM一无所知的人在4天内编写的(现在已经删除了)。此外，LLVM还提供了一些工具来简化开发。
- LLVM正在积极发展中，并不断得到扩展、增强和改进。查看左侧栏上的状态更新以查看开发速率。
- LLVM是在osi批准的“Apache License Version 2.0”许可证下免费获得的。
- LLVM目前被许多商业、非营利或学术实体使用，他们贡献了许多扩展和新功能。

## LLVM Audience

LLVM可以用于许多不同类型的项目。你可能对LLVM感兴趣，如果你是:

- 对C和c++程序的编译时、链接时(过程间)和运行时转换感兴趣的编译器研究人员。
- 对可移植的、独立于语言的指令集和编译框架感兴趣的虚拟机研究人员/开发人员。
- 对编译器/硬件技术感兴趣的架构研究人员。
- 对静态分析或插装感兴趣的安全研究人员。
- 对编译器转换的快速原型系统感兴趣的讲师或开发人员。
- 希望从您的代码中获得更好性能的最终用户。

***

## Documentation

LLVM编译器基础设施支持广泛的项目，从工业级编译器到专门的JIT应用程序，再到小型研究项目。类似地，文档被分解为针对不同受众的几个高级分组:

### LLVM Design & Overview

Several introductory papers and presentations.

- [Introduction to the LLVM Compiler](https://llvm.org/pubs/2008-10-04-ACAT-LLVM-Intro.html)

  Presentation providing a users introduction to LLVM.

- [Intro to LLVM](http://www.aosabook.org/en/llvm.html)

  A chapter from the book “

  [The Architecture of Open Source Applications]: LLVM_intro.md

  ” that describes high-level design decisions that shaped LLVM.

- [LLVM: A Compilation Framework for Lifelong Program Analysis & Transformation](https://llvm.org/pubs/2004-01-30-CGO-LLVM.html)

  Design overview.

- [LLVM: An Infrastructure for Multi-Stage Optimization](https://llvm.org/pubs/2002-12-LattnerMSThesis.html)

  More details (quite old now).

### Documentation

Getting Started, How-tos, Developer Guides, and Tutorials.

- [Getting Started/Tutorials](https://llvm.org/docs/GettingStartedTutorials.html)

  For those new to the LLVM system.

  [Getting Started/Tutorials]: LLVM_Tutorials.md

- [User Guides](https://llvm.org/docs/UserGuides.html)

  User guides and How-tos.

- [Reference](https://llvm.org/docs/Reference.html)

  LLVM and API reference documentation.

- [Discourse Migration Guide](https://llvm.org/docs/DiscourseMigrationGuide.html)

  Guide for users to migrate to Discourse
