---
title: F# 交互窗口 (dotnet) 引用
description: 了解如何使用 F# 交互窗口 (dotnet fsi) 在控制台以交互方式运行 F# 代码，或执行 F# 脚本。
ms.date: 08/20/2020
f1_keywords:
- VS.ToolsOptionsPages.F#_Tools.F#_Interactive
ms.openlocfilehash: b1020d8ab8f2282c792fb5d00656b6d43c2c6610
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064114"
---
# <a name="interactive-programming-with-f"></a>使用 F\# 进行交互式编程

使用 F# 交互窗口 (dotnet fsi) 在控制台以交互方式运行 F# 代码，或执行 F# 脚本。 换句话说，F# Interactive 对 F# 语言执行 REPL（读取、计算、打印循环）。

若要从控制台运行 F# 交互窗口，请运行 `dotnet fsi`。 你将在任何 .NET SDK 中找到 `dotnet fsi`。

有关可用命令行选项的信息，请参阅 [F# Interactive 选项](../../language-reference/fsharp-interactive-options.md)。

若要通过 Visual Studio 运行 F# Interactive，可以单击标记为“F# Interactive”的相应工具栏按钮，或使用组合键 **Ctrl+Alt+F** 。 执行此操作将打开交互式窗口，该窗口是运行 F# Interactive 会话的工具窗口。 还可以选择一些你希望在交互式窗口中运行的代码，然后点击组合键 Alt+Enter。 F# Interactive 在标记为“F# Interactive”的工具窗口中启动。 当您使用此组合键时，请确保焦点位于编辑器窗口内。

无论您使用的是控制台还是 Visual Studio，都会出现命令提示符，并且解释器会等待您输入代码。 你可以像在代码文件中一样输入代码。 若要编译和执行代码，请输入两个分号 ( **;;** ) 以终止一行或几行输入。

F# Interactive 试图编译代码，如果成功，它将执行代码并打印其所编译类型和值的签名。 如果发生错误，解释器将打印错误消息。

在同一个会话中输入的代码可以访问之前输入的任何构造，以便你可以生成程序。 工具窗口中的大容量缓存允许你在需要时将代码复制到文件中。

当在 Visual Studio 中运行时，F# Interactive 将独立于你的项目运行，因此，你不能在 F# Interactive 中使用在项目中定义的构造，除非你将函数的代码复制到交互式窗口中。

如果打开的项目引用了某些库，可以通过“解决方案资源管理器”在 F# Interactive 中引用这些库。 若要在 F# Interactive 中引用库，请展开“引用”节点，打开库的快捷菜单，然后选择“发送至 F# Interactive”。

你可以通过调整设置控制 F# Interactive 命令行自变量（选项）。 在“工具”菜单上，选择“选项...”，然后展开“F# 工具”。 可以更改的两种设置是 F# Interactive 选项和“64 位F# Interactive”，只有在 64 位计算机上运行 F# Interactive 时，更改才有意义。 此设置确定是否需要运行 fsi.exe 或 fsianycpu.exe 的专用 64 位版本，它使用计算机体系结构确定是作为 32 位还是 64 位进程来运行。

## <a name="scripting-with-f"></a>使用 F 编写脚本\#

脚本使用 **.fsx** 或 **.fsscript** 文件扩展名。 可以不编译源代码再运行编译的程序集，仅运行 dotnet fsi 并指定 F# 源代码脚本的文件名，F# 交互窗口会实时读取并执行代码。

## <a name="differences-between-the-interactive-scripting-and-compiled-environments"></a>交互式、脚本编写和编译环境之间的差异

在 F# Interactive 中编译代码时，无论是以交互方式运行还是直接运行脚本，都会定义 **INTERACTIVE** 符号。 在编译器中编译代码时，将定义 **COMPILED** 符号。 因此，如果编译模式和交互模式下的代码不同，你可以使用预处理器指令进行条件编译以确定使用哪种模式。

当在 F# Interactive 中执行脚本时，某些指令可用，而在编译器中执行时，这些指令却不可用。 下表总结了使用 F# Interactive 时可用的指令。

|指令|描述|
|---------|-----------|
|**#help**|显示有关可用指令的信息。|
|**#I**|指定程序集搜索路径并用引号引起来。|
|**#load**|读取、编译并运行源文件。|
|**#quit**|终止 F# Interactive 会话。|
|**#r**|引用程序集。|
|**#time ["on"&#124;"off"]**|单独使用 **#time** 时，可在是否显示性能信息之间切换。 启用后，F# Interactive 将测量实际时间、CPU 时间，以及所解释并执行的代码的每个部分的垃圾回收信息。|

当在 F# Interactive 中指定文件或路径时，应指定字符串文本。 因此，文件和路径必须用引号引起来，也可以使用常见的转义符。 此外，你还可以使用 @ 字符，此时 F# Interactive 会将包含路径的字符串解释为原义字符串。 这会导致 F# Interactive 忽略转义符。

编译模式与交互模式的其中一个区别是访问命令行自变量的方法。 在编译模式下，使用 **System.Environment.GetCommandLineArgs** 。 在脚本中，使用 **fsi.CommandLineArgs** 。

下面的代码说明如何创建可读取脚本中命令行自变量的函数，并演示如何从脚本引用另一个程序集。 第一个代码文件 **MyAssembly.fs** 是所引用程序集的代码。 使用命令行 **fsc-a MyAssembly.fs** 编译此文件，然后使用命令行 **fsi --exec file1.fsx** test 以脚本执行第二个文件

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

```fsharp
// file1.fsx
#r "MyAssembly.dll"

printfn "Command line arguments: "

for arg in fsi.CommandLineArgs do
    printfn "%s" arg

printfn "%A" (MyAssembly.myFunction 10 40)
```

输出如下所示：

```console
Command line arguments:
file1.fsx
test
90
```

## <a name="package-management-in-f-interactive"></a>F# 交互窗口中的包管理

[!NOTE] 包管理可作为 `3.1.300` 和更高版本的 .NET SDK 随附的 `dotnet fsi` 版本以及所有 `5.*` 版本 .NET SDK 中的预览功能。 若要在此预览版本中启用它，请使用 `--langversion:preview` 参数运行 `dotnet fsi`。

用于在 F# 交互窗口中引用 DLL 的 `#r` 语法还可通过以下语法用于引用 nuget 包：

```fsharp
#r "nuget: <package name>"
```

例如，要引用 `FSharp.Data` 包，请使用以下 `#r` 引用：

```fsharp
#r "nuget: FSharp.Data"
```

执行此行后，最新版本的 `FSharp.Data` 包将下载到 nuget 缓存并在当前 F# 交互窗口会话中引用。

除了包名称外，还可以通过短语法引用包的特定版本：

```fsharp
#r "nuget: FSharp.Data, 3.3.2"
```

或者以更明确的方式引用：

```fsharp
#r "nuget: FSharp.Data, Version=3.3.2"
```

## <a name="related-articles"></a>相关文章

|Title|描述|
|-----|-----------|
|[F# Interactive 选项](../../language-reference/fsharp-interactive-options.md)|描述 F# Interactive (fsi.exe) 的命令行语法和选项。|
