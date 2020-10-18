---
title: 函数“<procedurename>”的返回类型不符合 CLS
ms.date: 07/20/2015
f1_keywords:
- bc40027
- vbc40027
helpviewer_keywords:
- BC40027
ms.assetid: 33c088c7-48e7-400c-920e-6d8967e1f3fc
ms.openlocfilehash: 9a877046a1b30e2e3773a41b8b44573e11ff1c96
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159698"
---
# <a name="bc40027-return-type-of-function-procedurename-is-not-cls-compliant"></a><span data-ttu-id="5bc22-102">BC40027：函数 "" 的返回类型 \<procedurename> 不符合 CLS</span><span class="sxs-lookup"><span data-stu-id="5bc22-102">BC40027: Return type of function '\<procedurename>' is not CLS-compliant</span></span>

<span data-ttu-id="5bc22-103">`Function`过程被标记为 `<CLSCompliant(True)>` ，但会返回一个标记为、未 `<CLSCompliant(False)>` 标记或不合格的类型，因为它是不符合要求的类型。</span><span class="sxs-lookup"><span data-stu-id="5bc22-103">A `Function` procedure is marked as `<CLSCompliant(True)>` but returns a type that is marked as `<CLSCompliant(False)>`, is not marked, or does not qualify because it is a noncompliant type.</span></span>

 <span data-ttu-id="5bc22-104">一个过程要符合[语言独立性和与语言无关的组件](../../../standard/language-independence-and-language-independent-components.md) (CLS)，必须只使用符合 CLS 的类型。</span><span class="sxs-lookup"><span data-stu-id="5bc22-104">For a procedure to be compliant with the [Language Independence and Language-Independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS), it must use only CLS-compliant types.</span></span> <span data-ttu-id="5bc22-105">这适用于参数的类型、返回类型及其所有本地变量的类型。</span><span class="sxs-lookup"><span data-stu-id="5bc22-105">This applies to the types of the parameters, the return type, and the types of all its local variables.</span></span>

 <span data-ttu-id="5bc22-106">以下 Visual Basic 数据类型不符合 CLS：</span><span class="sxs-lookup"><span data-stu-id="5bc22-106">The following Visual Basic data types are not CLS-compliant:</span></span>

- [<span data-ttu-id="5bc22-107">SByte 数据类型</span><span class="sxs-lookup"><span data-stu-id="5bc22-107">SByte Data Type</span></span>](../data-types/sbyte-data-type.md)

- [<span data-ttu-id="5bc22-108">UInteger 数据类型</span><span class="sxs-lookup"><span data-stu-id="5bc22-108">UInteger Data Type</span></span>](../data-types/uinteger-data-type.md)

- [<span data-ttu-id="5bc22-109">ULong 数据类型</span><span class="sxs-lookup"><span data-stu-id="5bc22-109">ULong Data Type</span></span>](../data-types/ulong-data-type.md)

- [<span data-ttu-id="5bc22-110">UShort 数据类型</span><span class="sxs-lookup"><span data-stu-id="5bc22-110">UShort Data Type</span></span>](../data-types/ushort-data-type.md)

 <span data-ttu-id="5bc22-111">当将 <xref:System.CLSCompliantAttribute> 应用到编程元素中时，需要将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合性。</span><span class="sxs-lookup"><span data-stu-id="5bc22-111">When you apply the <xref:System.CLSCompliantAttribute> to a programming element, you set the attribute's `isCompliant` parameter to either `True` or `False` to indicate compliance or noncompliance.</span></span> <span data-ttu-id="5bc22-112">此参数没有默认值，必须为其提供一个值。</span><span class="sxs-lookup"><span data-stu-id="5bc22-112">There is no default for this parameter, and you must supply a value.</span></span>

 <span data-ttu-id="5bc22-113">如果不将 <xref:System.CLSCompliantAttribute> 应用到元素，则它将被视为不符合规范。</span><span class="sxs-lookup"><span data-stu-id="5bc22-113">If you do not apply the <xref:System.CLSCompliantAttribute> to an element, it is considered to be noncompliant.</span></span>

 <span data-ttu-id="5bc22-114">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="5bc22-114">By default, this message is a warning.</span></span> <span data-ttu-id="5bc22-115">有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="5bc22-115">For information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="5bc22-116">**错误 ID：** BC40027</span><span class="sxs-lookup"><span data-stu-id="5bc22-116">**Error ID:** BC40027</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="5bc22-117">更正此错误</span><span class="sxs-lookup"><span data-stu-id="5bc22-117">To correct this error</span></span>

- <span data-ttu-id="5bc22-118">如果 `Function` 过程必须返回此特定类型，请删除 <xref:System.CLSCompliantAttribute> 。</span><span class="sxs-lookup"><span data-stu-id="5bc22-118">If the `Function` procedure must return this particular type, remove the <xref:System.CLSCompliantAttribute>.</span></span> <span data-ttu-id="5bc22-119">该过程不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="5bc22-119">The procedure cannot be CLS-compliant.</span></span>

- <span data-ttu-id="5bc22-120">如果该 `Function` 过程必须符合 cls，则将返回类型更改为最接近的符合 CLS 的类型。</span><span class="sxs-lookup"><span data-stu-id="5bc22-120">If the `Function` procedure must be CLS-compliant, change the return type to the closest CLS-compliant type.</span></span> <span data-ttu-id="5bc22-121">例如，如果不需要 2147483647 以上的数值范围，可以使用 `UInteger` 取代 `Integer` 。</span><span class="sxs-lookup"><span data-stu-id="5bc22-121">For example, in place of `UInteger` you might be able to use `Integer` if you do not need the value range above 2,147,483,647.</span></span> <span data-ttu-id="5bc22-122">如果确实需要更大范围，可以用 `UInteger` 代替 `Long`。</span><span class="sxs-lookup"><span data-stu-id="5bc22-122">If you do need the extended range, you can replace `UInteger` with `Long`.</span></span>

- <span data-ttu-id="5bc22-123">如果要与自动化或 COM 对象进行交互，请记住，某些类型的数据宽度与 .NET Framework 中的不同。</span><span class="sxs-lookup"><span data-stu-id="5bc22-123">If you are interfacing with Automation or COM objects, keep in mind that some types have different data widths than in the .NET Framework.</span></span> <span data-ttu-id="5bc22-124">例如，`int` 在其他环境中通常为 16 位。</span><span class="sxs-lookup"><span data-stu-id="5bc22-124">For example, `int` is often 16 bits in other environments.</span></span> <span data-ttu-id="5bc22-125">如果要将16位整数返回给此类组件，请 `Short` `Integer` 在托管的 Visual Basic 代码中将其声明为而不是。</span><span class="sxs-lookup"><span data-stu-id="5bc22-125">If you are returning a 16-bit integer to such a component, declare it as `Short` instead of `Integer` in your managed Visual Basic code.</span></span>
