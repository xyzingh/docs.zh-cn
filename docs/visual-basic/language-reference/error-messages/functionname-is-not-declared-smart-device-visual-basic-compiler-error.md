---
title: 未声明“<functionname>”（智能设备-Visual Basic 编译器错误）
ms.date: 07/20/2015
f1_keywords:
- bc30766
- vbc30766
helpviewer_keywords:
- BC30766
ms.assetid: 13918600-6087-40d7-8134-32aa9d3bfda4
ms.openlocfilehash: 1c57e1aaea2eb52133d37b782f8fa0ddd96943a9
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163397"
---
# <a name="bc30766-functionname-is-not-declared-smart-devicevisual-basic-compiler-error"></a><span data-ttu-id="76712-102">BC30766： " \<functionname> " 未声明 (智能设备/Visual Basic 编译器错误) </span><span class="sxs-lookup"><span data-stu-id="76712-102">BC30766: '\<functionname>' is not declared (Smart Device/Visual Basic Compiler Error)</span></span>

<span data-ttu-id="76712-103"><`functionname` 未声明>。</span><span class="sxs-lookup"><span data-stu-id="76712-103"><`functionname`> is not declared.</span></span> <span data-ttu-id="76712-104">文件 I/O 功能在 `Microsoft.VisualBasic` 命名空间中通常是可用的，但目标版本的 .NET Compact Framewor 不支持它。</span><span class="sxs-lookup"><span data-stu-id="76712-104">File I/O functionality is normally available in the `Microsoft.VisualBasic` namespace, but the targeted version of the .NET Compact Framework does not support it.</span></span>

 <span data-ttu-id="76712-105">**错误 ID：** BC30766</span><span class="sxs-lookup"><span data-stu-id="76712-105">**Error ID:** BC30766</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="76712-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="76712-106">To correct this error</span></span>

- <span data-ttu-id="76712-107">利用 `System.IO` 命名空间中定义的函数执行文件操作。</span><span class="sxs-lookup"><span data-stu-id="76712-107">Perform file operations with functions defined in the `System.IO` namespace.</span></span>

## <a name="see-also"></a><span data-ttu-id="76712-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="76712-108">See also</span></span>

- <xref:System.IO>
- [<span data-ttu-id="76712-109">使用 Visual Basic 访问文件</span><span class="sxs-lookup"><span data-stu-id="76712-109">File Access with Visual Basic</span></span>](../../developing-apps/programming/drives-directories-files/file-access.md)
