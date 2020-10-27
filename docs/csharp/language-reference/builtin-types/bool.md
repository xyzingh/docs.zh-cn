---
description: 了解 C# 中的内置布尔类型
title: bool 类型 - C# 参考
ms.date: 11/26/2019
f1_keywords:
- bool
- bool_CSharpKeyword
- "true"
- "false"
- true_CSharpKeyword
- false_CSharpKeyword
helpviewer_keywords:
- bool data type [C#]
- Boolean [C#]
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
ms.openlocfilehash: e74fd76fcb19faa5860e48140da0fbd3db4afa47
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471884"
---
# <a name="bool-c-reference"></a><span data-ttu-id="e27d2-103">bool（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="e27d2-103">bool (C# reference)</span></span>

<span data-ttu-id="e27d2-104">`bool` 类型关键字是 .NET <xref:System.Boolean?displayProperty=nameWithType> 结构类型的别名，它表示一个布尔值，可为 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="e27d2-104">The `bool` type keyword is an alias for the .NET <xref:System.Boolean?displayProperty=nameWithType> structure type that represents a Boolean value, which can be either `true` or `false`.</span></span>

<span data-ttu-id="e27d2-105">若要使用 `bool` 类型的值执行逻辑运算，请使用[布尔逻辑](../operators/boolean-logical-operators.md)运算符。</span><span class="sxs-lookup"><span data-stu-id="e27d2-105">To perform logical operations with values of the `bool` type, use [Boolean logical](../operators/boolean-logical-operators.md) operators.</span></span> <span data-ttu-id="e27d2-106">`bool` 类型是 [比较](../operators/comparison-operators.md)和[相等](../operators/equality-operators.md)运算符的结果类型。</span><span class="sxs-lookup"><span data-stu-id="e27d2-106">The `bool` type is the result type of [comparison](../operators/comparison-operators.md) and [equality](../operators/equality-operators.md) operators.</span></span> <span data-ttu-id="e27d2-107">`bool` 表达式可以是 [if](../keywords/if-else.md)、[do](../keywords/do.md)、[while](../keywords/while.md) 和 [for](../keywords/for.md) 语句中以及[条件运算符 `?:`](../operators/conditional-operator.md) 中的控制条件表达式。</span><span class="sxs-lookup"><span data-stu-id="e27d2-107">A `bool` expression can be a controlling conditional expression in the [if](../keywords/if-else.md), [do](../keywords/do.md), [while](../keywords/while.md), and [for](../keywords/for.md) statements and in the [conditional operator `?:`](../operators/conditional-operator.md).</span></span>

<span data-ttu-id="e27d2-108">`bool` 类型的默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="e27d2-108">The default value of the `bool` type is `false`.</span></span>

## <a name="literals"></a><span data-ttu-id="e27d2-109">文本</span><span class="sxs-lookup"><span data-stu-id="e27d2-109">Literals</span></span>

<span data-ttu-id="e27d2-110">可使用 `true` 和 `false` 文本来初始化 `bool` 变量或传递 `bool` 值：</span><span class="sxs-lookup"><span data-stu-id="e27d2-110">You can use the `true` and `false` literals to initialize a `bool` variable or to pass a `bool` value:</span></span>

[!code-csharp-interactive[bool literals](snippets/shared/BoolType.cs#Literals)]

## <a name="three-valued-boolean-logic"></a><span data-ttu-id="e27d2-111">三值布尔逻辑</span><span class="sxs-lookup"><span data-stu-id="e27d2-111">Three-valued Boolean logic</span></span>

<span data-ttu-id="e27d2-112">如需支持三值逻辑（例如，在使用支持三值布尔类型的数据库时），请使用可为空 `bool?` 类型。</span><span class="sxs-lookup"><span data-stu-id="e27d2-112">Use the nullable `bool?` type, if you need to support the three-valued logic, for example, when you work with databases that support a three-valued Boolean type.</span></span> <span data-ttu-id="e27d2-113">对于 `bool?` 操作数，预定义的 `&` 和 `|` 运算符支持三值逻辑。</span><span class="sxs-lookup"><span data-stu-id="e27d2-113">For the `bool?` operands, the predefined `&` and `|` operators support the three-valued logic.</span></span> <span data-ttu-id="e27d2-114">有关详细信息，请参阅[布尔逻辑运算符](../operators/boolean-logical-operators.md)一文的[可以为 null 的布尔逻辑运算符](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators)部分。</span><span class="sxs-lookup"><span data-stu-id="e27d2-114">For more information, see the [Nullable Boolean logical operators](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) section of the [Boolean logical operators](../operators/boolean-logical-operators.md) article.</span></span>

<span data-ttu-id="e27d2-115">有关可为空的值类型的详细信息，请参阅[可为空的值类型](nullable-value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="e27d2-115">For more information about nullable value types, see [Nullable value types](nullable-value-types.md).</span></span>

## <a name="conversions"></a><span data-ttu-id="e27d2-116">转换</span><span class="sxs-lookup"><span data-stu-id="e27d2-116">Conversions</span></span>

<span data-ttu-id="e27d2-117">C# 仅提供了两个涉及 `bool` 类型的转换。</span><span class="sxs-lookup"><span data-stu-id="e27d2-117">C# provides only two conversions that involve the `bool` type.</span></span> <span data-ttu-id="e27d2-118">它们是对相应的可以为空的 `bool?` 类型的隐式转换以及对 `bool?` 类型的显式转换。</span><span class="sxs-lookup"><span data-stu-id="e27d2-118">Those are an implicit conversion to the corresponding nullable `bool?` type and an explicit conversion from the `bool?` type.</span></span> <span data-ttu-id="e27d2-119">但是，.NET 提供了其他方法可用来转换到 `bool` 类型从或此类型进行转换。</span><span class="sxs-lookup"><span data-stu-id="e27d2-119">However, .NET provides additional methods that you can use to convert to or from the `bool` type.</span></span> <span data-ttu-id="e27d2-120">有关详细信息，请参阅 <xref:System.Boolean?displayProperty=nameWithType> API 参考页的[转换为布尔值和从布尔值转换](/dotnet/api/system.boolean#converting-to-and-from-boolean-values)部分。</span><span class="sxs-lookup"><span data-stu-id="e27d2-120">For more information, see the [Converting to and from Boolean values](/dotnet/api/system.boolean#converting-to-and-from-boolean-values) section of the <xref:System.Boolean?displayProperty=nameWithType> API reference page.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="e27d2-121">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="e27d2-121">C# language specification</span></span>

<span data-ttu-id="e27d2-122">有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)中的 [bool 类型](~/_csharplang/spec/types.md#the-bool-type)部分。</span><span class="sxs-lookup"><span data-stu-id="e27d2-122">For more information, see [The bool type](~/_csharplang/spec/types.md#the-bool-type) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e27d2-123">请参阅</span><span class="sxs-lookup"><span data-stu-id="e27d2-123">See also</span></span>

- [<span data-ttu-id="e27d2-124">C# 参考</span><span class="sxs-lookup"><span data-stu-id="e27d2-124">C# reference</span></span>](../index.md)
- [<span data-ttu-id="e27d2-125">值类型</span><span class="sxs-lookup"><span data-stu-id="e27d2-125">Value types</span></span>](value-types.md)
- [<span data-ttu-id="e27d2-126">true 和 false 运算符</span><span class="sxs-lookup"><span data-stu-id="e27d2-126">true and false operators</span></span>](../operators/true-false-operators.md)
