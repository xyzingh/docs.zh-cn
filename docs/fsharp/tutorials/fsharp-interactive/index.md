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
# <a name="interactive-programming-with-f"></a><span data-ttu-id="5d505-103">使用 F\# 进行交互式编程</span><span class="sxs-lookup"><span data-stu-id="5d505-103">Interactive programming with F\#</span></span>

<span data-ttu-id="5d505-104">使用 F# 交互窗口 (dotnet fsi) 在控制台以交互方式运行 F# 代码，或执行 F# 脚本。</span><span class="sxs-lookup"><span data-stu-id="5d505-104">F# Interactive (dotnet fsi) is used to run F# code interactively at the console, or to execute F# scripts.</span></span> <span data-ttu-id="5d505-105">换句话说，F# Interactive 对 F# 语言执行 REPL（读取、计算、打印循环）。</span><span class="sxs-lookup"><span data-stu-id="5d505-105">In other words, F# interactive executes a REPL (Read, Evaluate, Print Loop) for the F# language.</span></span>

<span data-ttu-id="5d505-106">若要从控制台运行 F# 交互窗口，请运行 `dotnet fsi`。</span><span class="sxs-lookup"><span data-stu-id="5d505-106">To run F# Interactive from the console, run `dotnet fsi`.</span></span> <span data-ttu-id="5d505-107">你将在任何 .NET SDK 中找到 `dotnet fsi`。</span><span class="sxs-lookup"><span data-stu-id="5d505-107">You will find `dotnet fsi` in any .NET SDK.</span></span>

<span data-ttu-id="5d505-108">有关可用命令行选项的信息，请参阅 [F# Interactive 选项](../../language-reference/fsharp-interactive-options.md)。</span><span class="sxs-lookup"><span data-stu-id="5d505-108">For information about command line options available, see [F# Interactive Options](../../language-reference/fsharp-interactive-options.md).</span></span>

<span data-ttu-id="5d505-109">若要通过 Visual Studio 运行 F# Interactive，可以单击标记为“F# Interactive”的相应工具栏按钮，或使用组合键 **Ctrl+Alt+F** 。</span><span class="sxs-lookup"><span data-stu-id="5d505-109">To run F# Interactive through Visual Studio, you can click the appropriate toolbar button labeled **F# Interactive** , or use the keys **Ctrl+Alt+F** .</span></span> <span data-ttu-id="5d505-110">执行此操作将打开交互式窗口，该窗口是运行 F# Interactive 会话的工具窗口。</span><span class="sxs-lookup"><span data-stu-id="5d505-110">Doing this will open the interactive window, a tool window running an F# Interactive session.</span></span> <span data-ttu-id="5d505-111">还可以选择一些你希望在交互式窗口中运行的代码，然后点击组合键 Alt+Enter。</span><span class="sxs-lookup"><span data-stu-id="5d505-111">You can also select some code that you want to run in the interactive window and hit the key combination **Alt+Enter** .</span></span> <span data-ttu-id="5d505-112">F# Interactive 在标记为“F# Interactive”的工具窗口中启动。</span><span class="sxs-lookup"><span data-stu-id="5d505-112">F# Interactive starts in a tool window labeled **F# Interactive** .</span></span> <span data-ttu-id="5d505-113">当您使用此组合键时，请确保焦点位于编辑器窗口内。</span><span class="sxs-lookup"><span data-stu-id="5d505-113">When you use this key combination, make sure that the editor window has the focus.</span></span>

<span data-ttu-id="5d505-114">无论您使用的是控制台还是 Visual Studio，都会出现命令提示符，并且解释器会等待您输入代码。</span><span class="sxs-lookup"><span data-stu-id="5d505-114">Whether you are using the console or Visual Studio, a command prompt appears and the interpreter awaits your input.</span></span> <span data-ttu-id="5d505-115">你可以像在代码文件中一样输入代码。</span><span class="sxs-lookup"><span data-stu-id="5d505-115">You can enter code just as you would in a code file.</span></span> <span data-ttu-id="5d505-116">若要编译和执行代码，请输入两个分号 ( **;;** ) 以终止一行或几行输入。</span><span class="sxs-lookup"><span data-stu-id="5d505-116">To compile and execute the code, enter two semicolons ( **;;** ) to terminate a line or several lines of input.</span></span>

<span data-ttu-id="5d505-117">F# Interactive 试图编译代码，如果成功，它将执行代码并打印其所编译类型和值的签名。</span><span class="sxs-lookup"><span data-stu-id="5d505-117">F# Interactive attempts to compile the code and, if successful, it executes the code and prints the signature of the types and values that it compiled.</span></span> <span data-ttu-id="5d505-118">如果发生错误，解释器将打印错误消息。</span><span class="sxs-lookup"><span data-stu-id="5d505-118">If errors occur, the interpreter prints the error messages.</span></span>

<span data-ttu-id="5d505-119">在同一个会话中输入的代码可以访问之前输入的任何构造，以便你可以生成程序。</span><span class="sxs-lookup"><span data-stu-id="5d505-119">Code entered in the same session has access to any constructs entered previously, so you can build up programs.</span></span> <span data-ttu-id="5d505-120">工具窗口中的大容量缓存允许你在需要时将代码复制到文件中。</span><span class="sxs-lookup"><span data-stu-id="5d505-120">An extensive buffer in the tool window allows you to copy the code into a file if needed.</span></span>

<span data-ttu-id="5d505-121">当在 Visual Studio 中运行时，F# Interactive 将独立于你的项目运行，因此，你不能在 F# Interactive 中使用在项目中定义的构造，除非你将函数的代码复制到交互式窗口中。</span><span class="sxs-lookup"><span data-stu-id="5d505-121">When run in Visual Studio, F# Interactive runs independently of your project, so, for example, you cannot use constructs defined in your project in F# Interactive unless you copy the code for the function into the interactive window.</span></span>

<span data-ttu-id="5d505-122">如果打开的项目引用了某些库，可以通过“解决方案资源管理器”在 F# Interactive 中引用这些库。</span><span class="sxs-lookup"><span data-stu-id="5d505-122">If you have a project open that references some libraries, you can reference these in F# Interactive through **Solution Explorer** .</span></span> <span data-ttu-id="5d505-123">若要在 F# Interactive 中引用库，请展开“引用”节点，打开库的快捷菜单，然后选择“发送至 F# Interactive”。</span><span class="sxs-lookup"><span data-stu-id="5d505-123">To reference a library in F# Interactive, expand the **References** node, open the shortcut menu for the library, and choose **Send to F# Interactive** .</span></span>

<span data-ttu-id="5d505-124">你可以通过调整设置控制 F# Interactive 命令行自变量（选项）。</span><span class="sxs-lookup"><span data-stu-id="5d505-124">You can control the F# Interactive command line arguments (options) by adjusting the settings.</span></span> <span data-ttu-id="5d505-125">在“工具”菜单上，选择“选项...”，然后展开“F# 工具”。</span><span class="sxs-lookup"><span data-stu-id="5d505-125">On the **Tools** menu, select **Options...** , and then expand **F# Tools** .</span></span> <span data-ttu-id="5d505-126">可以更改的两种设置是 F# Interactive 选项和“64 位F# Interactive”，只有在 64 位计算机上运行 F# Interactive 时，更改才有意义。</span><span class="sxs-lookup"><span data-stu-id="5d505-126">The two settings that you can change are the F# Interactive options and the **64-bit F# Interactive** setting, which is relevant only if you are running F# Interactive on a 64-bit machine.</span></span> <span data-ttu-id="5d505-127">此设置确定是否需要运行 fsi.exe 或 fsianycpu.exe 的专用 64 位版本，它使用计算机体系结构确定是作为 32 位还是 64 位进程来运行。</span><span class="sxs-lookup"><span data-stu-id="5d505-127">This setting determines whether you want to run the dedicated 64-bit version of fsi.exe or fsianycpu.exe, which uses the machine architecture to determine whether to run as a 32-bit or 64-bit process.</span></span>

## <a name="scripting-with-f"></a><span data-ttu-id="5d505-128">使用 F 编写脚本\#</span><span class="sxs-lookup"><span data-stu-id="5d505-128">Scripting with F\#</span></span>

<span data-ttu-id="5d505-129">脚本使用 **.fsx** 或 **.fsscript** 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="5d505-129">Scripts use the file extension **.fsx** or **.fsscript** .</span></span> <span data-ttu-id="5d505-130">可以不编译源代码再运行编译的程序集，仅运行 dotnet fsi 并指定 F# 源代码脚本的文件名，F# 交互窗口会实时读取并执行代码。</span><span class="sxs-lookup"><span data-stu-id="5d505-130">Instead of compiling source code and then later running the compiled assembly, you can just run **dotnet fsi** and specify the filename of the script of F# source code, and F# interactive reads the code and executes it in real time.</span></span>

## <a name="differences-between-the-interactive-scripting-and-compiled-environments"></a><span data-ttu-id="5d505-131">交互式、脚本编写和编译环境之间的差异</span><span class="sxs-lookup"><span data-stu-id="5d505-131">Differences between the interactive, scripting, and compiled environments</span></span>

<span data-ttu-id="5d505-132">在 F# Interactive 中编译代码时，无论是以交互方式运行还是直接运行脚本，都会定义 **INTERACTIVE** 符号。</span><span class="sxs-lookup"><span data-stu-id="5d505-132">When you are compiling code in F# Interactive, whether you are running interactively or running a script, the symbol **INTERACTIVE** is defined.</span></span> <span data-ttu-id="5d505-133">在编译器中编译代码时，将定义 **COMPILED** 符号。</span><span class="sxs-lookup"><span data-stu-id="5d505-133">When you are compiling code in the compiler, the symbol **COMPILED** is defined.</span></span> <span data-ttu-id="5d505-134">因此，如果编译模式和交互模式下的代码不同，你可以使用预处理器指令进行条件编译以确定使用哪种模式。</span><span class="sxs-lookup"><span data-stu-id="5d505-134">Thus, if code needs to be different in compiled and interactive modes, you can use preprocessor directives for conditional compilation to determine which to use.</span></span>

<span data-ttu-id="5d505-135">当在 F# Interactive 中执行脚本时，某些指令可用，而在编译器中执行时，这些指令却不可用。</span><span class="sxs-lookup"><span data-stu-id="5d505-135">Some directives are available when you are executing scripts in F# Interactive that are not available when you are executing the compiler.</span></span> <span data-ttu-id="5d505-136">下表总结了使用 F# Interactive 时可用的指令。</span><span class="sxs-lookup"><span data-stu-id="5d505-136">The following table summarizes directives that are available when you are using F# Interactive.</span></span>

|<span data-ttu-id="5d505-137">指令</span><span class="sxs-lookup"><span data-stu-id="5d505-137">Directive</span></span>|<span data-ttu-id="5d505-138">描述</span><span class="sxs-lookup"><span data-stu-id="5d505-138">Description</span></span>|
|---------|-----------|
|<span data-ttu-id="5d505-139">**#help**</span><span class="sxs-lookup"><span data-stu-id="5d505-139">**#help**</span></span>|<span data-ttu-id="5d505-140">显示有关可用指令的信息。</span><span class="sxs-lookup"><span data-stu-id="5d505-140">Displays information about available directives.</span></span>|
|<span data-ttu-id="5d505-141">**#I**</span><span class="sxs-lookup"><span data-stu-id="5d505-141">**#I**</span></span>|<span data-ttu-id="5d505-142">指定程序集搜索路径并用引号引起来。</span><span class="sxs-lookup"><span data-stu-id="5d505-142">Specifies an assembly search path in quotation marks.</span></span>|
|<span data-ttu-id="5d505-143">**#load**</span><span class="sxs-lookup"><span data-stu-id="5d505-143">**#load**</span></span>|<span data-ttu-id="5d505-144">读取、编译并运行源文件。</span><span class="sxs-lookup"><span data-stu-id="5d505-144">Reads a source file, compiles it, and runs it.</span></span>|
|<span data-ttu-id="5d505-145">**#quit**</span><span class="sxs-lookup"><span data-stu-id="5d505-145">**#quit**</span></span>|<span data-ttu-id="5d505-146">终止 F# Interactive 会话。</span><span class="sxs-lookup"><span data-stu-id="5d505-146">Terminates an F# Interactive session.</span></span>|
|<span data-ttu-id="5d505-147">**#r**</span><span class="sxs-lookup"><span data-stu-id="5d505-147">**#r**</span></span>|<span data-ttu-id="5d505-148">引用程序集。</span><span class="sxs-lookup"><span data-stu-id="5d505-148">References an assembly.</span></span>|
|<span data-ttu-id="5d505-149">**#time ["on"&#124;"off"]**</span><span class="sxs-lookup"><span data-stu-id="5d505-149">**#time ["on"&#124;"off"]**</span></span>|<span data-ttu-id="5d505-150">单独使用 **#time** 时，可在是否显示性能信息之间切换。</span><span class="sxs-lookup"><span data-stu-id="5d505-150">By itself, **#time** toggles whether to display performance information.</span></span> <span data-ttu-id="5d505-151">启用后，F# Interactive 将测量实际时间、CPU 时间，以及所解释并执行的代码的每个部分的垃圾回收信息。</span><span class="sxs-lookup"><span data-stu-id="5d505-151">When it is enabled, F# Interactive measures real time, CPU time, and garbage collection information for each section of code that is interpreted and executed.</span></span>|

<span data-ttu-id="5d505-152">当在 F# Interactive 中指定文件或路径时，应指定字符串文本。</span><span class="sxs-lookup"><span data-stu-id="5d505-152">When you specify files or paths in F# Interactive, a string literal is expected.</span></span> <span data-ttu-id="5d505-153">因此，文件和路径必须用引号引起来，也可以使用常见的转义符。</span><span class="sxs-lookup"><span data-stu-id="5d505-153">Therefore, files and paths must be in quotation marks, and the usual escape characters apply.</span></span> <span data-ttu-id="5d505-154">此外，你还可以使用 @ 字符，此时 F# Interactive 会将包含路径的字符串解释为原义字符串。</span><span class="sxs-lookup"><span data-stu-id="5d505-154">Also, you can use the @ character to cause F# Interactive to interpret a string that contains a path as a verbatim string.</span></span> <span data-ttu-id="5d505-155">这会导致 F# Interactive 忽略转义符。</span><span class="sxs-lookup"><span data-stu-id="5d505-155">This causes F# Interactive to ignore any escape characters.</span></span>

<span data-ttu-id="5d505-156">编译模式与交互模式的其中一个区别是访问命令行自变量的方法。</span><span class="sxs-lookup"><span data-stu-id="5d505-156">One of the differences between compiled and interactive mode is the way you access command line arguments.</span></span> <span data-ttu-id="5d505-157">在编译模式下，使用 **System.Environment.GetCommandLineArgs** 。</span><span class="sxs-lookup"><span data-stu-id="5d505-157">In compiled mode, use **System.Environment.GetCommandLineArgs** .</span></span> <span data-ttu-id="5d505-158">在脚本中，使用 **fsi.CommandLineArgs** 。</span><span class="sxs-lookup"><span data-stu-id="5d505-158">In scripts, use **fsi.CommandLineArgs** .</span></span>

<span data-ttu-id="5d505-159">下面的代码说明如何创建可读取脚本中命令行自变量的函数，并演示如何从脚本引用另一个程序集。</span><span class="sxs-lookup"><span data-stu-id="5d505-159">The following code illustrates how to create a function that reads the command line arguments in a script and also demonstrates how to reference another assembly from a script.</span></span> <span data-ttu-id="5d505-160">第一个代码文件 **MyAssembly.fs** 是所引用程序集的代码。</span><span class="sxs-lookup"><span data-stu-id="5d505-160">The first code file, **MyAssembly.fs** , is the code for the assembly being referenced.</span></span> <span data-ttu-id="5d505-161">使用命令行 **fsc-a MyAssembly.fs** 编译此文件，然后使用命令行 **fsi --exec file1.fsx** test 以脚本执行第二个文件</span><span class="sxs-lookup"><span data-stu-id="5d505-161">Compile this file with the command line: **fsc -a MyAssembly.fs** and then execute the second file as a script with the command line: **fsi --exec file1.fsx** test</span></span>

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

<span data-ttu-id="5d505-162">输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d505-162">The output is as follows:</span></span>

```console
Command line arguments:
file1.fsx
test
90
```

## <a name="package-management-in-f-interactive"></a><span data-ttu-id="5d505-163">F# 交互窗口中的包管理</span><span class="sxs-lookup"><span data-stu-id="5d505-163">Package Management in F# Interactive</span></span>

[!NOTE] <span data-ttu-id="5d505-164">包管理可作为 `3.1.300` 和更高版本的 .NET SDK 随附的 `dotnet fsi` 版本以及所有 `5.*` 版本 .NET SDK 中的预览功能。</span><span class="sxs-lookup"><span data-stu-id="5d505-164">Package management is available as a preview feature in versions of `dotnet fsi` shipped in the `3.1.300` and greater versions of the .NET SDK, as well as all `5.*` versions of the .NET SDK.</span></span> <span data-ttu-id="5d505-165">若要在此预览版本中启用它，请使用 `--langversion:preview` 参数运行 `dotnet fsi`。</span><span class="sxs-lookup"><span data-stu-id="5d505-165">To enable it in this preview release, run `dotnet fsi` with the `--langversion:preview` argument.</span></span>

<span data-ttu-id="5d505-166">用于在 F# 交互窗口中引用 DLL 的 `#r` 语法还可通过以下语法用于引用 nuget 包：</span><span class="sxs-lookup"><span data-stu-id="5d505-166">The `#r` syntax for referencing a DLL in F# Interactive can also be used to reference a nuget package via the following syntax:</span></span>

```fsharp
#r "nuget: <package name>"
```

<span data-ttu-id="5d505-167">例如，要引用 `FSharp.Data` 包，请使用以下 `#r` 引用：</span><span class="sxs-lookup"><span data-stu-id="5d505-167">For example, to reference the `FSharp.Data` package, use the following `#r` reference:</span></span>

```fsharp
#r "nuget: FSharp.Data"
```

<span data-ttu-id="5d505-168">执行此行后，最新版本的 `FSharp.Data` 包将下载到 nuget 缓存并在当前 F# 交互窗口会话中引用。</span><span class="sxs-lookup"><span data-stu-id="5d505-168">After executing this line, the latest version of the `FSharp.Data` package will be downloaded to your nuget cache and referenced in the current F# Interactive session.</span></span>

<span data-ttu-id="5d505-169">除了包名称外，还可以通过短语法引用包的特定版本：</span><span class="sxs-lookup"><span data-stu-id="5d505-169">In addition to the package name, specific versions of a package can be referenced via a short syntax:</span></span>

```fsharp
#r "nuget: FSharp.Data, 3.3.2"
```

<span data-ttu-id="5d505-170">或者以更明确的方式引用：</span><span class="sxs-lookup"><span data-stu-id="5d505-170">or in a more explicit fashion:</span></span>

```fsharp
#r "nuget: FSharp.Data, Version=3.3.2"
```

## <a name="related-articles"></a><span data-ttu-id="5d505-171">相关文章</span><span class="sxs-lookup"><span data-stu-id="5d505-171">Related articles</span></span>

|<span data-ttu-id="5d505-172">Title</span><span class="sxs-lookup"><span data-stu-id="5d505-172">Title</span></span>|<span data-ttu-id="5d505-173">描述</span><span class="sxs-lookup"><span data-stu-id="5d505-173">Description</span></span>|
|-----|-----------|
|[<span data-ttu-id="5d505-174">F# Interactive 选项</span><span class="sxs-lookup"><span data-stu-id="5d505-174">F# Interactive Options</span></span>](../../language-reference/fsharp-interactive-options.md)|<span data-ttu-id="5d505-175">描述 F# Interactive (fsi.exe) 的命令行语法和选项。</span><span class="sxs-lookup"><span data-stu-id="5d505-175">Describes command-line syntax and options for the F# Interactive, fsi.exe.</span></span>|
