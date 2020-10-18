---
title: 表达式不产生值
ms.date: 07/20/2015
f1_keywords:
- vbc30491
- bc30491
helpviewer_keywords:
- BC30491
ms.assetid: 8399d7ae-bc0a-49e6-81dc-2e7229708bc9
ms.openlocfilehash: f48159d91afef1f5d1b19dce5b0d2262cdab082f
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163072"
---
# <a name="bc30491-expression-does-not-produce-a-value"></a><span data-ttu-id="4f3d0-102">BC30491：表达式不生成值</span><span class="sxs-lookup"><span data-stu-id="4f3d0-102">BC30491: Expression does not produce a value</span></span>

<span data-ttu-id="4f3d0-103">您尝试使用的表达式不在生成值的上下文中生成值，如 `Sub` 在所需的上下文中调用 `Function` 。</span><span class="sxs-lookup"><span data-stu-id="4f3d0-103">You have tried to use an expression that does not produce a value in a value-producing context, such as calling a `Sub` in a context where a `Function` is expected.</span></span>

 <span data-ttu-id="4f3d0-104">**错误 ID：** BC30491</span><span class="sxs-lookup"><span data-stu-id="4f3d0-104">**Error ID:** BC30491</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="4f3d0-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="4f3d0-105">To correct this error</span></span>

- <span data-ttu-id="4f3d0-106">将表达式更改为一个生成值的表达式。</span><span class="sxs-lookup"><span data-stu-id="4f3d0-106">Change the expression to one that produces a value.</span></span>

## <a name="see-also"></a><span data-ttu-id="4f3d0-107">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4f3d0-107">See also</span></span>

- [<span data-ttu-id="4f3d0-108">错误类型</span><span class="sxs-lookup"><span data-stu-id="4f3d0-108">Error Types</span></span>](../../programming-guide/language-features/error-types.md)
