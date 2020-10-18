---
title: “<name1>”不明确，从命名空间或类型“<name2>”导入
ms.date: 07/20/2015
f1_keywords:
- vbc30561
- bc30561
helpviewer_keywords:
- BC30561
ms.assetid: 761091f7-1018-4299-b481-3966a4a2c126
ms.openlocfilehash: 73cc604f1e3a06687ca93779a01e698512be198b
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160179"
---
# <a name="bc30561-name1-is-ambiguous-imported-from-the-namespaces-or-types-name2"></a><span data-ttu-id="33978-102">BC30561： " \<name1> " 不明确，从命名空间或类型 "" 导入 \<name2></span><span class="sxs-lookup"><span data-stu-id="33978-102">BC30561: '\<name1>' is ambiguous, imported from the namespaces or types '\<name2>'</span></span>

<span data-ttu-id="33978-103">你提供的名称不明确，因此与另一个名称冲突。</span><span class="sxs-lookup"><span data-stu-id="33978-103">You have provided a name that is ambiguous and therefore conflicts with another name.</span></span> <span data-ttu-id="33978-104">Visual Basic 编译器没有任何冲突解决规则;你必须自己区分名称。</span><span class="sxs-lookup"><span data-stu-id="33978-104">The Visual Basic compiler does not have any conflict resolution rules; you must disambiguate names yourself.</span></span>

 <span data-ttu-id="33978-105">**错误 ID：** BC30561</span><span class="sxs-lookup"><span data-stu-id="33978-105">**Error ID:** BC30561</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="33978-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="33978-106">To correct this error</span></span>

- <span data-ttu-id="33978-107">删除命名空间导入，消除名称歧义。</span><span class="sxs-lookup"><span data-stu-id="33978-107">Disambiguate the name by removing namespace imports.</span></span>

- <span data-ttu-id="33978-108">完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="33978-108">Fully qualify the name.</span></span>

## <a name="see-also"></a><span data-ttu-id="33978-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="33978-109">See also</span></span>

- [<span data-ttu-id="33978-110">Imports 语句（.NET 命名空间和类型）</span><span class="sxs-lookup"><span data-stu-id="33978-110">Imports Statement (.NET Namespace and Type)</span></span>](../statements/imports-statement-net-namespace-and-type.md)
- [<span data-ttu-id="33978-111">Visual Basic 中的命名空间</span><span class="sxs-lookup"><span data-stu-id="33978-111">Namespaces in Visual Basic</span></span>](../../programming-guide/program-structure/namespaces.md)
- [<span data-ttu-id="33978-112">Namespace 语句</span><span class="sxs-lookup"><span data-stu-id="33978-112">Namespace Statement</span></span>](../statements/namespace-statement.md)
