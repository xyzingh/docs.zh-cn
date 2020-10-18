---
title: 属性“<propertyname>”的“Set”访问器不可访问
ms.date: 07/20/2015
f1_keywords:
- vbc31102
- bc31102
helpviewer_keywords:
- BC31102
ms.assetid: 6f7b31b7-3656-4ae1-8851-90f5f4c6950a
ms.openlocfilehash: 3cf828eb5f11090a74a65388e2b89a191046a456
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162240"
---
# <a name="bc31102-set-accessor-of-property-propertyname-is-not-accessible"></a><span data-ttu-id="8f776-102">BC31102：属性 "" 的 "Set" 访问器 \<propertyname> 不可访问</span><span class="sxs-lookup"><span data-stu-id="8f776-102">BC31102: 'Set' accessor of property '\<propertyname>' is not accessible</span></span>

<span data-ttu-id="8f776-103">当某个语句无权访问该属性的过程时，它将尝试存储该属性的值 `Set` 。</span><span class="sxs-lookup"><span data-stu-id="8f776-103">A statement attempts to store the value of a property when it does not have access to the property's `Set` procedure.</span></span>

 <span data-ttu-id="8f776-104">如果 [Set 语句](../statements/set-statement.md) 是使用比 [属性语句](../statements/property-statement.md)更严格的访问级别进行标记，则在以下情况下，尝试设置该属性值可能会失败：</span><span class="sxs-lookup"><span data-stu-id="8f776-104">If the [Set Statement](../statements/set-statement.md) is marked with a more restrictive access level than its [Property Statement](../statements/property-statement.md), an attempt to set the property value could fail in the following cases:</span></span>

- <span data-ttu-id="8f776-105">`Set`语句标记为[Private](../modifiers/private.md) ，并且调用代码位于定义该属性的类或结构之外。</span><span class="sxs-lookup"><span data-stu-id="8f776-105">The `Set` statement is marked [Private](../modifiers/private.md) and the calling code is outside the class or structure in which the property is defined.</span></span>

- <span data-ttu-id="8f776-106">`Set`语句被标记为[受保护](../modifiers/protected.md)，调用代码不在定义该属性的类或结构中，也不在派生类中。</span><span class="sxs-lookup"><span data-stu-id="8f776-106">The `Set` statement is marked [Protected](../modifiers/protected.md) and the calling code is not in the class or structure in which the property is defined, nor in a derived class.</span></span>

- <span data-ttu-id="8f776-107">`Set`语句被标记为[Friend](../modifiers/friend.md) ，调用代码不在定义该属性的程序集中。</span><span class="sxs-lookup"><span data-stu-id="8f776-107">The `Set` statement is marked [Friend](../modifiers/friend.md) and the calling code is not in the same assembly in which the property is defined.</span></span>

 <span data-ttu-id="8f776-108">**错误 ID：** BC31102</span><span class="sxs-lookup"><span data-stu-id="8f776-108">**Error ID:** BC31102</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="8f776-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="8f776-109">To correct this error</span></span>

- <span data-ttu-id="8f776-110">如果你可以控制定义属性的源代码，请考虑 `Set` 使用与属性本身相同的访问级别声明过程。</span><span class="sxs-lookup"><span data-stu-id="8f776-110">If you have control of the source code defining the property, consider declaring the `Set` procedure with the same access level as the property itself.</span></span>

- <span data-ttu-id="8f776-111">如果你不能控制定义属性的源代码，或者必须限制 `Set` 过程访问级别，而不是属性本身，请尝试将设置属性值的语句移到对属性具有更好访问权限的代码区域。</span><span class="sxs-lookup"><span data-stu-id="8f776-111">If you do not have control of the source code defining the property, or you must restrict the `Set` procedure access level more than the property itself, try to move the statement that sets the property value to a region of code that has better access to the property.</span></span>

## <a name="see-also"></a><span data-ttu-id="8f776-112">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8f776-112">See also</span></span>

- [<span data-ttu-id="8f776-113">Property 过程</span><span class="sxs-lookup"><span data-stu-id="8f776-113">Property Procedures</span></span>](../../programming-guide/language-features/procedures/property-procedures.md)
- [<span data-ttu-id="8f776-114">如何：声明具有混合访问级别的属性</span><span class="sxs-lookup"><span data-stu-id="8f776-114">How to: Declare a Property with Mixed Access Levels</span></span>](../../programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)
