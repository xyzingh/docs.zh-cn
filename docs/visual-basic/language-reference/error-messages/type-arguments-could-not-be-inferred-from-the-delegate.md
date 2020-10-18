---
title: 未能从委托中推理类型参数
ms.date: 07/20/2015
f1_keywords:
- bc36564
- vbc36564
helpviewer_keywords:
- BC36564
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
ms.openlocfilehash: f7937a34ab425da684f892250884d21e020e4c57
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161239"
---
# <a name="bc36564-type-arguments-could-not-be-inferred-from-the-delegate"></a><span data-ttu-id="a8a33-102">BC36564：无法从委托推断类型参数</span><span class="sxs-lookup"><span data-stu-id="a8a33-102">BC36564: Type arguments could not be inferred from the delegate</span></span>

<span data-ttu-id="a8a33-103">赋值语句使用 `AddressOf` 将泛型过程的地址赋给委托，但它不会为泛型过程提供任何类型参数。</span><span class="sxs-lookup"><span data-stu-id="a8a33-103">An assignment statement uses `AddressOf` to assign the address of a generic procedure to a delegate, but it does not supply any type arguments to the generic procedure.</span></span>

 <span data-ttu-id="a8a33-104">通常，在调用某个泛型类型时，要为该泛型类型定义的每个类型形参提供一个类型实参。</span><span class="sxs-lookup"><span data-stu-id="a8a33-104">Normally, when you invoke a generic type, you supply a type argument for each type parameter that the generic type defines.</span></span> <span data-ttu-id="a8a33-105">如果未提供任何类型实参，编译器将尝试推断要传递给类型形参的类型。</span><span class="sxs-lookup"><span data-stu-id="a8a33-105">If you do not supply any type arguments, the compiler attempts to infer the types to be passed to the type parameters.</span></span> <span data-ttu-id="a8a33-106">如果上下文未提供充足的信息供编译器推断类型，则将生成错误。</span><span class="sxs-lookup"><span data-stu-id="a8a33-106">If the context does not provide enough information for the compiler to infer the types, an error is generated.</span></span>

 <span data-ttu-id="a8a33-107">**错误 ID：** BC36564</span><span class="sxs-lookup"><span data-stu-id="a8a33-107">**Error ID:** BC36564</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="a8a33-108">更正此错误</span><span class="sxs-lookup"><span data-stu-id="a8a33-108">To correct this error</span></span>

- <span data-ttu-id="a8a33-109">为 `AddressOf` 表达式中的泛型过程指定类型参数。</span><span class="sxs-lookup"><span data-stu-id="a8a33-109">Specify the type arguments for the generic procedure in the `AddressOf` expression.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8a33-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a8a33-110">See also</span></span>

- [<span data-ttu-id="a8a33-111">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="a8a33-111">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
- [<span data-ttu-id="a8a33-112">AddressOf 运算符</span><span class="sxs-lookup"><span data-stu-id="a8a33-112">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="a8a33-113">Generic Procedures in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="a8a33-113">Generic Procedures in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-procedures.md)
- [<span data-ttu-id="a8a33-114">Type List</span><span class="sxs-lookup"><span data-stu-id="a8a33-114">Type List</span></span>](../statements/type-list.md)
- [<span data-ttu-id="a8a33-115">扩展方法</span><span class="sxs-lookup"><span data-stu-id="a8a33-115">Extension Methods</span></span>](../../programming-guide/language-features/procedures/extension-methods.md)
