---
title: “<membername>”不能通过 <typename>“<containertype>”在项目外部公开类型“<containertypename>”
ms.date: 07/20/2015
f1_keywords:
- bc30909
- vbc30909
helpviewer_keywords:
- BC30909
ms.assetid: ffa7395d-e182-4087-8ce8-079810fdae54
ms.openlocfilehash: a3972eabfe297b89c0e4d0f36943ac58e5bdf688
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162461"
---
# <a name="bc30909-membername-cannot-expose-type-typename-outside-the-project-through-containertype-containertypename"></a><span data-ttu-id="86589-102">BC30909： " \<membername> " 不能 \<typename> 通过 \<containertype> "" 在项目外部公开类型 "" \<containertypename></span><span class="sxs-lookup"><span data-stu-id="86589-102">BC30909: '\<membername>' cannot expose type '\<typename>' outside the project through \<containertype> '\<containertypename>'</span></span>

<span data-ttu-id="86589-103">变量、过程参数或函数返回在其容器外部公开，但它被声明为不得在容器外部公开的类型。</span><span class="sxs-lookup"><span data-stu-id="86589-103">A variable, procedure parameter, or function return is exposed outside its container, but it is declared as a type that must not be exposed outside the container.</span></span>

 <span data-ttu-id="86589-104">以下框架代码显示了生成此错误的情况。</span><span class="sxs-lookup"><span data-stu-id="86589-104">The following skeleton code shows a situation that generates this error.</span></span>

```vb
Private Class privateClass
End Class
Public Class mainClass
    Public exposedVar As New privateClass
End Class
```

 <span data-ttu-id="86589-105">声明为、、或的类型 `Protected` `Friend` 旨在在 `Protected Friend` `Private` 其声明上下文之外进行有限的访问。</span><span class="sxs-lookup"><span data-stu-id="86589-105">A type that is declared `Protected`, `Friend`, `Protected Friend`, or `Private` is intended to have limited access outside its declaration context.</span></span> <span data-ttu-id="86589-106">将其用作受限访问的变量的数据类型将会降低此目的。</span><span class="sxs-lookup"><span data-stu-id="86589-106">Using it as the data type of a variable with less restricted access would defeat this purpose.</span></span> <span data-ttu-id="86589-107">在前面的代码中， `exposedVar` 是，将 `Public` 公开 `privateClass` 给不应访问它的代码。</span><span class="sxs-lookup"><span data-stu-id="86589-107">In the preceding skeleton code, `exposedVar` is `Public` and would expose `privateClass` to code that should not have access to it.</span></span>

 <span data-ttu-id="86589-108">**错误 ID：** BC30909</span><span class="sxs-lookup"><span data-stu-id="86589-108">**Error ID:** BC30909</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="86589-109">更正此错误</span><span class="sxs-lookup"><span data-stu-id="86589-109">To correct this error</span></span>

- <span data-ttu-id="86589-110">更改变量、过程参数或函数返回的访问级别，使其至少与数据类型的访问级别具有相同的限制。</span><span class="sxs-lookup"><span data-stu-id="86589-110">Change the access level of the variable, procedure parameter, or function return to be at least as restrictive as the access level of its data type.</span></span>

## <a name="see-also"></a><span data-ttu-id="86589-111">另请参阅</span><span class="sxs-lookup"><span data-stu-id="86589-111">See also</span></span>

- [<span data-ttu-id="86589-112">Visual Basic 中的访问级别</span><span class="sxs-lookup"><span data-stu-id="86589-112">Access levels in Visual Basic</span></span>](../../programming-guide/language-features/declared-elements/access-levels.md)
