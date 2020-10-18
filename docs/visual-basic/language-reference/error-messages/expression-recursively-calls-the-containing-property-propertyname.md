---
title: 表达式递归调用包含属性“<propertyname>”
ms.date: 07/20/2015
f1_keywords:
- vbc42026
- BC42026
helpviewer_keywords:
- BC42026
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
ms.openlocfilehash: f5b8b226d46afa0555559de0930f20025ba27f2b
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162760"
---
# <a name="bc42026-expression-recursively-calls-the-containing-property-propertyname"></a><span data-ttu-id="5283d-102">BC42026：表达式递归调用包含属性 " \<propertyname> "</span><span class="sxs-lookup"><span data-stu-id="5283d-102">BC42026: Expression recursively calls the containing property '\<propertyname>'</span></span>

<span data-ttu-id="5283d-103">属性定义过程中的语句将 `Set` 值存储到属性的名称中。</span><span class="sxs-lookup"><span data-stu-id="5283d-103">A statement in the `Set` procedure of a property definition stores a value into the name of the property.</span></span>

 <span data-ttu-id="5283d-104">保存属性值的建议方法是在 `Private` 属性的容器中定义一个变量，并在和过程中使用它 `Get` `Set` 。</span><span class="sxs-lookup"><span data-stu-id="5283d-104">The recommended approach to holding the value of a property is to define a `Private` variable in the property's container and use it in both the `Get` and `Set` procedures.</span></span> <span data-ttu-id="5283d-105">然后，该 `Set` 过程应将传入值存储在此 `Private` 变量中。</span><span class="sxs-lookup"><span data-stu-id="5283d-105">The `Set` procedure should then store the incoming value in this `Private` variable.</span></span>

 <span data-ttu-id="5283d-106">此 `Get` 过程的行为类似于 `Function` 过程，因此它可以为属性名称赋值，并通过遇到语句来返回控件 `End Get` 。</span><span class="sxs-lookup"><span data-stu-id="5283d-106">The `Get` procedure behaves like a `Function` procedure, so it can assign a value to the property name and return control by encountering the `End Get` statement.</span></span> <span data-ttu-id="5283d-107">不过，建议的方法是 `Private` 在 [返回语句](../statements/return-statement.md)中包含变量作为值。</span><span class="sxs-lookup"><span data-stu-id="5283d-107">The recommended approach, however, is to include the `Private` variable as the value in a [Return Statement](../statements/return-statement.md).</span></span>

 <span data-ttu-id="5283d-108">此 `Set` 过程的行为类似于 `Sub` 过程，该过程不返回值。</span><span class="sxs-lookup"><span data-stu-id="5283d-108">The `Set` procedure behaves like a `Sub` procedure, which does not return a value.</span></span> <span data-ttu-id="5283d-109">因此，过程或属性名称在过程中没有特殊含义 `Set` ，因此不能在其中存储值。</span><span class="sxs-lookup"><span data-stu-id="5283d-109">Therefore, the procedure or property name has no special meaning within a `Set` procedure, and you cannot store a value into it.</span></span>

 <span data-ttu-id="5283d-110">下面的示例说明了可能导致此错误的方法，并遵循建议的方法。</span><span class="sxs-lookup"><span data-stu-id="5283d-110">The following example illustrates the approach that can cause this error, followed by the recommended approach.</span></span>

```vb
Public Class illustrateProperties
' The code in the following property causes this error.
    Public Property badProp() As Char
        Get
            Dim charValue As Char
            ' Insert code to update charValue.
            badProp = charValue
        End Get
        Set(ByVal Value As Char)
            ' The following statement causes this error.
            badProp = Value
            ' The value stored in the local variable badProp
            ' is not used by the Get procedure in this property.
        End Set
    End Property
' The following code uses the recommended approach.
    Private propValue As Char
    Public Property goodProp() As Char
        Get
            ' Insert code to update propValue.
            Return propValue
        End Get
        Set(ByVal Value As Char)
            propValue = Value
        End Set
    End Property
End Class
```

 <span data-ttu-id="5283d-111">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="5283d-111">By default, this message is a warning.</span></span> <span data-ttu-id="5283d-112">有关隐藏警告或将警告视为错误的详细信息，请参阅 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="5283d-112">For more information about hiding warnings or treating warnings as errors, please see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="5283d-113">**错误 ID：** BC42026</span><span class="sxs-lookup"><span data-stu-id="5283d-113">**Error ID:** BC42026</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="5283d-114">更正此错误</span><span class="sxs-lookup"><span data-stu-id="5283d-114">To correct this error</span></span>

- <span data-ttu-id="5283d-115">如前面的示例所示，重写属性定义以使用建议的方法。</span><span class="sxs-lookup"><span data-stu-id="5283d-115">Rewrite the property definition to use the recommended approach as illustrated in the preceding example.</span></span>

## <a name="see-also"></a><span data-ttu-id="5283d-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5283d-116">See also</span></span>

- [<span data-ttu-id="5283d-117">Property 过程</span><span class="sxs-lookup"><span data-stu-id="5283d-117">Property Procedures</span></span>](../../programming-guide/language-features/procedures/property-procedures.md)
- [<span data-ttu-id="5283d-118">Property Statement</span><span class="sxs-lookup"><span data-stu-id="5283d-118">Property Statement</span></span>](../statements/property-statement.md)
- [<span data-ttu-id="5283d-119">Set 语句</span><span class="sxs-lookup"><span data-stu-id="5283d-119">Set Statement</span></span>](../statements/set-statement.md)
