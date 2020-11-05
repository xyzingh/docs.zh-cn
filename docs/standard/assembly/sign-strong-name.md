---
title: 如何：使用强名称为程序集签名
description: 本文说明如何使用“签名”选项卡、程序集链接器、程序集属性或编译器选项对 .NET 程序集进行强名称签名。
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, signing with strong names
- signing assemblies
- assemblies [.NET], signing
- assemblies [.NET], strong-named
ms.assetid: 2c30799a-a826-46b4-a25d-c584027a6c67
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 5192f7f372b9ef7927930c3599aebc6fca9f1f0f
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687656"
---
# <a name="how-to-sign-an-assembly-with-a-strong-name"></a><span data-ttu-id="fe1a6-103">如何：使用强名称为程序集签名</span><span class="sxs-lookup"><span data-stu-id="fe1a6-103">How to: Sign an assembly with a strong name</span></span>

> [!NOTE]
> <span data-ttu-id="fe1a6-104">虽然 .NET Core 支持强名称程序集，而且 .NET Core 库中的所有程序集均已签名，但大多数第三方程序集不需要强名称。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-104">Although .NET Core supports strong-named assemblies, and all assemblies in the .NET Core library are signed, the majority of third-party assemblies do not need strong names.</span></span> <span data-ttu-id="fe1a6-105">有关详细信息，请参阅 GitHub 上的[强名称签名](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md)。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-105">For more information, see [Strong Name Signing](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md) on GitHub.</span></span>

<span data-ttu-id="fe1a6-106">可通过许多方法为程序集签署强名称：</span><span class="sxs-lookup"><span data-stu-id="fe1a6-106">There are a number of ways to sign an assembly with a strong name:</span></span>  
  
- <span data-ttu-id="fe1a6-107">在 Visual Studio 中，通过使用项目的 **“属性”** 对话框中的 **“签名”** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-107">By using the **Signing** tab in a project's **Properties** dialog box in Visual Studio.</span></span> <span data-ttu-id="fe1a6-108">这是为程序集签署强名称的最简单且最方便的方法。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-108">This is the easiest and most convenient way to sign an assembly with a strong name.</span></span>  
  
- <span data-ttu-id="fe1a6-109">通过使用[程序集链接器 (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) 来链接 .NET Framework 代码模块（.netmodule 文件）与密钥文件。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-109">By using the [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) to link a .NET Framework code module (a *.netmodule* file) with a key file.</span></span>  
  
- <span data-ttu-id="fe1a6-110">通过使用程序集特性将强名称信息插入代码中。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-110">By using assembly attributes to insert the strong name information into your code.</span></span> <span data-ttu-id="fe1a6-111">你可以使用 <xref:System.Reflection.AssemblyKeyFileAttribute> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 特性，具体取决于要使用的密钥文件所在的位置。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-111">You can use either the <xref:System.Reflection.AssemblyKeyFileAttribute> or the <xref:System.Reflection.AssemblyKeyNameAttribute> attribute, depending on where the key file to be used is located.</span></span>  
  
- <span data-ttu-id="fe1a6-112">通过使用编译器选项。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-112">By using compiler options.</span></span>  
  
 <span data-ttu-id="fe1a6-113">要使用强名称为程序集签名，必须具有加密密钥对。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-113">You must have a cryptographic key pair to sign an assembly with a strong name.</span></span> <span data-ttu-id="fe1a6-114">有关创建密钥对的详细信息，请参阅[如何：创建公钥/私钥对](create-public-private-key-pair.md)。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-114">For more information about creating a key pair, see [How to: Create a public-private key pair](create-public-private-key-pair.md).</span></span>  
  
## <a name="create-and-sign-an-assembly-with-a-strong-name-by-using-visual-studio"></a><span data-ttu-id="fe1a6-115">使用 Visual Studio 创建程序集并使用强名称为程序集签名</span><span class="sxs-lookup"><span data-stu-id="fe1a6-115">Create and sign an assembly with a strong name by using Visual Studio</span></span>  
  
1. <span data-ttu-id="fe1a6-116">在“解决方案资源管理器” 中，打开项目的快捷菜单，然后选择“属性” 。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-116">In **Solution Explorer** , open the shortcut menu for the project, and then choose **Properties**.</span></span>  
  
2. <span data-ttu-id="fe1a6-117">选择 **“签名”** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-117">Choose the **Signing** tab.</span></span>  
  
3. <span data-ttu-id="fe1a6-118">选择“为程序集签名”框。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-118">Select the **Sign the assembly** box.</span></span>  
  
4. <span data-ttu-id="fe1a6-119">在“选择强名称密钥文件”框中，选择“浏览”，然后导航到密钥文件 。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-119">In the **Choose a strong name key file** box, choose **Browse** , and then navigate to the key file.</span></span> <span data-ttu-id="fe1a6-120">若要创建新的密钥文件，请选择“新建”，并在“创建强名称密钥”对话框中输入其名称 。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-120">To create a new key file, choose **New** and enter its name in the **Create Strong Name Key** dialog box.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="fe1a6-121">为了[延迟为程序集签名](delay-sign.md)，请选择公钥文件。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-121">In order to [delay sign an assembly](delay-sign.md), choose a public key file.</span></span>  
  
### <a name="create-and-sign-an-assembly-with-a-strong-name-by-using-the-assembly-linker"></a><span data-ttu-id="fe1a6-122">使用程序集链接器创建程序集并使用强名称为程序集签名</span><span class="sxs-lookup"><span data-stu-id="fe1a6-122">Create and sign an assembly with a strong name by using the Assembly Linker</span></span>  
  
<span data-ttu-id="fe1a6-123">在 [Visual Studio 开发人员命令提示](../../framework/tools/developer-command-prompt-for-vs.md)处，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="fe1a6-123">At the [Developer Command Prompt for Visual Studio](../../framework/tools/developer-command-prompt-for-vs.md), enter the following command:</span></span>  

<span data-ttu-id="fe1a6-124">al /out:\<*assemblyName*> \<moduleName> /keyfile:\<*keyfileName*> </span><span class="sxs-lookup"><span data-stu-id="fe1a6-124">**al** **/out:**\<*assemblyName*> *\<moduleName>* **/keyfile:**\<*keyfileName*></span></span>  

<span data-ttu-id="fe1a6-125">其中：</span><span class="sxs-lookup"><span data-stu-id="fe1a6-125">Where:</span></span>  

- <span data-ttu-id="fe1a6-126">assemblyName 是程序集链接器将发出的强签名程序集（.dll 或 .exe 文件）的名称  。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-126">*assemblyName* is the name of the strongly signed assembly (a *.dll* or *.exe* file) that Assembly Linker will emit.</span></span>  
  
- <span data-ttu-id="fe1a6-127">moduleName 是包含一个或多个类型的 .NET Framework 代码模块（.netmodule 文件）的名称 。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-127">*moduleName* is the name of a .NET Framework code module (a *.netmodule* file) that includes one or more types.</span></span> <span data-ttu-id="fe1a6-128">可通过在 C# 或 Visual Basic 中使用 `/target:module` 开关对代码进行编译来创建.netmodule 文件。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-128">You can create a *.netmodule* file by compiling your code with the `/target:module` switch in C# or Visual Basic.</span></span>
  
- <span data-ttu-id="fe1a6-129">keyfileName 是包含密钥对的容器或文件的名称。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-129">*keyfileName* is the name of the container or file that contains the key pair.</span></span> <span data-ttu-id="fe1a6-130">程序集链接器解释与当前目录相关的相对路径。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-130">Assembly Linker interprets a relative path in relation to the current directory.</span></span>  

<span data-ttu-id="fe1a6-131">下面的示例使用密钥文件 sgKey.snk 为程序集 MyAssembly.dll 签署强名称 。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-131">The following example signs the assembly *MyAssembly.dll* with a strong name by using the key file *sgKey.snk*.</span></span>  

```console
al /out:MyAssembly.dll MyModule.netmodule /keyfile:sgKey.snk  
```  
  
<span data-ttu-id="fe1a6-132">有关此工具的详细信息，请参阅 [程序集链接器](../../framework/tools/al-exe-assembly-linker.md)。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-132">For more information about this tool, see [Assembly Linker](../../framework/tools/al-exe-assembly-linker.md).</span></span>  
  
## <a name="sign-an-assembly-with-a-strong-name-by-using-attributes"></a><span data-ttu-id="fe1a6-133">使用属性为程序集签署强名称</span><span class="sxs-lookup"><span data-stu-id="fe1a6-133">Sign an assembly with a strong name by using attributes</span></span>  
  
1. <span data-ttu-id="fe1a6-134">将 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=nameWithType> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 特性添加到源代码文件中，并指定包含为程序集签署强名称时要使用的密钥对的文件或容器的名称。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-134">Add the <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=nameWithType> or <xref:System.Reflection.AssemblyKeyNameAttribute> attribute to your source code file, and specify the name of the file or container that contains the key pair to use when signing the assembly with a strong name.</span></span>  

2. <span data-ttu-id="fe1a6-135">通常会编译源代码文件。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-135">Compile the source code file normally.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="fe1a6-136">当 C# 和 Visual Basic 编译器在源代码中遇到 <xref:System.Reflection.AssemblyKeyFileAttribute> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 特性时，会发出编译器警告（分别为 CS1699 和 BC41008）。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-136">The C# and Visual Basic compilers issue compiler warnings (CS1699 and BC41008, respectively) when they encounter the <xref:System.Reflection.AssemblyKeyFileAttribute> or <xref:System.Reflection.AssemblyKeyNameAttribute> attribute in source code.</span></span> <span data-ttu-id="fe1a6-137">你可以忽略这些警告。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-137">You can ignore the warnings.</span></span>  

<span data-ttu-id="fe1a6-138">下面的代码示例将 <xref:System.Reflection.AssemblyKeyFileAttribute> 属性用于名为 keyfile.snk 的密钥文件（位于编译程序集的目录中）。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-138">The following example uses the <xref:System.Reflection.AssemblyKeyFileAttribute> attribute with a key file called *keyfile.snk* , which is located in the directory where the assembly is compiled.</span></span>  

```cpp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")];
```

```csharp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")]
```

```vb
<Assembly:AssemblyKeyFileAttribute("keyfile.snk")>
```

<span data-ttu-id="fe1a6-139">在编译源文件时，也可以延迟为程序集签名。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-139">You can also delay sign an assembly when compiling your source file.</span></span> <span data-ttu-id="fe1a6-140">有关详细信息，请参阅[延迟为程序集签名](delay-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-140">For more information, see [Delay-sign an assembly](delay-sign.md).</span></span>  

## <a name="sign-an-assembly-with-a-strong-name-by-using-the-compiler"></a><span data-ttu-id="fe1a6-141">使用编译器为程序集签署强名称</span><span class="sxs-lookup"><span data-stu-id="fe1a6-141">Sign an assembly with a strong name by using the compiler</span></span>  

<span data-ttu-id="fe1a6-142">使用 C# 和 Visual Basic 中的 `/keyfile` 或 `/delaysign` 编译器选项，或使用 C++ 中的 `/KEYFILE` 或 `/DELAYSIGN` 链接器选项编译源代码文件。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-142">Compile your source code file or files with the `/keyfile` or `/delaysign` compiler option in C# and Visual Basic, or the `/KEYFILE` or `/DELAYSIGN` linker option in C++.</span></span> <span data-ttu-id="fe1a6-143">在选项名称后，添加冒号和密钥文件的名称。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-143">After the option name, add a colon and the name of the key file.</span></span> <span data-ttu-id="fe1a6-144">使用命令行编译器时，你可以将密钥文件复制到包含源代码文件的目录中。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-144">When using command-line compilers, you can copy the key file to the directory that contains your source code files.</span></span>  

<span data-ttu-id="fe1a6-145">有关延迟签名的信息，请参阅[延迟为程序集签名](delay-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-145">For information on delay signing, see [Delay-sign an assembly](delay-sign.md).</span></span>  

<span data-ttu-id="fe1a6-146">下面的示例使用 C# 编译器并借助密钥文件 sgKey.snk 为程序集 UtilityLibrary.dll 签署强名称 。</span><span class="sxs-lookup"><span data-stu-id="fe1a6-146">The following example uses the C# compiler and signs the assembly *UtilityLibrary.dll* with a strong name by using the key file *sgKey.snk*.</span></span>  

```cmd
csc /t:library UtilityLibrary.cs /keyfile:sgKey.snk  
```  

## <a name="see-also"></a><span data-ttu-id="fe1a6-147">请参阅</span><span class="sxs-lookup"><span data-stu-id="fe1a6-147">See also</span></span>

- [<span data-ttu-id="fe1a6-148">创建和使用具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="fe1a6-148">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
- [<span data-ttu-id="fe1a6-149">如何：创建公钥/私钥对</span><span class="sxs-lookup"><span data-stu-id="fe1a6-149">How to: Create a public-private key pair</span></span>](create-public-private-key-pair.md)
- [<span data-ttu-id="fe1a6-150">Al.exe（程序集链接器）</span><span class="sxs-lookup"><span data-stu-id="fe1a6-150">Al.exe (Assembly Linker)</span></span>](../../framework/tools/al-exe-assembly-linker.md)
- [<span data-ttu-id="fe1a6-151">延迟为程序集签名</span><span class="sxs-lookup"><span data-stu-id="fe1a6-151">Delay-sign an assembly</span></span>](delay-sign.md)
- [<span data-ttu-id="fe1a6-152">管理程序集和清单签名</span><span class="sxs-lookup"><span data-stu-id="fe1a6-152">Manage assembly and manifest signing</span></span>](/visualstudio/ide/managing-assembly-and-manifest-signing)
- [<span data-ttu-id="fe1a6-153">项目设计器的“签名”页</span><span class="sxs-lookup"><span data-stu-id="fe1a6-153">Signing page, Project Designer</span></span>](/visualstudio/ide/reference/signing-page-project-designer)
