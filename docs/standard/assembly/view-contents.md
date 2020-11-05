---
title: 如何：查看程序集内容
description: 可以使用 IL 反汇编程序来查看程序集的属性，以及对其他模块和程序集的引用。
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest, viewing information
- Ildasm.exe
- MSIL Disassembler
- assemblies [.NET], viewing contents
- viewing assembly information
- MSIL
- viewing MSIL information
ms.assetid: fb7baaab-4c0d-47ad-8fd3-4591cf834709
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: be2311c601effbebd519e33b7a5e13d49f44bd05
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687494"
---
# <a name="how-to-view-assembly-contents"></a><span data-ttu-id="b148d-103">如何：查看程序集内容</span><span class="sxs-lookup"><span data-stu-id="b148d-103">How to: View assembly contents</span></span>

<span data-ttu-id="b148d-104">可使用 [Ildasm.exe（IL 反汇编程序）](../../framework/tools/ildasm-exe-il-disassembler.md)查看文件中的 Microsoft 中间语言 (MSIL) 信息。</span><span class="sxs-lookup"><span data-stu-id="b148d-104">You can use the [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) to view Microsoft intermediate language (MSIL) information in a file.</span></span> <span data-ttu-id="b148d-105">如果要检查的文件是程序集，此信息可包括程序集的属性以及对其他模块和程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="b148d-105">If the file being examined is an assembly, this information can include the assembly's attributes and references to other modules and assemblies.</span></span> <span data-ttu-id="b148d-106">此信息有助于确定文件是程序集还是程序集的一部分，以及文件是否具有对其他模块或程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="b148d-106">This information can be helpful in determining whether a file is an assembly or part of an assembly and whether the file has references to other modules or assemblies.</span></span>

<span data-ttu-id="b148d-107">若要使用 Ildasm.exe 来显示程序集的内容，请在命令提示符下键入 ildasm \<assembly name>。</span><span class="sxs-lookup"><span data-stu-id="b148d-107">To display the contents of an assembly using *Ildasm.exe* , enter **ildasm \<assembly name>** at a command prompt.</span></span> <span data-ttu-id="b148d-108">例如，以下命令反汇编 Hello.exe 程序集。</span><span class="sxs-lookup"><span data-stu-id="b148d-108">For example, the following command disassembles the *Hello.exe* assembly.</span></span>

```cmd
ildasm Hello.exe
```

<span data-ttu-id="b148d-109">若要查看程序集清单信息，请在“MSIL 反汇编程序”窗口中双击“清单”图标。</span><span class="sxs-lookup"><span data-stu-id="b148d-109">To view assembly manifest information, double-click the **Manifest** icon in the MSIL Disassembler window.</span></span>

## <a name="example"></a><span data-ttu-id="b148d-110">示例</span><span class="sxs-lookup"><span data-stu-id="b148d-110">Example</span></span>

<span data-ttu-id="b148d-111">下例以基本的“Hello World”程序开始。</span><span class="sxs-lookup"><span data-stu-id="b148d-111">The following example starts with a basic "Hello World" program.</span></span> <span data-ttu-id="b148d-112">编译该程序后，使用 Ildasm.exe 反汇编 Hello.exe 程序集，并查看程序集清单 。</span><span class="sxs-lookup"><span data-stu-id="b148d-112">After compiling the program, use *Ildasm.exe* to disassemble the *Hello.exe* assembly and view the assembly manifest.</span></span>

```cpp
using namespace System;

class MainApp
{
public:
    static void Main()
    {
        Console::WriteLine("Hello World using C++/CLI!");
    }
};

int main()
{
    MainApp::Main();
}
```

```csharp
using System;

class MainApp
{
    public static void Main()
    {
        Console.WriteLine("Hello World using C#!");
    }
}
```

```vb
Class MainApp
    Public Shared Sub Main()
        Console.WriteLine("Hello World using Visual Basic!")
    End Sub
End Class
```

<span data-ttu-id="b148d-113">在 Hello.exe 程序集上运行 ildasm.exe 命令，然后在“MSIL 反汇编程序”窗口中双击“清单”图标生成以下输出 ：</span><span class="sxs-lookup"><span data-stu-id="b148d-113">Running the command *ildasm.exe* on the *Hello.exe* assembly and double-clicking the **Manifest** icon in the MSIL Disassembler window produces the following output:</span></span>

```output
// Metadata version: v4.0.30319
.assembly extern mscorlib
{
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..
  .ver 4:0:0:0
}
.assembly Hello
{
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 )
  .custom instance void [mscorlib]System.Runtime.CompilerServices.RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70 4E 6F 6E 45 78   // ....T..WrapNonEx
                                                                                                             63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )       // ceptionThrows.
  .hash algorithm 0x00008004
  .ver 0:0:0:0
}
.module Hello.exe
// MVID: {7C2770DB-1594-438D-BAE5-98764C39CCCA}
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00100000
.subsystem 0x0003       // WINDOWS_CUI
.corflags 0x00000001    //  ILONLY
// Image base: 0x00600000
```

<span data-ttu-id="b148d-114">下表描述了本例所使用 Hello.exe 程序集的程序集清单中的各项指令：</span><span class="sxs-lookup"><span data-stu-id="b148d-114">The following table describes each directive in the assembly manifest of the *Hello.exe* assembly used in the example:</span></span>

|<span data-ttu-id="b148d-115">指令</span><span class="sxs-lookup"><span data-stu-id="b148d-115">Directive</span></span>|<span data-ttu-id="b148d-116">描述</span><span class="sxs-lookup"><span data-stu-id="b148d-116">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="b148d-117">**.assembly extern \<assembly name>**</span><span class="sxs-lookup"><span data-stu-id="b148d-117">**.assembly extern \<assembly name>**</span></span>|<span data-ttu-id="b148d-118">指定包含当前模块所引用项目的另一程序集（在此示例中为 `mscorlib`）。</span><span class="sxs-lookup"><span data-stu-id="b148d-118">Specifies another assembly that contains items referenced by the current module (in this example, `mscorlib`).</span></span>|
|<span data-ttu-id="b148d-119">**.publickeytoken \<token>**</span><span class="sxs-lookup"><span data-stu-id="b148d-119">**.publickeytoken \<token>**</span></span>|<span data-ttu-id="b148d-120">指定引用程序集的实际密钥的标记。</span><span class="sxs-lookup"><span data-stu-id="b148d-120">Specifies the token of the actual key of the referenced assembly.</span></span>|
|<span data-ttu-id="b148d-121">**.ver \<version number>**</span><span class="sxs-lookup"><span data-stu-id="b148d-121">**.ver \<version number>**</span></span>|<span data-ttu-id="b148d-122">指定引用程序集的版本号。</span><span class="sxs-lookup"><span data-stu-id="b148d-122">Specifies the version number of the referenced assembly.</span></span>|
|<span data-ttu-id="b148d-123">**.assembly \<assembly name>**</span><span class="sxs-lookup"><span data-stu-id="b148d-123">**.assembly \<assembly name>**</span></span>|<span data-ttu-id="b148d-124">指定程序集名称。</span><span class="sxs-lookup"><span data-stu-id="b148d-124">Specifies the assembly name.</span></span>|
|<span data-ttu-id="b148d-125">**.hash algorithm \<int32 value>**</span><span class="sxs-lookup"><span data-stu-id="b148d-125">**.hash algorithm \<int32 value>**</span></span>|<span data-ttu-id="b148d-126">指定使用的哈希算法。</span><span class="sxs-lookup"><span data-stu-id="b148d-126">Specifies the hash algorithm used.</span></span>|
|<span data-ttu-id="b148d-127">**.ver \<version number>**</span><span class="sxs-lookup"><span data-stu-id="b148d-127">**.ver \<version number>**</span></span>|<span data-ttu-id="b148d-128">指定程序集的版本号。</span><span class="sxs-lookup"><span data-stu-id="b148d-128">Specifies the version number of the assembly.</span></span>|
|<span data-ttu-id="b148d-129">**.module \<file name>**</span><span class="sxs-lookup"><span data-stu-id="b148d-129">**.module \<file name>**</span></span>|<span data-ttu-id="b148d-130">指定组成程序集的模块名称。</span><span class="sxs-lookup"><span data-stu-id="b148d-130">Specifies the name of the modules that make up the assembly.</span></span> <span data-ttu-id="b148d-131">在此示例中，程序集只包含一个文件。</span><span class="sxs-lookup"><span data-stu-id="b148d-131">In this example, the assembly consists of only one file.</span></span>|
|<span data-ttu-id="b148d-132">**.subsystem \<value>**</span><span class="sxs-lookup"><span data-stu-id="b148d-132">**.subsystem \<value>**</span></span>|<span data-ttu-id="b148d-133">指定程序要求的应用程序环境。</span><span class="sxs-lookup"><span data-stu-id="b148d-133">Specifies the application environment required for the program.</span></span> <span data-ttu-id="b148d-134">在此示例中，值 3 表示该可执行文件从控制台运行。</span><span class="sxs-lookup"><span data-stu-id="b148d-134">In this example, the value 3 indicates that this executable is run from a console.</span></span>|
|<span data-ttu-id="b148d-135">.corflags</span><span class="sxs-lookup"><span data-stu-id="b148d-135">**.corflags**</span></span>|<span data-ttu-id="b148d-136">当前是元数据中的一个保留字段。</span><span class="sxs-lookup"><span data-stu-id="b148d-136">Currently a reserved field in the metadata.</span></span>|

<span data-ttu-id="b148d-137">根据程序集的内容，程序集清单可包含许多不同的指令。</span><span class="sxs-lookup"><span data-stu-id="b148d-137">An assembly manifest can contain a number of different directives, depending on the contents of the assembly.</span></span> <span data-ttu-id="b148d-138">有关程序集清单中指令的详尽列表，请参阅 Ecma 文档，特别是“第 II 部分：Metadata Definition and Semantics”（第 2 部分：元数据定义和语义）和“Partition III:CIL 指令集”：</span><span class="sxs-lookup"><span data-stu-id="b148d-138">For an extensive list of the directives in the assembly manifest, see the Ecma documentation, especially "Partition II: Metadata Definition and Semantics" and "Partition III: CIL Instruction Set":</span></span>

- [<span data-ttu-id="b148d-139">ECMA C# 和公共语言基础结构标准</span><span class="sxs-lookup"><span data-stu-id="b148d-139">ECMA C# and Common Language Infrastructure standards</span></span>](../components.md#applicable-standards)
- [<span data-ttu-id="b148d-140">标准 ECMA-335 - 公共语言基础结构 (CLI)</span><span class="sxs-lookup"><span data-stu-id="b148d-140">Standard ECMA-335 - Common Language Infrastructure (CLI)</span></span>](http://www.ecma-international.org/publications/standards/Ecma-335.htm)

## <a name="see-also"></a><span data-ttu-id="b148d-141">请参阅</span><span class="sxs-lookup"><span data-stu-id="b148d-141">See also</span></span>

- [<span data-ttu-id="b148d-142">应用程序域和程序集</span><span class="sxs-lookup"><span data-stu-id="b148d-142">Application domains and assemblies</span></span>](../../framework/app-domains/application-domains.md#application-domains-and-assemblies)
- [<span data-ttu-id="b148d-143">应用程序域和程序集帮助主题</span><span class="sxs-lookup"><span data-stu-id="b148d-143">Application domains and assemblies how-to topics</span></span>](../../framework/app-domains/application-domains-and-assemblies-how-to-topics.md)
- [<span data-ttu-id="b148d-144">Ildasm.exe（IL 反汇编程序）</span><span class="sxs-lookup"><span data-stu-id="b148d-144">Ildasm.exe (IL Disassembler)</span></span>](../../framework/tools/ildasm-exe-il-disassembler.md)
