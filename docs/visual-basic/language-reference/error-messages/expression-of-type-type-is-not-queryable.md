---
title: 类型 <type> 的表达式不可查询
ms.date: 07/20/2015
f1_keywords:
- bc36593
- vbc36593
helpviewer_keywords:
- BC36593
ms.assetid: 6f1f5860-bf97-4885-9ebb-bc87d028095c
ms.openlocfilehash: d605243c213166f20592fdc440a3362f957ebbf2
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163059"
---
# <a name="bc36593-expression-of-type-type-is-not-queryable"></a><span data-ttu-id="87b7b-102">BC36593：类型的表达式 \<type> 不可查询</span><span class="sxs-lookup"><span data-stu-id="87b7b-102">BC36593: Expression of type \<type> is not queryable</span></span>

<span data-ttu-id="87b7b-103">类型的表达式 \<type> 不可查询。</span><span class="sxs-lookup"><span data-stu-id="87b7b-103">Expression of type \<type> is not queryable.</span></span> <span data-ttu-id="87b7b-104">请确保不缺少 LINQ 提供程序的程序集引用和/或命名空间导入。</span><span class="sxs-lookup"><span data-stu-id="87b7b-104">Make sure you are not missing an assembly reference and/or namespace import for the LINQ provider.</span></span>

 <span data-ttu-id="87b7b-105">可查询类型在 <xref:System.Linq> 、 <xref:System.Data.Linq> 和 <xref:System.Xml.Linq> 命名空间中定义。</span><span class="sxs-lookup"><span data-stu-id="87b7b-105">Queryable types are defined in the <xref:System.Linq>, <xref:System.Data.Linq>, and <xref:System.Xml.Linq> namespaces.</span></span> <span data-ttu-id="87b7b-106">必须导入一个或多个此类命名空间才能执行 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="87b7b-106">You must import one or more of these namespaces to perform LINQ queries.</span></span>

 <span data-ttu-id="87b7b-107"><xref:System.Linq>命名空间使你能够通过使用 LINQ 查询对象（如集合和数组）。</span><span class="sxs-lookup"><span data-stu-id="87b7b-107">The <xref:System.Linq> namespace enables you to query objects such as collections and arrays by using LINQ.</span></span>

 <span data-ttu-id="87b7b-108"><xref:System.Data.Linq>命名空间使你能够通过使用 LINQ 查询 ADO.NET 数据集和 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="87b7b-108">The <xref:System.Data.Linq> namespace enables you to query ADO.NET Datasets and SQL Server databases by using LINQ.</span></span>

 <span data-ttu-id="87b7b-109"><xref:System.Xml.Linq>命名空间使你能够使用 LINQ 查询 xml，并使用 Visual Basic 中的 xml 功能。</span><span class="sxs-lookup"><span data-stu-id="87b7b-109">The <xref:System.Xml.Linq> namespace enables you to query XML by using LINQ and to use XML features in Visual Basic.</span></span>

 <span data-ttu-id="87b7b-110">**错误 ID：** BC36593</span><span class="sxs-lookup"><span data-stu-id="87b7b-110">**Error ID:** BC36593</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="87b7b-111">更正此错误</span><span class="sxs-lookup"><span data-stu-id="87b7b-111">To correct this error</span></span>

1. <span data-ttu-id="87b7b-112">将 `Import` <xref:System.Linq> 、 <xref:System.Data.Linq> 或命名空间的语句添加 <xref:System.Xml.Linq> 到代码文件中。</span><span class="sxs-lookup"><span data-stu-id="87b7b-112">Add an `Import` statement for the <xref:System.Linq>, <xref:System.Data.Linq>, or <xref:System.Xml.Linq> namespace to your code file.</span></span> <span data-ttu-id="87b7b-113">你还可以使用 "项目设计器 **" ("项目设计**器" 的 "**引用**" 页) 导入项目的命名空间。</span><span class="sxs-lookup"><span data-stu-id="87b7b-113">You can also import namespaces for your project by using the **References** page of the Project Designer (**My Project**).</span></span>

2. <span data-ttu-id="87b7b-114">确保已标识为查询源的类型是可查询类型。</span><span class="sxs-lookup"><span data-stu-id="87b7b-114">Ensure that the type that you have identified as the source of your query is a queryable type.</span></span> <span data-ttu-id="87b7b-115">即，实现或的类型 <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Linq.IQueryable%601> 。</span><span class="sxs-lookup"><span data-stu-id="87b7b-115">That is, a type that implements <xref:System.Collections.Generic.IEnumerable%601> or <xref:System.Linq.IQueryable%601>.</span></span>

## <a name="see-also"></a><span data-ttu-id="87b7b-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="87b7b-116">See also</span></span>

- <xref:System.Linq>
- <xref:System.Data.Linq>
- <xref:System.Xml.Linq>
- [<span data-ttu-id="87b7b-117">Visual Basic 中的 LINQ 简介</span><span class="sxs-lookup"><span data-stu-id="87b7b-117">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="87b7b-118">LINQ</span><span class="sxs-lookup"><span data-stu-id="87b7b-118">LINQ</span></span>](../../programming-guide/language-features/linq/index.md)
- [<span data-ttu-id="87b7b-119">XML</span><span class="sxs-lookup"><span data-stu-id="87b7b-119">XML</span></span>](../../programming-guide/language-features/xml/index.md)
- [<span data-ttu-id="87b7b-120">引用和 Imports 语句</span><span class="sxs-lookup"><span data-stu-id="87b7b-120">References and the Imports Statement</span></span>](../../programming-guide/program-structure/references-and-the-imports-statement.md)
- [<span data-ttu-id="87b7b-121">Imports 语句（.NET 命名空间和类型）</span><span class="sxs-lookup"><span data-stu-id="87b7b-121">Imports Statement (.NET Namespace and Type)</span></span>](../statements/imports-statement-net-namespace-and-type.md)
- [<span data-ttu-id="87b7b-122">项目设计器 -&gt;“引用”页 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="87b7b-122">References Page, Project Designer (Visual Basic)</span></span>](/visualstudio/ide/reference/references-page-project-designer-visual-basic)
