---
title: 需要声明
ms.date: 07/20/2015
f1_keywords:
- vbc30188
- bc30188
helpviewer_keywords:
- BC30188
ms.assetid: da6b1df3-fe6b-4415-88e6-0977e5189e0b
ms.openlocfilehash: 2755f5afcb96ca7a6c4d140908649390dd66d571
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162695"
---
# <a name="bc30188-declaration-expected"></a><span data-ttu-id="e4102-102">BC30188：应为声明</span><span class="sxs-lookup"><span data-stu-id="e4102-102">BC30188: Declaration expected</span></span>

<span data-ttu-id="e4102-103">Nondeclarative 语句，如赋值语句或循环语句，在任何过程外发生。</span><span class="sxs-lookup"><span data-stu-id="e4102-103">A nondeclarative statement, such as an assignment or loop statement, occurs outside any procedure.</span></span> <span data-ttu-id="e4102-104">仅允许在过程外使用声明。</span><span class="sxs-lookup"><span data-stu-id="e4102-104">Only declarations are allowed outside procedures.</span></span>

 <span data-ttu-id="e4102-105">或者，在没有声明关键字（如或）的情况下声明编程元素 `Dim` `Const` 。</span><span class="sxs-lookup"><span data-stu-id="e4102-105">Alternatively, a programming element is declared without a declaration keyword such as `Dim` or `Const`.</span></span>

 <span data-ttu-id="e4102-106">**错误 ID：** BC30188</span><span class="sxs-lookup"><span data-stu-id="e4102-106">**Error ID:** BC30188</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="e4102-107">更正此错误</span><span class="sxs-lookup"><span data-stu-id="e4102-107">To correct this error</span></span>

- <span data-ttu-id="e4102-108">将 nondeclarative 语句移到过程的主体。</span><span class="sxs-lookup"><span data-stu-id="e4102-108">Move the nondeclarative statement to the body of a procedure.</span></span>

- <span data-ttu-id="e4102-109">使用适当的声明关键字开始声明。</span><span class="sxs-lookup"><span data-stu-id="e4102-109">Begin the declaration with an appropriate declaration keyword.</span></span>

- <span data-ttu-id="e4102-110">确保声明关键字没有拼写错误。</span><span class="sxs-lookup"><span data-stu-id="e4102-110">Ensure that a declaration keyword is not misspelled.</span></span>

## <a name="see-also"></a><span data-ttu-id="e4102-111">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e4102-111">See also</span></span>

- [<span data-ttu-id="e4102-112">过程</span><span class="sxs-lookup"><span data-stu-id="e4102-112">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
- [<span data-ttu-id="e4102-113">Dim 语句</span><span class="sxs-lookup"><span data-stu-id="e4102-113">Dim Statement</span></span>](../statements/dim-statement.md)
