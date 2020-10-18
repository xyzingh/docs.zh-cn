---
title: “#Region”和“#End Region”语句在方法体/多行 lambda 内无效
ms.date: 07/20/2015
f1_keywords:
- bc32025
- vbc32025
helpviewer_keywords:
- BC32025
ms.assetid: 43707bf1-1c6b-4d82-b081-e5a17dca51c1
ms.openlocfilehash: c792fa1a42bde22959ae21439cb2a0a1e4be343f
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162279"
---
# <a name="bc32025-region-and-end-region-statements-are-not-valid-within-method-bodiesmultiline-lambdas"></a><span data-ttu-id="f6cf0-102">BC32025： "#Region" 和 "#End Region" 语句在方法体/多行 lambda 内无效</span><span class="sxs-lookup"><span data-stu-id="f6cf0-102">BC32025: '#Region' and '#End Region' statements are not valid within method bodies/multiline lambdas</span></span>

<span data-ttu-id="f6cf0-103">`#Region`必须在类、模块或命名空间级别声明块。</span><span class="sxs-lookup"><span data-stu-id="f6cf0-103">The `#Region` block must be declared at a class, module, or namespace level.</span></span> <span data-ttu-id="f6cf0-104">可折叠区域可以包含一个或多个过程，但不能在过程中开始或结束。</span><span class="sxs-lookup"><span data-stu-id="f6cf0-104">A collapsible region can include one or more procedures, but it cannot begin or end inside of a procedure.</span></span>

 <span data-ttu-id="f6cf0-105">**错误 ID：** BC32025</span><span class="sxs-lookup"><span data-stu-id="f6cf0-105">**Error ID:** BC32025</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="f6cf0-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="f6cf0-106">To correct this error</span></span>

1. <span data-ttu-id="f6cf0-107">确保使用或语句正确终止前面的过程 `End Function` `End Sub` 。</span><span class="sxs-lookup"><span data-stu-id="f6cf0-107">Ensure that the preceding procedure is properly terminated with an `End Function` or `End Sub` statement.</span></span>

2. <span data-ttu-id="f6cf0-108">确保 `#Region` 和 `#End Region` 指令位于同一个代码块中。</span><span class="sxs-lookup"><span data-stu-id="f6cf0-108">Ensure that the `#Region` and `#End Region` directives are in the same code block.</span></span>

## <a name="see-also"></a><span data-ttu-id="f6cf0-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f6cf0-109">See also</span></span>

- [<span data-ttu-id="f6cf0-110">#Region 指令</span><span class="sxs-lookup"><span data-stu-id="f6cf0-110">#Region Directive</span></span>](../directives/region-directive.md)
