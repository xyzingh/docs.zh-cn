---
title: 本地函数 - C# 编程指南
description: C# 中的本地函数是嵌套在另一成员中并且可以从其包含成员中调用的私有方法。
ms.date: 10/09/2020
helpviewer_keywords:
- local functions [C#]
ms.openlocfilehash: a2d389c8b1c687dc4885004fcdc33e0ed7ada977
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955676"
---
# <a name="local-functions-c-programming-guide"></a><span data-ttu-id="f35a9-103">本地函数（C# 编程指南）</span><span class="sxs-lookup"><span data-stu-id="f35a9-103">Local functions (C# Programming Guide)</span></span>

<span data-ttu-id="f35a9-104">从 C# 7.0 开始，C# *支持本地函数*。</span><span class="sxs-lookup"><span data-stu-id="f35a9-104">Starting with C# 7.0, C# supports *local functions*.</span></span> <span data-ttu-id="f35a9-105">本地函数是一种嵌套在另一成员中的类型的私有方法。</span><span class="sxs-lookup"><span data-stu-id="f35a9-105">Local functions are private methods of a type that are nested in another member.</span></span> <span data-ttu-id="f35a9-106">仅能从其包含成员中调用它们。</span><span class="sxs-lookup"><span data-stu-id="f35a9-106">They can only be called from their containing member.</span></span> <span data-ttu-id="f35a9-107">可以在以下位置中声明和调用本地函数：</span><span class="sxs-lookup"><span data-stu-id="f35a9-107">Local functions can be declared in and called from:</span></span>

- <span data-ttu-id="f35a9-108">方法（尤其是迭代器方法和异步方法）</span><span class="sxs-lookup"><span data-stu-id="f35a9-108">Methods, especially iterator methods and async methods</span></span>
- <span data-ttu-id="f35a9-109">构造函数</span><span class="sxs-lookup"><span data-stu-id="f35a9-109">Constructors</span></span>
- <span data-ttu-id="f35a9-110">属性访问器</span><span class="sxs-lookup"><span data-stu-id="f35a9-110">Property accessors</span></span>
- <span data-ttu-id="f35a9-111">事件访问器</span><span class="sxs-lookup"><span data-stu-id="f35a9-111">Event accessors</span></span>
- <span data-ttu-id="f35a9-112">匿名方法</span><span class="sxs-lookup"><span data-stu-id="f35a9-112">Anonymous methods</span></span>
- <span data-ttu-id="f35a9-113">Lambda 表达式</span><span class="sxs-lookup"><span data-stu-id="f35a9-113">Lambda expressions</span></span>
- <span data-ttu-id="f35a9-114">终结器</span><span class="sxs-lookup"><span data-stu-id="f35a9-114">Finalizers</span></span>
- <span data-ttu-id="f35a9-115">其他本地函数</span><span class="sxs-lookup"><span data-stu-id="f35a9-115">Other local functions</span></span>

<span data-ttu-id="f35a9-116">但是，不能在 expression-bodied 成员中声明本地函数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-116">However, local functions can't be declared inside an expression-bodied member.</span></span>

> [!NOTE]
> <span data-ttu-id="f35a9-117">在某些情况下，可以使用 lambda 表达式实现本地函数也支持的功能。</span><span class="sxs-lookup"><span data-stu-id="f35a9-117">In some cases, you can use a lambda expression to implement functionality also supported by a local function.</span></span> <span data-ttu-id="f35a9-118">有关比较，请参阅[本地函数与 lambda 表达式](#local-functions-vs-lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="f35a9-118">For a comparison, see [Local functions vs. lambda expressions](#local-functions-vs-lambda-expressions).</span></span>

<span data-ttu-id="f35a9-119">本地函数可使代码意图明确。</span><span class="sxs-lookup"><span data-stu-id="f35a9-119">Local functions make the intent of your code clear.</span></span> <span data-ttu-id="f35a9-120">任何读取代码的人都可以看到，此方法不可调用，包含方法除外。</span><span class="sxs-lookup"><span data-stu-id="f35a9-120">Anyone reading your code can see that the method is not callable except by the containing method.</span></span> <span data-ttu-id="f35a9-121">对于团队项目，它们也使得其他开发人员无法直接从类或结构中的其他位置错误调用此方法。</span><span class="sxs-lookup"><span data-stu-id="f35a9-121">For team projects, they also make it impossible for another developer to mistakenly call the method directly from elsewhere in the class or struct.</span></span>

## <a name="local-function-syntax"></a><span data-ttu-id="f35a9-122">本地函数语法</span><span class="sxs-lookup"><span data-stu-id="f35a9-122">Local function syntax</span></span>

<span data-ttu-id="f35a9-123">本地函数被定义为包含成员中的嵌套方法。</span><span class="sxs-lookup"><span data-stu-id="f35a9-123">A local function is defined as a nested method inside a containing member.</span></span> <span data-ttu-id="f35a9-124">其定义具有以下语法：</span><span class="sxs-lookup"><span data-stu-id="f35a9-124">Its definition has the following syntax:</span></span>

```csharp
<modifiers> <return-type> <method-name> <parameter-list>
```

<span data-ttu-id="f35a9-125">可以将以下修饰符用于本地函数：</span><span class="sxs-lookup"><span data-stu-id="f35a9-125">You can use the following modifiers with a local function:</span></span>

- [`async`](../../language-reference/keywords/async.md)
- [`unsafe`](../../language-reference/keywords/unsafe.md)
- <span data-ttu-id="f35a9-126">[`static`](../../language-reference/keywords/static.md)（在 C# 8.0 和更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="f35a9-126">[`static`](../../language-reference/keywords/static.md) (in C# 8.0 and later).</span></span> <span data-ttu-id="f35a9-127">静态本地函数无法捕获局部变量或实例状态。</span><span class="sxs-lookup"><span data-stu-id="f35a9-127">A static local function can't capture local variables or instance state.</span></span>
- <span data-ttu-id="f35a9-128">[`extern`](../../language-reference/keywords/extern.md)（在 C# 9.0 和更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="f35a9-128">[`extern`](../../language-reference/keywords/extern.md) (in C# 9.0 and later).</span></span> <span data-ttu-id="f35a9-129">外部本地函数必须为 `static`。</span><span class="sxs-lookup"><span data-stu-id="f35a9-129">An external local function must be `static`.</span></span>

<span data-ttu-id="f35a9-130">在包含成员中定义的所有本地变量（包括其方法参数）都可在非静态本地函数中访问。</span><span class="sxs-lookup"><span data-stu-id="f35a9-130">All local variables that are defined in the containing member, including its method parameters, are accessible in a non-static local function.</span></span>

<span data-ttu-id="f35a9-131">与方法定义不同，本地函数定义不能包含成员访问修饰符。</span><span class="sxs-lookup"><span data-stu-id="f35a9-131">Unlike a method definition, a local function definition cannot include the member access modifier.</span></span> <span data-ttu-id="f35a9-132">因为所有本地函数都是私有的，包括访问修饰符（如 `private` 关键字）会生成编译器错误 CS0106“修饰符‘private’对于此项无效”。</span><span class="sxs-lookup"><span data-stu-id="f35a9-132">Because all local functions are private, including an access modifier, such as the `private` keyword, generates compiler error CS0106, "The modifier 'private' is not valid for this item."</span></span>

<span data-ttu-id="f35a9-133">以下示例定义了一个名为 `AppendPathSeparator` 的本地函数，该函数对于名为 `GetText` 的方法是私有的：</span><span class="sxs-lookup"><span data-stu-id="f35a9-133">The following example defines a local function named `AppendPathSeparator` that is private to a method named `GetText`:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="Basic" :::

<span data-ttu-id="f35a9-134">从 C# 9.0 开始，你可以将属性应用于本地函数、其参数和类型参数，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f35a9-134">Beginning with C# 9.0, you can apply attributes to a local function, its parameters and type parameters, as the following example shows:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="WithAttributes" :::

<span data-ttu-id="f35a9-135">前面的示例使用[特殊属性](../../language-reference/attributes/nullable-analysis.md)来帮助编译器在可为空的上下文中进行静态分析。</span><span class="sxs-lookup"><span data-stu-id="f35a9-135">The preceding example uses a [special attribute](../../language-reference/attributes/nullable-analysis.md) to assist the compiler in static analysis in a nullable context.</span></span>

## <a name="local-functions-and-exceptions"></a><span data-ttu-id="f35a9-136">本地函数和异常</span><span class="sxs-lookup"><span data-stu-id="f35a9-136">Local functions and exceptions</span></span>

<span data-ttu-id="f35a9-137">本地函数的一个实用功能是可以允许立即显示异常。</span><span class="sxs-lookup"><span data-stu-id="f35a9-137">One of the useful features of local functions is that they can allow exceptions to surface immediately.</span></span> <span data-ttu-id="f35a9-138">对于方法迭代器，仅在枚举返回的序列时才显示异常，而非在检索迭代器时。</span><span class="sxs-lookup"><span data-stu-id="f35a9-138">For method iterators, exceptions are surfaced only when the returned sequence is enumerated, and not when the iterator is retrieved.</span></span> <span data-ttu-id="f35a9-139">对于异步方法，在等待返回的任务时，将观察到异步方法中引发的任何异常。</span><span class="sxs-lookup"><span data-stu-id="f35a9-139">For async methods, any exceptions thrown in an async method are observed when the returned task is awaited.</span></span>

<span data-ttu-id="f35a9-140">以下示例定义 `OddSequence` 方法，用于枚举指定范围中的奇数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-140">The following example defines an `OddSequence` method that enumerates odd numbers in a specified range.</span></span> <span data-ttu-id="f35a9-141">因为它会将一个大于 100 的数字传递到 `OddSequence` 迭代器方法，该方法将引发 <xref:System.ArgumentOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="f35a9-141">Because it passes a number greater than 100 to the `OddSequence` enumerator method, the method throws an <xref:System.ArgumentOutOfRangeException>.</span></span> <span data-ttu-id="f35a9-142">如示例中的输出所示，仅当循环访问数字时才显示异常，而非检索迭代器时。</span><span class="sxs-lookup"><span data-stu-id="f35a9-142">As the output from the example shows, the exception surfaces only when you iterate the numbers, and not when you retrieve the enumerator.</span></span>

:::code language="csharp" source="snippets/local-functions/IteratorWithoutLocal.cs" :::

<span data-ttu-id="f35a9-143">如果将迭代器逻辑放入本地函数，则在检索枚举器时会引发参数验证异常，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="f35a9-143">If you put iterator logic into a local function, argument validation exceptions are thrown when you retrieve the enumerator, as the following example shows:</span></span>

:::code language="csharp" source="snippets/local-functions/IteratorWithLocal.cs" :::

<span data-ttu-id="f35a9-144">你可以通过类似于异步操作的方式来使用本地函数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-144">You can use local functions in a similar way with asynchronous operations.</span></span> <span data-ttu-id="f35a9-145">等待相应的任务时，异步方法图面中引发的异常。</span><span class="sxs-lookup"><span data-stu-id="f35a9-145">Exceptions thrown in an async method surface when the corresponding task is awaited.</span></span> <span data-ttu-id="f35a9-146">本地函数允许代码快速失败，并允许同步引发和观察异常。</span><span class="sxs-lookup"><span data-stu-id="f35a9-146">Local functions allow your code to fail fast and allow your exception to be both thrown and observed synchronously.</span></span>

<span data-ttu-id="f35a9-147">以下示例使用名为 `GetMultipleAsync` 的异步方法暂停指定的秒数并返回一个值，该值是该秒数的任意倍数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-147">The following example uses an asynchronous method named `GetMultipleAsync` to pause for a specified number of seconds and return a value that is a random multiple of that number of seconds.</span></span> <span data-ttu-id="f35a9-148">最大延迟为 5 秒；如果该值大于 5，则结果为 <xref:System.ArgumentOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="f35a9-148">The maximum delay is 5 seconds; an <xref:System.ArgumentOutOfRangeException> results if the value is greater than 5.</span></span> <span data-ttu-id="f35a9-149">如下面的示例所示，仅当任务处于等待状态时，才会观察到将值 6 传递到 `GetMultipleAsync` 方法时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="f35a9-149">As the following example shows, the exception that is thrown when a value of 6 is passed to the `GetMultipleAsync` method is observed only when the task is awaited.</span></span>

:::code language="csharp" source="snippets/local-functions/AsyncWithoutLocal.cs" :::

<span data-ttu-id="f35a9-150">与方法迭代器类似，你可以重构前面的示例，将异步操作的代码放入本地函数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-150">Like with the method iterator, you can refactor the preceding example and put the code of asynchronous operation in a local function.</span></span> <span data-ttu-id="f35a9-151">如以下示例中的输出所示，调用 `GetMultiple` 方法后，会引发 <xref:System.ArgumentOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="f35a9-151">As the output from the following example shows, the <xref:System.ArgumentOutOfRangeException> is thrown as soon as the `GetMultiple` method is called.</span></span>

:::code language="csharp" source="snippets/local-functions/AsyncWithLocal.cs" :::

## <a name="local-functions-vs-lambda-expressions"></a><span data-ttu-id="f35a9-152">本地函数与 Lambda 表达式</span><span class="sxs-lookup"><span data-stu-id="f35a9-152">Local functions vs. lambda expressions</span></span>

<span data-ttu-id="f35a9-153">乍看之下，本地函数和 [lambda 表达式](../../language-reference/operators/lambda-expressions.md)非常相似。</span><span class="sxs-lookup"><span data-stu-id="f35a9-153">At first glance, local functions and [lambda expressions](../../language-reference/operators/lambda-expressions.md) are very similar.</span></span> <span data-ttu-id="f35a9-154">在许多情况下，选择使用 Lambda 表达式还是本地函数是风格和个人偏好的问题。</span><span class="sxs-lookup"><span data-stu-id="f35a9-154">In many cases, the choice between using lambda expressions and local functions is a matter of style and personal preference.</span></span> <span data-ttu-id="f35a9-155">但是，应该注意，从两者中选用一种的时机和条件其实是存在差别的。</span><span class="sxs-lookup"><span data-stu-id="f35a9-155">However, there are real differences in where you can use one or the other that you should be aware of.</span></span>

<span data-ttu-id="f35a9-156">让我们检查一下阶乘算法的本地函数实现和 lambda 表达式实现之间的差异。</span><span class="sxs-lookup"><span data-stu-id="f35a9-156">Let's examine the differences between the local function and lambda expression implementations of the factorial algorithm.</span></span> <span data-ttu-id="f35a9-157">首先使用本地函数的版本：</span><span class="sxs-lookup"><span data-stu-id="f35a9-157">First the version using a local function:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="FactorialWithLocal" :::

<span data-ttu-id="f35a9-158">将该实现与使用 Lambda 表达式的版本对比：</span><span class="sxs-lookup"><span data-stu-id="f35a9-158">Contrast that implementation with a version that uses lambda expressions:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="FactorialWithLambda" :::

<span data-ttu-id="f35a9-159">本地函数具有名称。</span><span class="sxs-lookup"><span data-stu-id="f35a9-159">The local functions have names.</span></span> <span data-ttu-id="f35a9-160">Lambda 表达式是赋给 `Func` 或 `Action` 类型变量的匿名方法。</span><span class="sxs-lookup"><span data-stu-id="f35a9-160">The lambda expressions are anonymous methods that are assigned to variables that are `Func` or `Action` types.</span></span> <span data-ttu-id="f35a9-161">在声明本地函数时，参数类型和返回类型是函数声明的一部分。</span><span class="sxs-lookup"><span data-stu-id="f35a9-161">When you declare a local function, the argument types and return type are part of the function declaration.</span></span> <span data-ttu-id="f35a9-162">参数类型和返回类型不是 Lambda 表达式主体的一部分，而是 Lambda 表达式变量类型声明的一部分。</span><span class="sxs-lookup"><span data-stu-id="f35a9-162">Instead of being part of the body of the lambda expression, the argument types and return type are part of the lambda expression's variable type declaration.</span></span> <span data-ttu-id="f35a9-163">这两种差别可以产生跟清楚的代码。</span><span class="sxs-lookup"><span data-stu-id="f35a9-163">Those two differences may result in clearer code.</span></span>

<span data-ttu-id="f35a9-164">本地函数的明确赋值规则与 Lambda 表达式的不同。</span><span class="sxs-lookup"><span data-stu-id="f35a9-164">Local functions have different rules for definite assignment than lambda expressions.</span></span> <span data-ttu-id="f35a9-165">从范围内的任意代码位置都可以引用本地函数声明。</span><span class="sxs-lookup"><span data-stu-id="f35a9-165">A local function declaration can be referenced from any code location where it is in scope.</span></span> <span data-ttu-id="f35a9-166">在可以访问（或通过引用 Lambda 表达式的委托调用）Lambda 表达式之前，必须先将 Lambda 表达式赋给委托变量。</span><span class="sxs-lookup"><span data-stu-id="f35a9-166">A lambda expression must be assigned to a delegate variable before it can be accessed (or called through the delegate referencing the lambda expression).</span></span> <span data-ttu-id="f35a9-167">请注意，使用 lambda 表达式的版本必须先定义 lambda 表达式 `nthFactorial`，然后再对其进行声明并实例化。</span><span class="sxs-lookup"><span data-stu-id="f35a9-167">Notice that the version using the lambda expression must declare and initialize the lambda expression `nthFactorial` before defining it.</span></span> <span data-ttu-id="f35a9-168">否则，会导致分配前引用 `nthFactorial` 时出现编译时错误。</span><span class="sxs-lookup"><span data-stu-id="f35a9-168">Not doing so results in a compile time error for referencing `nthFactorial` before assigning it.</span></span> <span data-ttu-id="f35a9-169">这些区别意味着使用本地函数创建递归算法会更轻松。</span><span class="sxs-lookup"><span data-stu-id="f35a9-169">These differences mean that recursive algorithms are easier to create using local functions.</span></span> <span data-ttu-id="f35a9-170">你可以声明和定义一个调用自身的本地函数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-170">You can declare and define a local function that calls itself.</span></span> <span data-ttu-id="f35a9-171">必须声明 Lambda 表达式，赋给默认值，然后才能将其重新赋给引用相同 Lambda 表达式的主体。</span><span class="sxs-lookup"><span data-stu-id="f35a9-171">Lambda expressions must be declared, and assigned a default value before they can be re-assigned to a body that references the same lambda expression.</span></span>

<span data-ttu-id="f35a9-172">明确分配规则也会影响本地函数或 Lambda 表达式捕获的任何变量。</span><span class="sxs-lookup"><span data-stu-id="f35a9-172">Definite assignment rules also affect any variables that are captured by the local function or lambda expression.</span></span> <span data-ttu-id="f35a9-173">本地函数和 Lambda 表达式规则都要求在将本地函数或 Lambda 表达式转换为委托时，明确分配任何捕获的变量。</span><span class="sxs-lookup"><span data-stu-id="f35a9-173">Both local functions and lambda expression rules demand that any captured variables are definitely assigned at the point when the local function or lambda expression is converted to a delegate.</span></span> <span data-ttu-id="f35a9-174">区别在于 Lambda 表达式在声明时转换为委托。</span><span class="sxs-lookup"><span data-stu-id="f35a9-174">The difference is that lambda expressions are converted to delegates when they are declared.</span></span> <span data-ttu-id="f35a9-175">只有在用作委托时，本地函数才转换为委托。</span><span class="sxs-lookup"><span data-stu-id="f35a9-175">Local functions are converted to delegates only when used as a delegate.</span></span> <span data-ttu-id="f35a9-176">如果声明了本地函数，但只是通过像调用方法一样调用该函数来引用该函数，它将不会转换成委托。</span><span class="sxs-lookup"><span data-stu-id="f35a9-176">If you declare a local function and only reference it by calling it like a method, it will not be converted to a delegate.</span></span> <span data-ttu-id="f35a9-177">使用该规则可在封闭范围内的任何方便的位置声明本地函数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-177">That rule enables you to declare a local function at any convenient location in its enclosing scope.</span></span> <span data-ttu-id="f35a9-178">声明本地函数的位置常见于父方法的末尾和返回任何语句后方。</span><span class="sxs-lookup"><span data-stu-id="f35a9-178">It's common to declare local functions at the end of the parent method, after any return statements.</span></span>

<span data-ttu-id="f35a9-179">第三，编译器可以执行静态分析，因此本地函数能够在封闭范围内明确分配捕获的变量。</span><span class="sxs-lookup"><span data-stu-id="f35a9-179">Third, the compiler can perform static analysis that enables local functions to definitely assign captured variables in the enclosing scope.</span></span> <span data-ttu-id="f35a9-180">请看以下示例：</span><span class="sxs-lookup"><span data-stu-id="f35a9-180">Consider this example:</span></span>

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

<span data-ttu-id="f35a9-181">编译器可以确定 `LocalFunction` 在调用时明确分配 `y`。</span><span class="sxs-lookup"><span data-stu-id="f35a9-181">The compiler can determine that `LocalFunction` definitely assigns `y` when called.</span></span> <span data-ttu-id="f35a9-182">因为在 `return` 语句之前调用了 `LocalFunction`，所以在 `return` 语句中明确分配了 `y`。</span><span class="sxs-lookup"><span data-stu-id="f35a9-182">Because `LocalFunction` is called before the `return` statement, `y` is definitely assigned at the `return` statement.</span></span>

<span data-ttu-id="f35a9-183">可实现示例分析的分析允许第四个差异。</span><span class="sxs-lookup"><span data-stu-id="f35a9-183">The analysis that enables the example analysis enables the fourth difference.</span></span> <span data-ttu-id="f35a9-184">根据它们的用途，本地函数可以避免 Lambda 表达式始终需要的堆分配。</span><span class="sxs-lookup"><span data-stu-id="f35a9-184">Depending on their use, local functions can avoid heap allocations that are always necessary for lambda expressions.</span></span> <span data-ttu-id="f35a9-185">如果本地函数永远不会转换为委托，并且本地函数捕获的变量都不会被其他转换为委托的 lambda 或本地函数捕获，则编译器可以避免堆分配。</span><span class="sxs-lookup"><span data-stu-id="f35a9-185">If a local function is never converted to a delegate, and none of the variables captured by the local function is captured by other lambdas or local functions that are converted to delegates, the compiler can avoid heap allocations.</span></span>

<span data-ttu-id="f35a9-186">请看以下异步示例：</span><span class="sxs-lookup"><span data-stu-id="f35a9-186">Consider this async example:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="AsyncWithLambda" :::

<span data-ttu-id="f35a9-187">该 lambda 表达式的闭包包含 `address`、`index` 和 `name` 变量。</span><span class="sxs-lookup"><span data-stu-id="f35a9-187">The closure for this lambda expression contains the `address`, `index` and `name` variables.</span></span> <span data-ttu-id="f35a9-188">就本地函数而言，实现闭包的对象可能为 `struct` 类型。</span><span class="sxs-lookup"><span data-stu-id="f35a9-188">In the case of local functions, the object that implements the closure may be a `struct` type.</span></span> <span data-ttu-id="f35a9-189">该结构类型将通过引用传递给本地函数。</span><span class="sxs-lookup"><span data-stu-id="f35a9-189">That struct type would be passed by reference to the local function.</span></span> <span data-ttu-id="f35a9-190">实现中的这个差异将保存在分配上。</span><span class="sxs-lookup"><span data-stu-id="f35a9-190">This difference in implementation would save on an allocation.</span></span>

<span data-ttu-id="f35a9-191">Lambda 表达式所需的实例化意味着额外的内存分配，后者可能是时间关键代码路径中的性能因素。</span><span class="sxs-lookup"><span data-stu-id="f35a9-191">The instantiation necessary for lambda expressions means extra memory allocations, which may be a performance factor in time-critical code paths.</span></span> <span data-ttu-id="f35a9-192">本地函数不会产生这种开销。</span><span class="sxs-lookup"><span data-stu-id="f35a9-192">Local functions do not incur this overhead.</span></span> <span data-ttu-id="f35a9-193">在以上示例中，本地函数版本具有的分配比 Lambda 表达式版本少 2 个。</span><span class="sxs-lookup"><span data-stu-id="f35a9-193">In the example above, the local functions version has two fewer allocations than the lambda expression version.</span></span>

> [!NOTE]
> <span data-ttu-id="f35a9-194">等效于此方法的本地函数还将类用于闭包。</span><span class="sxs-lookup"><span data-stu-id="f35a9-194">The local function equivalent of this method also uses a class for the closure.</span></span> <span data-ttu-id="f35a9-195">实现详细信息包括本地函数的闭包是作为 `class` 还是 `struct` 实现。</span><span class="sxs-lookup"><span data-stu-id="f35a9-195">Whether the closure for a local function is implemented as a `class` or a `struct` is an implementation detail.</span></span> <span data-ttu-id="f35a9-196">本地函数可能使用 `struct`，而 lambda 将始终使用 `class`。</span><span class="sxs-lookup"><span data-stu-id="f35a9-196">A local function may use a `struct` whereas a lambda will always use a `class`.</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="AsyncWithLocal" :::

<span data-ttu-id="f35a9-197">在本示例中尚未演示的最后一个优点是，可将本地函数作为迭代器实现，使用 `yield return` 语法生成一系列值。</span><span class="sxs-lookup"><span data-stu-id="f35a9-197">One final advantage not demonstrated in this sample is that local functions can be implemented as iterators, using the `yield return` syntax to produce a sequence of values.</span></span> <span data-ttu-id="f35a9-198">Lambda 表达式中不允许使用 `yield return` 语句。</span><span class="sxs-lookup"><span data-stu-id="f35a9-198">The `yield return` statement is not allowed in lambda expressions.</span></span>

<span data-ttu-id="f35a9-199">虽然本地函数对 lambda 表达式可能有点冗余，但实际上它们的目的和用法都不一样。</span><span class="sxs-lookup"><span data-stu-id="f35a9-199">While local functions may seem redundant to lambda expressions, they actually serve different purposes and have different uses.</span></span> <span data-ttu-id="f35a9-200">如果想要编写仅从上下文或其他方法中调用的函数，则使用本地函数更高效。</span><span class="sxs-lookup"><span data-stu-id="f35a9-200">Local functions are more efficient for the case when you want to write a function that is called only from the context of another method.</span></span>

## <a name="see-also"></a><span data-ttu-id="f35a9-201">请参阅</span><span class="sxs-lookup"><span data-stu-id="f35a9-201">See also</span></span>

- [<span data-ttu-id="f35a9-202">方法</span><span class="sxs-lookup"><span data-stu-id="f35a9-202">Methods</span></span>](methods.md)
