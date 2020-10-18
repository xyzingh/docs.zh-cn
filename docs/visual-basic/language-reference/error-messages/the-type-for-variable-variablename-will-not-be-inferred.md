---
title: 无法推断出变量“<variablename>”的类型，因为它绑定到封闭范围中的某个字段
ms.date: 07/20/2015
f1_keywords:
- vbc42110
- bc42110
helpviewer_keywords:
- BC42110
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
ms.openlocfilehash: 3e76ffea283de2843fc5586179074c01a053ece8
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161278"
---
# <a name="bc42110-the-type-for-variable-variablename-will-not-be-inferred-because-it-is-bound-to-a-field-in-an-enclosing-scope"></a><span data-ttu-id="6a4d6-102">BC42110：不会推断变量 "" 的类型， \<variablename> 因为它绑定到封闭范围中的某个字段</span><span class="sxs-lookup"><span data-stu-id="6a4d6-102">BC42110: The type for variable '\<variablename>' will not be inferred because it is bound to a field in an enclosing scope</span></span>

<span data-ttu-id="6a4d6-103">不会推断变量 "" 的类型， \<variablename> 因为它绑定到封闭范围中的某个字段。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-103">The type for variable '\<variablename>' will not be inferred because it is bound to a field in an enclosing scope.</span></span> <span data-ttu-id="6a4d6-104">更改 "" 的名称 \<variablename> ，或使用完全限定名称 (例如 "variablename" 或 "variablename" ) 。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-104">Either change the name of '\<variablename>', or use the fully qualified name (for example, 'Me.variablename' or 'MyBase.variablename').</span></span>

<span data-ttu-id="6a4d6-105">代码中的循环控制变量与类的字段或其他封闭范围的名称相同。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-105">A loop control variable in your code has the same name as a field of the class or other enclosing scope.</span></span> <span data-ttu-id="6a4d6-106">因为在没有子句的情况下使用控制变量 `As` ，它将绑定到封闭范围中的字段，并且编译器不会为其创建新的变量，也不会推断其类型。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-106">Because the control variable is used without an `As` clause, it is bound to the field in the enclosing scope, and the compiler does not create a new variable for it or infer its type.</span></span>

<span data-ttu-id="6a4d6-107">在下面的示例中， `Index` 语句中的控制变量 `For` 绑定到 `Index` 类中的字段 `Customer` 。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-107">In the following example, `Index`, the control variable in the `For` statement, is bound to the `Index` field in the `Customer` class.</span></span> <span data-ttu-id="6a4d6-108">编译器不会为控件变量创建新的变量，也不会 `Index` 推断其类型。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-108">The compiler does not create a new variable for the control variable `Index` or infer its type.</span></span>

```vb
Class Customer

    ' The class has a field named Index.
    Private Index As Integer

    Sub Main()

    ' The following line will raise this warning.
        For Index = 1 To 10
            ' ...
        Next

    End Sub
End Class
```

<span data-ttu-id="6a4d6-109">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-109">By default, this message is a warning.</span></span> <span data-ttu-id="6a4d6-110">有关如何隐藏警告或如何将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-110">For information about how to hide warnings or how to treat warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

<span data-ttu-id="6a4d6-111">**错误 ID：** BC42110</span><span class="sxs-lookup"><span data-stu-id="6a4d6-111">**Error ID:** BC42110</span></span>

## <a name="to-address-this-warning"></a><span data-ttu-id="6a4d6-112">解决此警告</span><span class="sxs-lookup"><span data-stu-id="6a4d6-112">To address this warning</span></span>

- <span data-ttu-id="6a4d6-113">将循环控制变量的名称更改为不属于类的字段名称的标识符，使该循环控制变量成为局部变量。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-113">Make the loop control variable local by changing its name to an identifier that is not also the name of a field of the class.</span></span>

  ```vb
  For I = 1 To 10
  ```

- <span data-ttu-id="6a4d6-114">阐明循环控制变量是通过 `Me.` 在变量名称的前面加上前缀来绑定到类字段。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-114">Clarify that the loop control variable binds to the class field by prefixing `Me.` to the variable name.</span></span>

  ```vb
  For Me.Index = 1 To 10
  ```

- <span data-ttu-id="6a4d6-115">使用 `As` 子句来指定循环控制变量的类型，而不是依赖于局部类型推理。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-115">Instead of relying on local type inference, use an `As` clause to specify a type for the loop control variable.</span></span>

  ```vb
  For Index As Integer = 1 To 10
  ```

## <a name="example"></a><span data-ttu-id="6a4d6-116">示例</span><span class="sxs-lookup"><span data-stu-id="6a4d6-116">Example</span></span>

 <span data-ttu-id="6a4d6-117">下面的代码显示了前面的示例，其中的第一个更正是就地的。</span><span class="sxs-lookup"><span data-stu-id="6a4d6-117">The following code shows the earlier example with the first correction in place.</span></span>

```vb
Class Customer

    ' The class has a field named Index.
    Private Index As Integer

    Sub Main()

        For I = 1 To 10
            ' ...
        Next

    End Sub
End Class
```

## <a name="see-also"></a><span data-ttu-id="6a4d6-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6a4d6-118">See also</span></span>

- [<span data-ttu-id="6a4d6-119">Option Infer 语句</span><span class="sxs-lookup"><span data-stu-id="6a4d6-119">Option Infer Statement</span></span>](../statements/option-infer-statement.md)
- [<span data-ttu-id="6a4d6-120">For Each...Next 语句</span><span class="sxs-lookup"><span data-stu-id="6a4d6-120">For Each...Next Statement</span></span>](../statements/for-each-next-statement.md)
- [<span data-ttu-id="6a4d6-121">For...Next 语句</span><span class="sxs-lookup"><span data-stu-id="6a4d6-121">For...Next Statement</span></span>](../statements/for-next-statement.md)
- [<span data-ttu-id="6a4d6-122">如何：引用对象的当前实例</span><span class="sxs-lookup"><span data-stu-id="6a4d6-122">How to: Refer to the Current Instance of an Object</span></span>](../../programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)
- [<span data-ttu-id="6a4d6-123">局部类型推理</span><span class="sxs-lookup"><span data-stu-id="6a4d6-123">Local Type Inference</span></span>](../../programming-guide/language-features/variables/local-type-inference.md)
- [<span data-ttu-id="6a4d6-124">Me、My、MyBase 和 MyClass</span><span class="sxs-lookup"><span data-stu-id="6a4d6-124">Me, My, MyBase, and MyClass</span></span>](../../programming-guide/program-structure/me-my-mybase-and-myclass.md)
