# 我的第一个语言前端与LLVM教程

# 1. 万花筒：万花筒简介和词法分析器

- [万花筒语言](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl01.html#the-kaleidoscope-language)
- [词法分析器](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl01.html#the-lexer)

## [1.1. 万花筒语言](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl01.html#id1)

[本教程使用一种名为“万花筒](http://en.wikipedia.org/wiki/Kaleidoscope)”（源自“美丽、形式和视图”的意思）的玩具语言进行说明。Kaleidoscope 是一种过程语言，允许您定义函数、使用条件、数学等。在本教程的过程中，我们将扩展 Kaleidoscope 以支持 if/then/else 结构、for 循环、用户定义的运算符、JIT使用简单的命令行界面、调试信息等进行编译。

我们希望让事情保持简单，因此 Kaleidoscope 中唯一的数据类型是 64 位浮点类型（在 C 语言中也称为“double”）。因此，所有值都是隐式双精度，并且该语言不需要类型声明。这为该语言提供了非常漂亮和简单的语法。例如，以下简单示例计算 [斐波那契数：](http://en.wikipedia.org/wiki/Fibonacci_number)

```
# Compute the x'th fibonacci number.
def fib(x)
  if x < 3 then
    1
  else
    fib(x-1)+fib(x-2)

# This expression will compute the 40th number.
fib(40)
```

我们还允许 Kaleidoscope 调用标准库函数——LLVM JIT 使这变得非常容易。这意味着您可以在使用函数之前使用“extern”关键字来定义它（这对于相互递归函数也很有用）。例如：

```
extern sin(arg);
extern cos(arg);
extern atan2(arg1 arg2);

atan2(sin(.4), cos(42))
```

一个更有趣的例子包含在第 6 章中，我们在其中编写了一个小的 Kaleidoscope 应用程序，它以不同的放大级别[显示 Mandelbrot 集。](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl06.html#kicking-the-tires)

让我们深入研究这种语言的实现！

## [1.2. 词法分析器](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl01.html#id2)

在实现一种语言时，首先需要的是能够处理文本文件并识别它所说的内容。执行此操作的传统方法是使用“[词法分析器](http://en.wikipedia.org/wiki/Lexical_analysis)”（又名“扫描器”）将输入分解为“Tokens”。词法分析器返回的每个token都包含一个token代码和一些潜在的元数据（例如，数字的数值）。首先，我们定义可能性：

```
// The lexer returns tokens [0-255] if it is an unknown character, otherwise one
// of these for known things.
enum Token {
  tok_eof = -1,

  // commands
  tok_def = -2,
  tok_extern = -3,

  // primary
  tok_identifier = -4,
  tok_number = -5,
};

static std::string IdentifierStr; // Filled in if tok_identifier
static double NumVal;             // Filled in if tok_number
```

我们的词法分析器返回的每个标记要么是 Token 枚举值之一，要么是一个“未知”字符，如“+”，作为其 ASCII 值返回。如果当前标记(token)是标识符(identifier)，则 `IdentifierStr`全局变量保存标识符的名称。如果当前标记是数字文字（如 1.0），则`NumVal`保留其值。为简单起见，我们使用全局变量，但这不是真正语言实现的最佳选择:)。

> token的返回：1.在Token里面，返回相应的枚举值；2.不在Token里面，返回字符的ASCII码；1.是数字，保留在NumVal中；2，是定义的字符，保留在IdentifierStr中。

词法分析器的实际实现是一个名为 `gettok`的函数. 调用该函数以从标准输入返回下一个标记。它的定义开始于：

```
/// gettok - Return the next token from standard input.
static int gettok() {
  static int LastChar = ' ';

  // Skip any whitespace.
  while (isspace(LastChar))
    LastChar = getchar();//循环结束后，LastChar里面是最后一个字符
```

`gettok`通过调用 C`getchar()`函数从标准输入一次读取一个字符来工作。它在识别它们时吃掉它们，并将最后读取但未处理的字符存储在 LastChar 中。它必须做的第一件事是忽略标记之间的空白。这是通过上面的循环完成的。

接下来`gettok`需要做的是识别标识符和特定关键字，如“def”。Kaleidoscope 使用这个简单的循环来做到这一点：

```
//isalpha() 判断是不是一个字符
if (isalpha(LastChar)) { // identifier: [a-zA-Z][a-zA-Z0-9]*  命名规则，首字符不能是数字
  IdentifierStr = LastChar;
  while (isalnum((LastChar = getchar())))
    IdentifierStr += LastChar;

  if (IdentifierStr == "def")
    return tok_def;
  if (IdentifierStr == "extern")
    return tok_extern;
  return tok_identifier;
}
```

请注意，**此代码会在对标识符进行词法分析时将`IdentifierStr`设置为全局**。此外，由于语言关键字由同一循环匹配，因此我们在这里以内联方式处理它们。数值相似：

```
if (isdigit(LastChar) || LastChar == '.') {   // Number: [0-9.]+ 浮点数
  std::string NumStr;
  do {
    NumStr += LastChar;
    LastChar = getchar();
  } while (isdigit(LastChar) || LastChar == '.');

  NumVal = strtod(NumStr.c_str(), 0);
  return tok_number;
}
```

这些都是用于处理输入的非常简单的代码。从输入中读取数值时，我们使用 C`strtod`函数将其转换为我们存储在`NumVal`中的数值 (`NumVal`是全局变量，数字需要存储在其中)。请注意，这并没有进行足够的错误检查：它会错误地读取“1.23.45.67”并像您输入“1.23”一样处理它。随意扩展它！接下来我们处理评论：

```
if (LastChar == '#') {//# 表示那些不知道的字符，都用这块代码
  // Comment until end of line.
  do
    LastChar = getchar();
  while (LastChar != EOF && LastChar != '\n' && LastChar != '\r');

  if (LastChar != EOF)
    return gettok();
}
```

我们通过跳到行尾来处理评论，然后返回下一个标记。最后，如果输入与上述情况之一不匹配，则它要么是像“+”这样的运算符字符，要么是文件末尾。这些是用这段代码处理的：

```
  // Check for end of file.  Don't eat the EOF.
  if (LastChar == EOF)
    return tok_eof;

  // Otherwise, just return the character as its ascii value.
  int ThisChar = LastChar;
  LastChar = getchar();
  return ThisChar;
}
```

这样，我们就有了基本 Kaleidoscope 语言的完整词法分析器（词法分析器的[完整代码清单](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl02.html#full-code-listing)可在本教程的[下一章中找到）。](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl02.html)接下来我们将[构建一个简单的解析器，使用它来构建抽象语法树](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl02.html)。当我们拥有它时，我们将包含一个驱动程序，以便您可以一起使用词法分析器和解析器。

[Next: 实现解析器和 AST](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/LangImpl02.html)