---
title: 可为空的值类型 - C# 参考
description: 了解 C# 中可以为 null 的值类型及其使用方法
ms.date: 11/04/2019
helpviewer_keywords:
- nullable value types [C#]
ms.openlocfilehash: 3ab2dff6b7399b0458a69d4498b2ebda24f6c5cc
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471830"
---
# <a name="nullable-value-types-c-reference"></a><span data-ttu-id="8522d-103">可为空的值类型（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="8522d-103">Nullable value types (C# reference)</span></span>

<span data-ttu-id="8522d-104">可为 null 值类型  `T?` 表示其基础[值类型](value-types.md) `T` 的所有值及额外的 [null](../keywords/null.md) 值。</span><span class="sxs-lookup"><span data-stu-id="8522d-104">A *nullable value type* `T?` represents all values of its underlying [value type](value-types.md) `T` and an additional [null](../keywords/null.md) value.</span></span> <span data-ttu-id="8522d-105">例如，可以将以下三个值中的任意一个指定给 `bool?` 变量：`true`、`false` 或 `null`。</span><span class="sxs-lookup"><span data-stu-id="8522d-105">For example, you can assign any of the following three values to a `bool?` variable: `true`, `false`, or `null`.</span></span> <span data-ttu-id="8522d-106">基础值类型 `T` 本身不能是可为空的值类型。</span><span class="sxs-lookup"><span data-stu-id="8522d-106">An underlying value type `T` cannot be a nullable value type itself.</span></span>

> [!NOTE]
> <span data-ttu-id="8522d-107">C# 8.0 引入了可为空引用类型功能。</span><span class="sxs-lookup"><span data-stu-id="8522d-107">C# 8.0 introduces the nullable reference types feature.</span></span> <span data-ttu-id="8522d-108">有关详细信息，请参阅[可为空引用类型](nullable-reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="8522d-108">For more information, see [Nullable reference types](nullable-reference-types.md).</span></span> <span data-ttu-id="8522d-109">从 C# 2 开始，提供可为空的值类型。</span><span class="sxs-lookup"><span data-stu-id="8522d-109">The nullable value types are available beginning with C# 2.</span></span>

<span data-ttu-id="8522d-110">任何可为空的值类型都是泛型 <xref:System.Nullable%601?displayProperty=nameWithType> 结构的实例。</span><span class="sxs-lookup"><span data-stu-id="8522d-110">Any nullable value type is an instance of the generic <xref:System.Nullable%601?displayProperty=nameWithType> structure.</span></span> <span data-ttu-id="8522d-111">可使用以下任何一种可互换形式引用具有基础类型 `T` 的可为空值类型：`Nullable<T>` 或 `T?`。</span><span class="sxs-lookup"><span data-stu-id="8522d-111">You can refer to a nullable value type with an underlying type `T` in any of the following interchangeable forms: `Nullable<T>` or `T?`.</span></span>

<span data-ttu-id="8522d-112">需要表示基础值类型的未定义值时，通常使用可为空的值类型。</span><span class="sxs-lookup"><span data-stu-id="8522d-112">You typically use a nullable value type when you need to represent the undefined value of an underlying value type.</span></span> <span data-ttu-id="8522d-113">例如，布尔值或 `bool` 变量只能为 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="8522d-113">For example, a Boolean, or `bool`, variable can only be either `true` or `false`.</span></span> <span data-ttu-id="8522d-114">但是，在某些应用程序中，变量值可能未定义或缺失。</span><span class="sxs-lookup"><span data-stu-id="8522d-114">However, in some applications a variable value can be undefined or missing.</span></span> <span data-ttu-id="8522d-115">例如，某个数据库字段可能包含 `true` 或 `false`，或者它可能不包含任何值，即 `NULL`。</span><span class="sxs-lookup"><span data-stu-id="8522d-115">For example, a database field may contain `true` or `false`, or it may contain no value at all, that is, `NULL`.</span></span> <span data-ttu-id="8522d-116">在这种情况下，可以使用 `bool?` 类型。</span><span class="sxs-lookup"><span data-stu-id="8522d-116">You can use the `bool?` type in that scenario.</span></span>

## <a name="declaration-and-assignment"></a><span data-ttu-id="8522d-117">声明和赋值</span><span class="sxs-lookup"><span data-stu-id="8522d-117">Declaration and assignment</span></span>

<span data-ttu-id="8522d-118">由于值类型可隐式转换为相应的可为空的值类型，因此可以像向其基础值类型赋值一样，向可为空值类型的变量赋值。</span><span class="sxs-lookup"><span data-stu-id="8522d-118">As a value type is implicitly convertible to the corresponding nullable value type, you can assign a value to a variable of a nullable value type as you would do that for its underlying value type.</span></span> <span data-ttu-id="8522d-119">还可分配 `null` 值。</span><span class="sxs-lookup"><span data-stu-id="8522d-119">You can also assign the `null` value.</span></span> <span data-ttu-id="8522d-120">例如：</span><span class="sxs-lookup"><span data-stu-id="8522d-120">For example:</span></span>

[!code-csharp[declare and assign](snippets/shared/NullableValueTypes.cs#Declaration)]

<span data-ttu-id="8522d-121">可为空值类型的默认值表示 `null`，也就是说，它是其 <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> 属性返回 `false` 的实例。</span><span class="sxs-lookup"><span data-stu-id="8522d-121">The default value of a nullable value type represents `null`, that is, it's an instance whose <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> property returns `false`.</span></span>

## <a name="examination-of-an-instance-of-a-nullable-value-type"></a><span data-ttu-id="8522d-122">检查可为空值类型的实例</span><span class="sxs-lookup"><span data-stu-id="8522d-122">Examination of an instance of a nullable value type</span></span>

<span data-ttu-id="8522d-123">从 C# 7.0 开始，可以将 [`is` 运算符与类型模式 ](../operators/type-testing-and-cast.md#type-testing-with-pattern-matching) 结合使用，既检查 `null` 的可为空值类型的实例，又检索基础类型的值：</span><span class="sxs-lookup"><span data-stu-id="8522d-123">Beginning with C# 7.0, you can use the [`is` operator with a type pattern](../operators/type-testing-and-cast.md#type-testing-with-pattern-matching) to both examine an instance of a nullable value type for `null` and retrieve a value of an underlying type:</span></span>

[!code-csharp-interactive[use pattern matching](snippets/shared/NullableValueTypes.cs#PatternMatching)]

<span data-ttu-id="8522d-124">始终可以使用以下只读属性来检查和获取可为空值类型变量的值：</span><span class="sxs-lookup"><span data-stu-id="8522d-124">You always can use the following read-only properties to examine and get a value of a nullable value type variable:</span></span>

- <span data-ttu-id="8522d-125"><xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> 指示可为空值类型的实例是否有基础类型的值。</span><span class="sxs-lookup"><span data-stu-id="8522d-125"><xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> indicates whether an instance of a nullable value type has a value of its underlying type.</span></span>

- <span data-ttu-id="8522d-126">如果 <xref:System.Nullable%601.HasValue%2A> 为 `true`，则 <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> 获取基础类型的值。</span><span class="sxs-lookup"><span data-stu-id="8522d-126"><xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> gets the value of an underlying type if <xref:System.Nullable%601.HasValue%2A> is `true`.</span></span> <span data-ttu-id="8522d-127">如果 <xref:System.Nullable%601.HasValue%2A> 为 `false`，则 <xref:System.Nullable%601.Value%2A> 属性将引发 <xref:System.InvalidOperationException>。</span><span class="sxs-lookup"><span data-stu-id="8522d-127">If <xref:System.Nullable%601.HasValue%2A> is `false`, the <xref:System.Nullable%601.Value%2A> property throws an <xref:System.InvalidOperationException>.</span></span>

<span data-ttu-id="8522d-128">以下示例中的使用 `HasValue` 属性在显示值之前测试变量是否包含该值：</span><span class="sxs-lookup"><span data-stu-id="8522d-128">The following example uses the `HasValue` property to test whether the variable contains a value before displaying it:</span></span>

[!code-csharp-interactive[use HasValue](snippets/shared/NullableValueTypes.cs#HasValue)]

<span data-ttu-id="8522d-129">还可将可为空的值类型的变量与 `null` 进行比较，而不是使用 `HasValue` 属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="8522d-129">You can also compare a variable of a nullable value type with `null` instead of using the `HasValue` property, as the following example shows:</span></span>

[!code-csharp-interactive[use comparison with null](snippets/shared/NullableValueTypes.cs#CompareWithNull)]

## <a name="conversion-from-a-nullable-value-type-to-an-underlying-type"></a><span data-ttu-id="8522d-130">从可为空的值类型转换为基础类型</span><span class="sxs-lookup"><span data-stu-id="8522d-130">Conversion from a nullable value type to an underlying type</span></span>

<span data-ttu-id="8522d-131">如果要将可为空值类型的值分配给不可以为 null 的值类型变量，则可能需要指定要分配的替代 `null` 的值。</span><span class="sxs-lookup"><span data-stu-id="8522d-131">If you want to assign a value of a nullable value type to a non-nullable value type variable, you might need to specify the value to be assigned in place of `null`.</span></span> <span data-ttu-id="8522d-132">使用 [Null 合并操作符`??`](../operators/null-coalescing-operator.md)执行此操作（也可将 <xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType> 方法用于相同的目的）：</span><span class="sxs-lookup"><span data-stu-id="8522d-132">Use the [null-coalescing operator `??`](../operators/null-coalescing-operator.md) to do that (you can also use the <xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType> method for the same purpose):</span></span>

[!code-csharp-interactive[?? operator](snippets/shared/NullableValueTypes.cs#NullCoalescing)]

<span data-ttu-id="8522d-133">如果要使用基础值类型的[默认值](default-values.md)来替代 `null`，请使用 <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="8522d-133">If you want to use the [default](default-values.md) value of the underlying value type in place of `null`, use the <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="8522d-134">还可以将可为空的值类型显式强制转换为不可为 null 的类型，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="8522d-134">You can also explicitly cast a nullable value type to a non-nullable type, as the following example shows:</span></span>

[!code-csharp[explicit cast](snippets/shared/NullableValueTypes.cs#Cast)]

<span data-ttu-id="8522d-135">在运行时，如果可为空的值类型的值为 `null`，则显式强制转换将抛出 <xref:System.InvalidOperationException>。</span><span class="sxs-lookup"><span data-stu-id="8522d-135">At run time, if the value of a nullable value type is `null`, the explicit cast throws an <xref:System.InvalidOperationException>.</span></span>

<span data-ttu-id="8522d-136">不可为 null 的值类型 `T` 隐式转换为相应的可为空值类型 `T?`。</span><span class="sxs-lookup"><span data-stu-id="8522d-136">A non-nullable value type `T` is implicitly convertible to the corresponding nullable value type `T?`.</span></span>

## <a name="lifted-operators"></a><span data-ttu-id="8522d-137">提升的运算符</span><span class="sxs-lookup"><span data-stu-id="8522d-137">Lifted operators</span></span>

<span data-ttu-id="8522d-138">预定义的一元运算符和二元[运算符](../operators/index.md)或值类型 `T` 支持的任何重载运算符也受相应的可为空值类型 `T?` 支持。</span><span class="sxs-lookup"><span data-stu-id="8522d-138">The predefined unary and binary [operators](../operators/index.md) or any overloaded operators that are supported by a value type `T` are also supported by the corresponding nullable value type `T?`.</span></span> <span data-ttu-id="8522d-139">如果一个或全部两个操作数为 `null` ，则这些运算符（也称为提升的运算符）将生成 `null`；否则，运算符使用其操作数所包含的值来计算结果。</span><span class="sxs-lookup"><span data-stu-id="8522d-139">These operators, also known as *lifted operators* , produce `null` if one or both operands are `null`; otherwise, the operator uses the contained values of its operands to calculate the result.</span></span> <span data-ttu-id="8522d-140">例如：</span><span class="sxs-lookup"><span data-stu-id="8522d-140">For example:</span></span>

[!code-csharp[lifted operators](snippets/shared/NullableValueTypes.cs#LiftedOperator)]

> [!NOTE]
> <span data-ttu-id="8522d-141">对于 `bool?` 类型，预定义的 `&` 和 `|` 运算符不遵循此部分中描述的规则：即使其中一个操作数为 `null`，运算符计算结果也可以不为 NULL。</span><span class="sxs-lookup"><span data-stu-id="8522d-141">For the `bool?` type, the predefined `&` and `|` operators don't follow the rules described in this section: the result of an operator evaluation can be non-null even if one of the operands is `null`.</span></span> <span data-ttu-id="8522d-142">有关详细信息，请参阅[布尔逻辑运算符](../operators/boolean-logical-operators.md)一文的[可以为 null 的布尔逻辑运算符](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators)部分。</span><span class="sxs-lookup"><span data-stu-id="8522d-142">For more information, see the [Nullable Boolean logical operators](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) section of the [Boolean logical operators](../operators/boolean-logical-operators.md) article.</span></span>

<span data-ttu-id="8522d-143">对于[比较运算符](../operators/comparison-operators.md) `<`、`>`、`<=` 和 `>=`，如果一个或全部两个操作数都为 `null`，则结果为 `false`；否则，将比较操作数的包含值。</span><span class="sxs-lookup"><span data-stu-id="8522d-143">For the [comparison operators](../operators/comparison-operators.md) `<`, `>`, `<=`, and `>=`, if one or both operands are `null`, the result is `false`; otherwise, the contained values of operands are compared.</span></span> <span data-ttu-id="8522d-144">请勿作出如下假定：由于某个特定的比较（例如 `<=`）返回 `false`，则相反的比较 (`>`) 返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="8522d-144">Do not assume that because a particular comparison (for example, `<=`) returns `false`, the opposite comparison (`>`) returns `true`.</span></span> <span data-ttu-id="8522d-145">以下示例显示 10</span><span class="sxs-lookup"><span data-stu-id="8522d-145">The following example shows that 10 is</span></span>

- <span data-ttu-id="8522d-146">既不大于等于 `null`，</span><span class="sxs-lookup"><span data-stu-id="8522d-146">neither greater than or equal to `null`</span></span>
- <span data-ttu-id="8522d-147">也不小于 `null`</span><span class="sxs-lookup"><span data-stu-id="8522d-147">nor less than `null`</span></span>

[!code-csharp-interactive[relational and equality operators](snippets/shared/NullableValueTypes.cs#ComparisonOperators)]

<span data-ttu-id="8522d-148">对于[相等运算符](../operators/equality-operators.md#equality-operator-) `==`，如果两个操作数都为 `null`，则结果为 `true`；如果只有一个操作数为 `null`，则结果为 `false`；否则，将比较操作数的包含值。</span><span class="sxs-lookup"><span data-stu-id="8522d-148">For the [equality operator](../operators/equality-operators.md#equality-operator-) `==`, if both operands are `null`, the result is `true`, if only one of the operands is `null`, the result is `false`; otherwise, the contained values of operands are compared.</span></span>

<span data-ttu-id="8522d-149">对于[不等运算符](../operators/equality-operators.md#inequality-operator-) `!=`，如果两个操作数都为 `null`，则结果为 `false`；如果只有一个操作数为 `null`，则结果为 `true`；否则，将比较操作数的包含值。</span><span class="sxs-lookup"><span data-stu-id="8522d-149">For the [inequality operator](../operators/equality-operators.md#inequality-operator-) `!=`, if both operands are `null`, the result is `false`, if only one of the operands is `null`, the result is `true`; otherwise, the contained values of operands are compared.</span></span>

<span data-ttu-id="8522d-150">如果在两个值类型之间存在[用户定义的转换](../operators/user-defined-conversion-operators.md)，则还可在相应的可为空值类型之间使用同一转换。</span><span class="sxs-lookup"><span data-stu-id="8522d-150">If there exists a [user-defined conversion](../operators/user-defined-conversion-operators.md) between two value types, the same conversion can also be used between the corresponding nullable value types.</span></span>

## <a name="boxing-and-unboxing"></a><span data-ttu-id="8522d-151">装箱和取消装箱</span><span class="sxs-lookup"><span data-stu-id="8522d-151">Boxing and unboxing</span></span>

<span data-ttu-id="8522d-152">可为空值类型的实例 `T?`[已装箱](../../programming-guide/types/boxing-and-unboxing.md)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8522d-152">An instance of a nullable value type `T?` is [boxed](../../programming-guide/types/boxing-and-unboxing.md) as follows:</span></span>

- <span data-ttu-id="8522d-153">如果 <xref:System.Nullable%601.HasValue%2A> 返回 `false`，则生成空引用。</span><span class="sxs-lookup"><span data-stu-id="8522d-153">If <xref:System.Nullable%601.HasValue%2A> returns `false`, the null reference is produced.</span></span>
- <span data-ttu-id="8522d-154">如果 <xref:System.Nullable%601.HasValue%2A> 返回 `true`，则基础值类型 `T` 的对应值将装箱，而不对 <xref:System.Nullable%601> 的实例进行装箱。</span><span class="sxs-lookup"><span data-stu-id="8522d-154">If <xref:System.Nullable%601.HasValue%2A> returns `true`, the corresponding value of the underlying value type `T` is boxed, not the instance of <xref:System.Nullable%601>.</span></span>

<span data-ttu-id="8522d-155">可将值类型 `T` 的已装箱值取消装箱到相应的可为空值类型 `T?`，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="8522d-155">You can unbox a boxed value of a value type `T` to the corresponding nullable value type `T?`, as the following example shows:</span></span>

[!code-csharp-interactive[boxing and unboxing](snippets/shared/NullableValueTypes.cs#Boxing)]

## <a name="how-to-identify-a-nullable-value-type"></a><span data-ttu-id="8522d-156">如何确定可为空的值类型</span><span class="sxs-lookup"><span data-stu-id="8522d-156">How to identify a nullable value type</span></span>

<span data-ttu-id="8522d-157">下面的示例演示了如何确定 <xref:System.Type?displayProperty=nameWithType> 实例是否表示已构造的可为空值类型，即，具有指定类型参数 `T` 的 <xref:System.Nullable%601?displayProperty=nameWithType> 类型：</span><span class="sxs-lookup"><span data-stu-id="8522d-157">The following example shows how to determine whether a <xref:System.Type?displayProperty=nameWithType> instance represents a constructed nullable value type, that is, the <xref:System.Nullable%601?displayProperty=nameWithType> type with a specified type parameter `T`:</span></span>

[!code-csharp-interactive[whether Type is nullable](snippets/shared/NullableValueTypes.cs#IsTypeNullable)]

<span data-ttu-id="8522d-158">如示例所示，使用 [typeof](../operators/type-testing-and-cast.md#typeof-operator) 运算符来创建 <xref:System.Type?displayProperty=nameWithType> 实例。</span><span class="sxs-lookup"><span data-stu-id="8522d-158">As the example shows, you use the [typeof](../operators/type-testing-and-cast.md#typeof-operator) operator to create a <xref:System.Type?displayProperty=nameWithType> instance.</span></span>

<span data-ttu-id="8522d-159">如果要确定实例是否是可为空的值类型，请不要使用 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 方法获取要通过前面的代码测试的 <xref:System.Type> 实例。</span><span class="sxs-lookup"><span data-stu-id="8522d-159">If you want to determine whether an instance is of a nullable value type, don't use the <xref:System.Object.GetType%2A?displayProperty=nameWithType> method to get a <xref:System.Type> instance to be tested with the preceding code.</span></span> <span data-ttu-id="8522d-160">如果对值类型可为空的实例调用 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 方法，该实例将[装箱](#boxing-and-unboxing)到 <xref:System.Object>。</span><span class="sxs-lookup"><span data-stu-id="8522d-160">When you call the <xref:System.Object.GetType%2A?displayProperty=nameWithType> method on an instance of a nullable value type, the instance is [boxed](#boxing-and-unboxing) to <xref:System.Object>.</span></span> <span data-ttu-id="8522d-161">由于对可为空的值类型的非 NULL 实例的装箱等同于对基础类型的值的装箱，因此 <xref:System.Object.GetType%2A> 会返回表示可为空的值类型的基础类型的 <xref:System.Type> 实例：</span><span class="sxs-lookup"><span data-stu-id="8522d-161">As boxing of a non-null instance of a nullable value type is equivalent to boxing of a value of the underlying type, <xref:System.Object.GetType%2A> returns a <xref:System.Type> instance that represents the underlying type of a nullable value type:</span></span>

[!code-csharp-interactive[GetType example](snippets/shared/NullableValueTypes.cs#GetType)]

<span data-ttu-id="8522d-162">另外，请勿使用 [is](../operators/type-testing-and-cast.md#is-operator) 运算符来确定实例是否是可为空的值类型。</span><span class="sxs-lookup"><span data-stu-id="8522d-162">Also, don't use the [is](../operators/type-testing-and-cast.md#is-operator) operator to determine whether an instance is of a nullable value type.</span></span> <span data-ttu-id="8522d-163">如以下示例所示，无法使用 `is` 运算符区分可为空值类型实例的类型与其基础类型实例：</span><span class="sxs-lookup"><span data-stu-id="8522d-163">As the following example shows, you cannot distinguish types of a nullable value type instance and its underlying type instance with the `is` operator:</span></span>

[!code-csharp-interactive[is operator example](snippets/shared/NullableValueTypes.cs#IsOperator)]

<span data-ttu-id="8522d-164">可使用以下示例中提供的代码来确定实例是否是可为空的值类型：</span><span class="sxs-lookup"><span data-stu-id="8522d-164">You can use the code presented in the following example to determine whether an instance is of a nullable value type:</span></span>

[!code-csharp-interactive[whether an instance is of a nullable type](snippets/shared/NullableValueTypes.cs#IsInstanceNullable)]

> [!NOTE]
> <span data-ttu-id="8522d-165">此部分中所述的方法不适用于[可为空的引用类型](nullable-reference-types.md)的情况。</span><span class="sxs-lookup"><span data-stu-id="8522d-165">The methods described in this section are not applicable in the case of [nullable reference types](nullable-reference-types.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="8522d-166">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="8522d-166">C# language specification</span></span>

<span data-ttu-id="8522d-167">有关更多信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的以下部分：</span><span class="sxs-lookup"><span data-stu-id="8522d-167">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="8522d-168">可以为 null 的类型</span><span class="sxs-lookup"><span data-stu-id="8522d-168">Nullable types</span></span>](~/_csharplang/spec/types.md#nullable-types)
- [<span data-ttu-id="8522d-169">提升的运算符</span><span class="sxs-lookup"><span data-stu-id="8522d-169">Lifted operators</span></span>](~/_csharplang/spec/expressions.md#lifted-operators)
- [<span data-ttu-id="8522d-170">隐式可为空转换</span><span class="sxs-lookup"><span data-stu-id="8522d-170">Implicit nullable conversions</span></span>](~/_csharplang/spec/conversions.md#implicit-nullable-conversions)
- [<span data-ttu-id="8522d-171">显式可为空转换</span><span class="sxs-lookup"><span data-stu-id="8522d-171">Explicit nullable conversions</span></span>](~/_csharplang/spec/conversions.md#explicit-nullable-conversions)
- [<span data-ttu-id="8522d-172">提升的转换运算符</span><span class="sxs-lookup"><span data-stu-id="8522d-172">Lifted conversion operators</span></span>](~/_csharplang/spec/conversions.md#lifted-conversion-operators)

## <a name="see-also"></a><span data-ttu-id="8522d-173">请参阅</span><span class="sxs-lookup"><span data-stu-id="8522d-173">See also</span></span>

- [<span data-ttu-id="8522d-174">C# 参考</span><span class="sxs-lookup"><span data-stu-id="8522d-174">C# reference</span></span>](../index.md)
- [<span data-ttu-id="8522d-175">“提升”的准确含义是什么？</span><span class="sxs-lookup"><span data-stu-id="8522d-175">What exactly does 'lifted' mean?</span></span>](/archive/blogs/ericlippert/what-exactly-does-lifted-mean)
- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Nullable?displayProperty=nameWithType>
- <xref:System.Nullable.GetUnderlyingType%2A?displayProperty=nameWithType>
- [<span data-ttu-id="8522d-176">可为空引用类型</span><span class="sxs-lookup"><span data-stu-id="8522d-176">Nullable reference types</span></span>](nullable-reference-types.md)
