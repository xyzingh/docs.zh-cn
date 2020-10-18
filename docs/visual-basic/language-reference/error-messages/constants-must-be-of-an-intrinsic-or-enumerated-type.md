---
title: 常量必须是内部类型或者枚举类型，不能是类、结构、类型参数或数组类型
ms.date: 07/20/2015
f1_keywords:
- vbc30424
- bc30424
helpviewer_keywords:
- BC30424
ms.assetid: 2d402c2f-27ad-428b-b699-d45cd62f7196
ms.openlocfilehash: e820287f0ddf462b30867d90501f7d730c9c6739
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163150"
---
# <a name="bc30424-constants-must-be-of-an-intrinsic-or-enumerated-type-not-a-class-structure-type-parameter-or-array-type"></a><span data-ttu-id="4433f-102">BC30424：常量必须是内部类型或枚举类型，不能是类、结构、类型参数或数组类型</span><span class="sxs-lookup"><span data-stu-id="4433f-102">BC30424: Constants must be of an intrinsic or enumerated type, not a class, structure, type parameter, or array type</span></span>

<span data-ttu-id="4433f-103">您尝试将常量声明为类、结构或数组类型，或者声明为由包含泛型类型定义的类型参数。</span><span class="sxs-lookup"><span data-stu-id="4433f-103">You have attempted to declare a constant as a class, structure, or array type, or as a type parameter defined by a containing generic type.</span></span>

 <span data-ttu-id="4433f-104">常量必须是内部类型 (、、、、、、、、、、、、、 `Boolean` `Byte` `Date` `Decimal` `Double` `Integer` `Long` `Object` `SByte` `Short` `Single` `String` `UInteger` `ULong` 或 `UShort`) 或 `Enum` 基于其中一个整型类型的类型。</span><span class="sxs-lookup"><span data-stu-id="4433f-104">Constants must be of an intrinsic type (`Boolean`, `Byte`, `Date`, `Decimal`, `Double`, `Integer`, `Long`, `Object`, `SByte`, `Short`, `Single`, `String`, `UInteger`, `ULong`, or `UShort`), or an `Enum` type based on one of the integral types.</span></span>

 <span data-ttu-id="4433f-105">**错误 ID：** BC30424</span><span class="sxs-lookup"><span data-stu-id="4433f-105">**Error ID:** BC30424</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="4433f-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="4433f-106">To correct this error</span></span>

1. <span data-ttu-id="4433f-107">将常量声明为内部类型或 `Enum` 类型。</span><span class="sxs-lookup"><span data-stu-id="4433f-107">Declare the constant as an intrinsic or `Enum` type.</span></span>

2. <span data-ttu-id="4433f-108">常数也可以是一个特殊值 `True` ，如、 `False` 或 `Nothing` 。</span><span class="sxs-lookup"><span data-stu-id="4433f-108">A constant can also be a special value such as `True`, `False`, or `Nothing`.</span></span> <span data-ttu-id="4433f-109">编译器将这些预定义的值视为适当的内部类型。</span><span class="sxs-lookup"><span data-stu-id="4433f-109">The compiler considers these predefined values to be of the appropriate intrinsic type.</span></span>

## <a name="see-also"></a><span data-ttu-id="4433f-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4433f-110">See also</span></span>

- [<span data-ttu-id="4433f-111">常量和枚举</span><span class="sxs-lookup"><span data-stu-id="4433f-111">Constants and Enumerations</span></span>](../constants-and-enumerations.md)
- [<span data-ttu-id="4433f-112">数据类型</span><span class="sxs-lookup"><span data-stu-id="4433f-112">Data Types</span></span>](../../programming-guide/language-features/data-types/index.md)
- [<span data-ttu-id="4433f-113">数据类型</span><span class="sxs-lookup"><span data-stu-id="4433f-113">Data Types</span></span>](../data-types/index.md)
