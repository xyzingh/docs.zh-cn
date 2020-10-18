---
title: 在 lambda 表达式中使用迭代变量可能会产生意外的结果
ms.date: 07/20/2015
f1_keywords:
- vbc42324
- bc42324
helpviewer_keywords:
- BC42324
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
ms.openlocfilehash: d0deea94084565ea91debe2b6db30def4cd9e00e
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161486"
---
# <a name="bc42324-using-the-iteration-variable-in-a-lambda-expression-may-have-unexpected-results"></a><span data-ttu-id="37705-102">BC42324：在 lambda 表达式中使用迭代变量可能会产生意外的结果</span><span class="sxs-lookup"><span data-stu-id="37705-102">BC42324: Using the iteration variable in a lambda expression may have unexpected results</span></span>

<span data-ttu-id="37705-103">在 lambda 表达式中使用迭代变量可能会产生意外的结果。</span><span class="sxs-lookup"><span data-stu-id="37705-103">Using the iteration variable in a lambda expression may have unexpected results.</span></span> <span data-ttu-id="37705-104">改为在循环内创建一个局部变量，并为其分配迭代变量的值。</span><span class="sxs-lookup"><span data-stu-id="37705-104">Instead, create a local variable within the loop and assign it the value of the iteration variable.</span></span>

 <span data-ttu-id="37705-105">如果在循环中声明的 lambda 表达式中使用循环迭代变量，则会出现此警告。</span><span class="sxs-lookup"><span data-stu-id="37705-105">This warning appears when you use a loop iteration variable in a lambda expression that is declared inside the loop.</span></span> <span data-ttu-id="37705-106">例如，下面的示例将导致出现警告。</span><span class="sxs-lookup"><span data-stu-id="37705-106">For example, the following example causes the warning to appear.</span></span>

```vb
For i As Integer = 1 To 10
    ' The warning is given for the use of i.
    Dim exampleFunc As Func(Of Integer) = Function() i
Next
```

 <span data-ttu-id="37705-107">下面的示例显示了可能出现的意外结果。</span><span class="sxs-lookup"><span data-stu-id="37705-107">The following example shows the unexpected results that might occur.</span></span>

```vb
Module Module1
    Sub Main()
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}

        For i As Integer = 0 To 4
            array1(i) = Function() i
        Next

        For Each funcElement In array1
            System.Console.WriteLine(funcElement())
        Next

    End Sub
End Module
```

 <span data-ttu-id="37705-108">`For`循环创建 lambda 表达式的数组，其中每个表达式都返回循环迭代变量的值 `i` 。</span><span class="sxs-lookup"><span data-stu-id="37705-108">The `For` loop creates an array of lambda expressions, each of which returns the value of the loop iteration variable `i`.</span></span> <span data-ttu-id="37705-109">当在循环中计算 lambda 表达式时 `For Each` ，可能会发现在循环中显示0、1、2、3和4的后续值 `i` `For` 。</span><span class="sxs-lookup"><span data-stu-id="37705-109">When the lambda expressions are evaluated in the `For Each` loop, you might expect to see 0, 1, 2, 3, and 4 displayed, the successive values of `i` in the `For` loop.</span></span> <span data-ttu-id="37705-110">相反，您将看到显示的五次的最终值 `i` ：</span><span class="sxs-lookup"><span data-stu-id="37705-110">Instead, you see the final value of `i` displayed five times:</span></span>

 `5`

 `5`

 `5`

 `5`

 `5`

 <span data-ttu-id="37705-111">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="37705-111">By default, this message is a warning.</span></span> <span data-ttu-id="37705-112">有关隐藏警告或将警告视为错误的详细信息，请参阅 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="37705-112">For more information about hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="37705-113">**错误 ID：** BC42324</span><span class="sxs-lookup"><span data-stu-id="37705-113">**Error ID:** BC42324</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="37705-114">更正此错误</span><span class="sxs-lookup"><span data-stu-id="37705-114">To correct this error</span></span>

- <span data-ttu-id="37705-115">将迭代变量的值分配给局部变量，并在 lambda 表达式中使用该局部变量。</span><span class="sxs-lookup"><span data-stu-id="37705-115">Assign the value of the iteration variable to a local variable, and use the local variable in the lambda expression.</span></span>

```vb
Module Module1
    Sub Main()
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}

        For i As Integer = 0 To 4
            Dim j = i
            array1(i) = Function() j
        Next

        For Each funcElement In array1
            System.Console.WriteLine(funcElement())
        Next

    End Sub
End Module
```

## <a name="see-also"></a><span data-ttu-id="37705-116">请参阅</span><span class="sxs-lookup"><span data-stu-id="37705-116">See also</span></span>

- [<span data-ttu-id="37705-117">Lambda 表达式</span><span class="sxs-lookup"><span data-stu-id="37705-117">Lambda Expressions</span></span>](../../programming-guide/language-features/procedures/lambda-expressions.md)
