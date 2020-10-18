---
title: 语句不能在“If”语句行之外结束块
ms.date: 07/20/2015
f1_keywords:
- vbc32005
- bc32005
helpviewer_keywords:
- BC32005
ms.assetid: 4039f51b-e0ee-4789-a89b-45d06de06b5d
ms.openlocfilehash: 4fd7577accd0b312ee1e3d2d990d256514d5f5f6
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161330"
---
# <a name="bc32005-statement-cannot-end-a-block-outside-of-a-line-if-statement"></a><span data-ttu-id="2163e-102">BC32005：语句不能在行 "If" 语句外结束块</span><span class="sxs-lookup"><span data-stu-id="2163e-102">BC32005: Statement cannot end a block outside of a line 'If' statement</span></span>

<span data-ttu-id="2163e-103">单行 `If` 语句包含用冒号分隔的多个语句 (： ) ，其中一个语句 `End` 用于单个行外的控制块 `If` 。</span><span class="sxs-lookup"><span data-stu-id="2163e-103">A single-line `If` statement contains several statements separated by colons (:), one of which is an `End` statement for a control block outside the single-line `If`.</span></span> <span data-ttu-id="2163e-104">单行 `If` 语句不使用 `End If` 语句。</span><span class="sxs-lookup"><span data-stu-id="2163e-104">Single-line `If` statements do not use the `End If` statement.</span></span>

 <span data-ttu-id="2163e-105">**错误 ID：** BC32005</span><span class="sxs-lookup"><span data-stu-id="2163e-105">**Error ID:** BC32005</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="2163e-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="2163e-106">To correct this error</span></span>

- <span data-ttu-id="2163e-107">在 `If` 包含语句的控制块外移动单行语句 `End If` 。</span><span class="sxs-lookup"><span data-stu-id="2163e-107">Move the single-line `If` statement outside the control block that contains the `End If` statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="2163e-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2163e-108">See also</span></span>

- [<span data-ttu-id="2163e-109">If...Then...Else 语句</span><span class="sxs-lookup"><span data-stu-id="2163e-109">If...Then...Else Statement</span></span>](../statements/if-then-else-statement.md)
