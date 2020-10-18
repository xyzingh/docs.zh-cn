---
title: 方法没有与委托兼容的签名
ms.date: 07/20/2015
f1_keywords:
- bc36563
- vbc36563
helpviewer_keywords:
- BC36563
ms.assetid: 3ca8b873-e98d-419b-95f2-d75bd2a9eb6c
ms.openlocfilehash: 62801552a39d29983c322e9a95a0494f155a2633
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160413"
---
# <a name="bc36563-method-does-not-have-a-signature-compatible-with-the-delegate"></a><span data-ttu-id="b52f9-102">BC36563：方法没有与委托兼容的签名</span><span class="sxs-lookup"><span data-stu-id="b52f9-102">BC36563: Method does not have a signature compatible with the delegate</span></span>

<span data-ttu-id="b52f9-103">方法的签名与你尝试使用的委托的签名不兼容。</span><span class="sxs-lookup"><span data-stu-id="b52f9-103">There is an incompatibility between the signatures of the method and the delegate you are trying to use.</span></span> <span data-ttu-id="b52f9-104">`Delegate` 语句定义参数类型和委托类的返回类型。</span><span class="sxs-lookup"><span data-stu-id="b52f9-104">The `Delegate` statement defines the parameter types and return types of a delegate class.</span></span> <span data-ttu-id="b52f9-105">任何具有匹配的兼容类型参数和返回类型的过程都可以用于创建此委托类型的实例。</span><span class="sxs-lookup"><span data-stu-id="b52f9-105">Any procedure that has matching parameters of compatible types and return types can be used to create an instance of this delegate type.</span></span>

 <span data-ttu-id="b52f9-106">**错误 ID：** BC36563</span><span class="sxs-lookup"><span data-stu-id="b52f9-106">**Error ID:** BC36563</span></span>

## <a name="see-also"></a><span data-ttu-id="b52f9-107">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b52f9-107">See also</span></span>

- [<span data-ttu-id="b52f9-108">AddressOf 运算符</span><span class="sxs-lookup"><span data-stu-id="b52f9-108">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="b52f9-109">Delegate 语句</span><span class="sxs-lookup"><span data-stu-id="b52f9-109">Delegate Statement</span></span>](../statements/delegate-statement.md)
- [<span data-ttu-id="b52f9-110">重载决策</span><span class="sxs-lookup"><span data-stu-id="b52f9-110">Overload Resolution</span></span>](../../programming-guide/language-features/procedures/overload-resolution.md)
- [<span data-ttu-id="b52f9-111">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="b52f9-111">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
