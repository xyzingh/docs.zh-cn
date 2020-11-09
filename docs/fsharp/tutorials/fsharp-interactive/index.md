---
title: F# 交互窗口 (dotnet) 引用
description: 了解如何使用 F# 交互窗口 (dotnet fsi) 在控制台以交互方式运行 F# 代码，或执行 F# 脚本。
ms.date: 10/31/2020
f1_keywords:
- VS.ToolsOptionsPages.F#_Tools.F#_Interactive
ms.openlocfilehash: 89570a54ecebe625a1612e4b97b01c3693e4707c
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400861"
---
# <a name="interactive-programming-with-f"></a><span data-ttu-id="8fcc1-103">使用 F\# 进行交互式编程</span><span class="sxs-lookup"><span data-stu-id="8fcc1-103">Interactive programming with F\#</span></span>

<span data-ttu-id="8fcc1-104">使用 F# 交互窗口 (dotnet fsi) 在控制台以交互方式运行 F# 代码，或执行 F# 脚本。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-104">F# Interactive (dotnet fsi) is used to run F# code interactively at the console, or to execute F# scripts.</span></span> <span data-ttu-id="8fcc1-105">换句话说，F# Interactive 对 F# 语言执行 REPL（读取、计算、打印循环）。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-105">In other words, F# interactive executes a REPL (Read, Evaluate, Print Loop) for the F# language.</span></span>

<span data-ttu-id="8fcc1-106">若要从控制台运行 F# 交互窗口，请运行 `dotnet fsi`。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-106">To run F# Interactive from the console, run `dotnet fsi`.</span></span> <span data-ttu-id="8fcc1-107">你将在任何 .NET SDK 中找到 `dotnet fsi`。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-107">You will find `dotnet fsi` in any .NET SDK.</span></span>

<span data-ttu-id="8fcc1-108">若要了解可用的命令行选项，请参阅 [F# 交互窗口选项](../../language-reference/fsharp-interactive-options.md)。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-108">For information about available command-line options, see [F# Interactive Options](../../language-reference/fsharp-interactive-options.md).</span></span>

## <a name="executing-code-directly-in-f-interactive"></a><span data-ttu-id="8fcc1-109">在 F# 交互窗口中直接执行代码</span><span class="sxs-lookup"><span data-stu-id="8fcc1-109">Executing code directly in F# Interactive</span></span>

<span data-ttu-id="8fcc1-110">由于 F# 交互窗口是 REPL（读取-求值-打印循环），因此可以在其中以交互方式执行代码。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-110">Because F# Interactive is a REPL (read-eval-print loop), you can execute code interactively in it.</span></span> <span data-ttu-id="8fcc1-111">下面的示例展示了通过命令行执行 `dotnet fsi` 后的交互会话：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-111">Here is an example of an interactive session after executing `dotnet fsi` from the command line:</span></span>

```console
Microsoft (R) F# Interactive version 11.0.0.0 for F# 5.0
Copyright (c) Microsoft Corporation. All Rights Reserved.

For help type #help;;

> let square x = x *  x;;
val square : x:int -> int

> square 12;;
val it : int = 144

> printfn "Hello, FSI!"
- ;;
Hello, FSI!
val it : unit = ()
```

<span data-ttu-id="8fcc1-112">你将会注意到两件主要的事情：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-112">You'll notice two main things:</span></span>

1. <span data-ttu-id="8fcc1-113">所有代码都必须以双分号 (`;;`) 结尾才能计算</span><span class="sxs-lookup"><span data-stu-id="8fcc1-113">All code must be terminated with a double semicolon (`;;`) to be evaluated</span></span>
2. <span data-ttu-id="8fcc1-114">代码计算并存储在 `it` 值中。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-114">Code is evaluated and stored in an `it` value.</span></span> <span data-ttu-id="8fcc1-115">可以交互方式引用 `it`。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-115">You can reference `it` interactively.</span></span>

<span data-ttu-id="8fcc1-116">F# 交互窗口还支持多行输入。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-116">F# Interactive also supports multi-line input.</span></span> <span data-ttu-id="8fcc1-117">只需要使用双分号 (`;;`) 终止提交。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-117">You just need to terminate your submission with a double semicolon (`;;`).</span></span> <span data-ttu-id="8fcc1-118">假设以下代码片段已粘贴到 F# 交互窗口中并由其计算：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-118">Consider the following snippet that has been pasted into and evaluated by F# Interactive:</span></span>

```console
> let getOddSquares xs =
-     xs
-     |> List.filter (fun x -> x % 2 <> 0)
-     |> List.map (fun x -> x * x)
-
- printfn "%A" (getOddSquares [1..10]);;
[1; 9; 25; 49; 81]
val getOddSquares : xs:int list -> int list
val it : unit = ()

>
```

<span data-ttu-id="8fcc1-119">代码的格式被保留，并有终止输入的双分号 (`;;`)。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-119">The code's formatting is preserved, and there is a double semicolon (`;;`) terminating the input.</span></span> <span data-ttu-id="8fcc1-120">然后，F# 交互窗口计算了代码，并打印出了结果！</span><span class="sxs-lookup"><span data-stu-id="8fcc1-120">F# Interactive then evaluated the code and printed the results!</span></span>

## <a name="scripting-with-f"></a><span data-ttu-id="8fcc1-121">使用 F 编写脚本\#</span><span class="sxs-lookup"><span data-stu-id="8fcc1-121">Scripting with F\#</span></span>

<span data-ttu-id="8fcc1-122">在 F# 交互窗口中以交互方式计算代码，它可以是一种很好的学习工具，但你很快就会发现，它不如在普通编辑器中编写代码那么高效。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-122">Evaluating code interactively in F# Interactive can be a great learning tool, but you'll quickly find that it's not as productive as writing code in a normal editor.</span></span> <span data-ttu-id="8fcc1-123">为了支持普通的代码编辑，可以编写 F# 脚本。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-123">To support normal code editing, you can write F# scripts.</span></span>

<span data-ttu-id="8fcc1-124">脚本使用文件扩展名 .fsx。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-124">Scripts use the file extension **.fsx**.</span></span> <span data-ttu-id="8fcc1-125">可以不编译源代码再运行编译的程序集，仅运行 dotnet fsi 并指定 F# 源代码脚本的文件名，F# 交互窗口会实时读取并执行代码。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-125">Instead of compiling source code and then later running the compiled assembly, you can just run **dotnet fsi** and specify the filename of the script of F# source code, and F# interactive reads the code and executes it in real time.</span></span> <span data-ttu-id="8fcc1-126">例如，假设以下脚本名为 `Script.fsx`：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-126">For example, consider the following script called `Script.fsx`:</span></span>

```fsharp
let getOddSquares xs =
    xs
    |> List.filter (fun x -> x % 2 <> 0)
    |> List.map (fun x -> x * x)

getOddSquares [1..10]
```

<span data-ttu-id="8fcc1-127">在计算机中创建此文件后，可以使用 `dotnet fsi` 运行它，然后直接在终端窗口中查看输出：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-127">When this file is created in your machine, you can run it with `dotnet fsi` and see the output directly in your terminal window:</span></span>

```console
dotnet fsi Script.fsx
[1; 9; 25; 49; 81]
```

<span data-ttu-id="8fcc1-128">F# 脚本在 [Visual Studio](../../get-started/get-started-visual-studio.md)、[Visual Studio Code](../../get-started/get-started-vscode.md) 和 [Visual Studio for Mac](../../get-started/get-started-with-visual-studio-for-mac.md) 中都是原生支持的。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-128">F# scripting is natively supported in [Visual Studio](../../get-started/get-started-visual-studio.md), [Visual Studio Code](../../get-started/get-started-vscode.md), and [Visual Studio for Mac](../../get-started/get-started-with-visual-studio-for-mac.md).</span></span>

## <a name="referencing-packages-in-f-interactive"></a><span data-ttu-id="8fcc1-129">在 F# 交互窗口中引用包</span><span class="sxs-lookup"><span data-stu-id="8fcc1-129">Referencing packages in F# Interactive</span></span>

> [!NOTE]
> <span data-ttu-id="8fcc1-130">包管理是 F# 5 功能，目前可以使用最新的 .NET 5 SDK 来使用它。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-130">Package management is an F# 5 feature and is currently available using the latest .NET 5 SDK.</span></span>

<span data-ttu-id="8fcc1-131">F# 交互窗口支持使用 `#r "nuget:"` 语法和可选版本来引用 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-131">F# Interactive supports referencing NuGet packages with the `#r "nuget:"` syntax and an optional version:</span></span>

```fsharp
#r "nuget: Newtonsoft.Json"
open Newtonsoft.Json

let data = {| Name = "Don Syme"; Occupation = "F# Creator" |}
JsonConvert.SerializeObject(data)
```

<span data-ttu-id="8fcc1-132">如果未指定版本，则采用最高可用版本的非预览包。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-132">If a version is not specified, the highest available non-preview package is taken.</span></span> <span data-ttu-id="8fcc1-133">若要引用特定版本，请通过逗号引入版本。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-133">To reference a specific version, introduce the version via a comma.</span></span> <span data-ttu-id="8fcc1-134">这在引用包的预览版本时非常方便。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-134">This can be handy when referencing a preview version of a package.</span></span> <span data-ttu-id="8fcc1-135">例如，假设下面的脚本使用 [DiffSharp](https://diffsharp.github.io/) 的预览版本：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-135">For example, consider this script using a preview version of [DiffSharp](https://diffsharp.github.io/):</span></span>

```fsharp
#r "nuget: DiffSharp-lite,1.0.0-preview-328097867"
open DiffSharp

// A 1D tensor
let t1 = dsharp.tensor [ 0.0 .. 0.2 .. 1.0 ]

// A 2x2 tensor
let t2 = dsharp.tensor [ [ 0; 1 ]; [ 2; 2 ] ]

// Define a scalar-to-scalar function
let f (x: Tensor) = sin (sqrt x)

printfn "%A" (f (dsharp.tensor 1.2))
```

<span data-ttu-id="8fcc1-136">你可以根据需要在脚本中指定任意数量的包引用。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-136">You can specify as many package references as you like in a script.</span></span>

## <a name="referencing-assemblies-on-disk-with-f-interactive"></a><span data-ttu-id="8fcc1-137">使用 F# 交互窗口引用磁盘上的程序集</span><span class="sxs-lookup"><span data-stu-id="8fcc1-137">Referencing assemblies on disk with F# interactive</span></span>

<span data-ttu-id="8fcc1-138">另外，如果磁盘上有程序集，并且你希望在脚本中引用此程序集，则可以使用 `#r` 语法指定程序集。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-138">Alternatively, if you have an assembly on disk and wish to reference that in a script, you can use the `#r` syntax to specify an assembly.</span></span> <span data-ttu-id="8fcc1-139">假设项目中的以下代码编译成 `MyAssembly.dll`：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-139">Consider the following code in a project compiled into `MyAssembly.dll`:</span></span>

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

<span data-ttu-id="8fcc1-140">编译后，就可以在名为 `Script.fsx` 的文件中引用它了，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-140">One compiled, you can reference it in a file called `Script.fsx` like so:</span></span>

```fsharp
#r "path/to/MyAssembly.dll"

printfn "%A" (MyAssembly.myFunction 10 40)
```

<span data-ttu-id="8fcc1-141">输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-141">The output is as follows:</span></span>

```console
dotnet fsi Script.fsx
90
```

<span data-ttu-id="8fcc1-142">你可以根据需要在脚本中指定任意数量的程序集引用。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-142">You can specify as many assembly references as you like in a script.</span></span>

## <a name="loading-other-scripts"></a><span data-ttu-id="8fcc1-143">加载其他脚本</span><span class="sxs-lookup"><span data-stu-id="8fcc1-143">Loading other scripts</span></span>

<span data-ttu-id="8fcc1-144">在编写脚本时，对不同的任务使用不同的脚本通常是有帮助的。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-144">When scripting, it can often be helpful to use different scripts for different tasks.</span></span> <span data-ttu-id="8fcc1-145">有时，不妨在另一个脚本中重用脚本中的代码。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-145">Sometimes you may want to reuse code from on script in another.</span></span> <span data-ttu-id="8fcc1-146">可以使用 `#load` 直接加载并计算它，而不用将它的内容复制粘贴到文件中。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-146">Rather than copy-pasting its contents into your file, you can simple load and evaluate it with `#load`.</span></span>

<span data-ttu-id="8fcc1-147">假设为以下 `Script1.fsx`：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-147">Consider the following `Script1.fsx`:</span></span>

```fsharp
let square x = x * x
```

<span data-ttu-id="8fcc1-148">以及正在使用的文件 `Script2.fsx`：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-148">And the consuming file, `Script2.fsx`:</span></span>

```fsharp
#load "Script1.fsx"
open Script1

printfn "%d" (square 12)
```

<span data-ttu-id="8fcc1-149">请注意，`open Script1` 声明是必需的。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-149">Note that the `open Script1` declaration is required.</span></span> <span data-ttu-id="8fcc1-150">这是因为 F# 脚本中的构造被编译成顶级模块，此模块是它所在脚本文件的名称。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-150">This is because constructs in an F# script are compiled into a top-level module that is the name of the script file it is in.</span></span>

<span data-ttu-id="8fcc1-151">可以这样计算 `Script2.fsx`：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-151">You can evaluate `Script2.fsx` like so:</span></span>

```console
dotnet fsi Script2.fsx
144
```

<span data-ttu-id="8fcc1-152">你可以根据需要在脚本中指定任意数量的 `#load` 指令。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-152">You can specify as many `#load` directives as you like in a script.</span></span>

## <a name="using-the-fsi-object-in-f-code"></a><span data-ttu-id="8fcc1-153">在 F# 代码中使用 `fsi` 对象</span><span class="sxs-lookup"><span data-stu-id="8fcc1-153">Using the `fsi` object in F# code</span></span>

<span data-ttu-id="8fcc1-154">F# 脚本有权访问表示 F# 交互窗口会话的自定义 `fsi` 对象。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-154">F# scripts have access to a custom `fsi` object that represents the F# Interactive session.</span></span> <span data-ttu-id="8fcc1-155">这样，就可以自定义输出格式等。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-155">It allows you to customize things like output formatting.</span></span> <span data-ttu-id="8fcc1-156">这也是访问命令行参数的方式。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-156">It is also how you can access command-line arguments.</span></span>

<span data-ttu-id="8fcc1-157">下面的示例展示了如何获取和使用命令行参数：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-157">The following example shows how to get and use command-line arguments:</span></span>

```fsharp
let args = fsi.CommandLineArgs

for arg in args do
    printfn "%s" arg
```

<span data-ttu-id="8fcc1-158">计算后，它会打印出所有参数。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-158">When evaluated, it prints all arguments.</span></span> <span data-ttu-id="8fcc1-159">第一个参数始终是要计算的脚本的名称：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-159">The first argument is always the name of the script that is evaluated:</span></span>

```dotnet
dotnet fsi Script1.fsx hello world from fsi
Script1.fsx
hello
world
from
fsi
```

<span data-ttu-id="8fcc1-160">也可以使用 `System.Environment.GetCommandLineArgs()` 访问相同的参数。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-160">You can also use `System.Environment.GetCommandLineArgs()` to access the same arguments.</span></span>

## <a name="f-interactive-directive-reference"></a><span data-ttu-id="8fcc1-161">F# 交互窗口指令参考</span><span class="sxs-lookup"><span data-stu-id="8fcc1-161">F# Interactive directive reference</span></span>

<span data-ttu-id="8fcc1-162">前面所示的 `#r` 和 `#load` 指令只在 F# 交互窗口中可用。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-162">The `#r` and `#load` directives seen previously are only available in F# Interactive.</span></span> <span data-ttu-id="8fcc1-163">有几个指令只在 F# 交互窗口可用：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-163">There are several directives only available in F# Interactive:</span></span>

|<span data-ttu-id="8fcc1-164">指令</span><span class="sxs-lookup"><span data-stu-id="8fcc1-164">Directive</span></span>|<span data-ttu-id="8fcc1-165">描述</span><span class="sxs-lookup"><span data-stu-id="8fcc1-165">Description</span></span>|
|---------|-----------|
|`#r "nuget:..."`|<span data-ttu-id="8fcc1-166">通过 NuGet 引用包</span><span class="sxs-lookup"><span data-stu-id="8fcc1-166">References a package from NuGet</span></span>|
|`#r "assembly-name.dll"`|<span data-ttu-id="8fcc1-167">引用磁盘上的程序集</span><span class="sxs-lookup"><span data-stu-id="8fcc1-167">References an assembly on disk</span></span>|
|`#load "file-name.fsx"`|<span data-ttu-id="8fcc1-168">读取、编译并运行源文件。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-168">Reads a source file, compiles it, and runs it.</span></span>|
|`#help`|<span data-ttu-id="8fcc1-169">显示有关可用指令的信息。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-169">Displays information about available directives.</span></span>|
|`#I`|<span data-ttu-id="8fcc1-170">指定程序集搜索路径并用引号引起来。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-170">Specifies an assembly search path in quotation marks.</span></span>|
|`#quit`|<span data-ttu-id="8fcc1-171">终止 F# Interactive 会话。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-171">Terminates an F# Interactive session.</span></span>|
|<span data-ttu-id="8fcc1-172">`#time "on"` 或 `#time "off"`</span><span class="sxs-lookup"><span data-stu-id="8fcc1-172">`#time "on"` or `#time "off"`</span></span>|<span data-ttu-id="8fcc1-173">`#time` 本身可以切换是否显示性能信息。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-173">By itself, `#time` toggles whether to display performance information.</span></span> <span data-ttu-id="8fcc1-174">当它为 `"on"` 时，F# 交互窗口度量所解释并执行的代码的每个部分的实际时间、CPU 时间和垃圾回收信息。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-174">When it is `"on"`, F# Interactive measures real time, CPU time, and garbage collection information for each section of code that is interpreted and executed.</span></span>|

<span data-ttu-id="8fcc1-175">当在 F# Interactive 中指定文件或路径时，应指定字符串文本。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-175">When you specify files or paths in F# Interactive, a string literal is expected.</span></span> <span data-ttu-id="8fcc1-176">因此，文件和路径必须用引号引起来，也可以使用常见的转义符。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-176">Therefore, files and paths must be in quotation marks, and the usual escape characters apply.</span></span> <span data-ttu-id="8fcc1-177">可以使用 `@` 字符让 F# 交互窗口将包含路径的字符串解释为逐字字符串。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-177">You can use the `@` character to cause F# Interactive to interpret a string that contains a path as a verbatim string.</span></span> <span data-ttu-id="8fcc1-178">这会导致 F# Interactive 忽略转义符。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-178">This causes F# Interactive to ignore any escape characters.</span></span>

## <a name="interactive-and-compiled-preprocessor-directives"></a><span data-ttu-id="8fcc1-179">交互和编译的预处理器指令</span><span class="sxs-lookup"><span data-stu-id="8fcc1-179">Interactive and compiled preprocessor directives</span></span>

<span data-ttu-id="8fcc1-180">在 F# 交互窗口中编译代码时，无论是以交互方式还是直接运行脚本，都会定义 INTERACTIVE 符号。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-180">When you compile code in F# Interactive, whether you are running interactively or running a script, the symbol **INTERACTIVE** is defined.</span></span> <span data-ttu-id="8fcc1-181">在编译器中编译代码时，则会定义 COMPILED 符号。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-181">When you compile code in the compiler, the symbol **COMPILED** is defined.</span></span> <span data-ttu-id="8fcc1-182">因此，如果代码需要在编译模式和交互模式下不同，可以使用这些预处理器指令进行条件编译，以确定使用哪个。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-182">Thus, if code needs to be different in compiled and interactive modes, you can use these preprocessor directives for conditional compilation to determine which to use.</span></span> <span data-ttu-id="8fcc1-183">例如：</span><span class="sxs-lookup"><span data-stu-id="8fcc1-183">For example:</span></span>

```fsharp
#if INTERACTIVE
// Some code that executes only in FSI
// ...
#endif
```

## <a name="using-f-interactive-in-visual-studio"></a><span data-ttu-id="8fcc1-184">在 Visual Studio 中使用 F# 交互窗口</span><span class="sxs-lookup"><span data-stu-id="8fcc1-184">Using F# Interactive in Visual Studio</span></span>

<span data-ttu-id="8fcc1-185">若要通过 Visual Studio 运行 F# Interactive，可以单击标记为“F# Interactive”的相应工具栏按钮，或使用组合键 **Ctrl+Alt+F** 。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-185">To run F# Interactive through Visual Studio, you can click the appropriate toolbar button labeled **F# Interactive** , or use the keys **Ctrl+Alt+F**.</span></span> <span data-ttu-id="8fcc1-186">执行此操作将打开交互式窗口，该窗口是运行 F# Interactive 会话的工具窗口。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-186">Doing this will open the interactive window, a tool window running an F# Interactive session.</span></span> <span data-ttu-id="8fcc1-187">还可以选择一些你希望在交互式窗口中运行的代码，然后点击组合键 Alt+Enter。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-187">You can also select some code that you want to run in the interactive window and hit the key combination **Alt+Enter**.</span></span> <span data-ttu-id="8fcc1-188">F# Interactive 在标记为“F# Interactive”的工具窗口中启动。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-188">F# Interactive starts in a tool window labeled **F# Interactive**.</span></span> <span data-ttu-id="8fcc1-189">当您使用此组合键时，请确保焦点位于编辑器窗口内。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-189">When you use this key combination, make sure that the editor window has the focus.</span></span>

<span data-ttu-id="8fcc1-190">无论您使用的是控制台还是 Visual Studio，都会出现命令提示符，并且解释器会等待您输入代码。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-190">Whether you are using the console or Visual Studio, a command prompt appears and the interpreter awaits your input.</span></span> <span data-ttu-id="8fcc1-191">你可以像在代码文件中一样输入代码。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-191">You can enter code just as you would in a code file.</span></span> <span data-ttu-id="8fcc1-192">若要编译和执行代码，请输入两个分号 ( **;;** ) 以终止一行或几行输入。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-192">To compile and execute the code, enter two semicolons ( **;;** ) to terminate a line or several lines of input.</span></span>

<span data-ttu-id="8fcc1-193">F# Interactive 试图编译代码，如果成功，它将执行代码并打印其所编译类型和值的签名。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-193">F# Interactive attempts to compile the code and, if successful, it executes the code and prints the signature of the types and values that it compiled.</span></span> <span data-ttu-id="8fcc1-194">如果发生错误，解释器将打印错误消息。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-194">If errors occur, the interpreter prints the error messages.</span></span>

<span data-ttu-id="8fcc1-195">在同一个会话中输入的代码可以访问之前输入的任何构造，以便你可以生成程序。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-195">Code entered in the same session has access to any constructs entered previously, so you can build up programs.</span></span> <span data-ttu-id="8fcc1-196">工具窗口中的大容量缓存允许你在需要时将代码复制到文件中。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-196">An extensive buffer in the tool window allows you to copy the code into a file if needed.</span></span>

<span data-ttu-id="8fcc1-197">当在 Visual Studio 中运行时，F# Interactive 将独立于你的项目运行，因此，你不能在 F# Interactive 中使用在项目中定义的构造，除非你将函数的代码复制到交互式窗口中。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-197">When run in Visual Studio, F# Interactive runs independently of your project, so, for example, you cannot use constructs defined in your project in F# Interactive unless you copy the code for the function into the interactive window.</span></span>

<span data-ttu-id="8fcc1-198">可以通过调整设置来控制 F# 交互窗口命令行参数（选项）。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-198">You can control the F# Interactive command-line arguments (options) by adjusting the settings.</span></span> <span data-ttu-id="8fcc1-199">在“工具”菜单上，选择“选项...”，然后展开“F# 工具”。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-199">On the **Tools** menu, select **Options...** , and then expand **F# Tools**.</span></span> <span data-ttu-id="8fcc1-200">可以更改的两种设置是 F# Interactive 选项和“64 位F# Interactive”，只有在 64 位计算机上运行 F# Interactive 时，更改才有意义。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-200">The two settings that you can change are the F# Interactive options and the **64-bit F# Interactive** setting, which is relevant only if you are running F# Interactive on a 64-bit machine.</span></span> <span data-ttu-id="8fcc1-201">此设置确定是要运行 fsi.exe 还是 fsianycpu.exe 的专用 64 位版本，它使用计算机体系结构来确定是作为 32 位还是 64 位进程来运行。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-201">This setting determines whether you want to run the dedicated 64-bit version of **fsi.exe** or **fsianycpu.exe** , which uses the machine architecture to determine whether to run as a 32-bit or 64-bit process.</span></span>

## <a name="related-articles"></a><span data-ttu-id="8fcc1-202">相关文章</span><span class="sxs-lookup"><span data-stu-id="8fcc1-202">Related articles</span></span>

|<span data-ttu-id="8fcc1-203">Title</span><span class="sxs-lookup"><span data-stu-id="8fcc1-203">Title</span></span>|<span data-ttu-id="8fcc1-204">描述</span><span class="sxs-lookup"><span data-stu-id="8fcc1-204">Description</span></span>|
|-----|-----------|
|[<span data-ttu-id="8fcc1-205">F# Interactive 选项</span><span class="sxs-lookup"><span data-stu-id="8fcc1-205">F# Interactive Options</span></span>](../../language-reference/fsharp-interactive-options.md)|<span data-ttu-id="8fcc1-206">描述 F# Interactive (fsi.exe) 的命令行语法和选项。</span><span class="sxs-lookup"><span data-stu-id="8fcc1-206">Describes command-line syntax and options for the F# Interactive, fsi.exe.</span></span>|
