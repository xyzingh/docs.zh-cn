---
title: 前导“.”或“!”只能出现在“With”语句内
ms.date: 07/20/2015
f1_keywords:
- vbc30157
- bc30157
helpviewer_keywords:
- BC30157
ms.assetid: 70daaee1-14f9-45b7-9f30-53794310b95e
ms.openlocfilehash: 4ff273d5930fe58a5bccf0f4f4c10e971d777d01
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162500"
---
# <a name="bc30157-leading--or--can-only-appear-inside-a-with-statement"></a><span data-ttu-id="14fc0-102">BC30157：前导 "." 或 "！" 只能出现在 "With" 语句内</span><span class="sxs-lookup"><span data-stu-id="14fc0-102">BC30157: Leading '.' or '!' can only appear inside a 'With' statement</span></span>

<span data-ttu-id="14fc0-103">不在块内部的 ) 或惊叹号 (！ ) 的句点 ( 没有 `With` 左侧的表达式。</span><span class="sxs-lookup"><span data-stu-id="14fc0-103">A period (.) or exclamation point (!) that is not inside a `With` block occurs without an expression on the left.</span></span> <span data-ttu-id="14fc0-104">成员访问 (`.`) 和字典成员访问 (`!`) 要求一个表达式，该表达式指定包含成员的元素。</span><span class="sxs-lookup"><span data-stu-id="14fc0-104">Member access (`.`) and dictionary member access (`!`) require an expression specifying the element that contains the member.</span></span> <span data-ttu-id="14fc0-105">这必须立即出现在访问器的左侧，或作为 `With` 包含成员访问的块的目标。</span><span class="sxs-lookup"><span data-stu-id="14fc0-105">This must appear immediately to the left of the accessor or as the target of a `With` block containing the member access.</span></span>

 <span data-ttu-id="14fc0-106">**错误 ID：** BC30157</span><span class="sxs-lookup"><span data-stu-id="14fc0-106">**Error ID:** BC30157</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="14fc0-107">更正此错误</span><span class="sxs-lookup"><span data-stu-id="14fc0-107">To correct this error</span></span>

1. <span data-ttu-id="14fc0-108">确保块的 `With` 格式正确。</span><span class="sxs-lookup"><span data-stu-id="14fc0-108">Ensure that the `With` block is correctly formatted.</span></span>

2. <span data-ttu-id="14fc0-109">如果没有 `With` 块，请在取值函数左侧添加一个表达式，该表达式的计算结果为包含成员的已定义元素。</span><span class="sxs-lookup"><span data-stu-id="14fc0-109">If there is no `With` block, add an expression to the left of the accessor that evaluates to a defined element containing the member.</span></span>

## <a name="see-also"></a><span data-ttu-id="14fc0-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="14fc0-110">See also</span></span>

- [<span data-ttu-id="14fc0-111">代码中的特殊字符</span><span class="sxs-lookup"><span data-stu-id="14fc0-111">Special Characters in Code</span></span>](../../programming-guide/program-structure/special-characters-in-code.md)
- [<span data-ttu-id="14fc0-112">With...End With 语句</span><span class="sxs-lookup"><span data-stu-id="14fc0-112">With...End With Statement</span></span>](../statements/with-end-with-statement.md)
