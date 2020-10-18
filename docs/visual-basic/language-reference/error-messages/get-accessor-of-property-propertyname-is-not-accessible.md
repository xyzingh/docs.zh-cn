---
title: 属性“<propertyname>”的“Get”访问器不可访问
ms.date: 07/20/2015
f1_keywords:
- vbc31103
- bc31103
helpviewer_keywords:
- BC31103
ms.assetid: 3c346c32-7669-4b04-841d-7a9df9cb703e
ms.openlocfilehash: bd6830e16ba3d1f76c61519b4456832a2efec716
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162903"
---
# <a name="bc31103-get-accessor-of-property-propertyname-is-not-accessible"></a><span data-ttu-id="cada7-102">BC31103：属性 "" 的 "Get" 访问器 \<propertyname> 不可访问</span><span class="sxs-lookup"><span data-stu-id="cada7-102">BC31103: 'Get' accessor of property '\<propertyname>' is not accessible</span></span>

<span data-ttu-id="cada7-103">当某个语句无权访问该属性的过程时，它将尝试检索该属性的值 `Get` 。</span><span class="sxs-lookup"><span data-stu-id="cada7-103">A statement attempts to retrieve the value of a property when it does not have access to the property's `Get` procedure.</span></span>

 <span data-ttu-id="cada7-104">如果 [Get 语句](../statements/get-statement.md) 使用比 [属性语句](../statements/property-statement.md)更严格的访问级别进行标记，则在以下情况下读取属性值的尝试可能会失败：</span><span class="sxs-lookup"><span data-stu-id="cada7-104">If the [Get Statement](../statements/get-statement.md) is marked with a more restrictive access level than its [Property Statement](../statements/property-statement.md), an attempt to read the property value could fail in the following cases:</span></span>

- <span data-ttu-id="cada7-105">`Get`语句标记为[Private](../modifiers/private.md) ，并且调用代码位于定义该属性的类或结构之外。</span><span class="sxs-lookup"><span data-stu-id="cada7-105">The `Get` statement is marked [Private](../modifiers/private.md) and the calling code is outside the class or structure in which the property is defined.</span></span>

- <span data-ttu-id="cada7-106">`Get`语句被标记为[受保护](../modifiers/protected.md)，调用代码不在定义该属性的类或结构中，也不在派生类中。</span><span class="sxs-lookup"><span data-stu-id="cada7-106">The `Get` statement is marked [Protected](../modifiers/protected.md) and the calling code is not in the class or structure in which the property is defined, nor in a derived class.</span></span>

- <span data-ttu-id="cada7-107">`Get`语句被标记为[Friend](../modifiers/friend.md) ，调用代码不在定义该属性的程序集中。</span><span class="sxs-lookup"><span data-stu-id="cada7-107">The `Get` statement is marked [Friend](../modifiers/friend.md) and the calling code is not in the same assembly in which the property is defined.</span></span>

 <span data-ttu-id="cada7-108">**错误 ID：** BC31103</span><span class="sxs-lookup"><span data-stu-id="cada7-108">**Error ID:** BC31103</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="cada7-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="cada7-109">To correct this error</span></span>

- <span data-ttu-id="cada7-110">如果你可以控制定义属性的源代码，请考虑 `Get` 使用与属性本身相同的访问级别声明过程。</span><span class="sxs-lookup"><span data-stu-id="cada7-110">If you have control of the source code defining the property, consider declaring the `Get` procedure with the same access level as the property itself.</span></span>

- <span data-ttu-id="cada7-111">如果你不能控制定义属性的源代码，或者必须限制 `Get` 过程访问级别，而不是属性本身，请尝试将读取属性值的语句移到对属性具有更好访问权限的代码区域。</span><span class="sxs-lookup"><span data-stu-id="cada7-111">If you do not have control of the source code defining the property, or you must restrict the `Get` procedure access level more than the property itself, try to move the statement that reads the property value to a region of code that has better access to the property.</span></span>

## <a name="see-also"></a><span data-ttu-id="cada7-112">另请参阅</span><span class="sxs-lookup"><span data-stu-id="cada7-112">See also</span></span>

- [<span data-ttu-id="cada7-113">Property 过程</span><span class="sxs-lookup"><span data-stu-id="cada7-113">Property Procedures</span></span>](../../programming-guide/language-features/procedures/property-procedures.md)
- [<span data-ttu-id="cada7-114">如何：声明具有混合访问级别的属性</span><span class="sxs-lookup"><span data-stu-id="cada7-114">How to: Declare a Property with Mixed Access Levels</span></span>](../../programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)
