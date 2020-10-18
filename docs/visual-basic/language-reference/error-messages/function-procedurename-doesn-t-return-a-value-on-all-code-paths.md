---
title: 函数“<procedurename>”并非在所有代码路径上都返回值
ms.date: 07/20/2015
f1_keywords:
- bc42105
- vbc42105
helpviewer_keywords:
- BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
ms.openlocfilehash: 19b305e337767dfb34718aed7b665f142851bd36
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163358"
---
# <a name="bc42105-function-procedurename-doesnt-return-a-value-on-all-code-paths"></a><span data-ttu-id="05b73-102">BC42105：函数 " \<procedurename> " 不会在所有代码路径上都返回值</span><span class="sxs-lookup"><span data-stu-id="05b73-102">BC42105: Function '\<procedurename>' doesn't return a value on all code paths</span></span>

<span data-ttu-id="05b73-103">函数 " \<procedurename> " 不会在所有代码路径上都返回值。</span><span class="sxs-lookup"><span data-stu-id="05b73-103">Function '\<procedurename>' doesn't return a value on all code paths.</span></span> <span data-ttu-id="05b73-104">是否缺少 "Return" 语句？</span><span class="sxs-lookup"><span data-stu-id="05b73-104">Are you missing a 'Return' statement?</span></span>

 <span data-ttu-id="05b73-105">`Function`过程至少有一个可能的路径，其代码中不返回值。</span><span class="sxs-lookup"><span data-stu-id="05b73-105">A `Function` procedure has at least one possible path through its code that does not return a value.</span></span>

 <span data-ttu-id="05b73-106">可以通过 `Function` 以下任一方式从过程返回值：</span><span class="sxs-lookup"><span data-stu-id="05b73-106">You can return a value from a `Function` procedure in any of the following ways:</span></span>

- <span data-ttu-id="05b73-107">在 [Return 语句](../statements/return-statement.md)中包含值。</span><span class="sxs-lookup"><span data-stu-id="05b73-107">Include the value in a [Return Statement](../statements/return-statement.md).</span></span>

- <span data-ttu-id="05b73-108">将值分配给 `Function` 过程名称，然后执行 `Exit Function` 语句。</span><span class="sxs-lookup"><span data-stu-id="05b73-108">Assign the value to the `Function` procedure name and then perform an `Exit Function` statement.</span></span>

- <span data-ttu-id="05b73-109">将值分配给 `Function` 过程名称，然后执行 `End Function` 语句。</span><span class="sxs-lookup"><span data-stu-id="05b73-109">Assign the value to the `Function` procedure name and then perform the `End Function` statement.</span></span>

 <span data-ttu-id="05b73-110">如果控件传递给 `Exit Function` 或 `End Function` 并且您没有为过程名称赋值，则该过程将返回返回数据类型的默认值。</span><span class="sxs-lookup"><span data-stu-id="05b73-110">If control passes to `Exit Function` or `End Function` and you have not assigned any value to the procedure name, the procedure returns the default value of the return data type.</span></span> <span data-ttu-id="05b73-111">有关详细信息，请参阅 [Function 语句](../statements/function-statement.md)中的 "行为"。</span><span class="sxs-lookup"><span data-stu-id="05b73-111">For more information, see "Behavior" in [Function Statement](../statements/function-statement.md).</span></span>

 <span data-ttu-id="05b73-112">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="05b73-112">By default, this message is a warning.</span></span> <span data-ttu-id="05b73-113">有关隐藏警告或将警告视为错误的详细信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="05b73-113">For more information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="05b73-114">**错误 ID：** BC42105</span><span class="sxs-lookup"><span data-stu-id="05b73-114">**Error ID:** BC42105</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="05b73-115">更正此错误</span><span class="sxs-lookup"><span data-stu-id="05b73-115">To correct this error</span></span>

- <span data-ttu-id="05b73-116">检查控制流逻辑，并确保在导致返回的每个语句之前赋值。</span><span class="sxs-lookup"><span data-stu-id="05b73-116">Check your control flow logic and make sure you assign a value before every statement that causes a return.</span></span>

     <span data-ttu-id="05b73-117">如果始终使用语句，则更容易保证每次从过程返回一个值 `Return` 。</span><span class="sxs-lookup"><span data-stu-id="05b73-117">It is easier to guarantee that every return from the procedure returns a value if you always use the `Return` statement.</span></span> <span data-ttu-id="05b73-118">如果执行此操作，则之前的最后一个语句 `End Function` 应为 `Return` 语句。</span><span class="sxs-lookup"><span data-stu-id="05b73-118">If you do this, the last statement before `End Function` should be a `Return` statement.</span></span>

## <a name="see-also"></a><span data-ttu-id="05b73-119">另请参阅</span><span class="sxs-lookup"><span data-stu-id="05b73-119">See also</span></span>

- [<span data-ttu-id="05b73-120">Function 过程</span><span class="sxs-lookup"><span data-stu-id="05b73-120">Function Procedures</span></span>](../../programming-guide/language-features/procedures/function-procedures.md)
- [<span data-ttu-id="05b73-121">Function 语句</span><span class="sxs-lookup"><span data-stu-id="05b73-121">Function Statement</span></span>](../statements/function-statement.md)
- [<span data-ttu-id="05b73-122">“项目设计器”->“编译”页 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="05b73-122">Compile Page, Project Designer (Visual Basic)</span></span>](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
