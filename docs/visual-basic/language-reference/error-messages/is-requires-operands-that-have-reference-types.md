---
title: “Is”要求具有引用类型的操作数，但此操作数的值类型为“<typename>”。
ms.date: 07/20/2015
f1_keywords:
- bc30020
- vbc30020
helpviewer_keywords:
- BC30020
ms.assetid: 228afebd-1203-4bd3-8d7a-c5c56f3cedc4
ms.openlocfilehash: 5c9f156272cd0c3cbaeadbc0e162129f41619cc6
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163345"
---
# <a name="bc30020-is-requires-operands-that-have-reference-types-but-this-operand-has-the-value-type-typename"></a><span data-ttu-id="98e86-102">BC30020： "Is" 需要具有引用类型的操作数，但此操作数的值类型为 " \<typename> "</span><span class="sxs-lookup"><span data-stu-id="98e86-102">BC30020: 'Is' requires operands that have reference types, but this operand has the value type '\<typename>'</span></span>

<span data-ttu-id="98e86-103">`Is`比较运算符确定两个对象变量是否引用相同的实例。</span><span class="sxs-lookup"><span data-stu-id="98e86-103">The `Is` comparison operator determines whether two object variables refer to the same instance.</span></span> <span data-ttu-id="98e86-104">没有为值类型定义此比较。</span><span class="sxs-lookup"><span data-stu-id="98e86-104">This comparison is not defined for value types.</span></span>

 <span data-ttu-id="98e86-105">**错误 ID：** BC30020</span><span class="sxs-lookup"><span data-stu-id="98e86-105">**Error ID:** BC30020</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="98e86-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="98e86-106">To correct this error</span></span>

- <span data-ttu-id="98e86-107">使用适当的算术比较运算符或 `Like` 运算符比较两个值类型。</span><span class="sxs-lookup"><span data-stu-id="98e86-107">Use the appropriate arithmetic comparison operator or the `Like` operator to compare two value types.</span></span>

## <a name="see-also"></a><span data-ttu-id="98e86-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="98e86-108">See also</span></span>

- [<span data-ttu-id="98e86-109">Is 运算符</span><span class="sxs-lookup"><span data-stu-id="98e86-109">Is Operator</span></span>](../operators/is-operator.md)
- [<span data-ttu-id="98e86-110">Like 运算符</span><span class="sxs-lookup"><span data-stu-id="98e86-110">Like Operator</span></span>](../operators/like-operator.md)
- [<span data-ttu-id="98e86-111">比较运算符</span><span class="sxs-lookup"><span data-stu-id="98e86-111">Comparison Operators</span></span>](../operators/comparison-operators.md)
