---
title: 如何：引用具有强名称的程序集
description: 本文介绍如何在编译时或运行时引用具有强名称的 .NET 程序集中的类型或资源。
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, compile-time references
- compile-time assembly referencing
- assemblies [.NET], strong-named
- assembly binding, strong-named
ms.assetid: 4c6a406a-b5eb-44fa-b4ed-4e95bb95a813
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 478f786995cfc4b57f0b18b2159775db104e9cfb
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687687"
---
# <a name="how-to-reference-a-strong-named-assembly"></a><span data-ttu-id="b5ad5-103">如何：引用具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="b5ad5-103">How to: Reference a strong-named assembly</span></span>
<span data-ttu-id="b5ad5-104">引用强名称程序集中的类型或资源的过程通常是透明的。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-104">The process for referencing types or resources in a strong-named assembly is usually transparent.</span></span> <span data-ttu-id="b5ad5-105">可在编译时（早期绑定）或在运行时进行引用。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-105">You can make the reference either at compile time (early binding) or at run time.</span></span>  
  
<span data-ttu-id="b5ad5-106">向编译器指示要编译的程序集显式引用另一程序集时，会发生编译时引用。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-106">A compile-time reference occurs when you indicate to the compiler that the assembly to be compiled explicitly references another assembly.</span></span> <span data-ttu-id="b5ad5-107">使用编译时引用时，编译器会自动获取目标强名称程序集的公钥，并将其放在正在编译的程序集的程序集引用中。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-107">When you use compile-time referencing, the compiler automatically gets the public key of the targeted strong-named assembly and places it in the assembly reference of the assembly being compiled.</span></span>
  
> [!NOTE]
> <span data-ttu-id="b5ad5-108">具有强名称的程序集只能使用其他具有强名称的程序集的类型。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-108">A strong-named assembly can only use types from other strong-named assemblies.</span></span> <span data-ttu-id="b5ad5-109">否则，将会危害具有强名称的程序集的安全性。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-109">Otherwise, the security of the strong-named assembly would be compromised.</span></span>  
  
## <a name="make-a-compile-time-reference-to-a-strong-named-assembly"></a><span data-ttu-id="b5ad5-110">对具有强名称的程序集进行编译时引用</span><span class="sxs-lookup"><span data-stu-id="b5ad5-110">Make a compile-time reference to a strong-named assembly</span></span>  

<span data-ttu-id="b5ad5-111">在命令提示符下，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b5ad5-111">At a command prompt, type the following command:</span></span>  

<span data-ttu-id="b5ad5-112">\<*compiler command*> /reference:\<*assembly name*></span><span class="sxs-lookup"><span data-stu-id="b5ad5-112">\<*compiler command*> **/reference:**\<*assembly name*></span></span>  

<span data-ttu-id="b5ad5-113">在此命令中，compiler command 是所用语言的编译器命令，assembly name 是引用的强名称程序集的名称 。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-113">In this command, *compiler command* is the compiler command for the language you are using, and *assembly name* is the name of the strong-named assembly being referenced.</span></span> <span data-ttu-id="b5ad5-114">还可使用其他编译器选项，如用于创建库程序集的 /t:library 选项。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-114">You can also use other compiler options, such as the **/t:library** option for creating a library assembly.</span></span>  

<span data-ttu-id="b5ad5-115">以下示例创建名为 myAssembly.dll 的程序集，该程序集从名为 myAssembly.cs 的代码模块中引用名为 myLibAssembly.dll 的强名称程序集  。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-115">The following example creates an assembly called *myAssembly.dll* that references a strong-named assembly called *myLibAssembly.dll* from a code module called *myAssembly.cs*.</span></span>  

```cmd
csc /t:library myAssembly.cs /reference:myLibAssembly.dll  
```  

## <a name="make-a-run-time-reference-to-a-strong-named-assembly"></a><span data-ttu-id="b5ad5-116">对强名称程序集进行运行时引用</span><span class="sxs-lookup"><span data-stu-id="b5ad5-116">Make a run-time reference to a strong-named assembly</span></span>  
  
<span data-ttu-id="b5ad5-117">对强名称程序集进行运行时引用（例如使用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> 方法）时，必须使用引用的强名称程序集的显示名称。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-117">When you make a run-time reference to a strong-named assembly, for example by using the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> method, you must use the display name of the referenced strong-named assembly.</span></span> <span data-ttu-id="b5ad5-118">显示名称的语法如下：</span><span class="sxs-lookup"><span data-stu-id="b5ad5-118">The syntax of a display name is as follows:</span></span>  

<span data-ttu-id="b5ad5-119">\<*assembly name*>**,** \<*version number*>**,** \<*culture*>**,** \<*public key token*></span><span class="sxs-lookup"><span data-stu-id="b5ad5-119">\<*assembly name*>**,** \<*version number*>**,** \<*culture*>**,** \<*public key token*></span></span>  

<span data-ttu-id="b5ad5-120">例如：</span><span class="sxs-lookup"><span data-stu-id="b5ad5-120">For example:</span></span>  

```console
myDll, Version=1.1.0.0, Culture=en, PublicKeyToken=03689116d3a4ae33
```  

<span data-ttu-id="b5ad5-121">在此示例中，`PublicKeyToken` 是十六进制格式的公钥标记。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-121">In this example, `PublicKeyToken` is the hexadecimal form of the public key token.</span></span> <span data-ttu-id="b5ad5-122">如果没有区域性值，请使用 `Culture=neutral`。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-122">If there is no culture value, use `Culture=neutral`.</span></span>  

<span data-ttu-id="b5ad5-123">下面的代码示例演示如何将此信息用于 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="b5ad5-123">The following code example shows how to use this information with the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method.</span></span>  

```cpp
Assembly^ myDll =
    Assembly::Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```csharp
Assembly myDll =
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```vb
Dim myDll As Assembly = _
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1")
```

<span data-ttu-id="b5ad5-124">可使用以下[强名称 (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) 命令为特定程序集打印十六进制格式的公钥和公钥标记：</span><span class="sxs-lookup"><span data-stu-id="b5ad5-124">You can print the hexadecimal format of the public key and public key token for a specific assembly by using the following [Strong Name (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) command:</span></span>  

<span data-ttu-id="b5ad5-125">sn-Tp \<** *assembly* **></span><span class="sxs-lookup"><span data-stu-id="b5ad5-125">**sn -Tp \<** *assembly* **>**</span></span>  

<span data-ttu-id="b5ad5-126">如果有公钥文件，则可改用以下命令（请注意命令行选项大小写的区别）：</span><span class="sxs-lookup"><span data-stu-id="b5ad5-126">If you have a public key file, you can use the following command instead (note the difference in case on the command-line option):</span></span>  

<span data-ttu-id="b5ad5-127">sn-tp \<** *public key file* **></span><span class="sxs-lookup"><span data-stu-id="b5ad5-127">**sn -tp \<** *public key file* **>**</span></span>  

## <a name="see-also"></a><span data-ttu-id="b5ad5-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="b5ad5-128">See also</span></span>

- [<span data-ttu-id="b5ad5-129">创建和使用具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="b5ad5-129">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
