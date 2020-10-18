---
title: 将“ByRef”参数“<parametername>”的值复制回匹配的参数将导致从类型“<typename1>”到类型“<typename2>”的收缩转换
ms.date: 07/20/2015
f1_keywords:
- bc32053
- vbc32053
helpviewer_keywords:
- BC32053
ms.assetid: 281564b7-99f7-451f-b10d-f985e831bb25
ms.openlocfilehash: b9a38d3eb4e25d5c9ac765adf47df72e45fd082a
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160927"
---
# <a name="bc32053-copying-the-value-of-byref-parameter-parametername-back-to-the-matching-argument-narrows-from-type-typename1-to-type-typename2"></a><span data-ttu-id="536a3-102">BC32053：将 "ByRef" 参数 "" 的值复制 \<parametername> 回匹配的参数将导致从类型 " \<typename1> " 到类型 " \<typename2> " 的收缩</span><span class="sxs-lookup"><span data-stu-id="536a3-102">BC32053: Copying the value of 'ByRef' parameter '\<parametername>' back to the matching argument narrows from type '\<typename1>' to type '\<typename2>'</span></span>

<span data-ttu-id="536a3-103">使用扩展到相应参数类型的自变量调用过程，并从参数到自变量的转换为收缩。</span><span class="sxs-lookup"><span data-stu-id="536a3-103">A procedure is called with an argument that widens to the corresponding parameter type, and the conversion from the parameter to the argument is narrowing.</span></span>

 <span data-ttu-id="536a3-104">在定义类或结构时，可以定义一个或多个转换运算符来将该类或结构类型转换为其他类型。</span><span class="sxs-lookup"><span data-stu-id="536a3-104">When you define a class or structure, you can define one or more conversion operators to convert that class or structure type to other types.</span></span> <span data-ttu-id="536a3-105">也可以定义反向转换运算符来将这些其他类型转换回类或结构类型。</span><span class="sxs-lookup"><span data-stu-id="536a3-105">You can also define reverse conversion operators to convert those other types back to your class or structure type.</span></span> <span data-ttu-id="536a3-106">当你在过程调用中使用你的类或结构类型时，Visual Basic 可以使用这些转换运算符将参数的类型转换为其对应参数的类型。</span><span class="sxs-lookup"><span data-stu-id="536a3-106">When you use your class or structure type in a procedure call, Visual Basic can use these conversion operators to convert the type of an argument to the type of its corresponding parameter.</span></span>

 <span data-ttu-id="536a3-107">如果传递参数 [ByRef](../modifiers/byref.md)，Visual Basic 有时会将参数值复制到过程的局部变量中，而不是传递引用。</span><span class="sxs-lookup"><span data-stu-id="536a3-107">If you pass the argument [ByRef](../modifiers/byref.md), Visual Basic sometimes copies the argument value into a local variable in the procedure instead of passing a reference.</span></span> <span data-ttu-id="536a3-108">在这种情况下，当过程返回时，Visual Basic 必须随后将局部变量值复制回调用代码中的参数。</span><span class="sxs-lookup"><span data-stu-id="536a3-108">In such a case, when the procedure returns, Visual Basic must then copy the local variable value back into the argument in the calling code.</span></span>

 <span data-ttu-id="536a3-109">如果将 `ByRef` 实参值复制到过程中，并且实参与形参为同一类型，则不必进行转换。</span><span class="sxs-lookup"><span data-stu-id="536a3-109">If a `ByRef` argument value is copied into the procedure and the argument and parameter are of the same type, no conversion is necessary.</span></span> <span data-ttu-id="536a3-110">但是，如果类型不同，则 Visual Basic 必须双向转换。</span><span class="sxs-lookup"><span data-stu-id="536a3-110">But if the types are different, Visual Basic must convert in both directions.</span></span> <span data-ttu-id="536a3-111">如果其中一个类型是你的类或结构类型，则 Visual Basic 必须将其转换为另一种类型。</span><span class="sxs-lookup"><span data-stu-id="536a3-111">If one of the types is your class or structure type, Visual Basic must convert it both to and from the other type.</span></span> <span data-ttu-id="536a3-112">如果其中一个转换为扩大，则反向转换可能会收缩。</span><span class="sxs-lookup"><span data-stu-id="536a3-112">If one of these conversions is widening, the reverse conversion might be narrowing.</span></span>

 <span data-ttu-id="536a3-113">**错误 ID：** BC32053</span><span class="sxs-lookup"><span data-stu-id="536a3-113">**Error ID:** BC32053</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="536a3-114">更正此错误</span><span class="sxs-lookup"><span data-stu-id="536a3-114">To correct this error</span></span>

- <span data-ttu-id="536a3-115">如果可能，请使用与过程参数相同的类型的调用参数，这样 Visual Basic 不需要进行任何转换。</span><span class="sxs-lookup"><span data-stu-id="536a3-115">If possible, use a calling argument of the same type as the procedure parameter, so Visual Basic does not need to do any conversion.</span></span>

- <span data-ttu-id="536a3-116">如果需要调用实参类型与形参类型不同的过程，但不需要将值返回到调用实参中，请将形参定义为 [ByVal](../modifiers/byval.md) 而不是 `ByRef`。</span><span class="sxs-lookup"><span data-stu-id="536a3-116">If you need to call the procedure with an argument type different from the parameter type but do not need to return a value into the calling argument, define the parameter to be [ByVal](../modifiers/byval.md) instead of `ByRef`.</span></span>

- <span data-ttu-id="536a3-117">如果需要将值返回到调用自变量中，请尽可能将反向转换运算符定义为 [扩大](../modifiers/widening.md)转换运算符。</span><span class="sxs-lookup"><span data-stu-id="536a3-117">If you need to return a value into the calling argument, define the reverse conversion operator as [Widening](../modifiers/widening.md), if possible.</span></span>

## <a name="see-also"></a><span data-ttu-id="536a3-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="536a3-118">See also</span></span>

- [<span data-ttu-id="536a3-119">过程</span><span class="sxs-lookup"><span data-stu-id="536a3-119">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
- [<span data-ttu-id="536a3-120">过程形参和实参</span><span class="sxs-lookup"><span data-stu-id="536a3-120">Procedure Parameters and Arguments</span></span>](../../programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)
- [<span data-ttu-id="536a3-121">按值和按引用传递参数</span><span class="sxs-lookup"><span data-stu-id="536a3-121">Passing Arguments by Value and by Reference</span></span>](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
- [<span data-ttu-id="536a3-122">运算符过程</span><span class="sxs-lookup"><span data-stu-id="536a3-122">Operator Procedures</span></span>](../../programming-guide/language-features/procedures/operator-procedures.md)
- [<span data-ttu-id="536a3-123">Operator Statement</span><span class="sxs-lookup"><span data-stu-id="536a3-123">Operator Statement</span></span>](../statements/operator-statement.md)
- [<span data-ttu-id="536a3-124">如何：定义运算符</span><span class="sxs-lookup"><span data-stu-id="536a3-124">How to: Define an Operator</span></span>](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [<span data-ttu-id="536a3-125">如何：定义转换运算符</span><span class="sxs-lookup"><span data-stu-id="536a3-125">How to: Define a Conversion Operator</span></span>](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [<span data-ttu-id="536a3-126">Visual Basic 中的类型转换</span><span class="sxs-lookup"><span data-stu-id="536a3-126">Type Conversions in Visual Basic</span></span>](../../programming-guide/language-features/data-types/type-conversions.md)
- [<span data-ttu-id="536a3-127">Widening and Narrowing Conversions</span><span class="sxs-lookup"><span data-stu-id="536a3-127">Widening and Narrowing Conversions</span></span>](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
