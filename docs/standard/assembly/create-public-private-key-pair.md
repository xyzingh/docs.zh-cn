---
title: 如何：创建公钥/私钥对
description: 了解如何创建加密的公钥和私钥对，该公钥和私钥对用于在编译过程中创建强名称程序集。
ms.date: 08/20/2019
helpviewer_keywords:
- key pairs for strong-named assemblies
- signing assemblies
- assemblies [.NET], signing
- cryptographic key pairs
- snk files (key pair files)
- public-private key pairs
- .snk files
- strong-named assemblies, key pairs
ms.assetid: 05026813-f3bd-4d7c-9e0b-fc588eb3d114
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: c42e98a7e27ded9a21445fae35ade843e834076a
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163488"
---
# <a name="how-to-create-a-public-private-key-pair"></a><span data-ttu-id="9eb10-103">如何：创建公钥/私钥对</span><span class="sxs-lookup"><span data-stu-id="9eb10-103">How to: Create a public-private key pair</span></span>

<span data-ttu-id="9eb10-104">若要使用强名称为程序集签名，必须具有公钥/私钥对。</span><span class="sxs-lookup"><span data-stu-id="9eb10-104">To sign an assembly with a strong name, you must have a public/private key pair.</span></span> <span data-ttu-id="9eb10-105">这一对加密的公钥和私钥用于在编译过程中创建强名称程序集。</span><span class="sxs-lookup"><span data-stu-id="9eb10-105">This public and private cryptographic key pair is used during compilation to create a strong-named assembly.</span></span> <span data-ttu-id="9eb10-106">可以使用[强名称工具 (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) 创建密钥对。</span><span class="sxs-lookup"><span data-stu-id="9eb10-106">You can create a key pair using the [Strong Name tool (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md).</span></span> <span data-ttu-id="9eb10-107">密钥对文件通常具有 .snk 扩展名。</span><span class="sxs-lookup"><span data-stu-id="9eb10-107">Key pair files usually have an *.snk* extension.</span></span>

> [!NOTE]
> <span data-ttu-id="9eb10-108">在 Visual Studio 中，C# 和 Visual Basic 项目属性页包括“签名”选项卡，通过该选项卡，无需使用 Sn.exe 即可选择现有密钥文件或生成新密钥文件。</span><span class="sxs-lookup"><span data-stu-id="9eb10-108">In Visual Studio, the C# and Visual Basic project property pages include a **Signing** tab that enables you to select existing key files or to generate new key files without using *Sn.exe*.</span></span> <span data-ttu-id="9eb10-109">在 Visual C++ 中，可以在“属性页”窗口的“配置属性”部分的“链接器”部分中，在“高级”属性页中指定现有密钥文件的位置。</span><span class="sxs-lookup"><span data-stu-id="9eb10-109">In Visual C++, you can specify the location of an existing key file in the **Advanced** property page in the **Linker** section of the **Configuration Properties** section of the **Property Pages** window.</span></span> <span data-ttu-id="9eb10-110">从 Visual Studio 2005 开始，使用 <xref:System.Reflection.AssemblyKeyFileAttribute> 属性标识密钥文件对的方法已过时。</span><span class="sxs-lookup"><span data-stu-id="9eb10-110">The use of the <xref:System.Reflection.AssemblyKeyFileAttribute> attribute to identify key file pairs was made obsolete beginning with Visual Studio 2005.</span></span>

## <a name="create-a-key-pair"></a><span data-ttu-id="9eb10-111">创建密钥对</span><span class="sxs-lookup"><span data-stu-id="9eb10-111">Create a key pair</span></span>

<span data-ttu-id="9eb10-112">要创建密钥对，请在命令提示符处键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="9eb10-112">To create a key pair, at a command prompt, type the following command:</span></span>

<span data-ttu-id="9eb10-113">sn –k \<*file name*></span><span class="sxs-lookup"><span data-stu-id="9eb10-113">**sn –k** \<*file name*></span></span>

<span data-ttu-id="9eb10-114">此命令中，“文件名”是包含密钥对的输出文件的名称。</span><span class="sxs-lookup"><span data-stu-id="9eb10-114">In this command, *file name* is the name of the output file containing the key pair.</span></span>

<span data-ttu-id="9eb10-115">以下示例创建名为 sgKey.snk 的密钥对。</span><span class="sxs-lookup"><span data-stu-id="9eb10-115">The following example creates a key pair called *sgKey.snk*.</span></span>

```cmd
sn -k sgKey.snk
```

<span data-ttu-id="9eb10-116">如果打算延迟为程序集签名并控制整个密钥对（密钥对不太可能在测试方案之外），可使用以下命令生成密钥对，然后从中将公钥提取到一个单独的文件中。</span><span class="sxs-lookup"><span data-stu-id="9eb10-116">If you intend to delay sign an assembly and you control the whole key pair (which is unlikely outside test scenarios), you can use the following commands to generate a key pair and then extract the public key from it into a separate file.</span></span> <span data-ttu-id="9eb10-117">首先，创建密钥对：</span><span class="sxs-lookup"><span data-stu-id="9eb10-117">First, create the key pair:</span></span>

```cmd
sn -k keypair.snk
```

<span data-ttu-id="9eb10-118">接下来，从密钥对中提取公钥，并将其复制到一个单独的文件中：</span><span class="sxs-lookup"><span data-stu-id="9eb10-118">Next, extract the public key from the key pair and copy it to a separate file:</span></span>

```cmd
sn -p keypair.snk public.snk
```

<span data-ttu-id="9eb10-119">创建密钥对之后，必须将文件放在强名称签名工具可以找到的位置。</span><span class="sxs-lookup"><span data-stu-id="9eb10-119">Once you create the key pair, you must put the file where the strong name signing tools can find it.</span></span>

<span data-ttu-id="9eb10-120">当使用强名称对程序集进行签名时，[程序集链接器 (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) 查找与当前目录和输出目录相关的密钥文件。</span><span class="sxs-lookup"><span data-stu-id="9eb10-120">When signing an assembly with a strong name, the [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) looks for the key file relative to the current directory and to the output directory.</span></span> <span data-ttu-id="9eb10-121">当使用命令行编译器时，只需将密钥复制到包含代码模块的当前目录即可。</span><span class="sxs-lookup"><span data-stu-id="9eb10-121">When using command-line compilers, you can simply copy the key to the current directory containing your code modules.</span></span>

<span data-ttu-id="9eb10-122">如果使用 Visual Studio 的早期版本，且项目属性中没有“签名”选项卡，建议将具有如下指定文件属性的项目目录作为密钥文件位置：</span><span class="sxs-lookup"><span data-stu-id="9eb10-122">If you are using an earlier version of Visual Studio that does not have a **Signing** tab in the project properties, the recommended key file location is the project directory with the file attribute specified as follows:</span></span>

```cpp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")];
```

```csharp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")]
```

```vb
<Assembly:AssemblyKeyFileAttribute("keyfile.snk")>
```

## <a name="see-also"></a><span data-ttu-id="9eb10-123">请参阅</span><span class="sxs-lookup"><span data-stu-id="9eb10-123">See also</span></span>

- [<span data-ttu-id="9eb10-124">创建和使用具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="9eb10-124">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
