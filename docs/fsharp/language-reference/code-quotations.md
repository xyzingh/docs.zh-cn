---
title: 代码引用
description: '了解 F # 代码引用，它是一种语言功能，可用于以编程方式生成和使用 F # 代码表达式。'
ms.date: 08/13/2020
ms.openlocfilehash: dc37fdbd6cd29e5ee94e5c0186dfe2bfeb666f32
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557189"
---
# <a name="code-quotations"></a><span data-ttu-id="55998-103">代码引用</span><span class="sxs-lookup"><span data-stu-id="55998-103">Code quotations</span></span>

<span data-ttu-id="55998-104">本文介绍 *代码引用* ，它是一种语言功能，可用于以编程方式生成和使用 F # 代码表达式。</span><span class="sxs-lookup"><span data-stu-id="55998-104">This article describes *code quotations* , a language feature that enables you to generate and work with F# code expressions programmatically.</span></span> <span data-ttu-id="55998-105">利用此功能，您可以生成一个表示 F # 代码的抽象语法树。</span><span class="sxs-lookup"><span data-stu-id="55998-105">This feature lets you generate an abstract syntax tree that represents F# code.</span></span> <span data-ttu-id="55998-106">然后，可以根据应用程序的需要遍历和处理抽象语法树。</span><span class="sxs-lookup"><span data-stu-id="55998-106">The abstract syntax tree can then be traversed and processed according to the needs of your application.</span></span> <span data-ttu-id="55998-107">例如，您可以使用树生成 F # 代码或以某种其他语言生成代码。</span><span class="sxs-lookup"><span data-stu-id="55998-107">For example, you can use the tree to generate F# code or generate code in some other language.</span></span>

## <a name="quoted-expressions"></a><span data-ttu-id="55998-108">带引号的表达式</span><span class="sxs-lookup"><span data-stu-id="55998-108">Quoted Expressions</span></span>

<span data-ttu-id="55998-109">*带引号的表达式* 是代码中的 F # 表达式，它以不作为程序的一部分进行编译，而是编译为表示 F # 表达式的对象。</span><span class="sxs-lookup"><span data-stu-id="55998-109">A *quoted expression* is an F# expression in your code that is delimited in such a way that it is not compiled as part of your program, but instead is compiled into an object that represents an F# expression.</span></span> <span data-ttu-id="55998-110">可以通过以下两种方式之一来标记带引号的表达式：使用类型信息或不包含类型信息。</span><span class="sxs-lookup"><span data-stu-id="55998-110">You can mark a quoted expression in one of two ways: either with type information or without type information.</span></span> <span data-ttu-id="55998-111">如果要包括类型信息，请使用符号 `<@` 并 `@>` 分隔带引号的表达式。</span><span class="sxs-lookup"><span data-stu-id="55998-111">If you want to include type information, you use the symbols `<@` and `@>` to delimit the quoted expression.</span></span> <span data-ttu-id="55998-112">如果不需要类型信息，则使用符号 `<@@` 和 `@@>` 。</span><span class="sxs-lookup"><span data-stu-id="55998-112">If you do not need type information, you use the symbols `<@@` and `@@>`.</span></span> <span data-ttu-id="55998-113">下面的代码显示类型化和非类型化的引用。</span><span class="sxs-lookup"><span data-stu-id="55998-113">The following code shows typed and untyped quotations.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet501.fs)]

<span data-ttu-id="55998-114">如果不包含类型信息，遍历大型表达式树的速度将更快。</span><span class="sxs-lookup"><span data-stu-id="55998-114">Traversing a large expression tree is faster if you do not include type information.</span></span> <span data-ttu-id="55998-115">使用类型化符号括起来的表达式的结果类型为 `Expr<'T>` ，其中类型参数具有由 F # 编译器的类型推理算法确定的表达式的类型。</span><span class="sxs-lookup"><span data-stu-id="55998-115">The resulting type of an expression quoted with the typed symbols is `Expr<'T>`, where the type parameter has the type of the expression as determined by the F# compiler's type inference algorithm.</span></span> <span data-ttu-id="55998-116">使用不带类型信息的代码引用时，带引号的表达式的类型为非泛型类型 [Expr](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr.html)。</span><span class="sxs-lookup"><span data-stu-id="55998-116">When you use code quotations without type information, the type of the quoted expression is the non-generic type [Expr](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr.html).</span></span> <span data-ttu-id="55998-117">可以调用类型化类的 [原始](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr-1.html#Raw) 属性 `Expr` 来获取非类型化 `Expr` 对象。</span><span class="sxs-lookup"><span data-stu-id="55998-117">You can call the [Raw](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr-1.html#Raw) property on the typed `Expr` class to obtain the untyped `Expr` object.</span></span>

<span data-ttu-id="55998-118">有多种静态方法可让你以编程方式在类中生成 F # 表达式对象， `Expr` 而无需使用带引号的表达式。</span><span class="sxs-lookup"><span data-stu-id="55998-118">There are a variety of static methods that allow you to generate F# expression objects programmatically in the `Expr` class without using quoted expressions.</span></span>

<span data-ttu-id="55998-119">请注意，代码引号必须包含完整的表达式。</span><span class="sxs-lookup"><span data-stu-id="55998-119">Note that a code quotation must include a complete expression.</span></span> <span data-ttu-id="55998-120">`let`例如，对于绑定，需要绑定名称和使用绑定的其他表达式的定义。</span><span class="sxs-lookup"><span data-stu-id="55998-120">For a `let` binding, for example, you need both the definition of the bound name and an additional expression that uses the binding.</span></span> <span data-ttu-id="55998-121">在详细语法中，这是跟在关键字后面的表达式 `in` 。</span><span class="sxs-lookup"><span data-stu-id="55998-121">In verbose syntax, this is an expression that follows the `in` keyword.</span></span> <span data-ttu-id="55998-122">在模块的顶层，这只是模块中的下一个表达式，但在引号中，它是显式必需的。</span><span class="sxs-lookup"><span data-stu-id="55998-122">At the top-level in a module, this is just the next expression in the module, but in a quotation, it is explicitly required.</span></span>

<span data-ttu-id="55998-123">因此，下面的表达式无效。</span><span class="sxs-lookup"><span data-stu-id="55998-123">Therefore, the following expression is not valid.</span></span>

```fsharp
// Not valid:
// <@ let f x = x + 1 @>
```

<span data-ttu-id="55998-124">但下面的表达式是有效的。</span><span class="sxs-lookup"><span data-stu-id="55998-124">But the following expressions are valid.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet502.fs)]

<span data-ttu-id="55998-125">若要计算 F # 引号，必须使用 [f # 引号计算](https://github.com/fsprojects/FSharp.Quotations.Evaluator)器。</span><span class="sxs-lookup"><span data-stu-id="55998-125">To evaluate F# quotations, you must use the [F# Quotation Evaluator](https://github.com/fsprojects/FSharp.Quotations.Evaluator).</span></span> <span data-ttu-id="55998-126">它提供对计算和执行 F # 表达式对象的支持。</span><span class="sxs-lookup"><span data-stu-id="55998-126">It provides support for evaluating and executing F# expression objects.</span></span>

<span data-ttu-id="55998-127">F # 引号还会保留类型约束信息。</span><span class="sxs-lookup"><span data-stu-id="55998-127">F# quotations also retain type constraint information.</span></span> <span data-ttu-id="55998-128">请看下面的示例：</span><span class="sxs-lookup"><span data-stu-id="55998-128">Consider the following example:</span></span>

```fsharp
open FSharp.Linq.RuntimeHelpers

let eval q = LeafExpressionConverter.EvaluateQuotation q

let inline negate x = -x
// val inline negate: x: ^a ->  ^a when  ^a : (static member ( ~- ) :  ^a ->  ^a)

<@ negate 1.0 @>  |> eval
```

<span data-ttu-id="55998-129">函数生成的约束 `inline` 保留在代码 qutoation 中。</span><span class="sxs-lookup"><span data-stu-id="55998-129">The constraint generated by the `inline` function is retained in the code qutoation.</span></span> <span data-ttu-id="55998-130">`negate`现在可以计算该函数的 quotated 窗体。</span><span class="sxs-lookup"><span data-stu-id="55998-130">The `negate` function's quotated form can now be evaluated.</span></span>

## <a name="expr-type"></a><span data-ttu-id="55998-131">Expr 类型</span><span class="sxs-lookup"><span data-stu-id="55998-131">Expr Type</span></span>

<span data-ttu-id="55998-132">类型的实例 `Expr` 表示 F # 表达式。</span><span class="sxs-lookup"><span data-stu-id="55998-132">An instance of the `Expr` type represents an F# expression.</span></span> <span data-ttu-id="55998-133">`Expr`F # 库文档中记录了泛型和非泛型类型。</span><span class="sxs-lookup"><span data-stu-id="55998-133">Both the generic and the non-generic `Expr` types are documented in the F# library documentation.</span></span> <span data-ttu-id="55998-134">有关详细信息，请参阅 [Fsharp.core Namespace](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations.html) 和 [类](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr.html)。</span><span class="sxs-lookup"><span data-stu-id="55998-134">For more information, see [FSharp.Quotations Namespace](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations.html) and [Quotations.Expr Class](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-fsharpexpr.html).</span></span>

## <a name="splicing-operators"></a><span data-ttu-id="55998-135">拼接运算符</span><span class="sxs-lookup"><span data-stu-id="55998-135">Splicing Operators</span></span>

<span data-ttu-id="55998-136">拼接使你能够将文本代码引用与你以编程方式或从其他代码引用创建的表达式组合在一起。</span><span class="sxs-lookup"><span data-stu-id="55998-136">Splicing enables you to combine literal code quotations with expressions that you have created programmatically or from another code quotation.</span></span> <span data-ttu-id="55998-137">使用 `%` 和 `%%` 运算符可以将 F # 表达式对象添加到代码引用中。</span><span class="sxs-lookup"><span data-stu-id="55998-137">The `%` and `%%` operators enable you to add an F# expression object into a code quotation.</span></span> <span data-ttu-id="55998-138">使用运算符将 `%` 类型化表达式对象插入类型化的引用中; 使用 `%%` 运算符将非类型化的表达式对象插入非类型化的引用。</span><span class="sxs-lookup"><span data-stu-id="55998-138">You use the `%` operator to insert a typed expression object into a typed quotation; you use the `%%` operator to insert an untyped expression object into an untyped quotation.</span></span> <span data-ttu-id="55998-139">这两个运算符均为一元前缀运算符。</span><span class="sxs-lookup"><span data-stu-id="55998-139">Both operators are unary prefix operators.</span></span> <span data-ttu-id="55998-140">因此 `expr` ，如果是类型的非类型化表达式 `Expr` ，以下代码是有效的。</span><span class="sxs-lookup"><span data-stu-id="55998-140">Thus if `expr` is an untyped expression of type `Expr`, the following code is valid.</span></span>

```fsharp
<@@ 1 + %%expr @@>
```

<span data-ttu-id="55998-141">如果 `expr` 是类型的类型化的引号 `Expr<int>` ，则以下代码有效。</span><span class="sxs-lookup"><span data-stu-id="55998-141">And if `expr` is a typed quotation of type `Expr<int>`, the following code is valid.</span></span>

```fsharp
<@ 1 + %expr @>
```

## <a name="example"></a><span data-ttu-id="55998-142">示例</span><span class="sxs-lookup"><span data-stu-id="55998-142">Example</span></span>

### <a name="description"></a><span data-ttu-id="55998-143">说明</span><span class="sxs-lookup"><span data-stu-id="55998-143">Description</span></span>

<span data-ttu-id="55998-144">下面的示例演示如何使用代码引用将 F # 代码放入 expression 对象，然后打印表示该表达式的 F # 代码。</span><span class="sxs-lookup"><span data-stu-id="55998-144">The following example illustrates the use of code quotations to put F# code into an expression object and then print the F# code that represents the expression.</span></span> <span data-ttu-id="55998-145">定义了一个函数， `println` 该函数包含一个递归函数 `print` ，该函数 `Expr` 以友好格式显示类型)  (的 F # 表达式对象。</span><span class="sxs-lookup"><span data-stu-id="55998-145">A function `println` is defined that contains a recursive function `print` that displays an F# expression object (of type `Expr`) in a friendly format.</span></span> <span data-ttu-id="55998-146">[Fsharp.core](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-patternsmodule.html)和[fsharp.core DerivedPatterns](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-derivedpatternsmodule.html)模块中有几个活动模式，可用于分析表达式对象。</span><span class="sxs-lookup"><span data-stu-id="55998-146">There are several active patterns in the [FSharp.Quotations.Patterns](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-patternsmodule.html) and [FSharp.Quotations.DerivedPatterns](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-derivedpatternsmodule.html) modules that can be used to analyze expression objects.</span></span> <span data-ttu-id="55998-147">此示例不包括可能出现在 F # 表达式中的所有可能的模式。</span><span class="sxs-lookup"><span data-stu-id="55998-147">This example does not include all the possible patterns that might appear in an F# expression.</span></span> <span data-ttu-id="55998-148">任何无法识别的模式都会触发与通配符模式的匹配 (`_`) 并使用方法呈现，该 `ToString` 方法在类型上， `Expr` 使你知道要添加到匹配表达式的活动模式。</span><span class="sxs-lookup"><span data-stu-id="55998-148">Any unrecognized pattern triggers a match to the wildcard pattern (`_`) and is rendered by using the `ToString` method, which, on the `Expr` type, lets you know the active pattern to add to your match expression.</span></span>

### <a name="code"></a><span data-ttu-id="55998-149">代码</span><span class="sxs-lookup"><span data-stu-id="55998-149">Code</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet601.fs)]

### <a name="output"></a><span data-ttu-id="55998-150">输出</span><span class="sxs-lookup"><span data-stu-id="55998-150">Output</span></span>

```fsharp
fun (x:System.Int32) -> x + 1
a + 1
let f = fun (x:System.Int32) -> x + 10 in f 10
```

## <a name="example"></a><span data-ttu-id="55998-151">示例</span><span class="sxs-lookup"><span data-stu-id="55998-151">Example</span></span>

### <a name="description"></a><span data-ttu-id="55998-152">说明</span><span class="sxs-lookup"><span data-stu-id="55998-152">Description</span></span>

<span data-ttu-id="55998-153">您还可以使用 [exprshape.rebuildshapecombination 模块](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-exprshapemodule.html) 中的三个活动模式来遍历具有较少活动模式的表达式树。</span><span class="sxs-lookup"><span data-stu-id="55998-153">You can also use the three active patterns in the [ExprShape module](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-exprshapemodule.html) to traverse expression trees with fewer active patterns.</span></span> <span data-ttu-id="55998-154">当你希望遍历树但你不需要大多数节点中的所有信息时，这些活动模式会很有用。</span><span class="sxs-lookup"><span data-stu-id="55998-154">These active patterns can be useful when you want to traverse a tree but you do not need all the information in most of the nodes.</span></span> <span data-ttu-id="55998-155">当使用这些模式时，任何 F # 表达式都将与以下三种模式之一匹配： `ShapeVar` 如果表达式是变量，则为; 如果表达式 `ShapeLambda` 是 lambda 表达式，则为; 如果 `ShapeCombination` 表达式为其他任何内容，则为。</span><span class="sxs-lookup"><span data-stu-id="55998-155">When you use these patterns, any F# expression matches one of the following three patterns: `ShapeVar` if the expression is a variable, `ShapeLambda` if the expression is a lambda expression, or `ShapeCombination` if the expression is anything else.</span></span> <span data-ttu-id="55998-156">如果使用活动模式遍历表达式树，如前面的代码示例所示，您必须使用更多的模式来处理所有可能的 F # 表达式类型，并且您的代码将更复杂。</span><span class="sxs-lookup"><span data-stu-id="55998-156">If you traverse an expression tree by using the active patterns as in the previous code example, you have to use many more patterns to handle all possible F# expression types, and your code will be more complex.</span></span> <span data-ttu-id="55998-157">有关详细信息，请参阅 [exprshape.rebuildshapecombination. ShapeVar&#124;ShapeLambda&#124;ShapeCombination Active Pattern](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-exprshapemodule.html#(%20|ShapeVar|ShapeLambda|ShapeCombination|%20))。</span><span class="sxs-lookup"><span data-stu-id="55998-157">For more information, see [ExprShape.ShapeVar&#124;ShapeLambda&#124;ShapeCombination Active Pattern](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-exprshapemodule.html#(%20|ShapeVar|ShapeLambda|ShapeCombination|%20)).</span></span>

<span data-ttu-id="55998-158">下面的代码示例可用作更复杂的遍历的基础。</span><span class="sxs-lookup"><span data-stu-id="55998-158">The following code example can be used as a basis for more complex traversals.</span></span> <span data-ttu-id="55998-159">在此代码中，将为包含函数调用的表达式创建表达式树 `add` 。</span><span class="sxs-lookup"><span data-stu-id="55998-159">In this code, an expression tree is created for an expression that involves a function call, `add`.</span></span> <span data-ttu-id="55998-160">[SpecificCall](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-derivedpatternsmodule.html#(%20|SpecificCall|_|%20))活动模式用于检测对 `add` 表达式树中的任何调用。</span><span class="sxs-lookup"><span data-stu-id="55998-160">The [SpecificCall](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-quotations-derivedpatternsmodule.html#(%20|SpecificCall|_|%20)) active pattern is used to detect any call to `add` in the expression tree.</span></span> <span data-ttu-id="55998-161">此活动模式将调用的参数分配给 `exprList` 值。</span><span class="sxs-lookup"><span data-stu-id="55998-161">This active pattern assigns the arguments of the call to the `exprList` value.</span></span> <span data-ttu-id="55998-162">在这种情况下，只有两个，因此会将其拉出，并以递归方式对参数调用函数。</span><span class="sxs-lookup"><span data-stu-id="55998-162">In this case, there are only two, so these are pulled out and the function is called recursively on the arguments.</span></span> <span data-ttu-id="55998-163">`mul`通过使用接合运算符 () ，将结果插入到表示对的调用 `%%` 。</span><span class="sxs-lookup"><span data-stu-id="55998-163">The results are inserted into a code quotation that represents a call to `mul` by using the splice operator (`%%`).</span></span> <span data-ttu-id="55998-164">`println`上一示例中的函数用于显示结果。</span><span class="sxs-lookup"><span data-stu-id="55998-164">The `println` function from the previous example is used to display the results.</span></span>

<span data-ttu-id="55998-165">其他活动模式分支中的代码只是重新生成相同的表达式树，因此，结果表达式中的唯一更改是从到的更改 `add` `mul` 。</span><span class="sxs-lookup"><span data-stu-id="55998-165">The code in the other active pattern branches just regenerates the same expression tree, so the only change in the resulting expression is the change from `add` to `mul`.</span></span>

### <a name="code"></a><span data-ttu-id="55998-166">代码</span><span class="sxs-lookup"><span data-stu-id="55998-166">Code</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet701.fs)]

### <a name="output"></a><span data-ttu-id="55998-167">Output</span><span class="sxs-lookup"><span data-stu-id="55998-167">Output</span></span>

```fsharp
1 + Module1.add(2,Module1.add(3,4))
1 + Module1.mul(2,Module1.mul(3,4))
```

## <a name="see-also"></a><span data-ttu-id="55998-168">请参阅</span><span class="sxs-lookup"><span data-stu-id="55998-168">See also</span></span>

- [<span data-ttu-id="55998-169">F# 语言参考</span><span class="sxs-lookup"><span data-stu-id="55998-169">F# Language Reference</span></span>](index.md)
