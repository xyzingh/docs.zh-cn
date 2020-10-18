---
title: 将“ByRef”参数“<typename1>”的值复制回匹配参数时，发生从“<typename2>”到“<parametername>”的隐式转换。
ms.date: 07/20/2015
f1_keywords:
- vbc41999
- bc41999
helpviewer_keywords:
- BC41999
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
ms.openlocfilehash: a95a4b792742efcc165f7c7a9592582d34618f11
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162799"
---
# <a name="bc41999-implicit-conversion-from-typename1-to-typename2-in-copying-the-value-of-byref-parameter-parametername-back-to-the-matching-argument"></a><span data-ttu-id="b268d-102">BC41999： \<typename1> 将 \<typename2> "ByRef" 参数 "" 的值复制 \<parametername> 回匹配参数时，从 "" 到 "" 的隐式转换。</span><span class="sxs-lookup"><span data-stu-id="b268d-102">BC41999: Implicit conversion from '\<typename1>' to '\<typename2>' in copying the value of 'ByRef' parameter '\<parametername>' back to the matching argument.</span></span>

<span data-ttu-id="b268d-103">使用与对应参数的类型不同的 [ByRef](../modifiers/byref.md) 参数调用过程。</span><span class="sxs-lookup"><span data-stu-id="b268d-103">A procedure is called with a [ByRef](../modifiers/byref.md) argument of a different type than that of its corresponding parameter.</span></span>

 <span data-ttu-id="b268d-104">如果传递参数 `ByRef` ，Visual Basic 有时会将参数值复制到过程的局部变量中，而不是传递引用。</span><span class="sxs-lookup"><span data-stu-id="b268d-104">If you pass an argument `ByRef`, Visual Basic sometimes copies the argument value into a local variable in the procedure instead of passing a reference.</span></span> <span data-ttu-id="b268d-105">在这种情况下，当过程返回时，Visual Basic 必须随后将局部变量值复制回调用代码中的参数。</span><span class="sxs-lookup"><span data-stu-id="b268d-105">In such a case, when the procedure returns, Visual Basic must then copy the local variable value back into the argument in the calling code.</span></span>

 <span data-ttu-id="b268d-106">如果将 `ByRef` 实参值复制到过程中，并且实参与形参为同一类型，则不必进行转换。</span><span class="sxs-lookup"><span data-stu-id="b268d-106">If a `ByRef` argument value is copied into the procedure and the argument and parameter are of the same type, no conversion is necessary.</span></span> <span data-ttu-id="b268d-107">但是，如果类型不同，则 Visual Basic 必须双向转换。</span><span class="sxs-lookup"><span data-stu-id="b268d-107">But if the types are different, Visual Basic must convert in both directions.</span></span> <span data-ttu-id="b268d-108">由于不能 `CType` 在过程参数或参数上使用或任何其他转换关键字，因此此类转换始终是隐式的。</span><span class="sxs-lookup"><span data-stu-id="b268d-108">Because you cannot use `CType` or any of the other conversion keywords on a procedure argument or parameter, such a conversion is always implicit.</span></span>

 <span data-ttu-id="b268d-109">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="b268d-109">By default, this message is a warning.</span></span> <span data-ttu-id="b268d-110">有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="b268d-110">For information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="b268d-111">**错误 ID：** BC41999</span><span class="sxs-lookup"><span data-stu-id="b268d-111">**Error ID:** BC41999</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="b268d-112">更正此错误</span><span class="sxs-lookup"><span data-stu-id="b268d-112">To correct this error</span></span>

- <span data-ttu-id="b268d-113">如果可能，请使用与过程参数相同的类型的调用参数，这样 Visual Basic 不需要进行任何转换。</span><span class="sxs-lookup"><span data-stu-id="b268d-113">If possible, use a calling argument of the same type as the procedure parameter, so Visual Basic does not need to do any conversion.</span></span>

- <span data-ttu-id="b268d-114">如果需要调用实参类型与形参类型不同的过程，但不需要将值返回到调用实参中，请将形参定义为 [ByVal](../modifiers/byval.md) 而不是 `ByRef`。</span><span class="sxs-lookup"><span data-stu-id="b268d-114">If you need to call the procedure with an argument type different from the parameter type but do not need to return a value into the calling argument, define the parameter to be [ByVal](../modifiers/byval.md) instead of `ByRef`.</span></span>

## <a name="see-also"></a><span data-ttu-id="b268d-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b268d-115">See also</span></span>

- [<span data-ttu-id="b268d-116">过程</span><span class="sxs-lookup"><span data-stu-id="b268d-116">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
- [<span data-ttu-id="b268d-117">过程形参和实参</span><span class="sxs-lookup"><span data-stu-id="b268d-117">Procedure Parameters and Arguments</span></span>](../../programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)
- [<span data-ttu-id="b268d-118">按值和按引用传递参数</span><span class="sxs-lookup"><span data-stu-id="b268d-118">Passing Arguments by Value and by Reference</span></span>](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
- [<span data-ttu-id="b268d-119">隐式转换和显式转换</span><span class="sxs-lookup"><span data-stu-id="b268d-119">Implicit and Explicit Conversions</span></span>](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
