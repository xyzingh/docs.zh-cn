---
description: continue 语句 - C# 参考
title: continue 语句 - C# 参考
ms.date: 07/20/2015
f1_keywords:
- continue_CSharpKeyword
- continue
helpviewer_keywords:
- continue keyword [C#]
ms.assetid: 8a5ac96f-f98a-4519-b32d-345847ed7be0
ms.openlocfilehash: 6c70934c3b861e1a1433e5c0b95bb32e9d717c53
ms.sourcegitcommit: eb7e87496f42361b1da98562dd75b516c9d58bbc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91877647"
---
# <a name="continue-c-reference"></a><span data-ttu-id="947bb-103">continue（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="947bb-103">continue (C# Reference)</span></span>

<span data-ttu-id="947bb-104">`continue` 语句将控制传递到其中出现的封闭 [while](./while.md)、[do](./do.md)、[for](./for.md) 或 [foreach](./foreach-in.md) 语句的下一次迭代。</span><span class="sxs-lookup"><span data-stu-id="947bb-104">The `continue` statement passes control to the next iteration of the enclosing [while](./while.md), [do](./do.md), [for](./for.md), or [foreach](./foreach-in.md) statement in which it appears.</span></span>

## <a name="example"></a><span data-ttu-id="947bb-105">示例</span><span class="sxs-lookup"><span data-stu-id="947bb-105">Example</span></span>

<span data-ttu-id="947bb-106">在本示例中，计数器最初是从 1 到 10 进行计数。</span><span class="sxs-lookup"><span data-stu-id="947bb-106">In this example, a counter is initialized to count from 1 to 10.</span></span> <span data-ttu-id="947bb-107">通过结合使用 `continue` 语句和表达式 `(i < 9)`，在 `i` 小于 9 的迭代中跳过 `continue` 和 `for` 主体末尾之间的语句。</span><span class="sxs-lookup"><span data-stu-id="947bb-107">By using the `continue` statement in conjunction with the expression `(i < 9)`, the statements between `continue` and the end of the `for` body are skipped in the iterations where `i` is less than 9.</span></span> <span data-ttu-id="947bb-108">在 `for` 循环的最后两次迭代（其中 i == 9，i == 10）中，不执行 `continue` 语句，且 `i` 的值将输出到控制台。</span><span class="sxs-lookup"><span data-stu-id="947bb-108">In the last two iterations of the `for` loop (where i == 9 and i == 10), the `continue` statement is not executed and the value of `i` is printed to the console.</span></span>

[!code-csharp[csrefKeywordsJump#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#3)]

## <a name="c-language-specification"></a><span data-ttu-id="947bb-109">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="947bb-109">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="947bb-110">请参阅</span><span class="sxs-lookup"><span data-stu-id="947bb-110">See also</span></span>

- [<span data-ttu-id="947bb-111">C# 参考</span><span class="sxs-lookup"><span data-stu-id="947bb-111">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="947bb-112">C# 编程指南</span><span class="sxs-lookup"><span data-stu-id="947bb-112">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="947bb-113">C# 关键字</span><span class="sxs-lookup"><span data-stu-id="947bb-113">C# Keywords</span></span>](./index.md)
- [<span data-ttu-id="947bb-114">break 语句</span><span class="sxs-lookup"><span data-stu-id="947bb-114">break Statement</span></span>](/cpp/cpp/break-statement-cpp)
