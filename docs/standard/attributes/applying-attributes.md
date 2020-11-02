---
title: 应用特性
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- assemblies [.NET], attributes
- attributes [.NET], applying
ms.assetid: dd7604eb-9fa3-4b60-b2dd-b47739fa3148
ms.openlocfilehash: 24fe58ddf48e40b422652baa4c5bba86eea6b84f
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889226"
---
# <a name="apply-attributes"></a><span data-ttu-id="c4781-102">应用属性</span><span class="sxs-lookup"><span data-stu-id="c4781-102">Apply attributes</span></span>

<span data-ttu-id="c4781-103">使用以下过程将特性应用于代码的元素。</span><span class="sxs-lookup"><span data-stu-id="c4781-103">Use the following process to apply an attribute to an element of your code.</span></span>

1. <span data-ttu-id="c4781-104">定义新特性或使用现有的 .NET 特性。</span><span class="sxs-lookup"><span data-stu-id="c4781-104">Define a new attribute or use an existing .NET attribute.</span></span>

2. <span data-ttu-id="c4781-105">通过将特性置于紧邻元素之前，将该特性应用于代码元素。</span><span class="sxs-lookup"><span data-stu-id="c4781-105">Apply the attribute to the code element by placing it immediately before the element.</span></span>

     <span data-ttu-id="c4781-106">每种语言都有其自己的特性语法。</span><span class="sxs-lookup"><span data-stu-id="c4781-106">Each language has its own attribute syntax.</span></span> <span data-ttu-id="c4781-107">在 C++ 和 C# 中，特性是用方括号括起来的，并通过空格与元素分开（可能包括换行符）。</span><span class="sxs-lookup"><span data-stu-id="c4781-107">In C++ and C#, the attribute is surrounded by square brackets and separated from the element by white space, which can include a line break.</span></span> <span data-ttu-id="c4781-108">在 Visual Basic 中，特性是用尖括号括起来的，且必须位于同一逻辑线上；如果需要换行符，可使用行继续字符。</span><span class="sxs-lookup"><span data-stu-id="c4781-108">In Visual Basic, the attribute is surrounded by angle brackets and must be on the same logical line; the line continuation character can be used if a line break is desired.</span></span>

3. <span data-ttu-id="c4781-109">指定特性的位置参数和命名参数。</span><span class="sxs-lookup"><span data-stu-id="c4781-109">Specify positional parameters and named parameters for the attribute.</span></span>

     <span data-ttu-id="c4781-110">位置参数是必需的，且必须位于所有命名参数之前；它们对应于特性的其中一个构造函数的参数。</span><span class="sxs-lookup"><span data-stu-id="c4781-110">*Positional* parameters are required and must come before any named parameters; they correspond to the parameters of one of the attribute's constructors.</span></span> <span data-ttu-id="c4781-111">命名参数是可选的且对应于特性的读/写属性。</span><span class="sxs-lookup"><span data-stu-id="c4781-111">*Named* parameters are optional and correspond to read/write properties of the attribute.</span></span> <span data-ttu-id="c4781-112">在 C++ 和 C# 中，为每个可选参数指定 `name=value`，其中 `name` 是属性名。</span><span class="sxs-lookup"><span data-stu-id="c4781-112">In C++, and C#, specify `name=value` for each optional parameter, where `name` is the name of the property.</span></span> <span data-ttu-id="c4781-113">在 Visual Basic 中，指定 `name:=value`。</span><span class="sxs-lookup"><span data-stu-id="c4781-113">In Visual Basic, specify `name:=value`.</span></span>

 <span data-ttu-id="c4781-114">编译代码时，特性将被发到元数据中，并且通过运行时反射服务可用于公共语言运行时和任何自定义工具或应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4781-114">The attribute is emitted into metadata when you compile your code and is available to the common language runtime and any custom tool or application through the runtime reflection services.</span></span>

 <span data-ttu-id="c4781-115">按照惯例，所有特性名称都以“Attribute”结尾。</span><span class="sxs-lookup"><span data-stu-id="c4781-115">By convention, all attribute names end with "Attribute".</span></span> <span data-ttu-id="c4781-116">但是，面向运行时的几种语言（如 Visual Basic 和 C#）无需指定特性的全名。</span><span class="sxs-lookup"><span data-stu-id="c4781-116">However, several languages that target the runtime, such as Visual Basic and C#, do not require you to specify the full name of an attribute.</span></span> <span data-ttu-id="c4781-117">例如，若要初始化 <xref:System.ObsoleteAttribute?displayProperty=nameWithType>，只需将它引用为 Obsolete 即可。</span><span class="sxs-lookup"><span data-stu-id="c4781-117">For example, if you want to initialize <xref:System.ObsoleteAttribute?displayProperty=nameWithType>, you only need to reference it as **Obsolete** .</span></span>

## <a name="apply-an-attribute-to-a-method"></a><span data-ttu-id="c4781-118">将特性应用于方法</span><span class="sxs-lookup"><span data-stu-id="c4781-118">Apply an attribute to a method</span></span>

 <span data-ttu-id="c4781-119">以下代码示例显示如何使用 System.ObsoleteAttribute（其将代码标记为已过时）。</span><span class="sxs-lookup"><span data-stu-id="c4781-119">The following code example shows how to use **System.ObsoleteAttribute** , which marks code as obsolete.</span></span> <span data-ttu-id="c4781-120">将字符串 `"Will be removed in next version"` 传递给特性。</span><span class="sxs-lookup"><span data-stu-id="c4781-120">The string `"Will be removed in next version"` is passed to the attribute.</span></span> <span data-ttu-id="c4781-121">当特性描述的代码被调用时，此特性会导致产生编译器警告，显示传递的字符串。</span><span class="sxs-lookup"><span data-stu-id="c4781-121">This attribute causes a compiler warning that displays the passed string when code that the attribute describes is called.</span></span>

 [!code-cpp[Conceptual.Attributes.Usage#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source1.cpp#3)]
 [!code-csharp[Conceptual.Attributes.Usage#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source1.cs#3)]
 [!code-vb[Conceptual.Attributes.Usage#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source1.vb#3)]

## <a name="apply-attributes-at-the-assembly-level"></a><span data-ttu-id="c4781-122">在程序集级别应用特性</span><span class="sxs-lookup"><span data-stu-id="c4781-122">Apply attributes at the assembly level</span></span>

 <span data-ttu-id="c4781-123">如果要在程序集级别应用属性，请使用 assembly`Assembly`（Visual Basic 中用`assembly` ）关键字。</span><span class="sxs-lookup"><span data-stu-id="c4781-123">If you want to apply an attribute at the assembly level, use the `assembly` (`Assembly` in Visual Basic) keyword.</span></span> <span data-ttu-id="c4781-124">下列代码显示在程序集级别应用的 **AssemblyTitleAttribute** 。</span><span class="sxs-lookup"><span data-stu-id="c4781-124">The following code shows the **AssemblyTitleAttribute** applied at the assembly level.</span></span>

 [!code-cpp[Conceptual.Attributes.Usage#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source1.cpp#2)]
 [!code-csharp[Conceptual.Attributes.Usage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source1.cs#2)]
 [!code-vb[Conceptual.Attributes.Usage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source1.vb#2)]

 <span data-ttu-id="c4781-125">应用此特性时，字符串 `"My Assembly"` 将被放置在文件元数据部分的程序集清单中。</span><span class="sxs-lookup"><span data-stu-id="c4781-125">When this attribute is applied, the string `"My Assembly"` is placed in the assembly manifest in the metadata portion of the file.</span></span> <span data-ttu-id="c4781-126">可通过后列方法查看特性：使用 [MSIL 反汇编程序 (Ildasm.exe)](../../framework/tools/ildasm-exe-il-disassembler.md)，或创建一个自定义程序来检索特性。</span><span class="sxs-lookup"><span data-stu-id="c4781-126">You can view the attribute either by using the [MSIL Disassembler (Ildasm.exe)](../../framework/tools/ildasm-exe-il-disassembler.md) or by creating a custom program to retrieve the attribute.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4781-127">请参阅</span><span class="sxs-lookup"><span data-stu-id="c4781-127">See also</span></span>

- [<span data-ttu-id="c4781-128">特性</span><span class="sxs-lookup"><span data-stu-id="c4781-128">Attributes</span></span>](index.md)
- [<span data-ttu-id="c4781-129">检索存储在特性中的信息</span><span class="sxs-lookup"><span data-stu-id="c4781-129">Retrieving Information Stored in Attributes</span></span>](retrieving-information-stored-in-attributes.md)
- [<span data-ttu-id="c4781-130">概念</span><span class="sxs-lookup"><span data-stu-id="c4781-130">Concepts</span></span>](/cpp/windows/attributed-programming-concepts)
- [<span data-ttu-id="c4781-131">特性 (C#)</span><span class="sxs-lookup"><span data-stu-id="c4781-131">Attributes (C#)</span></span>](../../csharp/programming-guide/concepts/attributes/index.md)
- [<span data-ttu-id="c4781-132">特性概述 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c4781-132">Attributes overview (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/attributes/index.md)
