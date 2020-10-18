---
title: 类型参数不能用作限定符
ms.date: 07/20/2015
f1_keywords:
- vbc32098
- bc32098
helpviewer_keywords:
- BC32098
ms.assetid: bab05325-dde8-4621-a5f6-368b5b7b2d76
ms.openlocfilehash: 14e6094b0cc129eba86db1808c0f0575955f5e75
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161187"
---
# <a name="bc32098-type-parameters-cannot-be-used-as-qualifiers"></a><span data-ttu-id="22fb6-102">BC32098：不能将类型参数用作限定符</span><span class="sxs-lookup"><span data-stu-id="22fb6-102">BC32098: Type parameters cannot be used as qualifiers</span></span>

<span data-ttu-id="22fb6-103">使用包含类型参数的限定字符串限定编程元素。</span><span class="sxs-lookup"><span data-stu-id="22fb6-103">A programming element is qualified with a qualification string that includes a type parameter.</span></span>

<span data-ttu-id="22fb6-104">类型参数表示在构造泛型类型时要提供的类型的要求。</span><span class="sxs-lookup"><span data-stu-id="22fb6-104">A type parameter represents a requirement for a type that is to be supplied when the generic type is constructed.</span></span> <span data-ttu-id="22fb6-105">它不表示特定的已定义类型。</span><span class="sxs-lookup"><span data-stu-id="22fb6-105">It does not represent a specific defined type.</span></span> <span data-ttu-id="22fb6-106">限定字符串必须只包含在编译时定义的元素。</span><span class="sxs-lookup"><span data-stu-id="22fb6-106">A qualification string must include only elements that are defined at compile time.</span></span>

<span data-ttu-id="22fb6-107">以下代码可能会生成此错误：</span><span class="sxs-lookup"><span data-stu-id="22fb6-107">The following code can generate this error:</span></span>

```vb
Public Function CheckText(Of c As System.Windows.Forms.Control)(
    badText As String) As Boolean

    Dim saveText As c.Text
    ' Insert code to look for badText within saveText.
End Function
```

 <span data-ttu-id="22fb6-108">**错误 ID：** BC32098</span><span class="sxs-lookup"><span data-stu-id="22fb6-108">**Error ID:** BC32098</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="22fb6-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="22fb6-109">To correct this error</span></span>

1. <span data-ttu-id="22fb6-110">从限定字符串中删除类型参数，或将其替换为定义的类型。</span><span class="sxs-lookup"><span data-stu-id="22fb6-110">Remove the type parameter from the qualification string, or replace it with a defined type.</span></span>

2. <span data-ttu-id="22fb6-111">如果需要使用构造类型来查找要限定的编程元素，则必须使用其他程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="22fb6-111">If you need to use a constructed type to locate the programming element being qualified, you must use additional program logic.</span></span>

## <a name="see-also"></a><span data-ttu-id="22fb6-112">另请参阅</span><span class="sxs-lookup"><span data-stu-id="22fb6-112">See also</span></span>

- [<span data-ttu-id="22fb6-113">References to Declared Elements</span><span class="sxs-lookup"><span data-stu-id="22fb6-113">References to Declared Elements</span></span>](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [<span data-ttu-id="22fb6-114">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="22fb6-114">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
- [<span data-ttu-id="22fb6-115">Type List</span><span class="sxs-lookup"><span data-stu-id="22fb6-115">Type List</span></span>](../statements/type-list.md)
