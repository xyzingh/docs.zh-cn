---
title: 范围变量 <variable> 隐藏封闭块中的变量、以前定义的范围变量或在查询表达式中隐式声明的变量
ms.date: 07/20/2015
f1_keywords:
- bc36633
- vbc36633
helpviewer_keywords:
- BC36633
ms.assetid: 5d5470e4-3de5-49c2-8831-1087625f4a77
ms.openlocfilehash: 90fed3dd27f18fe87c326cc36dfb774822fc4b21
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162344"
---
# <a name="bc36633-range-variable-variable-hides-a-variable-in-an-enclosing-block-a-previously-defined-range-variable-or-an-implicitly-declared-variable-in-a-query-expression"></a><span data-ttu-id="4b3ee-102">BC36633：范围变量 \<variable> 隐藏封闭块中的变量、以前定义的范围变量或者查询表达式中隐式声明的变量</span><span class="sxs-lookup"><span data-stu-id="4b3ee-102">BC36633: Range variable \<variable> hides a variable in an enclosing block, a previously defined range variable, or an implicitly declared variable in a query expression</span></span>

<span data-ttu-id="4b3ee-103">在、、或子句中指定的范围变量名称会 `Select` `From` `Aggregate` `Let` 复制以前在查询中指定的范围变量的名称，或查询隐式声明的变量的名称，例如字段名称或聚合函数的名称。</span><span class="sxs-lookup"><span data-stu-id="4b3ee-103">A range variable name specified in a `Select`, `From`, `Aggregate`, or `Let` clause duplicates the name of a range variable already specified previously in the query, or the name of a variable that is implicitly declared by the query, such as a field name or the name of an aggregate function.</span></span>

 <span data-ttu-id="4b3ee-104">**错误 ID：** BC36633</span><span class="sxs-lookup"><span data-stu-id="4b3ee-104">**Error ID:** BC36633</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="4b3ee-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="4b3ee-105">To correct this error</span></span>

- <span data-ttu-id="4b3ee-106">确保特定查询范围内的所有范围变量都具有唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="4b3ee-106">Ensure that all range variables in a particular query scope have unique names.</span></span> <span data-ttu-id="4b3ee-107">可以将查询括在括号中，以确保嵌套查询具有唯一的作用域。</span><span class="sxs-lookup"><span data-stu-id="4b3ee-107">You can enclose a query in parentheses to ensure that nested queries have a unique scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="4b3ee-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4b3ee-108">See also</span></span>

- [<span data-ttu-id="4b3ee-109">Visual Basic 中的 LINQ 简介</span><span class="sxs-lookup"><span data-stu-id="4b3ee-109">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="4b3ee-110">From 子句</span><span class="sxs-lookup"><span data-stu-id="4b3ee-110">From Clause</span></span>](../queries/from-clause.md)
- [<span data-ttu-id="4b3ee-111">Let 子句</span><span class="sxs-lookup"><span data-stu-id="4b3ee-111">Let Clause</span></span>](../queries/let-clause.md)
- [<span data-ttu-id="4b3ee-112">Aggregate Clause</span><span class="sxs-lookup"><span data-stu-id="4b3ee-112">Aggregate Clause</span></span>](../queries/aggregate-clause.md)
- [<span data-ttu-id="4b3ee-113">Select 子句</span><span class="sxs-lookup"><span data-stu-id="4b3ee-113">Select Clause</span></span>](../queries/select-clause.md)
