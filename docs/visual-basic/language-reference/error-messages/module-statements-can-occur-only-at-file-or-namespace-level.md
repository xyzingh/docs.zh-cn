---
title: “Module”语句只能出现在文件级或命名空间级
ms.date: 07/20/2015
f1_keywords:
- bc30617
- vbc30617
helpviewer_keywords:
- BC30617
ms.assetid: 5e9de8e5-d26b-4fb2-9e28-814413fe9cef
ms.openlocfilehash: b946a527d3de3a030ac03691c77afcf440f518ee
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160309"
---
# <a name="bc30617-module-statements-can-occur-only-at-file-or-namespace-level"></a><span data-ttu-id="d2e0d-102">BC30617： "Module" 语句只能出现在文件级或命名空间级</span><span class="sxs-lookup"><span data-stu-id="d2e0d-102">BC30617: 'Module' statements can occur only at file or namespace level</span></span>

<span data-ttu-id="d2e0d-103">`Module` 语句必须紧跟在 `Option` 和 `Imports` 语句、全局特性和命名空间声明之后、但在其他所有声明之前。</span><span class="sxs-lookup"><span data-stu-id="d2e0d-103">`Module` statements must appear at the top of your source file immediately after `Option` and `Imports` statements, global attributes, and namespace declarations, but before all other declarations.</span></span>

 <span data-ttu-id="d2e0d-104">**错误 ID：** BC30617</span><span class="sxs-lookup"><span data-stu-id="d2e0d-104">**Error ID:** BC30617</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="d2e0d-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="d2e0d-105">To correct this error</span></span>

- <span data-ttu-id="d2e0d-106">将 `Module` 语句移动到命名空间声明或源文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="d2e0d-106">Move the `Module` statement to the top of your namespace declaration or source file.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2e0d-107">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d2e0d-107">See also</span></span>

- [<span data-ttu-id="d2e0d-108">Module 语句</span><span class="sxs-lookup"><span data-stu-id="d2e0d-108">Module Statement</span></span>](../statements/module-statement.md)
