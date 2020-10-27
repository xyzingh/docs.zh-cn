---
title: 元组类型 - C# 参考
description: 了解 C# 元组：轻型数据结构，可用于对相关的数据元素进行松散分组
ms.date: 07/09/2020
helpviewer_keywords:
- value tuples [C#]
ms.openlocfilehash: d996c7afecba1b58bfd8337fa444fd71790dd482
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471767"
---
# <a name="tuple-types-c-reference"></a><span data-ttu-id="1eb11-103">元组类型（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="1eb11-103">Tuple types (C# reference)</span></span>

<span data-ttu-id="1eb11-104">元组功能在 C# 7.0 及更高版本中可用，它提供了简洁的语法，用于将多个数据元素分组成一个轻型数据结构。</span><span class="sxs-lookup"><span data-stu-id="1eb11-104">Available in C# 7.0 and later, the *tuples* feature provides concise syntax to group multiple data elements in a lightweight data structure.</span></span> <span data-ttu-id="1eb11-105">下面的示例演示了如何声明元组变量、对它进行初始化并访问其数据成员：</span><span class="sxs-lookup"><span data-stu-id="1eb11-105">The following example shows how you can declare a tuple variable, initialize it, and access its data members:</span></span>

[!code-csharp-interactive[tuple intro](snippets/shared/ValueTuples.cs#Introduction)]

<span data-ttu-id="1eb11-106">如前面的示例所示，若要定义元组类型，需要指定其所有数据成员的类型，或者，可以指定[字段名称](#tuple-field-names)。</span><span class="sxs-lookup"><span data-stu-id="1eb11-106">As the preceding example shows, to define a tuple type, you specify types of all its data members and, optionally, the [field names](#tuple-field-names).</span></span> <span data-ttu-id="1eb11-107">虽然不能在元组类型中定义方法，但可以使用 .NET 提供的方法，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-107">You cannot define methods in a tuple type, but you can use the methods provided by .NET, as the following example shows:</span></span>

[!code-csharp-interactive[tuple methods](snippets/shared/ValueTuples.cs#MethodOnTuples)]

<span data-ttu-id="1eb11-108">从 C# 7.3 开始，元组类型支持[相等运算符](../operators/equality-operators.md) `==` 和 `!=`。</span><span class="sxs-lookup"><span data-stu-id="1eb11-108">Beginning with C# 7.3, tuple types support [equality operators](../operators/equality-operators.md) `==` and `!=`.</span></span> <span data-ttu-id="1eb11-109">有关详细信息，请参阅[元组相等](#tuple-equality)部分。</span><span class="sxs-lookup"><span data-stu-id="1eb11-109">For more information, see the [Tuple equality](#tuple-equality) section.</span></span>

<span data-ttu-id="1eb11-110">元组类型是[值类型](value-types.md)；元组元素是公共字段。</span><span class="sxs-lookup"><span data-stu-id="1eb11-110">Tuple types are [value types](value-types.md); tuple elements are public fields.</span></span> <span data-ttu-id="1eb11-111">这使得元组为可变的值类型。</span><span class="sxs-lookup"><span data-stu-id="1eb11-111">That makes tuples *mutable* value types.</span></span>

> [!NOTE]
> <span data-ttu-id="1eb11-112">元组功能需要 <xref:System.ValueTuple?displayProperty=nameWithType> 类型和相关的泛型类型（例如 <xref:System.ValueTuple%602?displayProperty=nameWithType>），这些类型在 .NET Core 和 .NET Framework 4.7 及更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="1eb11-112">The tuples feature requires the <xref:System.ValueTuple?displayProperty=nameWithType> type and related generic types (for example, <xref:System.ValueTuple%602?displayProperty=nameWithType>), which are available in .NET Core and .NET Framework 4.7 and later.</span></span> <span data-ttu-id="1eb11-113">若要在面向 .NET Framework 4.6.2 或更早版本的项目中使用元组，请将 NuGet 包 [`System.ValueTuple`](https://www.nuget.org/packages/System.ValueTuple/) 添加到项目。</span><span class="sxs-lookup"><span data-stu-id="1eb11-113">To use tuples in a project that targets .NET Framework 4.6.2 or earlier, add the NuGet package [`System.ValueTuple`](https://www.nuget.org/packages/System.ValueTuple/) to the project.</span></span>

<span data-ttu-id="1eb11-114">可以使用任意数量的元素定义元组：</span><span class="sxs-lookup"><span data-stu-id="1eb11-114">You can define tuples with an arbitrary large number of elements:</span></span>

[!code-csharp-interactive[large tuple](snippets/shared/ValueTuples.cs#LargeTuple)]

## <a name="use-cases-of-tuples"></a><span data-ttu-id="1eb11-115">元组的用例</span><span class="sxs-lookup"><span data-stu-id="1eb11-115">Use cases of tuples</span></span>

<span data-ttu-id="1eb11-116">元组最常见的用例之一是作为方法返回类型。</span><span class="sxs-lookup"><span data-stu-id="1eb11-116">One of the most common use cases of tuples is as a method return type.</span></span> <span data-ttu-id="1eb11-117">也就是说，你可以将方法结果分组为元组返回类型，而不是定义 [`out` 方法参数](../keywords/out-parameter-modifier.md)，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-117">That is, instead of defining [`out` method parameters](../keywords/out-parameter-modifier.md), you can group method results in a tuple return type, as the following example shows:</span></span>

[!code-csharp-interactive[multiple method outputs](snippets/shared/ValueTuples.cs#MultipleReturns)]

<span data-ttu-id="1eb11-118">如前面的示例所示，可以直接使用返回的元组实例，或者可以在单独的变量中[析构](#tuple-assignment-and-deconstruction)它。</span><span class="sxs-lookup"><span data-stu-id="1eb11-118">As the preceding example shows, you can work with the returned tuple instance directly or [deconstruct](#tuple-assignment-and-deconstruction) it in separate variables.</span></span>

<span data-ttu-id="1eb11-119">还可以使用元组类型，而不是[匿名类型](../../programming-guide/classes-and-structs/anonymous-types.md)；例如，在 LINQ 查询中。</span><span class="sxs-lookup"><span data-stu-id="1eb11-119">You can also use tuple types instead of [anonymous types](../../programming-guide/classes-and-structs/anonymous-types.md); for example, in LINQ queries.</span></span> <span data-ttu-id="1eb11-120">有关详细信息，请参阅[在匿名类型和元组类型之间选择](../../../standard/base-types/choosing-between-anonymous-and-tuple.md)。</span><span class="sxs-lookup"><span data-stu-id="1eb11-120">For more information, see [Choosing between anonymous and tuple types](../../../standard/base-types/choosing-between-anonymous-and-tuple.md).</span></span>

<span data-ttu-id="1eb11-121">通常，你会使用元组对相关的数据元素进行松散分组。</span><span class="sxs-lookup"><span data-stu-id="1eb11-121">Typically, you use tuples to group loosely related data elements.</span></span> <span data-ttu-id="1eb11-122">这通常在专用和内部实用工具方法中有用。</span><span class="sxs-lookup"><span data-stu-id="1eb11-122">That is usually useful within private and internal utility methods.</span></span> <span data-ttu-id="1eb11-123">对于公共 API 用例，请考虑定义[类](../keywords/class.md)或[结构](struct.md)类型。</span><span class="sxs-lookup"><span data-stu-id="1eb11-123">In the case of public API, consider defining a [class](../keywords/class.md) or a [structure](struct.md) type.</span></span>

## <a name="tuple-field-names"></a><span data-ttu-id="1eb11-124">元组字段名称</span><span class="sxs-lookup"><span data-stu-id="1eb11-124">Tuple field names</span></span>

<span data-ttu-id="1eb11-125">可以在元组初始化表达式中或元组类型的定义中显式指定元组字段的名称，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-125">You can explicitly specify the names of tuple fields either in a tuple initialization expression or in the definition of a tuple type, as the following example shows:</span></span>

[!code-csharp-interactive[explicit field names](snippets/shared/ValueTuples.cs#ExplicitFieldNames)]

<span data-ttu-id="1eb11-126">从 C# 7.1 开始，如果未指定字段名称，则可以根据元组初始化表达式中相应变量的名称推断出此名称，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-126">Beginning with C# 7.1, if you don't specify a field name, it may be inferred from the name of the corresponding variable in a tuple initialization expression, as the following example shows:</span></span>

[!code-csharp-interactive[inferred field names](snippets/shared/ValueTuples.cs#InferFieldNames)]

<span data-ttu-id="1eb11-127">这称为元组投影初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="1eb11-127">That's known as tuple projection initializers.</span></span> <span data-ttu-id="1eb11-128">在以下情况下，变量名称不会被投影到元组字段名称中：</span><span class="sxs-lookup"><span data-stu-id="1eb11-128">The name of a variable isn't projected onto a tuple field name in the following cases:</span></span>

- <span data-ttu-id="1eb11-129">候选名称是元组类型的成员名称，例如 `Item3`、`ToString` 或 `Rest`。</span><span class="sxs-lookup"><span data-stu-id="1eb11-129">The candidate name is a member name of a tuple type, for example, `Item3`, `ToString`, or `Rest`.</span></span>
- <span data-ttu-id="1eb11-130">候选名称是另一元组的显式或隐式字段名称的重复项。</span><span class="sxs-lookup"><span data-stu-id="1eb11-130">The candidate name is a duplicate of another tuple field name, either explicit or implicit.</span></span>

<span data-ttu-id="1eb11-131">在这些情况下，你可以显式指定字段的名称，或按字段的默认名称访问字段。</span><span class="sxs-lookup"><span data-stu-id="1eb11-131">In those cases you either explicitly specify the name of a field or access a field by its default name.</span></span>

<span data-ttu-id="1eb11-132">元组字段的默认名称为 `Item1`、`Item2`、`Item3` 等。</span><span class="sxs-lookup"><span data-stu-id="1eb11-132">The default names of tuple fields are `Item1`, `Item2`, `Item3` and so on.</span></span> <span data-ttu-id="1eb11-133">始终可以使用字段的默认名称，即使字段名称是显式指定的或推断出的，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-133">You can always use the default name of a field, even when a field name is specified explicitly or inferred, as the following example shows:</span></span>

[!code-csharp-interactive[default field names](snippets/shared/ValueTuples.cs#DefaultFieldNames)]

<span data-ttu-id="1eb11-134">[元组赋值](#tuple-assignment-and-deconstruction)和[元组相等比较](#tuple-equality)不会考虑字段名称。</span><span class="sxs-lookup"><span data-stu-id="1eb11-134">[Tuple assignment](#tuple-assignment-and-deconstruction) and [tuple equality comparisons](#tuple-equality) don't take field names into account.</span></span>

<span data-ttu-id="1eb11-135">在编译时，编译器会将非默认字段名称替换为相应的默认名称。</span><span class="sxs-lookup"><span data-stu-id="1eb11-135">At compile time, the compiler replaces non-default field names with the corresponding default names.</span></span> <span data-ttu-id="1eb11-136">因此，显式指定或推断的字段名称在运行时不可用。</span><span class="sxs-lookup"><span data-stu-id="1eb11-136">As a result, explicitly specified or inferred field names aren't available at run time.</span></span>

## <a name="tuple-assignment-and-deconstruction"></a><span data-ttu-id="1eb11-137">元组赋值和析构</span><span class="sxs-lookup"><span data-stu-id="1eb11-137">Tuple assignment and deconstruction</span></span>

<span data-ttu-id="1eb11-138">C# 支持满足以下两个条件的元组类型之间的赋值：</span><span class="sxs-lookup"><span data-stu-id="1eb11-138">C# supports assignment between tuple types that satisfy both of the following conditions:</span></span>

- <span data-ttu-id="1eb11-139">两个元组类型有相同数量的元素</span><span class="sxs-lookup"><span data-stu-id="1eb11-139">both tuple types have the same number of elements</span></span>
- <span data-ttu-id="1eb11-140">对于每个元组位置，右侧元组元素的类型与左侧相应的元组元素的类型相同或可以隐式转换为左侧相应的元组元素的类型</span><span class="sxs-lookup"><span data-stu-id="1eb11-140">for each tuple position, the type of the right-hand tuple element is the same as or implicitly convertible to the type of the corresponding left-hand tuple element</span></span>

<span data-ttu-id="1eb11-141">元组元素是按照元组元素的顺序赋值的。</span><span class="sxs-lookup"><span data-stu-id="1eb11-141">Tuple element values are assigned following the order of tuple elements.</span></span> <span data-ttu-id="1eb11-142">元组字段的名称会被忽略且不会被赋值，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-142">The names of tuple fields are ignored and not assigned, as the following example shows:</span></span>

[!code-csharp-interactive[tuple assignment](snippets/shared/ValueTuples.cs#Assignment)]

<span data-ttu-id="1eb11-143">还可以使用赋值运算符 `=` 在单独的变量中析构元组实例。</span><span class="sxs-lookup"><span data-stu-id="1eb11-143">You can also use the assignment operator `=` to *deconstruct* a tuple instance in separate variables.</span></span> <span data-ttu-id="1eb11-144">为此，可以使用以下方式之一进行操作：</span><span class="sxs-lookup"><span data-stu-id="1eb11-144">You can do that in one of the following ways:</span></span>

- <span data-ttu-id="1eb11-145">在括号内显式声明每个变量的类型：</span><span class="sxs-lookup"><span data-stu-id="1eb11-145">Explicitly declare the type of each variable inside parentheses:</span></span>

  [!code-csharp-interactive[specify types of variables](snippets/shared/ValueTuples.cs#DeconstructExplicit)]

- <span data-ttu-id="1eb11-146">在括号外使用 `var` 关键字来声明隐式类型化变量，并让编译器推断其类型：</span><span class="sxs-lookup"><span data-stu-id="1eb11-146">Use the `var` keyword outside the parentheses to declare implicitly typed variables and let the compiler infer their types:</span></span>

  [!code-csharp-interactive[implicitly typed variables](snippets/shared/ValueTuples.cs#DeconstructVar)]

- <span data-ttu-id="1eb11-147">使用现有变量：</span><span class="sxs-lookup"><span data-stu-id="1eb11-147">Use existing variables:</span></span>

  [!code-csharp-interactive[existing variables](snippets/shared/ValueTuples.cs#DeconstructExisting)]

<span data-ttu-id="1eb11-148">有关析构元组和其他类型的详细信息，请参阅[析构元组和其他类型](../../deconstruct.md)。</span><span class="sxs-lookup"><span data-stu-id="1eb11-148">For more information about deconstruction of tuples and other types, see [Deconstructing tuples and other types](../../deconstruct.md).</span></span>

## <a name="tuple-equality"></a><span data-ttu-id="1eb11-149">元组相等</span><span class="sxs-lookup"><span data-stu-id="1eb11-149">Tuple equality</span></span>

<span data-ttu-id="1eb11-150">从 C# 7.3 开始，元组类型支持 `==` 和 `!=` 运算符。</span><span class="sxs-lookup"><span data-stu-id="1eb11-150">Beginning with C# 7.3, tuple types support the `==` and `!=` operators.</span></span> <span data-ttu-id="1eb11-151">这些运算符按照元组元素的顺序将左侧操作数的成员与相应的右侧操作数的成员进行比较。</span><span class="sxs-lookup"><span data-stu-id="1eb11-151">These operators compare members of the left-hand operand with the corresponding members of the right-hand operand following the order of tuple elements.</span></span>

[!code-csharp-interactive[tuple equality](snippets/shared/ValueTuples.cs#TupleEquality)]

<span data-ttu-id="1eb11-152">如前面的示例所示，`==` 和 `!=` 操作不会考虑元组字段名称。</span><span class="sxs-lookup"><span data-stu-id="1eb11-152">As the preceding example shows, the `==` and `!=` operations don't take into account tuple field names.</span></span>

<span data-ttu-id="1eb11-153">同时满足以下两个条件时，两个元组可比较：</span><span class="sxs-lookup"><span data-stu-id="1eb11-153">Two tuples are comparable when both of the following conditions are satisfied:</span></span>

- <span data-ttu-id="1eb11-154">两个元组具有相同数量的元素。</span><span class="sxs-lookup"><span data-stu-id="1eb11-154">Both tuples have the same number of elements.</span></span> <span data-ttu-id="1eb11-155">例如，如果 `t1` 和 `t2` 具有不同数目的元素，`t1 != t2` 则不会进行编译。</span><span class="sxs-lookup"><span data-stu-id="1eb11-155">For example, `t1 != t2` doesn't compile if `t1` and `t2` have different numbers of elements.</span></span>
- <span data-ttu-id="1eb11-156">对于每个元组位置，可以使用 `==` 和 `!=` 运算符对左右侧元组操作数中的相应元素进行比较。</span><span class="sxs-lookup"><span data-stu-id="1eb11-156">For each tuple position, the corresponding elements from the left-hand and right-hand tuple operands are comparable with the `==` and `!=` operators.</span></span> <span data-ttu-id="1eb11-157">例如，`(1, (2, 3)) == ((1, 2), 3)` 不会进行编译，因为 `1` 不可与 `(1, 2)` 比较。</span><span class="sxs-lookup"><span data-stu-id="1eb11-157">For example, `(1, (2, 3)) == ((1, 2), 3)` doesn't compile because `1` is not comparable with `(1, 2)`.</span></span>

<span data-ttu-id="1eb11-158">`==` 和 `!=` 运算符将以短路方式对元组进行比较。</span><span class="sxs-lookup"><span data-stu-id="1eb11-158">The `==` and `!=` operators compare tuples in short-circuiting way.</span></span> <span data-ttu-id="1eb11-159">也就是说，一旦遇见一对不相等的元素或达到元组的末尾，操作将立即停止。</span><span class="sxs-lookup"><span data-stu-id="1eb11-159">That is, an operation stops as soon as it meets a pair of non equal elements or reaches the ends of tuples.</span></span> <span data-ttu-id="1eb11-160">但是，在进行任何比较之前，将对所有元组元素进行计算，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="1eb11-160">However, before any comparison, *all* tuple elements are evaluated, as the following example shows:</span></span>

[!code-csharp-interactive[tuple element evaluation](snippets/shared/ValueTuples.cs#TupleEvaluationForEquality)]

## <a name="tuples-as-out-parameters"></a><span data-ttu-id="1eb11-161">元组作为 out 参数</span><span class="sxs-lookup"><span data-stu-id="1eb11-161">Tuples as out parameters</span></span>

<span data-ttu-id="1eb11-162">通常，你会将具有 [`out` 参数](../keywords/out-parameter-modifier.md)的方法重构为返回元组的方法。</span><span class="sxs-lookup"><span data-stu-id="1eb11-162">Typically, you refactor a method that has [`out` parameters](../keywords/out-parameter-modifier.md) into a method that returns a tuple.</span></span> <span data-ttu-id="1eb11-163">但是，在某些情况下，`out` 参数可以是元组类型。</span><span class="sxs-lookup"><span data-stu-id="1eb11-163">However, there are cases in which an `out` parameter can be of a tuple type.</span></span> <span data-ttu-id="1eb11-164">下面的示例演示了如何将元组作为 `out` 参数使用：</span><span class="sxs-lookup"><span data-stu-id="1eb11-164">The following example shows how to work with tuples as `out` parameters:</span></span>

[!code-csharp-interactive[tuple as out parameter](snippets/shared/ValueTuples.cs#TupleAsOutParameter)]

## <a name="tuples-vs-systemtuple"></a><span data-ttu-id="1eb11-165">元组与 `System.Tuple`</span><span class="sxs-lookup"><span data-stu-id="1eb11-165">Tuples vs `System.Tuple`</span></span>

<span data-ttu-id="1eb11-166"><xref:System.ValueTuple?displayProperty=nameWithType> 类型支持的 C# 元组不同于 <xref:System.Tuple?displayProperty=nameWithType> 类型表示的元组。</span><span class="sxs-lookup"><span data-stu-id="1eb11-166">C# tuples, which are backed by <xref:System.ValueTuple?displayProperty=nameWithType> types, are different from tuples that are represented by <xref:System.Tuple?displayProperty=nameWithType> types.</span></span> <span data-ttu-id="1eb11-167">主要区别如下：</span><span class="sxs-lookup"><span data-stu-id="1eb11-167">The main differences are as follows:</span></span>

- <span data-ttu-id="1eb11-168">`ValueTuple` 类型是[值类型](value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="1eb11-168">`ValueTuple` types are [value types](value-types.md).</span></span> <span data-ttu-id="1eb11-169">`Tuple` 类型是[引用类型](../keywords/reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="1eb11-169">`Tuple` types are [reference types](../keywords/reference-types.md).</span></span>
- <span data-ttu-id="1eb11-170">`ValueTuple` 类型是可变的。</span><span class="sxs-lookup"><span data-stu-id="1eb11-170">`ValueTuple` types are mutable.</span></span> <span data-ttu-id="1eb11-171">`Tuple` 类型是不可变的。</span><span class="sxs-lookup"><span data-stu-id="1eb11-171">`Tuple` types are immutable.</span></span>
- <span data-ttu-id="1eb11-172">`ValueTuple` 类型的数据成员是字段。</span><span class="sxs-lookup"><span data-stu-id="1eb11-172">Data members of `ValueTuple` types are fields.</span></span> <span data-ttu-id="1eb11-173">`Tuple` 类型的数据成员是属性。</span><span class="sxs-lookup"><span data-stu-id="1eb11-173">Data members of `Tuple` types are properties.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="1eb11-174">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="1eb11-174">C# language specification</span></span>

<span data-ttu-id="1eb11-175">有关详细信息，请参阅以下功能建议说明：</span><span class="sxs-lookup"><span data-stu-id="1eb11-175">For more information, see the following feature proposal notes:</span></span>

- [<span data-ttu-id="1eb11-176">推断元组名称（也称为元组投影初始值设定项）</span><span class="sxs-lookup"><span data-stu-id="1eb11-176">Infer tuple names (aka. tuple projection initializers)</span></span>](~/_csharplang/proposals/csharp-7.1/infer-tuple-names.md)
- [<span data-ttu-id="1eb11-177">支持对元组类型使用 `==` 和 `!=`</span><span class="sxs-lookup"><span data-stu-id="1eb11-177">Support for `==` and `!=` on tuple types</span></span>](~/_csharplang/proposals/csharp-7.3/tuple-equality.md)

## <a name="see-also"></a><span data-ttu-id="1eb11-178">请参阅</span><span class="sxs-lookup"><span data-stu-id="1eb11-178">See also</span></span>

- [<span data-ttu-id="1eb11-179">C# 参考</span><span class="sxs-lookup"><span data-stu-id="1eb11-179">C# reference</span></span>](../index.md)
- [<span data-ttu-id="1eb11-180">值类型</span><span class="sxs-lookup"><span data-stu-id="1eb11-180">Value types</span></span>](value-types.md)
- [<span data-ttu-id="1eb11-181">在匿名类型和元组类型之间选择</span><span class="sxs-lookup"><span data-stu-id="1eb11-181">Choosing between anonymous and tuple types</span></span>](../../../standard/base-types/choosing-between-anonymous-and-tuple.md)
- <xref:System.ValueTuple?displayProperty=nameWithType>
