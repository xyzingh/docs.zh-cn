---
title: “Extension”特性只能应用于“Module”、“Sub”或“Function”声明。
ms.date: 07/20/2015
f1_keywords:
- bc36550
- vbc36550
helpviewer_keywords:
- BC36550
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
ms.openlocfilehash: bd4d14721b93800831dbce897535b4f5956fe9c7
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160745"
---
# <a name="bc36550-extension-attribute-can-be-applied-only-to-module-sub-or-function-declarations"></a><span data-ttu-id="4eea1-102">BC36550： "Extension" 特性只能应用于 "Module"、"Sub" 或 "Function" 声明</span><span class="sxs-lookup"><span data-stu-id="4eea1-102">BC36550: 'Extension' attribute can be applied only to 'Module', 'Sub', or 'Function' declarations</span></span>

<span data-ttu-id="4eea1-103">在 Visual Basic 中扩展数据类型的唯一方法是在标准模块内定义扩展方法。</span><span class="sxs-lookup"><span data-stu-id="4eea1-103">The only way to extend a data type in Visual Basic is to define an extension method inside a standard module.</span></span> <span data-ttu-id="4eea1-104">扩展方法可以是 `Sub` 过程或 `Function` 过程。</span><span class="sxs-lookup"><span data-stu-id="4eea1-104">The extension method can be a `Sub` procedure or a `Function` procedure.</span></span> <span data-ttu-id="4eea1-105">必须用 `<Extension()>` 命名空间中的扩展属性标记所有扩展方法 <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="4eea1-105">All extension methods must be marked with the extension attribute, `<Extension()>`, from the <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="4eea1-106">或者，包含扩展方法的模块可以用相同的方式进行标记。</span><span class="sxs-lookup"><span data-stu-id="4eea1-106">Optionally, a module that contains an extension method may be marked in the same way.</span></span> <span data-ttu-id="4eea1-107">扩展属性的其他使用无效。</span><span class="sxs-lookup"><span data-stu-id="4eea1-107">No other use of the extension attribute is valid.</span></span>

<span data-ttu-id="4eea1-108">**错误 ID：** BC36550</span><span class="sxs-lookup"><span data-stu-id="4eea1-108">**Error ID:** BC36550</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="4eea1-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="4eea1-109">To correct this error</span></span>

- <span data-ttu-id="4eea1-110">删除扩展属性。</span><span class="sxs-lookup"><span data-stu-id="4eea1-110">Remove the extension attribute.</span></span>

- <span data-ttu-id="4eea1-111">将扩展重新设计为封闭模块中定义的方法。</span><span class="sxs-lookup"><span data-stu-id="4eea1-111">Redesign your extension as a method, defined in an enclosing module.</span></span>

## <a name="example"></a><span data-ttu-id="4eea1-112">示例</span><span class="sxs-lookup"><span data-stu-id="4eea1-112">Example</span></span>

<span data-ttu-id="4eea1-113">下面的示例定义了 `Print` `String` 数据类型的方法。</span><span class="sxs-lookup"><span data-stu-id="4eea1-113">The following example defines a `Print` method for the `String` data type.</span></span>

```vb
Imports StringUtility
Imports System.Runtime.CompilerServices
Namespace StringUtility
    <Extension()>
    Module StringExtensions
        <Extension()>
        Public Sub Print (ByVal str As String)
            Console.WriteLine(str)
        End Sub
    End Module
End Namespace
```

## <a name="see-also"></a><span data-ttu-id="4eea1-114">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4eea1-114">See also</span></span>

- [<span data-ttu-id="4eea1-115">属性概述</span><span class="sxs-lookup"><span data-stu-id="4eea1-115">Attributes overview</span></span>](../../programming-guide/concepts/attributes/index.md)
- [<span data-ttu-id="4eea1-116">扩展方法</span><span class="sxs-lookup"><span data-stu-id="4eea1-116">Extension Methods</span></span>](../../programming-guide/language-features/procedures/extension-methods.md)
- [<span data-ttu-id="4eea1-117">Module 语句</span><span class="sxs-lookup"><span data-stu-id="4eea1-117">Module Statement</span></span>](../statements/module-statement.md)
