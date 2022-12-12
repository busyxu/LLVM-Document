### Directory Layout

#### llvm/cmake

生成的build文件

 ```
 llvm/cmake/modules
 ```

  为 llvm 用户定义的选项构建配置。检查编译器版本和链接器标志。

  ```
  llvm/cmake/platforms
  ```

  Android NDK、iOS 系统和非 Windows 主机的工具链配置，以 MSVC 为目标。

#### llvm/examples

- 一些简单的示例展示了如何使用 LLVM 作为自定义语言的编译器——包括降低、优化和代码生成。
- Kaleidoscope Tutorial：Kaleidoscope 语言教程贯穿于为一种非平凡语言实现一个漂亮的小编译器，包括手写的词法分析器、解析器、AST，以及使用 LLVM 的代码生成支持——包括静态的（提前的）和各种即时 (JIT) 编译的方法。 [完全初学者的万花筒教程](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/index.html)。
- [BuildingAJIT： BuildingAJIT 教程](https://llvm.org/docs/tutorial/BuildingAJIT1.html)的示例，展示了 LLVM 的 ORC JIT API 如何与 LLVM 的其他部分交互。它还教导如何重新组合它们以构建适合您的用例的自定义 JIT。

#### llvm/include

从 LLVM 库导出的公共头文件。三个主要子目录：

```
llvm/include/llvm
```

所有 LLVM 特定的头文件，以及 LLVM 不同部分的子目录：`Analysis`,`CodeGen`,`Target`,`Transforms`等

```
llvm/include/llvm/Support
```

LLVM 提供的通用支持库，但不一定特定于 LLVM。例如，一些 C++ STL 实用程序和命令行选项处理库将头文件存储在此处。

```
llvm/include/llvm/Config
```

配置的头文件`cmake.`它们包装“standard”UNIX 和 C 头文件。源代码可以包含这些头文件，这些头文件会自动处理`cmake` 生成的条件`#includes`。

#### llvm/lib

大多数源文件都在这里。通过将代码放入库中，LLVM 可以轻松地在[工具](https://llvm.org/docs/GettingStarted.html#tools)之间共享代码。

```
llvm/lib/IR/
```

实现 Instruction 和 BasicBlock 等核心类的核心 LLVM 源文件。

```
llvm/lib/AsmParser/
```

LLVM 汇编语言解析器库的源代码。

```
llvm/lib/Bitcode/
```

用于读取和写入位码的代码。

```
llvm/lib/Analysis/
```

各种程序分析，如调用图、归纳变量、自然循环识别等。

```
llvm/lib/Transforms/
```

IR 到 IR 程序转换，例如积极的死代码消除、稀疏条件常数传播、内联、循环不变代码运动、死全局消除等等。

```
llvm/lib/Target/
```

描述代码生成的目标体系结构的文件。例如， `llvm/lib/Target/X86`保存 X86 机器描述。

```
llvm/lib/CodeGen/
```

代码生成器的主要部分：指令选择器、指令调度和寄存器分配。

```
llvm/lib/MC/
```

这些库在机器代码级别表示和处理代码。处理程序集和目标文件发射。

```
llvm/lib/ExecutionEngine/
```

用于在运行时在解释和 JIT 编译场景中直接执行位代码的库。

```
llvm/lib/Support/
```

`llvm/include/ADT/` 和.h中的头文件对应的源代码`llvm/include/Support/`。

#### llvm/bindings

包含 LLVM 编译器基础结构的绑定，以允许使用 C 或 C++ 以外的语言编写的程序利用 LLVM 基础结构。LLVM 项目为 Go、OCaml 和 Python 提供语言绑定。

#### llvm/projects

项目严格来说不是 LLVM 的一部分，而是随 LLVM 一起提供的。这也是创建您自己的利用 LLVM 构建系统的基于 LLVM 的项目的目录。

#### llvm/test

功能和回归测试以及对 LLVM 基础设施的其他健全性检查。这些旨在快速运行并覆盖很多领域而不是详尽无遗。

#### test-suite

用于 LLVM 的综合正确性、性能和基准测试套件。这是一个，因为它包含大量的各种许可下的第三方代码。有关详细信息，请参阅[测试指南](https://llvm.org/docs/TestingGuide.html)文档。`separate git repository <https://github.com/llvm/llvm-test-suite>`

#### llvm/tools

由上述库构建的可执行文件，它们构成了用户界面的主要部分。您始终可以通过键入来获得工具的帮助。下面简单介绍一下最重要的工具。更详细的信息在[命令指南](https://llvm.org/docs/CommandGuide/index.html)中。`tool_name -help`

```
bugpoint
```

`bugpoint`用于通过将给定的测试用例缩小到仍然会导致问题（无论是崩溃还是编译错误）的最少passes数 and/or 指令   来调试优化passes或代码生成后端。有关使用`bugpoint`的更多信息， 请参阅[HowToSubmitABug.html](https://llvm.org/docs/HowToSubmitABug.html)。

```
llvm-ar
```

存档器生成包含给定 LLVM 位码文件的存档，可选地带有索引以加快查找速度。

```
llvm-as
```

汇编程序将人类可读的 LLVM 程序集转换为 LLVM 位码。

```
llvm-dis
```

反汇编器将 LLVM 位码转换为人类可读的 LLVM 程序集。

```
llvm-link
```

`llvm-link`，毫不奇怪，将多个 LLVM 模块链接到一个程序中。

```
lli
```

`lli`是LLVM解释器，可以直接执行LLVM bitcode（虽然很慢...）.对于支持它的体系结构（目前是 x86、Sparc 和 PowerPC），默认情况下，`lli`它将充当即时编译器（如果编译了该功能），并且执行代码的速度比解释器快得多*。*

```
llc
```

`llc`是 LLVM 后端编译器，它将 LLVM 位码转换为本机代码汇编文件。

```
opt
```

opt`读取 LLVM 位码，应用一系列 LLVM 到 LLVM 转换（在命令行中指定），并输出结果位码。' ' 是获取 LLVM 中可用程序转换列表的好方法。`opt -help

 `opt`还可以对输入的 LLVM 位码文件运行特定分析并打印结果。主要用于调试分析，或熟悉分析的作用。

#### llvm/utils

用于处理 LLVM 源代码的实用程序；有些是构建过程的一部分，因为它们是部分基础设施的代码生成器。

```
codegen-diff
```


 `codegen-diff`查找 LLC 生成的代码和 LLI 生成的代码之间的差异。如果您正在调试其中一个，假设另一个生成正确的输出，这将很有用。如需完整的用户手册，请运行`perldoc codegen-diff`


```
emacs/
```

LLVM 程序集文件和 TableGen 描述文件的 Emacs 和 XEmacs 语法突出显示。`README`有关使用它们的信息，请参阅。

```
getsrcs.sh
```

查找并输出所有非生成的源文件，如果希望跨目录进行大量开发并且不想查找每个文件，则很有用。使用它的一种方法是运行，例如：xemacs utils/getsources.sh 从 LLVM 源代码树的顶部运行。

```
llvmgrep
```

对 LLVM 中的每个源文件执行`egrep -H -n`，并向其传递一个在`llvmgrep`的命令行上提供的正则表达式。这是搜索特定正则表达式的源库的有效方法。

```
TableGen/
```

包含用于从通用 TableGen 描述文件生成寄存器描述、指令集描述甚至汇编程序的工具。

```
vim/
```

LLVM 汇编文件和 TableGen 描述文件的 `vim` 语法高亮显示。有关如何使用它们的信息 ,请参阅`README`

### 使用LLVM工具链的示例

这里给出了将 LLVM 与 Clang 前端结合使用的示例。

#### clang的示例

1. 首先，创建一个简单的 C 文件，将其命名为“hello.c”：

   ```
   #include <stdio.h>
   
   int main() {
     printf("hello world\n");
     return 0;
   }
   ```

2. 接下来，将 C 文件编译成本机可执行文件：

   ```
   % clang hello.c -o hello
   ```

	> 默认情况下，Clang 就像 GCC 一样工作。标准的 -S 和 -c 参数照常工作（分别生成本机 .s 或 .o 文件）。

3. 接下来，将 C 文件编译成 LLVM 位码文件：

   ```
   % clang -O3 -emit-llvm hello.c -c -o hello.bc
   ```

   `-emit-llvm` 选项可以与 `-S` 或 `-c` 选项一起使用来，为代码分别产生 LLVM`.ll`或`.bc`文件。这允许您在 bitcode 文件上使用[标准的 LLVM 工具。](https://llvm.org/docs/CommandGuide/index.html)	

4. 以两种形式运行程序。要运行该程序，请使用：

	```
	% ./hello
	```

	和

	```
	% lli hello.bc
	```

	第二个示例展示了如何调用 LLVM JIT [lli](https://llvm.org/docs/CommandGuide/lli.html)。

5. 使用该`llvm-dis`实用程序查看 LLVM 汇编代码：

   ```
   % llvm-dis < hello.bc | less
   ```

6. 使用 LLC 代码生成器将程序编译为本机汇编：

   ```
   % llc hello.bc -o hello.s
   ```

7. 将本地汇编语言文件汇编成程序：

   ```
   % /opt/SUNWspro/bin/cc -xarch=v9 hello.s -o hello.native   # On Solaris
   
   % gcc hello.s -o hello.native                              # On others
   ```

8. 执行本机代码程序：

   ```
   % ./hello.native
   ```

   请注意，使用 clang 直接编译为本机代码（即当该 `-emit-llvm`选项不存在时）会为您直接执行步骤 6/7/8。
