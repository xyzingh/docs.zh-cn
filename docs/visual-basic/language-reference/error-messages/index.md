---
title: Visual Basic 错误消息
titleSuffix: ''
ms.date: 10/13/2020
helpviewer_keywords:
- errors [Visual Basic]
- error messages
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
ms.openlocfilehash: 70973b6d34ed1a84a38af3694e144dfcefa61c20
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163371"
---
# <a name="error-messages-in-visual-basic"></a><span data-ttu-id="a11e0-102">Visual Basic 中的错误消息</span><span class="sxs-lookup"><span data-stu-id="a11e0-102">Error messages in Visual Basic</span></span>

<span data-ttu-id="a11e0-103">在编译或运行 Visual Basic 应用程序时，可能会出现以下类型的错误：</span><span class="sxs-lookup"><span data-stu-id="a11e0-103">When you compile or run a Visual Basic application, the following types of errors can occur:</span></span>

- <span data-ttu-id="a11e0-104">编译时错误，在编译应用程序时发生。</span><span class="sxs-lookup"><span data-stu-id="a11e0-104">Compile-time errors, which occur when you compile an application.</span></span>

- <span data-ttu-id="a11e0-105">运行时错误，在应用程序运行时发生。</span><span class="sxs-lookup"><span data-stu-id="a11e0-105">Run-time errors, which occur when an application is running.</span></span>

<span data-ttu-id="a11e0-106">若要了解如何排查特定错误，请参阅[为 Visual Basic 程序员提供的附加资源](../../getting-started/additional-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="a11e0-106">For information about how to troubleshoot a specific error, see [Additional Resources for Visual Basic Programmers](../../getting-started/additional-resources.md).</span></span>

## <a name="run-time-errors"></a><span data-ttu-id="a11e0-107">运行时错误</span><span class="sxs-lookup"><span data-stu-id="a11e0-107">Run-time errors</span></span>

<span data-ttu-id="a11e0-108">如果 Visual Basic 应用程序尝试执行系统无法执行的操作，则会发生运行时错误，并且 Visual Basic 会引发 <xref:System.Exception> 对象。</span><span class="sxs-lookup"><span data-stu-id="a11e0-108">If a Visual Basic application tries to perform an action that the system can't execute, a run-time error occurs, and Visual Basic throws an <xref:System.Exception> object.</span></span> <span data-ttu-id="a11e0-109">Visual Basic 可以通过使用语句，生成任何数据类型（包括对象）的自定义错误 `Exception` `Throw` 。</span><span class="sxs-lookup"><span data-stu-id="a11e0-109">Visual Basic can generate custom errors of any data type, including `Exception` objects, by using the `Throw` statement.</span></span> <span data-ttu-id="a11e0-110">应用程序可以通过显示捕获到的异常的错误号和消息来识别错误。</span><span class="sxs-lookup"><span data-stu-id="a11e0-110">An application can identify the error by displaying the error number and message of a caught exception.</span></span> <span data-ttu-id="a11e0-111">如果未捕获到错误，应用程序会结束。</span><span class="sxs-lookup"><span data-stu-id="a11e0-111">If an error isn't caught, the application ends.</span></span>

<span data-ttu-id="a11e0-112">代码可用于捕获和检查运行时错误。</span><span class="sxs-lookup"><span data-stu-id="a11e0-112">The code can trap and examine run-time errors.</span></span> <span data-ttu-id="a11e0-113">如果将生成错误的代码封闭在 `Try` 代码块中，则可以在匹配的 `Catch` 代码块中捕获抛出的任何错误。</span><span class="sxs-lookup"><span data-stu-id="a11e0-113">If you enclose the code that produces the error in a `Try` block, you can catch any thrown error within a matching `Catch` block.</span></span> <span data-ttu-id="a11e0-114">若要了解如何在运行时捕获错误并在代码中响应错误，请参阅 [Try...Catch...Finally 语句](../statements/try-catch-finally-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="a11e0-114">For information about how to trap errors at run time and respond to them in your code, see [Try...Catch...Finally Statement](../statements/try-catch-finally-statement.md).</span></span>

## <a name="compile-time-errors"></a><span data-ttu-id="a11e0-115">编译时错误</span><span class="sxs-lookup"><span data-stu-id="a11e0-115">Compile-time errors</span></span>

<span data-ttu-id="a11e0-116">如果 Visual Basic 编译器遇到代码问题，则会发生编译时错误。</span><span class="sxs-lookup"><span data-stu-id="a11e0-116">If the Visual Basic compiler encounters a problem in the code, a compile-time error occurs.</span></span> <span data-ttu-id="a11e0-117">在 Visual Studio 代码编辑器中，你可以轻松地识别导致错误的代码行，因为该代码行下出现一条波浪线。</span><span class="sxs-lookup"><span data-stu-id="a11e0-117">In the Visual Studio code editor, you can easily identify which line of code caused the error because a wavy line appears under that line of code.</span></span> <span data-ttu-id="a11e0-118">指向波形下划线或打开“错误列表”\*\*\*\*，即可看到错误消息（还可以查看其他消息）。</span><span class="sxs-lookup"><span data-stu-id="a11e0-118">The error message appears if you either point to the wavy underline or open the **Error List**, which also shows other messages.</span></span>

<span data-ttu-id="a11e0-119">如果标识符具有波浪形下划线并且在最右边的字符下出现短下划线，则可以为类、构造函数、方法、属性、字段或枚举生成存根。</span><span class="sxs-lookup"><span data-stu-id="a11e0-119">If an identifier has a wavy underline and a short underline appears under the rightmost character, you can generate a stub for the class, constructor, method, property, field, or enum.</span></span> <span data-ttu-id="a11e0-120">有关详细信息，请参阅 [使用 Visual Studio (生成) ](/visualstudio/ide/visual-csharp-intellisense#generate-from-usage)。</span><span class="sxs-lookup"><span data-stu-id="a11e0-120">For more information, see [Generate From Usage (Visual Studio)](/visualstudio/ide/visual-csharp-intellisense#generate-from-usage).</span></span>

<span data-ttu-id="a11e0-121">通过解决 Visual Basic 编译器警告提示的问题，可以编写运行速度更快、bug 更少的代码。</span><span class="sxs-lookup"><span data-stu-id="a11e0-121">By resolving warnings from the Visual Basic compiler, you might be able to write code that runs faster and has fewer bugs.</span></span> <span data-ttu-id="a11e0-122">这些警告可以识别可能会在应用程序运行时生成错误的代码。</span><span class="sxs-lookup"><span data-stu-id="a11e0-122">These warnings identify code that may cause errors when the application is run.</span></span> <span data-ttu-id="a11e0-123">例如，如果尝试调用未赋值的对象变量的成员、让未设置返回值的函数返回值或执行有逻辑错误的 `Try` 代码块来捕获异常，编译器都会生成警告。</span><span class="sxs-lookup"><span data-stu-id="a11e0-123">For example, the compiler warns you if you try to invoke a member of an unassigned object variable, return from a function without setting the return value, or execute a `Try` block with errors in the logic to catch exceptions.</span></span> <span data-ttu-id="a11e0-124">若要详细了解警告（包括如何启用和禁用警告），请参阅[在 Visual Basic 中配置警告](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="a11e0-124">For more information about warnings, including how to turn them on and off, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>
