---
title: “<elementname>”已过时（Visual Basic 警告）
ms.date: 07/20/2015
f1_keywords:
- vbc40008
- bc40008
helpviewer_keywords:
- BC40008
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
ms.openlocfilehash: 555030d97434852eab64cc8b4bda2e901649d17d
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163137"
---
# <a name="bc40008-elementname-is-obsolete-visual-basic-warning"></a><span data-ttu-id="ec8ad-102">BC40008： " \<elementname> " 已过时 (Visual Basic 警告) </span><span class="sxs-lookup"><span data-stu-id="ec8ad-102">BC40008: '\<elementname>' is obsolete (Visual Basic Warning)</span></span>

<span data-ttu-id="ec8ad-103">语句试图访问编程元素，此元素已标记有 <xref:System.ObsoleteAttribute> 特性及将其视为警告的指令。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-103">A statement attempts to access a programming element which has been marked with the <xref:System.ObsoleteAttribute> attribute and the directive to treat it as a warning.</span></span>

 <span data-ttu-id="ec8ad-104">可以通过将 <xref:System.ObsoleteAttribute> 应用于任意编程元素，将其标记为不再使用。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-104">You can mark any programming element as being no longer in use by applying <xref:System.ObsoleteAttribute> to it.</span></span> <span data-ttu-id="ec8ad-105">如果执行此操作，则可以将特性的 <xref:System.ObsoleteAttribute.IsError%2A> 属性设置为 `True` 或 `False`。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-105">If you do this, you can set the attribute's <xref:System.ObsoleteAttribute.IsError%2A> property to either `True` or `False`.</span></span> <span data-ttu-id="ec8ad-106">如果设置为 `True`，则编译器将尝试使用该元素的操作视为错误。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-106">If you set it to `True`, the compiler treats an attempt to use the element as an error.</span></span> <span data-ttu-id="ec8ad-107">如果设置为 `False`，或将其默认为 `False`，则编译器会在有操作尝试使用该元素时发出警告。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-107">If you set it to `False`, or let it default to `False`, the compiler issues a warning if there is an attempt to use the element.</span></span>

 <span data-ttu-id="ec8ad-108">默认情况下，此消息是一个警告，因为 <xref:System.ObsoleteAttribute.IsError%2A> 的 <xref:System.ObsoleteAttribute> 属性为 `False`。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-108">By default, this message is a warning, because the <xref:System.ObsoleteAttribute.IsError%2A> property of <xref:System.ObsoleteAttribute> is `False`.</span></span> <span data-ttu-id="ec8ad-109">有关隐藏警告或将警告视为错误的详细信息，请参阅 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-109">For more information about hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="ec8ad-110">**错误 ID：** BC40008</span><span class="sxs-lookup"><span data-stu-id="ec8ad-110">**Error ID:** BC40008</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="ec8ad-111">更正此错误</span><span class="sxs-lookup"><span data-stu-id="ec8ad-111">To correct this error</span></span>

- <span data-ttu-id="ec8ad-112">确保源代码引用的元素名称拼写正确。</span><span class="sxs-lookup"><span data-stu-id="ec8ad-112">Ensure that the source-code reference is spelling the element name correctly.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec8ad-113">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ec8ad-113">See also</span></span>

- [<span data-ttu-id="ec8ad-114">属性概述</span><span class="sxs-lookup"><span data-stu-id="ec8ad-114">Attributes overview</span></span>](../../programming-guide/concepts/attributes/index.md)
