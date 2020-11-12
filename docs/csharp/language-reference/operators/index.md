---
title: C# 运算符和表达式 - C# 参考
description: 了解 C# 运算符和表达式、运算符优先级和运算符结合性
ms.date: 08/04/2020
f1_keywords:
- cs.operators
helpviewer_keywords:
- operators [C#]
- operator precedence [C#]
- operator associativity [C#]
- expressions [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
ms.openlocfilehash: 9e7ca2087938317f7369043e21fd455dbad7f07b
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94439652"
---
# <a name="c-operators-and-expressions-c-reference"></a><span data-ttu-id="5e271-103">C# 运算符和表达式（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="5e271-103">C# operators and expressions (C# reference)</span></span>

<span data-ttu-id="5e271-104">C# 提供了许多运算符。</span><span class="sxs-lookup"><span data-stu-id="5e271-104">C# provides a number of operators.</span></span> <span data-ttu-id="5e271-105">其中许多都受到[内置类型](../builtin-types/built-in-types.md)的支持，可用于对这些类型的值执行基本操作。</span><span class="sxs-lookup"><span data-stu-id="5e271-105">Many of them are supported by the [built-in types](../builtin-types/built-in-types.md) and allow you to perform basic operations with values of those types.</span></span> <span data-ttu-id="5e271-106">这些运算符包括以下组：</span><span class="sxs-lookup"><span data-stu-id="5e271-106">Those operators include the following groups:</span></span>

- <span data-ttu-id="5e271-107">[算术运算符](arithmetic-operators.md)，将对数值操作数执行算术运算</span><span class="sxs-lookup"><span data-stu-id="5e271-107">[Arithmetic operators](arithmetic-operators.md) that perform arithmetic operations with numeric operands</span></span>
- <span data-ttu-id="5e271-108">[比较运算符](comparison-operators.md)，将比较数值操作数</span><span class="sxs-lookup"><span data-stu-id="5e271-108">[Comparison operators](comparison-operators.md) that compare numeric operands</span></span>
- <span data-ttu-id="5e271-109">[布尔逻辑运算符](boolean-logical-operators.md)，将对 [`bool`](../builtin-types/bool.md) 操作数执行逻辑运算</span><span class="sxs-lookup"><span data-stu-id="5e271-109">[Boolean logical operators](boolean-logical-operators.md) that perform logical operations with [`bool`](../builtin-types/bool.md) operands</span></span>
- <span data-ttu-id="5e271-110">[位运算符和移位运算符](bitwise-and-shift-operators.md)，将对整数类型的操作数执行位运算或移位运算</span><span class="sxs-lookup"><span data-stu-id="5e271-110">[Bitwise and shift operators](bitwise-and-shift-operators.md) that perform bitwise or shift operations with operands of the integral types</span></span>
- <span data-ttu-id="5e271-111">[相等运算符](equality-operators.md)，将检查其操作数是否相等</span><span class="sxs-lookup"><span data-stu-id="5e271-111">[Equality operators](equality-operators.md) that check if their operands are equal or not</span></span>

<span data-ttu-id="5e271-112">通常可以[重载](operator-overloading.md)这些运算符，也就是说，可以为用户定义类型的操作数指定运算符行为。</span><span class="sxs-lookup"><span data-stu-id="5e271-112">Typically, you can [overload](operator-overloading.md) those operators, that is, specify the operator behavior for the operands of a user-defined type.</span></span>

<span data-ttu-id="5e271-113">最简单的 C# 表达式是文本（例如[整数](../builtin-types/integral-numeric-types.md#integer-literals)和[实数](../builtin-types/floating-point-numeric-types.md#real-literals)）和变量名称。</span><span class="sxs-lookup"><span data-stu-id="5e271-113">The simplest C# expressions are literals (for example, [integer](../builtin-types/integral-numeric-types.md#integer-literals) and [real](../builtin-types/floating-point-numeric-types.md#real-literals) numbers) and names of variables.</span></span> <span data-ttu-id="5e271-114">可以使用运算符将它们组合成复杂的表达式。</span><span class="sxs-lookup"><span data-stu-id="5e271-114">You can combine them into complex expressions by using operators.</span></span> <span data-ttu-id="5e271-115">运算符[优先级](#operator-precedence)和[结合性](#operator-associativity)决定了表达式中操作的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="5e271-115">Operator [precedence](#operator-precedence) and [associativity](#operator-associativity) determine the order in which the operations in an expression are performed.</span></span> <span data-ttu-id="5e271-116">可以使用括号更改由运算符优先级和结合性决定的计算顺序。</span><span class="sxs-lookup"><span data-stu-id="5e271-116">You can use parentheses to change the order of evaluation imposed by operator precedence and associativity.</span></span>

<span data-ttu-id="5e271-117">在下面的代码中，表达式的示例位于赋值的右侧：</span><span class="sxs-lookup"><span data-stu-id="5e271-117">In the following code, examples of expressions are at the right-hand side of assignments:</span></span>

[!code-csharp[expression examples](snippets/shared/Overview.cs#Expressions)]

<span data-ttu-id="5e271-118">通常情况下，表达式会生成结果，并可包含在其他表达式中。</span><span class="sxs-lookup"><span data-stu-id="5e271-118">Typically, an expression produces a result and can be included in another expression.</span></span> <span data-ttu-id="5e271-119">[`void`](../builtin-types/void.md) 方法调用是不生成结果的表达式的示例。</span><span class="sxs-lookup"><span data-stu-id="5e271-119">A [`void`](../builtin-types/void.md) method call is an example of an expression that doesn't produce a result.</span></span> <span data-ttu-id="5e271-120">它只能用作[语句](../../programming-guide/statements-expressions-operators/statements.md)，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="5e271-120">It can be used only as a [statement](../../programming-guide/statements-expressions-operators/statements.md), as the following example shows:</span></span>

```csharp
Console.WriteLine("Hello, world!");
```

<span data-ttu-id="5e271-121">下面是 C# 提供的一些其他类型的表达式：</span><span class="sxs-lookup"><span data-stu-id="5e271-121">Here are some other kinds of expressions that C# provides:</span></span>

- <span data-ttu-id="5e271-122">[内插字符串表达式](../tokens/interpolated.md)，提供创建格式化字符串的便利语法：</span><span class="sxs-lookup"><span data-stu-id="5e271-122">[Interpolated string expressions](../tokens/interpolated.md) that provide convenient syntax to create formatted strings:</span></span>

  [!code-csharp-interactive[interpolated string](snippets/shared/Overview.cs#InterpolatedString)]

- <span data-ttu-id="5e271-123">[Lambda 表达式](lambda-expressions.md)，可用于创建匿名函数：</span><span class="sxs-lookup"><span data-stu-id="5e271-123">[Lambda expressions](lambda-expressions.md) that allow you to create anonymous functions:</span></span>

  [!code-csharp-interactive[lambda expression](snippets/shared/Overview.cs#Lambda)]

- <span data-ttu-id="5e271-124">[查询表达式](../keywords/query-keywords.md)，可用于直接以 C# 使用查询功能：</span><span class="sxs-lookup"><span data-stu-id="5e271-124">[Query expressions](../keywords/query-keywords.md) that allow you to use query capabilities directly in C#:</span></span>

  [!code-csharp-interactive[query expression](snippets/shared/Overview.cs#Query)]

<span data-ttu-id="5e271-125">可使用[表达式主体定义](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)为方法、构造函数、属性、索引器或终结器提供简洁的定义。</span><span class="sxs-lookup"><span data-stu-id="5e271-125">You can use an [expression body definition](../../programming-guide/statements-expressions-operators/expression-bodied-members.md) to provide a concise definition for a method, constructor, property, indexer, or finalizer.</span></span>

## <a name="operator-precedence"></a><span data-ttu-id="5e271-126">运算符优先级</span><span class="sxs-lookup"><span data-stu-id="5e271-126">Operator precedence</span></span>

<span data-ttu-id="5e271-127">在包含多个运算符的表达式中，先按优先级较高的运算符计算，再按优先级较低的运算符计算。</span><span class="sxs-lookup"><span data-stu-id="5e271-127">In an expression with multiple operators, the operators with higher precedence are evaluated before the operators with lower precedence.</span></span> <span data-ttu-id="5e271-128">在下面的示例中，首先执行乘法，因为其优先级高于加法：</span><span class="sxs-lookup"><span data-stu-id="5e271-128">In the following example, the multiplication is performed first because it has higher precedence than addition:</span></span>

```csharp-interactive
var a = 2 + 2 * 2;
Console.WriteLine(a); //  output: 6
```

<span data-ttu-id="5e271-129">使用括号更改运算符优先级所施加的计算顺序：</span><span class="sxs-lookup"><span data-stu-id="5e271-129">Use parentheses to change the order of evaluation imposed by operator precedence:</span></span>

```csharp-interactive
var a = (2 + 2) * 2;
Console.WriteLine(a); //  output: 8
```

<span data-ttu-id="5e271-130">下表按最高优先级到最低优先级的顺序列出 C# 运算符。</span><span class="sxs-lookup"><span data-stu-id="5e271-130">The following table lists the C# operators starting with the highest precedence to the lowest.</span></span> <span data-ttu-id="5e271-131">每行中运算符的优先级相同。</span><span class="sxs-lookup"><span data-stu-id="5e271-131">The operators within each row have the same precedence.</span></span>

| <span data-ttu-id="5e271-132">运算符</span><span class="sxs-lookup"><span data-stu-id="5e271-132">Operators</span></span> | <span data-ttu-id="5e271-133">类别或名称</span><span class="sxs-lookup"><span data-stu-id="5e271-133">Category or name</span></span> |
| --------- | ---------------- |
| <span data-ttu-id="5e271-134">[x.y](member-access-operators.md#member-access-expression-)、[f(x)](member-access-operators.md#invocation-expression-)、[a[i]](member-access-operators.md#indexer-operator-)、[`x?.y`](member-access-operators.md#null-conditional-operators--and-)、[`x?[y]`](member-access-operators.md#null-conditional-operators--and-)、[x++](arithmetic-operators.md#increment-operator-)、[x--](arithmetic-operators.md#decrement-operator---)、[x!](null-forgiving.md)、[new](new-operator.md)、[typeof](type-testing-and-cast.md#typeof-operator)、[checked](../keywords/checked.md)、[unchecked](../keywords/unchecked.md)、[default](default.md)、[nameof](nameof.md)、[delegate](delegate-operator.md)、[sizeof](sizeof.md)、[stackalloc](stackalloc.md)、[x->y](pointer-related-operators.md#pointer-member-access-operator--)</span><span class="sxs-lookup"><span data-stu-id="5e271-134">[x.y](member-access-operators.md#member-access-expression-), [f(x)](member-access-operators.md#invocation-expression-), [a&#91;i&#93;](member-access-operators.md#indexer-operator-), [`x?.y`](member-access-operators.md#null-conditional-operators--and-), [`x?[y]`](member-access-operators.md#null-conditional-operators--and-), [x++](arithmetic-operators.md#increment-operator-), [x--](arithmetic-operators.md#decrement-operator---), [x!](null-forgiving.md), [new](new-operator.md), [typeof](type-testing-and-cast.md#typeof-operator), [checked](../keywords/checked.md), [unchecked](../keywords/unchecked.md), [default](default.md), [nameof](nameof.md), [delegate](delegate-operator.md), [sizeof](sizeof.md), [stackalloc](stackalloc.md), [x->y](pointer-related-operators.md#pointer-member-access-operator--)</span></span> | <span data-ttu-id="5e271-135">基本</span><span class="sxs-lookup"><span data-stu-id="5e271-135">Primary</span></span> |
| <span data-ttu-id="5e271-136">[+x](arithmetic-operators.md#unary-plus-and-minus-operators)、[-x](arithmetic-operators.md#unary-plus-and-minus-operators)、[\!x](boolean-logical-operators.md#logical-negation-operator-)、[~x](bitwise-and-shift-operators.md#bitwise-complement-operator-)、[++x](arithmetic-operators.md#increment-operator-)、[--x](arithmetic-operators.md#decrement-operator---)、[^x](member-access-operators.md#index-from-end-operator-)、[(T)x](type-testing-and-cast.md#cast-expression)、[await](await.md)、[&x](pointer-related-operators.md#address-of-operator-)、[\*x](pointer-related-operators.md#pointer-indirection-operator-)、[true 和 false](true-false-operators.md)</span><span class="sxs-lookup"><span data-stu-id="5e271-136">[+x](arithmetic-operators.md#unary-plus-and-minus-operators), [-x](arithmetic-operators.md#unary-plus-and-minus-operators), [\!x](boolean-logical-operators.md#logical-negation-operator-), [~x](bitwise-and-shift-operators.md#bitwise-complement-operator-), [++x](arithmetic-operators.md#increment-operator-), [--x](arithmetic-operators.md#decrement-operator---), [^x](member-access-operators.md#index-from-end-operator-), [(T)x](type-testing-and-cast.md#cast-expression), [await](await.md), [&x](pointer-related-operators.md#address-of-operator-), [\*x](pointer-related-operators.md#pointer-indirection-operator-), [true and false](true-false-operators.md)</span></span> | <span data-ttu-id="5e271-137">一元</span><span class="sxs-lookup"><span data-stu-id="5e271-137">Unary</span></span> |
| [<span data-ttu-id="5e271-138">x..y</span><span class="sxs-lookup"><span data-stu-id="5e271-138">x..y</span></span>](member-access-operators.md#range-operator-) | <span data-ttu-id="5e271-139">范围</span><span class="sxs-lookup"><span data-stu-id="5e271-139">Range</span></span> |
| [<span data-ttu-id="5e271-140">switch</span><span class="sxs-lookup"><span data-stu-id="5e271-140">switch</span></span>](switch-expression.md) | <span data-ttu-id="5e271-141">`switch` 表达式</span><span class="sxs-lookup"><span data-stu-id="5e271-141">`switch` expression</span></span> |
| [<span data-ttu-id="5e271-142">with</span><span class="sxs-lookup"><span data-stu-id="5e271-142">with</span></span>](with-expression.md) | <span data-ttu-id="5e271-143">`with` 表达式</span><span class="sxs-lookup"><span data-stu-id="5e271-143">`with` expression</span></span> |
| <span data-ttu-id="5e271-144">[x \* y](arithmetic-operators.md#multiplication-operator-)、[x / y](arithmetic-operators.md#division-operator-)、[x % y](arithmetic-operators.md#remainder-operator-)</span><span class="sxs-lookup"><span data-stu-id="5e271-144">[x \* y](arithmetic-operators.md#multiplication-operator-), [x / y](arithmetic-operators.md#division-operator-), [x % y](arithmetic-operators.md#remainder-operator-)</span></span> | <span data-ttu-id="5e271-145">乘法</span><span class="sxs-lookup"><span data-stu-id="5e271-145">Multiplicative</span></span>|
| <span data-ttu-id="5e271-146">[x + y](arithmetic-operators.md#addition-operator-)、[x – y](arithmetic-operators.md#subtraction-operator--)</span><span class="sxs-lookup"><span data-stu-id="5e271-146">[x + y](arithmetic-operators.md#addition-operator-), [x – y](arithmetic-operators.md#subtraction-operator--)</span></span> | <span data-ttu-id="5e271-147">加法</span><span class="sxs-lookup"><span data-stu-id="5e271-147">Additive</span></span> |
| <span data-ttu-id="5e271-148">[x \<\<  y](bitwise-and-shift-operators.md#left-shift-operator-), [x >> y](bitwise-and-shift-operators.md#right-shift-operator-)</span><span class="sxs-lookup"><span data-stu-id="5e271-148">[x \<\<  y](bitwise-and-shift-operators.md#left-shift-operator-), [x >> y](bitwise-and-shift-operators.md#right-shift-operator-)</span></span> | <span data-ttu-id="5e271-149">移位</span><span class="sxs-lookup"><span data-stu-id="5e271-149">Shift</span></span> |
| <span data-ttu-id="5e271-150">[x \< y](comparison-operators.md#less-than-operator-), [x > y](comparison-operators.md#greater-than-operator-)、[x \<= y](comparison-operators.md#less-than-or-equal-operator-), [x >= y](comparison-operators.md#greater-than-or-equal-operator-)、[is](type-testing-and-cast.md#is-operator)、[as](type-testing-and-cast.md#as-operator)</span><span class="sxs-lookup"><span data-stu-id="5e271-150">[x \< y](comparison-operators.md#less-than-operator-), [x > y](comparison-operators.md#greater-than-operator-), [x \<= y](comparison-operators.md#less-than-or-equal-operator-), [x >= y](comparison-operators.md#greater-than-or-equal-operator-), [is](type-testing-and-cast.md#is-operator), [as](type-testing-and-cast.md#as-operator)</span></span> | <span data-ttu-id="5e271-151">关系和类型测试</span><span class="sxs-lookup"><span data-stu-id="5e271-151">Relational and type-testing</span></span> |
| <span data-ttu-id="5e271-152">[x == y](equality-operators.md#equality-operator-)、[x != y](equality-operators.md#inequality-operator-)</span><span class="sxs-lookup"><span data-stu-id="5e271-152">[x == y](equality-operators.md#equality-operator-), [x != y](equality-operators.md#inequality-operator-)</span></span> | <span data-ttu-id="5e271-153">相等</span><span class="sxs-lookup"><span data-stu-id="5e271-153">Equality</span></span> |
| `x & y` | <span data-ttu-id="5e271-154">[布尔逻辑 AND](boolean-logical-operators.md#logical-and-operator-) 或[按位逻辑 AND](bitwise-and-shift-operators.md#logical-and-operator-)</span><span class="sxs-lookup"><span data-stu-id="5e271-154">[Boolean logical AND](boolean-logical-operators.md#logical-and-operator-) or [bitwise logical AND](bitwise-and-shift-operators.md#logical-and-operator-)</span></span> |
| `x ^ y` | <span data-ttu-id="5e271-155">[布尔逻辑 XOR](boolean-logical-operators.md#logical-exclusive-or-operator-) 或[按位逻辑 XOR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-)</span><span class="sxs-lookup"><span data-stu-id="5e271-155">[Boolean logical XOR](boolean-logical-operators.md#logical-exclusive-or-operator-) or [bitwise logical XOR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-)</span></span> |
| <code>x &#124; y</code> | <span data-ttu-id="5e271-156">[布尔逻辑 OR](boolean-logical-operators.md#logical-or-operator-) 或[按位逻辑 OR](bitwise-and-shift-operators.md#logical-or-operator-)</span><span class="sxs-lookup"><span data-stu-id="5e271-156">[Boolean logical OR](boolean-logical-operators.md#logical-or-operator-) or [bitwise logical OR](bitwise-and-shift-operators.md#logical-or-operator-)</span></span> |
| [<span data-ttu-id="5e271-157">x && y</span><span class="sxs-lookup"><span data-stu-id="5e271-157">x && y</span></span>](boolean-logical-operators.md#conditional-logical-and-operator-) | <span data-ttu-id="5e271-158">条件“与”</span><span class="sxs-lookup"><span data-stu-id="5e271-158">Conditional AND</span></span> |
| [<span data-ttu-id="5e271-159">x &#124;&#124; y</span><span class="sxs-lookup"><span data-stu-id="5e271-159">x &#124;&#124; y</span></span>](boolean-logical-operators.md#conditional-logical-or-operator-) | <span data-ttu-id="5e271-160">条件“或”</span><span class="sxs-lookup"><span data-stu-id="5e271-160">Conditional OR</span></span> |
| [<span data-ttu-id="5e271-161">x ?? y</span><span class="sxs-lookup"><span data-stu-id="5e271-161">x ?? y</span></span>](null-coalescing-operator.md) | <span data-ttu-id="5e271-162">Null 合并运算符</span><span class="sxs-lookup"><span data-stu-id="5e271-162">Null-coalescing operator</span></span> |
| [<span data-ttu-id="5e271-163">c ? t : f</span><span class="sxs-lookup"><span data-stu-id="5e271-163">c ? t : f</span></span>](conditional-operator.md) | <span data-ttu-id="5e271-164">条件运算符</span><span class="sxs-lookup"><span data-stu-id="5e271-164">Conditional operator</span></span> |
| <span data-ttu-id="5e271-165">[x = y](assignment-operator.md)、[x += y](arithmetic-operators.md#compound-assignment)、[x -= y](arithmetic-operators.md#compound-assignment)、[x \*= y](arithmetic-operators.md#compound-assignment)、[x /= y](arithmetic-operators.md#compound-assignment)、[x %= y](arithmetic-operators.md#compound-assignment)、[x &= y](boolean-logical-operators.md#compound-assignment)、[x &#124;= y](boolean-logical-operators.md#compound-assignment)、[x ^= y](boolean-logical-operators.md#compound-assignment)、[x <<= y](bitwise-and-shift-operators.md#compound-assignment)、[x >>= y](bitwise-and-shift-operators.md#compound-assignment)、[x ??= y](null-coalescing-operator.md)、[=>](lambda-operator.md)</span><span class="sxs-lookup"><span data-stu-id="5e271-165">[x = y](assignment-operator.md), [x += y](arithmetic-operators.md#compound-assignment), [x -= y](arithmetic-operators.md#compound-assignment), [x \*= y](arithmetic-operators.md#compound-assignment), [x /= y](arithmetic-operators.md#compound-assignment), [x %= y](arithmetic-operators.md#compound-assignment), [x &= y](boolean-logical-operators.md#compound-assignment), [x &#124;= y](boolean-logical-operators.md#compound-assignment), [x ^= y](boolean-logical-operators.md#compound-assignment), [x <<= y](bitwise-and-shift-operators.md#compound-assignment), [x >>= y](bitwise-and-shift-operators.md#compound-assignment), [x ??= y](null-coalescing-operator.md), [=>](lambda-operator.md)</span></span> | <span data-ttu-id="5e271-166">赋值和 lambda 声明</span><span class="sxs-lookup"><span data-stu-id="5e271-166">Assignment and lambda declaration</span></span> |

## <a name="operator-associativity"></a><span data-ttu-id="5e271-167">运算符结合性</span><span class="sxs-lookup"><span data-stu-id="5e271-167">Operator associativity</span></span>

<span data-ttu-id="5e271-168">当运算符的优先级相同，运算符的结合性决定了运算的执行顺序：</span><span class="sxs-lookup"><span data-stu-id="5e271-168">When operators have the same precedence, associativity of the operators determines the order in which the operations are performed:</span></span>

- <span data-ttu-id="5e271-169">左结合运算符按从左到右的顺序计算。</span><span class="sxs-lookup"><span data-stu-id="5e271-169">*Left-associative* operators are evaluated in order from left to right.</span></span> <span data-ttu-id="5e271-170">除[赋值运算符](assignment-operator.md)和 [null 合并运算符](null-coalescing-operator.md)外，所有二元运算符都是左结合运算符。</span><span class="sxs-lookup"><span data-stu-id="5e271-170">Except for the [assignment operators](assignment-operator.md) and the [null-coalescing operators](null-coalescing-operator.md), all binary operators are left-associative.</span></span> <span data-ttu-id="5e271-171">例如，`a + b - c` 将计算为 `(a + b) - c`。</span><span class="sxs-lookup"><span data-stu-id="5e271-171">For example, `a + b - c` is evaluated as `(a + b) - c`.</span></span>
- <span data-ttu-id="5e271-172">右结合运算符按从右到左的顺序计算。</span><span class="sxs-lookup"><span data-stu-id="5e271-172">*Right-associative* operators are evaluated in order from right to left.</span></span> <span data-ttu-id="5e271-173">赋值运算符、null 合并运算符和[条件运算符`?:`](conditional-operator.md)是右结合运算符。</span><span class="sxs-lookup"><span data-stu-id="5e271-173">The assignment operators, the null-coalescing operators, and the [conditional operator `?:`](conditional-operator.md) are right-associative.</span></span> <span data-ttu-id="5e271-174">例如，`x = y = z` 将计算为 `x = (y = z)`。</span><span class="sxs-lookup"><span data-stu-id="5e271-174">For example, `x = y = z` is evaluated as `x = (y = z)`.</span></span>

<span data-ttu-id="5e271-175">使用括号更改运算符结合性所施加的计算顺序：</span><span class="sxs-lookup"><span data-stu-id="5e271-175">Use parentheses to change the order of evaluation imposed by operator associativity:</span></span>

```csharp-interactive
int a = 13 / 5 / 2;
int b = 13 / (5 / 2);
Console.WriteLine($"a = {a}, b = {b}");  // output: a = 1, b = 6
```

## <a name="operand-evaluation"></a><span data-ttu-id="5e271-176">操作数计算</span><span class="sxs-lookup"><span data-stu-id="5e271-176">Operand evaluation</span></span>

<span data-ttu-id="5e271-177">与运算符的优先级和结合性无关，从左到右计算表达式中的操作数。</span><span class="sxs-lookup"><span data-stu-id="5e271-177">Unrelated to operator precedence and associativity, operands in an expression are evaluated from left to right.</span></span> <span data-ttu-id="5e271-178">以下示例展示了运算符和操作数的计算顺序：</span><span class="sxs-lookup"><span data-stu-id="5e271-178">The following examples demonstrate the order in which operators and operands are evaluated:</span></span>

| <span data-ttu-id="5e271-179">表达式</span><span class="sxs-lookup"><span data-stu-id="5e271-179">Expression</span></span> | <span data-ttu-id="5e271-180">计算顺序</span><span class="sxs-lookup"><span data-stu-id="5e271-180">Order of evaluation</span></span> |
| ---------- | ------------------- |
|`a + b`|<span data-ttu-id="5e271-181">a, b, +</span><span class="sxs-lookup"><span data-stu-id="5e271-181">a, b, +</span></span>|
|`a + b * c`|<span data-ttu-id="5e271-182">a, b, c, \*, +</span><span class="sxs-lookup"><span data-stu-id="5e271-182">a, b, c, \*, +</span></span>|
|`a / b + c * d`|<span data-ttu-id="5e271-183">a, b, /, c, d, \*, +</span><span class="sxs-lookup"><span data-stu-id="5e271-183">a, b, /, c, d, \*, +</span></span>|
|`a / (b + c) * d`|<span data-ttu-id="5e271-184">a, b, c, +, /, d, \*</span><span class="sxs-lookup"><span data-stu-id="5e271-184">a, b, c, +, /, d, \*</span></span>|

<span data-ttu-id="5e271-185">通常，会计算所有运算符操作数。</span><span class="sxs-lookup"><span data-stu-id="5e271-185">Typically, all operator operands are evaluated.</span></span> <span data-ttu-id="5e271-186">但是，某些运算符有条件地计算操作数。</span><span class="sxs-lookup"><span data-stu-id="5e271-186">However, some operators evaluate operands conditionally.</span></span> <span data-ttu-id="5e271-187">也就是说，此类运算符的最左侧操作数的值定义了是否应计算其他操作数，或计算其他哪些操作数。</span><span class="sxs-lookup"><span data-stu-id="5e271-187">That is, the value of the leftmost operand of such an operator defines if (or which) other operands should be evaluated.</span></span> <span data-ttu-id="5e271-188">这些运算符有条件逻辑 [AND (`&&`)](boolean-logical-operators.md#conditional-logical-and-operator-) 和 [OR (`||`)](boolean-logical-operators.md#conditional-logical-or-operator-) 运算符、[null 合并运算符 `??` 和 `??=`](null-coalescing-operator.md)、[null 条件运算符 `?.` 和 `?[]`](member-access-operators.md#null-conditional-operators--and-) 以及[条件运算符`?:`](conditional-operator.md)。</span><span class="sxs-lookup"><span data-stu-id="5e271-188">These operators are the conditional logical [AND (`&&`)](boolean-logical-operators.md#conditional-logical-and-operator-) and [OR (`||`)](boolean-logical-operators.md#conditional-logical-or-operator-) operators, the [null-coalescing operators `??` and `??=`](null-coalescing-operator.md), the [null-conditional operators `?.` and `?[]`](member-access-operators.md#null-conditional-operators--and-), and the [conditional operator `?:`](conditional-operator.md).</span></span> <span data-ttu-id="5e271-189">有关详细信息，请参阅每个运算符的说明。</span><span class="sxs-lookup"><span data-stu-id="5e271-189">For more information, see the description of each operator.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="5e271-190">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="5e271-190">C# language specification</span></span>

<span data-ttu-id="5e271-191">有关更多信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的以下部分：</span><span class="sxs-lookup"><span data-stu-id="5e271-191">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="5e271-192">表达式</span><span class="sxs-lookup"><span data-stu-id="5e271-192">Expressions</span></span>](~/_csharplang/spec/expressions.md)
- [<span data-ttu-id="5e271-193">运算符</span><span class="sxs-lookup"><span data-stu-id="5e271-193">Operators</span></span>](~/_csharplang/spec/expressions.md#operators)

## <a name="see-also"></a><span data-ttu-id="5e271-194">请参阅</span><span class="sxs-lookup"><span data-stu-id="5e271-194">See also</span></span>

- [<span data-ttu-id="5e271-195">C# 参考</span><span class="sxs-lookup"><span data-stu-id="5e271-195">C# reference</span></span>](../index.md)
- [<span data-ttu-id="5e271-196">运算符重载</span><span class="sxs-lookup"><span data-stu-id="5e271-196">Operator overloading</span></span>](operator-overloading.md)
- [<span data-ttu-id="5e271-197">表达式树</span><span class="sxs-lookup"><span data-stu-id="5e271-197">Expression trees</span></span>](../../programming-guide/concepts/expression-trees/index.md)
