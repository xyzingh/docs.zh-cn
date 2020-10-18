---
title: 表达式的类型为“<typename>”，这是受限类型，不能用于访问从“Object”或“ValueType”继承的成员
ms.date: 07/20/2015
f1_keywords:
- bc31393
- vbc31393
helpviewer_keywords:
- BC31393
ms.assetid: 2963cf3f-c527-4aa7-b67c-ee80b6d23186
ms.openlocfilehash: 3e19c0d71ee47ac61e9704f0fcd2637f01aa0896
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163046"
---
# <a name="bc31393-expression-has-the-type-typename-which-is-a-restricted-type-and-cannot-be-used-to-access-members-inherited-from-object-or-valuetype"></a><span data-ttu-id="41d20-102">BC31393： Expression 的类型为 " \<typename> "，这是受限类型，不能用于访问从 "Object" 或 "ValueType" 继承的成员</span><span class="sxs-lookup"><span data-stu-id="41d20-102">BC31393: Expression has the type '\<typename>' which is a restricted type and cannot be used to access members inherited from 'Object' or 'ValueType'</span></span>

<span data-ttu-id="41d20-103">表达式的计算结果为不能由公共语言运行时 (CLR) 但访问需要装箱的成员的类型。</span><span class="sxs-lookup"><span data-stu-id="41d20-103">An expression evaluates to a type that cannot be boxed by the common language runtime (CLR) but accesses a member that requires boxing.</span></span>

 <span data-ttu-id="41d20-104">*装箱* 是指将一个类型转换为 `Object` ，或有时转换为 <xref:System.ValueType>所需的处理。</span><span class="sxs-lookup"><span data-stu-id="41d20-104">*Boxing* refers to the processing necessary to convert a type to `Object` or, on occasion, to <xref:System.ValueType>.</span></span> <span data-ttu-id="41d20-105">公共语言运行时无法对某些结构类型（例如、和）进行 box <xref:System.ArgIterator> <xref:System.RuntimeArgumentHandle> <xref:System.TypedReference> 。</span><span class="sxs-lookup"><span data-stu-id="41d20-105">The common language runtime cannot box certain structure types, for example <xref:System.ArgIterator>, <xref:System.RuntimeArgumentHandle>, and <xref:System.TypedReference>.</span></span>

 <span data-ttu-id="41d20-106">此表达式尝试使用受限类型调用从或继承的方法 <xref:System.Object> <xref:System.ValueType> ，例如 <xref:System.Object.GetHashCode%2A> 或 <xref:System.Object.ToString%2A> 。</span><span class="sxs-lookup"><span data-stu-id="41d20-106">This expression attempts to use the restricted type to call a method inherited from <xref:System.Object> or <xref:System.ValueType>, such as <xref:System.Object.GetHashCode%2A> or <xref:System.Object.ToString%2A>.</span></span> <span data-ttu-id="41d20-107">若要访问此方法，Visual Basic 尝试了导致此错误的隐式装箱转换。</span><span class="sxs-lookup"><span data-stu-id="41d20-107">To access this method, Visual Basic has attempted an implicit boxing conversion that causes this error.</span></span>

 <span data-ttu-id="41d20-108">**错误 ID：** BC31393</span><span class="sxs-lookup"><span data-stu-id="41d20-108">**Error ID:** BC31393</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="41d20-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="41d20-109">To correct this error</span></span>

1. <span data-ttu-id="41d20-110">查找计算结果为引用类型的表达式。</span><span class="sxs-lookup"><span data-stu-id="41d20-110">Locate the expression that evaluates to the cited type.</span></span>

2. <span data-ttu-id="41d20-111">查找语句中尝试调用从或继承的方法的部分 <xref:System.Object> <xref:System.ValueType> 。</span><span class="sxs-lookup"><span data-stu-id="41d20-111">Locate the part of your statement that attempts to call the method inherited from <xref:System.Object> or <xref:System.ValueType>.</span></span>

3. <span data-ttu-id="41d20-112">重写语句以避免方法调用。</span><span class="sxs-lookup"><span data-stu-id="41d20-112">Rewrite the statement to avoid the method call.</span></span>

## <a name="see-also"></a><span data-ttu-id="41d20-113">另请参阅</span><span class="sxs-lookup"><span data-stu-id="41d20-113">See also</span></span>

- [<span data-ttu-id="41d20-114">隐式转换和显式转换</span><span class="sxs-lookup"><span data-stu-id="41d20-114">Implicit and Explicit Conversions</span></span>](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
