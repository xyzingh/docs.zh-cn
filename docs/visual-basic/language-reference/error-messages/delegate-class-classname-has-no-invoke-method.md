---
title: 委托类“<classname>”没有 Invoke 方法，所以此类型的表达式不能作为方法调用的目标
ms.date: 07/20/2015
f1_keywords:
- vbc30220
- bc30220
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
ms.openlocfilehash: 4e0fc61c7356008755134f670fa1fab0165cfd48
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162786"
---
# <a name="bc30220-delegate-class-classname-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a><span data-ttu-id="f0ba2-102">BC30220：委托类 " \<classname> " 没有 Invoke 方法，所以此类型的表达式不能作为方法调用的目标</span><span class="sxs-lookup"><span data-stu-id="f0ba2-102">BC30220: Delegate class '\<classname>' has no Invoke method, so an expression of this type cannot be the target of a method call</span></span>

<span data-ttu-id="f0ba2-103">`Invoke`通过委托调用失败，因为 `Invoke` 未在委托类上实现。</span><span class="sxs-lookup"><span data-stu-id="f0ba2-103">A call to `Invoke` through a delegate has failed because `Invoke` is not implemented on the delegate class.</span></span>

 <span data-ttu-id="f0ba2-104">**错误 ID：** BC30220</span><span class="sxs-lookup"><span data-stu-id="f0ba2-104">**Error ID:** BC30220</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="f0ba2-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="f0ba2-105">To correct this error</span></span>

1. <span data-ttu-id="f0ba2-106">请确保已使用语句创建了委托类的实例 `Dim` ，并且已使用运算符将一个过程分配给了该委托实例 `AddressOf` 。</span><span class="sxs-lookup"><span data-stu-id="f0ba2-106">Ensure that an instance of the delegate class has been created with a `Dim` statement and that a procedure has been assigned to the delegate instance with the `AddressOf` operator.</span></span>

2. <span data-ttu-id="f0ba2-107">找到实现委托类的代码，并确保它实现 `Invoke` 过程。</span><span class="sxs-lookup"><span data-stu-id="f0ba2-107">Locate the code that implements the delegate class and make sure it implements the `Invoke` procedure.</span></span>

## <a name="see-also"></a><span data-ttu-id="f0ba2-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f0ba2-108">See also</span></span>

- [<span data-ttu-id="f0ba2-109">委托</span><span class="sxs-lookup"><span data-stu-id="f0ba2-109">Delegates</span></span>](../../programming-guide/language-features/delegates/index.md)
- [<span data-ttu-id="f0ba2-110">Delegate 语句</span><span class="sxs-lookup"><span data-stu-id="f0ba2-110">Delegate Statement</span></span>](../statements/delegate-statement.md)
- [<span data-ttu-id="f0ba2-111">AddressOf 运算符</span><span class="sxs-lookup"><span data-stu-id="f0ba2-111">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="f0ba2-112">Dim 语句</span><span class="sxs-lookup"><span data-stu-id="f0ba2-112">Dim Statement</span></span>](../statements/dim-statement.md)
