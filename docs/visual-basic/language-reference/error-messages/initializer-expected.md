---
title: 应为初始值设定项
ms.date: 07/20/2015
f1_keywords:
- vbc30996
- bc30996
helpviewer_keywords:
- BC30996
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
ms.openlocfilehash: cbe77bab3e4f8bf2094c70c1c16d95ee897c729e
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163007"
---
# <a name="bc30996-initializer-expected"></a><span data-ttu-id="65dab-102">BC30996：应为初始值设定项</span><span class="sxs-lookup"><span data-stu-id="65dab-102">BC30996: Initializer expected</span></span>

<span data-ttu-id="65dab-103">您尝试使用对象初始值设定项声明类的实例，其中初始化列表为空，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="65dab-103">You have tried to declare an instance of a class by using an object initializer in which the initialization list is empty, as shown in the following example.</span></span>

 `' Not valid.`

 `' Dim aStudent As New Student With {}`

 <span data-ttu-id="65dab-104">至少必须在初始值设定项列表中初始化一个字段或属性，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="65dab-104">At least one field or property must be initialized in the initializer list, as shown in the following example.</span></span>

 `Dim aStudent As New Student With {.year = "Senior"}`

 <span data-ttu-id="65dab-105">**错误 ID：** BC30996</span><span class="sxs-lookup"><span data-stu-id="65dab-105">**Error ID:** BC30996</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="65dab-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="65dab-106">To correct this error</span></span>

- <span data-ttu-id="65dab-107">在初始值设定项中初始化至少一个字段或属性，或不使用对象初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="65dab-107">Initialize at least one field or property in the initializer, or do not use an object initializer.</span></span>

## <a name="see-also"></a><span data-ttu-id="65dab-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="65dab-108">See also</span></span>

- [<span data-ttu-id="65dab-109">对象初始值设定项：命名和匿名类型</span><span class="sxs-lookup"><span data-stu-id="65dab-109">Object Initializers: Named and Anonymous Types</span></span>](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [<span data-ttu-id="65dab-110">如何：使用对象初始值设定项声明对象</span><span class="sxs-lookup"><span data-stu-id="65dab-110">How to: Declare an Object by Using an Object Initializer</span></span>](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
