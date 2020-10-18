---
title: 类型“<typename>”的“For Each”不明确，因为此类型实现了“System.Collections.Generic.IEnumerable(Of T)”的多个实例化
ms.date: 07/20/2015
f1_keywords:
- vbc32096
- bc32096
helpviewer_keywords:
- BC32096
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
ms.openlocfilehash: 0f19836efeabcf1d9e5097667c719c1f7d99cbbb
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163462"
---
# <a name="bc32096-for-each-on-type-typename-is-ambiguous-because-the-type-implements-multiple-instantiations-of-systemcollectionsgenericienumerableof-t"></a><span data-ttu-id="d797a-102">类型 "" 的 BC32096： "" \<typename> 不明确，因为该类型实现 ("的多个实例化，而 T) "</span><span class="sxs-lookup"><span data-stu-id="d797a-102">BC32096: 'For Each' on type '\<typename>' is ambiguous because the type implements multiple instantiations of 'System.Collections.Generic.IEnumerable(Of T)'</span></span>

<span data-ttu-id="d797a-103">`For Each`语句指定具有多个方法的迭代器变量 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 。</span><span class="sxs-lookup"><span data-stu-id="d797a-103">A `For Each` statement specifies an iterator variable that has more than one <xref:System.Collections.IEnumerable.GetEnumerator%2A> method.</span></span>

 <span data-ttu-id="d797a-104">迭代器变量必须是在 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> .NET Framework 的命名空间之一中实现或接口的类型 `Collections` 。</span><span class="sxs-lookup"><span data-stu-id="d797a-104">The iterator variable must be of a type that implements the <xref:System.Collections.IEnumerable?displayProperty=nameWithType> or <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> interface in one of the `Collections` namespaces of the .NET Framework.</span></span> <span data-ttu-id="d797a-105">类可以实现多个构造泛型接口，每个构造使用不同的类型参数。</span><span class="sxs-lookup"><span data-stu-id="d797a-105">It is possible for a class to implement more than one constructed generic interface, using a different type argument for each construction.</span></span> <span data-ttu-id="d797a-106">如果用于执行此的类用于迭代器变量，则该变量有多种 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="d797a-106">If a class that does this is used for the iterator variable, that variable has more than one <xref:System.Collections.IEnumerable.GetEnumerator%2A> method.</span></span> <span data-ttu-id="d797a-107">在这种情况下，Visual Basic 无法选择要调用的方法。</span><span class="sxs-lookup"><span data-stu-id="d797a-107">In such a case, Visual Basic cannot choose which method to call.</span></span>

 <span data-ttu-id="d797a-108">**错误 ID：** BC32096</span><span class="sxs-lookup"><span data-stu-id="d797a-108">**Error ID:** BC32096</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="d797a-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="d797a-109">To correct this error</span></span>

- <span data-ttu-id="d797a-110">使用 [DirectCast 运算符](../operators/directcast-operator.md) 或 [TryCast 运算符](../operators/trycast-operator.md) 将迭代器变量类型强制转换为定义 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 要使用的方法的接口。</span><span class="sxs-lookup"><span data-stu-id="d797a-110">Use [DirectCast Operator](../operators/directcast-operator.md) or [TryCast Operator](../operators/trycast-operator.md) to cast the iterator variable type to the interface defining the <xref:System.Collections.IEnumerable.GetEnumerator%2A> method you want to use.</span></span>

## <a name="see-also"></a><span data-ttu-id="d797a-111">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d797a-111">See also</span></span>

- [<span data-ttu-id="d797a-112">For Each...Next 语句</span><span class="sxs-lookup"><span data-stu-id="d797a-112">For Each...Next Statement</span></span>](../statements/for-each-next-statement.md)
- [<span data-ttu-id="d797a-113">接口</span><span class="sxs-lookup"><span data-stu-id="d797a-113">Interfaces</span></span>](../../programming-guide/language-features/interfaces/index.md)
