# Getting Started/Tutorials

For those new to the LLVM system.

- [Getting Started with the LLVM System](https://llvm.org/docs/GettingStarted.html)

  Discusses how to get up and running quickly with the LLVM infrastructure. Everything from unpacking and compilation of the distribution to execution of some tools.

  > 安装&配环境没介绍

  [Directory Layout]: Directory_Layout.md

  ___

  

- [LLVM Tutorial: Table of Contents](https://llvm.org/docs/tutorial/index.html)

  Tutorials about using LLVM. Includes a tutorial about making a custom language with LLVM.

  ## Kaleidoscope: Implementing a Language with LLVM

  [My First Language Frontend with LLVM Tutorial](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/index.html)

  This is the “Kaleidoscope” Language tutorial, showing how to implement a simple language using LLVM components in C++.

  - [1. Kaleidoscope: Kaleidoscope Introduction and the Lexer](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl01.html)

    [Kaleidoscope Introduction and the Lexer]: Kaleidoscope1.md

  - [2. Kaleidoscope: Implementing a Parser and AST](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl02.html)

  - [3. Kaleidoscope: Code generation to LLVM IR](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl03.html)

  - [4. Kaleidoscope: Adding JIT and Optimizer Support](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl04.html)

  - [5. Kaleidoscope: Extending the Language: Control Flow](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl05.html)

  - [6. Kaleidoscope: Extending the Language: User-defined Operators](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl06.html)

  - [7. Kaleidoscope: Extending the Language: Mutable Variables](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl07.html)

  - [8. Kaleidoscope: Compiling to Object Code](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl08.html)

  - [9. Kaleidoscope: Adding Debug Information](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl09.html)

  - [10. Kaleidoscope: Conclusion and other useful LLVM tidbits](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl10.html)

  ## Building a JIT in LLVM

  - [1. Building a JIT: Starting out with KaleidoscopeJIT](https://llvm.org/docs/tutorial/BuildingAJIT1.html)
  - [2. Building a JIT: Adding Optimizations – An introduction to ORC Layers](https://llvm.org/docs/tutorial/BuildingAJIT2.html)
  - [3. Building a JIT: Per-function Lazy Compilation](https://llvm.org/docs/tutorial/BuildingAJIT3.html)
  - [4. Building a JIT: Extreme Laziness - Using LazyReexports to JIT from ASTs](https://llvm.org/docs/tutorial/BuildingAJIT4.html)

  ## External Tutorials

  - [Tutorial: Creating an LLVM Backend for the Cpu0 Architecture](http://jonathan2251.github.io/lbd/)

    A step-by-step tutorial for developing an LLVM backend. Under active development at https://github.com/Jonathan2251/lbd (please contribute!).

  - [Howto: Implementing LLVM Integrated Assembler](http://www.embecosm.com/appnotes/ean10/ean10-howto-llvmas-1.0.html)

    A simple guide for how to implement an LLVM integrated assembler for an architecture.

  ## Advanced Topics

  1. [Writing an Optimization for LLVM](https://llvm.org/pubs/2004-09-22-LCPCLLVMTutorial.html)

  ___

  

- [LLVM Programmer’s Manual](https://llvm.org/docs/ProgrammersManual.html)

  Introduction to the general layout of the LLVM sourcebase, important classes and APIs, and some tips & tricks.

  ___

  

- [Performance Tips for Frontend Authors](https://llvm.org/docs/Frontend/PerformanceTips.html)

  A collection of tips for frontend authors on how to generate IR which LLVM is able to effectively optimize.

  ___

  

- [Getting Started with the LLVM System using Microsoft Visual Studio](https://llvm.org/docs/GettingStartedVS.html)

  An addendum to the main Getting Started guide for those using Visual Studio on Windows.

  ___

  

- [Architecture & Platform Information for Compiler Writers](https://llvm.org/docs/CompilerWriterInfo.html)

  A list of helpful links for compiler writers.

  ___

  

- [MyFirstTypoFix](https://llvm.org/docs/MyFirstTypoFix.html)

  This tutorial will guide you through the process of making a change to LLVM, and contributing it back to the LLVM project.