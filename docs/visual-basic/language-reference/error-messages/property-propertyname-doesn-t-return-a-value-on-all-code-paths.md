---
title: 属性“<propertyname>”并非在所有代码路径上都返回值
ms.date: 07/20/2015
f1_keywords:
- bc42107
- vbc42107
helpviewer_keywords:
- BC42107
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
ms.openlocfilehash: 0736e2cbcdea1422d40161c88f898d487f72e3bc
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162383"
---
# <a name="bc42107-property-propertyname-doesnt-return-a-value-on-all-code-paths"></a><span data-ttu-id="1072c-102">BC42107：属性 " \<propertyname> " 不会在所有代码路径上都返回值</span><span class="sxs-lookup"><span data-stu-id="1072c-102">BC42107: Property '\<propertyname>' doesn't return a value on all code paths</span></span>

<span data-ttu-id="1072c-103">属性 " \<propertyname> " 不会在所有代码路径上都返回值。</span><span class="sxs-lookup"><span data-stu-id="1072c-103">Property '\<propertyname>' doesn't return a value on all code paths.</span></span> <span data-ttu-id="1072c-104">使用该结果时，可能会在运行时发生 null 引用异常。</span><span class="sxs-lookup"><span data-stu-id="1072c-104">A null reference exception could occur at run time when the result is used.</span></span>

<span data-ttu-id="1072c-105">属性 `Get` 过程至少有一个可能的路径，其代码中不返回值。</span><span class="sxs-lookup"><span data-stu-id="1072c-105">A property `Get` procedure has at least one possible path through its code that does not return a value.</span></span>

 <span data-ttu-id="1072c-106">可以通过 `Get` 以下任一方式从属性过程返回值：</span><span class="sxs-lookup"><span data-stu-id="1072c-106">You can return a value from a property `Get` procedure in any of the following ways:</span></span>

- <span data-ttu-id="1072c-107">将值分配给属性名称，然后执行 `Exit Property` 语句。</span><span class="sxs-lookup"><span data-stu-id="1072c-107">Assign the value to the property name and then perform an `Exit Property` statement.</span></span>

- <span data-ttu-id="1072c-108">将值分配给属性名称，然后执行 `End Get` 语句。</span><span class="sxs-lookup"><span data-stu-id="1072c-108">Assign the value to the property name and then perform the `End Get` statement.</span></span>

- <span data-ttu-id="1072c-109">在 [Return 语句](../statements/return-statement.md)中包含值。</span><span class="sxs-lookup"><span data-stu-id="1072c-109">Include the value in a [Return Statement](../statements/return-statement.md).</span></span>

<span data-ttu-id="1072c-110">如果控件传递给 `Exit Property` 或 `End Get` ，并且没有为属性名称分配任何值，则该 `Get` 过程将返回属性数据类型的默认值。</span><span class="sxs-lookup"><span data-stu-id="1072c-110">If control passes to `Exit Property` or `End Get` and you have not assigned any value to the property name, the `Get` procedure returns the default value of the property's data type.</span></span> <span data-ttu-id="1072c-111">有关详细信息，请参阅 [Function 语句](../statements/function-statement.md)中的 "行为"。</span><span class="sxs-lookup"><span data-stu-id="1072c-111">For more information, see "Behavior" in [Function Statement](../statements/function-statement.md).</span></span>

<span data-ttu-id="1072c-112">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="1072c-112">By default, this message is a warning.</span></span> <span data-ttu-id="1072c-113">有关隐藏警告或将警告视为错误的详细信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="1072c-113">For more information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

<span data-ttu-id="1072c-114">**错误 ID：** BC42107</span><span class="sxs-lookup"><span data-stu-id="1072c-114">**Error ID:** BC42107</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="1072c-115">更正此错误</span><span class="sxs-lookup"><span data-stu-id="1072c-115">To correct this error</span></span>

- <span data-ttu-id="1072c-116">检查控制流逻辑，并确保在导致返回的每个语句之前赋值。</span><span class="sxs-lookup"><span data-stu-id="1072c-116">Check your control flow logic and make sure you assign a value before every statement that causes a return.</span></span>

  <span data-ttu-id="1072c-117">如果始终使用语句，则更容易保证每次从过程返回一个值 `Return` 。</span><span class="sxs-lookup"><span data-stu-id="1072c-117">It's easier to guarantee that every return from the procedure returns a value if you always use the `Return` statement.</span></span> <span data-ttu-id="1072c-118">如果执行此操作，则之前的最后一个语句 `End Get` 应为 `Return` 语句。</span><span class="sxs-lookup"><span data-stu-id="1072c-118">If you do this, the last statement before `End Get` should be a `Return` statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="1072c-119">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1072c-119">See also</span></span>

- [<span data-ttu-id="1072c-120">Property 过程</span><span class="sxs-lookup"><span data-stu-id="1072c-120">Property Procedures</span></span>](../../programming-guide/language-features/procedures/property-procedures.md)
- [<span data-ttu-id="1072c-121">Property Statement</span><span class="sxs-lookup"><span data-stu-id="1072c-121">Property Statement</span></span>](../statements/property-statement.md)
- [<span data-ttu-id="1072c-122">Get 语句</span><span class="sxs-lookup"><span data-stu-id="1072c-122">Get Statement</span></span>](../statements/get-statement.md)
