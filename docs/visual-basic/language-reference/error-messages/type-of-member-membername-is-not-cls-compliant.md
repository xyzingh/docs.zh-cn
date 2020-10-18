---
title: 成员“<membername>”的类型不符合 CLS
ms.date: 07/20/2015
f1_keywords:
- bc40025
- vbc40025
helpviewer_keywords:
- BC40025
ms.assetid: adbd34bb-43d2-4266-90e7-cd1afaf49b4e
ms.openlocfilehash: c8c14a2d6df8804967807af881384bc7d9ccd99f
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163475"
---
# <a name="bc40025-type-of-member-membername-is-not-cls-compliant"></a><span data-ttu-id="e5c86-102">BC40025：成员 "" 的类型 \<membername> 不符合 CLS</span><span class="sxs-lookup"><span data-stu-id="e5c86-102">BC40025: Type of member '\<membername>' is not CLS-compliant</span></span>

<span data-ttu-id="e5c86-103">为此成员指定的数据类型不是 [语言独立性的一部分，并且 Language-Independent 组件](../../../standard/language-independence-and-language-independent-components.md) (CLS) 。</span><span class="sxs-lookup"><span data-stu-id="e5c86-103">The data type specified for this member is not part of the [Language Independence and Language-Independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS).</span></span> <span data-ttu-id="e5c86-104">这不是你的组件中的错误，因为 .NET Framework 和 Visual Basic 支持此数据类型。</span><span class="sxs-lookup"><span data-stu-id="e5c86-104">This is not an error within your component, because the .NET Framework and Visual Basic support this data type.</span></span> <span data-ttu-id="e5c86-105">但是，以严格符合 CLS 的代码编写的另一个组件可能不支持此数据类型。</span><span class="sxs-lookup"><span data-stu-id="e5c86-105">However, another component written in strictly CLS-compliant code might not support this data type.</span></span> <span data-ttu-id="e5c86-106">此类组件可能无法与组件成功交互。</span><span class="sxs-lookup"><span data-stu-id="e5c86-106">Such a component might not be able to interact successfully with your component.</span></span>

 <span data-ttu-id="e5c86-107">以下 Visual Basic 数据类型不符合 CLS：</span><span class="sxs-lookup"><span data-stu-id="e5c86-107">The following Visual Basic data types are not CLS-compliant:</span></span>

- [<span data-ttu-id="e5c86-108">SByte 数据类型</span><span class="sxs-lookup"><span data-stu-id="e5c86-108">SByte Data Type</span></span>](../data-types/sbyte-data-type.md)

- [<span data-ttu-id="e5c86-109">UInteger 数据类型</span><span class="sxs-lookup"><span data-stu-id="e5c86-109">UInteger Data Type</span></span>](../data-types/uinteger-data-type.md)

- [<span data-ttu-id="e5c86-110">ULong 数据类型</span><span class="sxs-lookup"><span data-stu-id="e5c86-110">ULong Data Type</span></span>](../data-types/ulong-data-type.md)

- [<span data-ttu-id="e5c86-111">UShort 数据类型</span><span class="sxs-lookup"><span data-stu-id="e5c86-111">UShort Data Type</span></span>](../data-types/ushort-data-type.md)

 <span data-ttu-id="e5c86-112">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="e5c86-112">By default, this message is a warning.</span></span> <span data-ttu-id="e5c86-113">有关隐藏警告或将警告视为错误的详细信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="e5c86-113">For more information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="e5c86-114">**错误 ID：** BC40025</span><span class="sxs-lookup"><span data-stu-id="e5c86-114">**Error ID:** BC40025</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="e5c86-115">更正此错误</span><span class="sxs-lookup"><span data-stu-id="e5c86-115">To correct this error</span></span>

- <span data-ttu-id="e5c86-116">如果你的组件只与其他 .NET Framework 组件交互，或者不与任何其他组件进行交互，则无需更改任何内容。</span><span class="sxs-lookup"><span data-stu-id="e5c86-116">If your component interfaces only with other .NET Framework components, or does not interface with any other components, you do not need to change anything.</span></span>

- <span data-ttu-id="e5c86-117">如果与不是为 .NET Framework 编写的组件进行交互，则可以通过反射或文档来确定它是否支持此数据类型。</span><span class="sxs-lookup"><span data-stu-id="e5c86-117">If you are interfacing with a component not written for the .NET Framework, you might be able to determine, either through reflection or from documentation, whether it supports this data type.</span></span> <span data-ttu-id="e5c86-118">如果是这样，则无需更改任何内容。</span><span class="sxs-lookup"><span data-stu-id="e5c86-118">If it does, you do not need to change anything.</span></span>

- <span data-ttu-id="e5c86-119">如果与不支持此数据类型的组件进行交互，则必须将其替换为最接近的符合 CLS 的类型。</span><span class="sxs-lookup"><span data-stu-id="e5c86-119">If you are interfacing with a component that does not support this data type, you must replace it with the closest CLS-compliant type.</span></span> <span data-ttu-id="e5c86-120">例如，如果不需要 2147483647 以上的数值范围，可以使用 `UInteger` 取代 `Integer` 。</span><span class="sxs-lookup"><span data-stu-id="e5c86-120">For example, in place of `UInteger` you might be able to use `Integer` if you do not need the value range above 2,147,483,647.</span></span> <span data-ttu-id="e5c86-121">如果确实需要更大范围，可以用 `UInteger` 代替 `Long`。</span><span class="sxs-lookup"><span data-stu-id="e5c86-121">If you do need the extended range, you can replace `UInteger` with `Long`.</span></span>

- <span data-ttu-id="e5c86-122">如果要与自动化或 COM 对象进行交互，请记住，某些类型的数据宽度与 .NET Framework 中的不同。</span><span class="sxs-lookup"><span data-stu-id="e5c86-122">If you are interfacing with Automation or COM objects, keep in mind that some types have different data widths than in the .NET Framework.</span></span> <span data-ttu-id="e5c86-123">例如，`uint` 在其他环境中通常为 16 位。</span><span class="sxs-lookup"><span data-stu-id="e5c86-123">For example, `uint` is often 16 bits in other environments.</span></span> <span data-ttu-id="e5c86-124">如果要将16位参数传递给此类组件，请 `UShort` `UInteger` 在托管的 Visual Basic 代码中将其声明为而不是。</span><span class="sxs-lookup"><span data-stu-id="e5c86-124">If you are passing a 16-bit argument to such a component, declare it as `UShort` instead of `UInteger` in your managed Visual Basic code.</span></span>

## <a name="see-also"></a><span data-ttu-id="e5c86-125">请参阅</span><span class="sxs-lookup"><span data-stu-id="e5c86-125">See also</span></span>

- [<span data-ttu-id="e5c86-126">反射</span><span class="sxs-lookup"><span data-stu-id="e5c86-126">Reflection</span></span>](../../../framework/reflection-and-codedom/reflection.md)
