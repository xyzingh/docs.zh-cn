---
title: 运算符声明必须是以下其中之一： +,-, *,-,-, ^、 &amp; 、Like、Mod、And、Or、Xor、Not、 <<、 >>、=、 <>、<、<=、>、>=、CType、IsTrue、IsFalse
ms.date: 07/20/2015
f1_keywords:
- bc33000
- vbc33000
helpviewer_keywords:
- BC33000
ms.assetid: 15c5d8eb-3a8c-4141-8f41-33151afabf97
ms.openlocfilehash: a94e62e33427987a302a6244b2b8ce8d295e4f11
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159893"
---
# <a name="bc33000-operator-declaration-must-be-one-of----amp-like-mod-and-or-xor-not--"></a><span data-ttu-id="aa712-102">BC33000：运算符声明必须是以下之一： +,-, \*、 \, /、^、 &amp; 、Like、Mod、And、Or、Xor、Not、 \<\<, >> .。。</span><span class="sxs-lookup"><span data-stu-id="aa712-102">BC33000: Operator declaration must be one of:  +,-,\*,\,/,^, &amp;, Like, Mod, And, Or, Xor, Not, \<\<, >>...</span></span>

<span data-ttu-id="aa712-103">您只能声明一个适合重载的运算符。</span><span class="sxs-lookup"><span data-stu-id="aa712-103">You can declare only an operator that is eligible for overloading.</span></span> <span data-ttu-id="aa712-104">下表列出了可以声明的运算符。</span><span class="sxs-lookup"><span data-stu-id="aa712-104">The following table lists the operators you can declare.</span></span>

|<span data-ttu-id="aa712-105">类型</span><span class="sxs-lookup"><span data-stu-id="aa712-105">Type</span></span>|<span data-ttu-id="aa712-106">运算符</span><span class="sxs-lookup"><span data-stu-id="aa712-106">Operators</span></span>|
|----------|---------------|
|<span data-ttu-id="aa712-107">一元</span><span class="sxs-lookup"><span data-stu-id="aa712-107">Unary</span></span>|<span data-ttu-id="aa712-108">`+`, `-`, `IsFalse`, `IsTrue`, `Not`</span><span class="sxs-lookup"><span data-stu-id="aa712-108">`+`, `-`, `IsFalse`, `IsTrue`, `Not`</span></span>|
|<span data-ttu-id="aa712-109">二进制</span><span class="sxs-lookup"><span data-stu-id="aa712-109">Binary</span></span>|<span data-ttu-id="aa712-110">`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`</span><span class="sxs-lookup"><span data-stu-id="aa712-110">`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`</span></span>|
|<span data-ttu-id="aa712-111">转换（一元）</span><span class="sxs-lookup"><span data-stu-id="aa712-111">Conversion (unary)</span></span>|`CType`|

 <span data-ttu-id="aa712-112">请注意， `=` 二元列表中的运算符是比较运算符，而不是赋值运算符。</span><span class="sxs-lookup"><span data-stu-id="aa712-112">Note that the `=` operator in the binary list is the comparison operator, not the assignment operator.</span></span>

 <span data-ttu-id="aa712-113">**错误 ID：** BC33000</span><span class="sxs-lookup"><span data-stu-id="aa712-113">**Error ID:** BC33000</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="aa712-114">更正此错误</span><span class="sxs-lookup"><span data-stu-id="aa712-114">To correct this error</span></span>

- <span data-ttu-id="aa712-115">从一组可重载运算符中选择一个运算符。</span><span class="sxs-lookup"><span data-stu-id="aa712-115">Select an operator from the set of overloadable operators.</span></span>

- <span data-ttu-id="aa712-116">如果你需要重载无法直接重载的运算符这一功能，请创建用于获取适当参数并返回适当值的 `Function` 过程。</span><span class="sxs-lookup"><span data-stu-id="aa712-116">If you need the functionality of overloading an operator that you cannot overload directly, create a `Function` procedure that takes the appropriate parameters and returns the appropriate value.</span></span>

## <a name="see-also"></a><span data-ttu-id="aa712-117">另请参阅</span><span class="sxs-lookup"><span data-stu-id="aa712-117">See also</span></span>

- [<span data-ttu-id="aa712-118">Operator Statement</span><span class="sxs-lookup"><span data-stu-id="aa712-118">Operator Statement</span></span>](../statements/operator-statement.md)
- [<span data-ttu-id="aa712-119">运算符过程</span><span class="sxs-lookup"><span data-stu-id="aa712-119">Operator Procedures</span></span>](../../programming-guide/language-features/procedures/operator-procedures.md)
- [<span data-ttu-id="aa712-120">如何：定义运算符</span><span class="sxs-lookup"><span data-stu-id="aa712-120">How to: Define an Operator</span></span>](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [<span data-ttu-id="aa712-121">如何：定义转换运算符</span><span class="sxs-lookup"><span data-stu-id="aa712-121">How to: Define a Conversion Operator</span></span>](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [<span data-ttu-id="aa712-122">Function 语句</span><span class="sxs-lookup"><span data-stu-id="aa712-122">Function Statement</span></span>](../statements/function-statement.md)
