---
title: 命名空间 - C# 编程指南
description: 了解 C# 编程中的命名空间。 请参阅命名空间属性概述，并查看其他资源。
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, namespaces
- namespaces [C#]
ms.assetid: b1c4ab46-3fad-4ffa-9deb-dd50a2d8c65a
ms.openlocfilehash: 41a666fd5f368e6990e08a36700e18f648939213
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440336"
---
# <a name="namespaces-c-programming-guide"></a><span data-ttu-id="6f38f-104">命名空间（C# 编程指南）</span><span class="sxs-lookup"><span data-stu-id="6f38f-104">Namespaces (C# Programming Guide)</span></span>

<span data-ttu-id="6f38f-105">在 C# 编程中，命名空间在两个方面被大量使用。</span><span class="sxs-lookup"><span data-stu-id="6f38f-105">Namespaces are heavily used in C# programming in two ways.</span></span> <span data-ttu-id="6f38f-106">首先，.NET 使用命名空间来组织它的许多类，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f38f-106">First, .NET uses namespaces to organize its many classes, as follows:</span></span>  

[!code-csharp[csProgGuide#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#22)]

<span data-ttu-id="6f38f-107"><xref:System> 是一个命名空间，<xref:System.Console> 是该命名空间中的一个类。</span><span class="sxs-lookup"><span data-stu-id="6f38f-107"><xref:System> is a namespace and <xref:System.Console> is a class in that namespace.</span></span> <span data-ttu-id="6f38f-108">可以使用 `using` 关键字，如此则不必使用完整的名称，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="6f38f-108">The `using` keyword can be used so that the complete name is not required, as in the following example:</span></span>

[!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]

[!code-csharp[csProgGuide#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#23)]

<span data-ttu-id="6f38f-109">有关详细信息，请参阅 [using 指令](../../language-reference/keywords/using-directive.md)。</span><span class="sxs-lookup"><span data-stu-id="6f38f-109">For more information, see the [using Directive](../../language-reference/keywords/using-directive.md).</span></span>

<span data-ttu-id="6f38f-110">其次，在较大的编程项目中，声明自己的命名空间可以帮助控制类和方法名称的范围。</span><span class="sxs-lookup"><span data-stu-id="6f38f-110">Second, declaring your own namespaces can help you control the scope of class and method names in larger programming projects.</span></span> <span data-ttu-id="6f38f-111">使用 [namespace](../../language-reference/keywords/namespace.md) 关键字可声明命名空间，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="6f38f-111">Use the [namespace](../../language-reference/keywords/namespace.md) keyword to declare a namespace, as in the following example:</span></span>

[!code-csharp[csProgGuideNamespaces#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#6)]

<span data-ttu-id="6f38f-112">命名空间的名称必须是有效的 C# [标识符名称](../inside-a-program/identifier-names.md)。</span><span class="sxs-lookup"><span data-stu-id="6f38f-112">The name of the namespace must be a valid C# [identifier name](../inside-a-program/identifier-names.md).</span></span>

## <a name="namespaces-overview"></a><span data-ttu-id="6f38f-113">命名空间概述</span><span class="sxs-lookup"><span data-stu-id="6f38f-113">Namespaces overview</span></span>

<span data-ttu-id="6f38f-114">命名空间具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="6f38f-114">Namespaces have the following properties:</span></span>

- <span data-ttu-id="6f38f-115">它们组织大型代码项目。</span><span class="sxs-lookup"><span data-stu-id="6f38f-115">They organize large code projects.</span></span>
- <span data-ttu-id="6f38f-116">通过使用 `.` 运算符分隔它们。</span><span class="sxs-lookup"><span data-stu-id="6f38f-116">They are delimited by using the `.` operator.</span></span>
- <span data-ttu-id="6f38f-117">`using` 指令可免去为每个类指定命名空间的名称。</span><span class="sxs-lookup"><span data-stu-id="6f38f-117">The `using` directive obviates the requirement to specify the name of the namespace for every class.</span></span>
- <span data-ttu-id="6f38f-118">`global` 命名空间是“根”命名空间：`global::System` 始终引用 .NET <xref:System> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="6f38f-118">The `global` namespace is the "root" namespace: `global::System` will always refer to the .NET <xref:System> namespace.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="6f38f-119">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="6f38f-119">C# language specification</span></span>

<span data-ttu-id="6f38f-120">有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)中的[命名空间](~/_csharplang/spec/namespaces.md)部分。</span><span class="sxs-lookup"><span data-stu-id="6f38f-120">For more information, see the [Namespaces](~/_csharplang/spec/namespaces.md) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6f38f-121">请参阅</span><span class="sxs-lookup"><span data-stu-id="6f38f-121">See also</span></span>

- [<span data-ttu-id="6f38f-122">C# 编程指南</span><span class="sxs-lookup"><span data-stu-id="6f38f-122">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="6f38f-123">使用命名空间</span><span class="sxs-lookup"><span data-stu-id="6f38f-123">Using Namespaces</span></span>](using-namespaces.md)
- [<span data-ttu-id="6f38f-124">如何使用 My 命名空间</span><span class="sxs-lookup"><span data-stu-id="6f38f-124">How to use the My namespace</span></span>](how-to-use-the-my-namespace.md)
- [<span data-ttu-id="6f38f-125">标识符名称</span><span class="sxs-lookup"><span data-stu-id="6f38f-125">Identifier names</span></span>](../inside-a-program/identifier-names.md)
- [<span data-ttu-id="6f38f-126">using 指令</span><span class="sxs-lookup"><span data-stu-id="6f38f-126">using Directive</span></span>](../../language-reference/keywords/using-directive.md)
- [<span data-ttu-id="6f38f-127">::运算符</span><span class="sxs-lookup"><span data-stu-id="6f38f-127">:: Operator</span></span>](../../language-reference/operators/namespace-alias-qualifier.md)
