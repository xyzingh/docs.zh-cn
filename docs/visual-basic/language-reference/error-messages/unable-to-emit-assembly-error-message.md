---
title: 无法发出程序集：<error message>
ms.date: 08/14/2018
f1_keywords:
- vbc30145
- bc30145
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
ms.openlocfilehash: c088f273c100b1a7eefcf74047865093f378e970
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161655"
---
# <a name="bc30145-unable-to-emit-assembly-error-message"></a><span data-ttu-id="f8309-102">BC30145：无法发出程序集： \<error message></span><span class="sxs-lookup"><span data-stu-id="f8309-102">BC30145: Unable to emit assembly: \<error message></span></span>

<span data-ttu-id="f8309-103">Visual Basic 编译器调用程序集链接器 (*Al.exe*（也称为 Alink) ）以生成包含清单的程序集，并且链接器在创建该程序集的辐射阶段报告错误。</span><span class="sxs-lookup"><span data-stu-id="f8309-103">The Visual Basic compiler calls the Assembly Linker (*Al.exe*, also known as Alink) to generate an assembly with a manifest, and the linker reports an error in the emission stage of creating the assembly.</span></span>

<span data-ttu-id="f8309-104">**错误 ID：** BC30145</span><span class="sxs-lookup"><span data-stu-id="f8309-104">**Error ID:** BC30145</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="f8309-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="f8309-105">To correct this error</span></span>

1. <span data-ttu-id="f8309-106">检查引用的错误消息并参考主题 [Al.exe](../../../framework/tools/al-exe-assembly-linker.md) 以获取进一步的说明和建议。</span><span class="sxs-lookup"><span data-stu-id="f8309-106">Examine the quoted error message and consult the topic [Al.exe](../../../framework/tools/al-exe-assembly-linker.md) for further explanation and advice.</span></span>

2. <span data-ttu-id="f8309-107">尝试使用 [Al.exe](../../../framework/tools/al-exe-assembly-linker.md) 或 [Sn.exe (强名称工具) ](../../../framework/tools/sn-exe-strong-name-tool.md)，手动对程序集进行签名。</span><span class="sxs-lookup"><span data-stu-id="f8309-107">Try signing the assembly manually, using either the [Al.exe](../../../framework/tools/al-exe-assembly-linker.md) or the [Sn.exe (Strong Name Tool)](../../../framework/tools/sn-exe-strong-name-tool.md).</span></span>

3. <span data-ttu-id="f8309-108">如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。</span><span class="sxs-lookup"><span data-stu-id="f8309-108">If the error persists, gather information about the circumstances and notify Microsoft Product Support Services.</span></span>

### <a name="to-sign-the-assembly-manually"></a><span data-ttu-id="f8309-109">手动对程序集进行签名</span><span class="sxs-lookup"><span data-stu-id="f8309-109">To sign the assembly manually</span></span>

1. <span data-ttu-id="f8309-110">使用 [Sn.exe (强名称工具) ](../../../framework/tools/sn-exe-strong-name-tool.md)) 来创建公钥/私钥对文件。</span><span class="sxs-lookup"><span data-stu-id="f8309-110">Use the [Sn.exe (Strong Name Tool)](../../../framework/tools/sn-exe-strong-name-tool.md)) to create a public/private key pair file.</span></span>

   <span data-ttu-id="f8309-111">此文件的扩展名为 *.snk* 。</span><span class="sxs-lookup"><span data-stu-id="f8309-111">This file has an *.snk* extension.</span></span>

2. <span data-ttu-id="f8309-112">从项目中删除生成错误的 COM 引用。</span><span class="sxs-lookup"><span data-stu-id="f8309-112">Delete the COM reference that is generating the error from your project.</span></span>

3. <span data-ttu-id="f8309-113">打开 [Visual Studio 的开发人员命令提示](../../../framework/tools/developer-command-prompt-for-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="f8309-113">Open the [Developer Command Prompt for Visual Studio](../../../framework/tools/developer-command-prompt-for-vs.md).</span></span>

   <span data-ttu-id="f8309-114">在 Windows 10 中，在任务栏上的搜索框中输入 " **开发人员命令提示** "。</span><span class="sxs-lookup"><span data-stu-id="f8309-114">In Windows 10, enter **Developer command prompt** into the search box on the task bar.</span></span> <span data-ttu-id="f8309-115">然后，从结果列表中选择 **VS 2017 开发人员命令提示** 。</span><span class="sxs-lookup"><span data-stu-id="f8309-115">Then, select **Developer Command Prompt for VS 2017** from the results list.</span></span>

4. <span data-ttu-id="f8309-116">将目录更改为要在其中放置程序集包装的目录。</span><span class="sxs-lookup"><span data-stu-id="f8309-116">Change the directory to the directory where you want to place your assembly wrapper.</span></span>

5. <span data-ttu-id="f8309-117">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f8309-117">Enter the following command:</span></span>

    ```cmd
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>
    ```

   <span data-ttu-id="f8309-118">你可能会输入的实际命令的示例如下：</span><span class="sxs-lookup"><span data-stu-id="f8309-118">An example of the actual command you might enter is:</span></span>

    ```cmd
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"
    ```

   > [!TIP]
   > <span data-ttu-id="f8309-119">如果路径或文件包含空格，请使用双引号。</span><span class="sxs-lookup"><span data-stu-id="f8309-119">Use double quotation marks if a path or file contains spaces.</span></span>

6. <span data-ttu-id="f8309-120">在 Visual Studio 中，将 .NET 程序集引用添加到刚创建的文件。</span><span class="sxs-lookup"><span data-stu-id="f8309-120">In Visual Studio, add a .NET Assembly reference to the file you just created.</span></span>

## <a name="see-also"></a><span data-ttu-id="f8309-121">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f8309-121">See also</span></span>

- [<span data-ttu-id="f8309-122">Al.exe</span><span class="sxs-lookup"><span data-stu-id="f8309-122">Al.exe</span></span>](../../../framework/tools/al-exe-assembly-linker.md)
- [<span data-ttu-id="f8309-123">Sn.exe（强名称工具）</span><span class="sxs-lookup"><span data-stu-id="f8309-123">Sn.exe (Strong Name Tool)</span></span>](../../../framework/tools/sn-exe-strong-name-tool.md)
- [<span data-ttu-id="f8309-124">如何：创建公钥/私钥对</span><span class="sxs-lookup"><span data-stu-id="f8309-124">How to: Create a Public-Private Key Pair</span></span>](../../../standard/assembly/create-public-private-key-pair.md)
- [<span data-ttu-id="f8309-125">与我们交流</span><span class="sxs-lookup"><span data-stu-id="f8309-125">Talk to Us</span></span>](/visualstudio/ide/feedback-options)
