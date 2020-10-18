---
title: “System.Nullable(Of T)”的方法不能用作“AddressOf”运算符的操作数
ms.date: 07/20/2015
f1_keywords:
- vbc32126
- bc32126
helpviewer_keywords:
- BC32126
ms.assetid: 2325668b-e2ad-40ee-a1ec-30450236c20d
ms.openlocfilehash: 173cf19537e3f9ffc4cff6cef71f34b6d365e5d3
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160387"
---
# <a name="bc32126-methods-of-systemnullableof-t-cannot-be-used-as-operands-of-the-addressof-operator"></a><span data-ttu-id="606c4-102">BC32126：不能将 ") " 的 ("" 的方法用作 "AddressOf" 运算符的操作数</span><span class="sxs-lookup"><span data-stu-id="606c4-102">BC32126: Methods of 'System.Nullable(Of T)' cannot be used as operands of the 'AddressOf' operator</span></span>

<span data-ttu-id="606c4-103">语句将 `AddressOf` 运算符与表示结构过程的操作数一起使用 <xref:System.Nullable%601> 。</span><span class="sxs-lookup"><span data-stu-id="606c4-103">A statement uses the `AddressOf` operator with an operand that represents a procedure of the <xref:System.Nullable%601> structure.</span></span>

 <span data-ttu-id="606c4-104">**错误 ID：** BC32126</span><span class="sxs-lookup"><span data-stu-id="606c4-104">**Error ID:** BC32126</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="606c4-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="606c4-105">To correct this error</span></span>

- <span data-ttu-id="606c4-106">将子句中的过程名称替换 `AddressOf` 为不是的成员的操作数 <xref:System.Nullable%601> 。</span><span class="sxs-lookup"><span data-stu-id="606c4-106">Replace the procedure name in the `AddressOf` clause with an operand that is not a member of <xref:System.Nullable%601>.</span></span>

- <span data-ttu-id="606c4-107">编写一个类，用于包装要使用的的方法 <xref:System.Nullable%601> 。</span><span class="sxs-lookup"><span data-stu-id="606c4-107">Write a class that wraps the method of <xref:System.Nullable%601> that you want to use.</span></span> <span data-ttu-id="606c4-108">在下面的示例中， `NullableWrapper` 类定义了一个名为的新方法 `GetValueOrDefault` 。</span><span class="sxs-lookup"><span data-stu-id="606c4-108">In the following example, the `NullableWrapper` class defines a new method named `GetValueOrDefault`.</span></span> <span data-ttu-id="606c4-109">由于此新方法不是的成员 <xref:System.Nullable%601> ，因此可将其应用到可以 `nullInstance` 为 null 的类型的实例，以形成的参数 `AddressOf` 。</span><span class="sxs-lookup"><span data-stu-id="606c4-109">Because this new method is not a member of <xref:System.Nullable%601>, it can be applied to `nullInstance`, an instance of a nullable type, to form an argument for `AddressOf`.</span></span>

```vb
Module Module1

    Delegate Function Deleg() As Integer

    Sub Main()
        Dim nullInstance As New Nullable(Of Integer)(1)

        Dim del As Deleg

        ' GetValueOrDefault is a method of the Nullable generic
        ' type. It cannot be used as an operand of AddressOf.
        ' del = AddressOf nullInstance.GetValueOrDefault

        ' The following line uses the GetValueOrDefault method
        ' defined in the NullableWrapper class.
        del = AddressOf (New NullableWrapper(
            Of Integer)(nullInstance)).GetValueOrDefault

        Console.WriteLine(del.Invoke())
    End Sub

    Class NullableWrapper(Of T As Structure)
        Private m_Value As Nullable(Of T)

        Sub New(ByVal Value As Nullable(Of T))
            m_Value = Value
        End Sub

        Public Function GetValueOrDefault() As T
            Return m_Value.Value
        End Function
    End Class
End Module
```

## <a name="see-also"></a><span data-ttu-id="606c4-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="606c4-110">See also</span></span>

- <xref:System.Nullable%601>
- [<span data-ttu-id="606c4-111">AddressOf 运算符</span><span class="sxs-lookup"><span data-stu-id="606c4-111">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="606c4-112">可以为 null 的值类型</span><span class="sxs-lookup"><span data-stu-id="606c4-112">Nullable Value Types</span></span>](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [<span data-ttu-id="606c4-113">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="606c4-113">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
