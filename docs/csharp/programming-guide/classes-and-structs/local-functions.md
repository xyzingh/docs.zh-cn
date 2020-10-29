---
title: 本地函数 - C# 编程指南
description: C# 中的本地函数是嵌套在另一成员中并且可以从其包含成员中调用的私有方法。
ms.date: 10/16/2020
helpviewer_keywords:
- local functions [C#]
ms.openlocfilehash: 75accda2e40443073274ece4d8964c13a0945dad
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92332895"
---
# <a name="local-functions-c-programming-guide"></a><span data-ttu-id="61320-103">本地函数（C# 编程指南）</span><span class="sxs-lookup"><span data-stu-id="61320-103">Local functions (C# Programming Guide)</span></span>

<span data-ttu-id="61320-104">从 C# 7.0 开始，C# *支持本地函数* 。</span><span class="sxs-lookup"><span data-stu-id="61320-104">Starting with C# 7.0, C# supports *local functions* .</span></span> <span data-ttu-id="61320-105">本地函数是一种嵌套在另一成员中的类型的私有方法。</span><span class="sxs-lookup"><span data-stu-id="61320-105">Local functions are private methods of a type that are nested in another member.</span></span> <span data-ttu-id="61320-106">仅能从其包含成员中调用它们。</span><span class="sxs-lookup"><span data-stu-id="61320-106">They can only be called from their containing member.</span></span> <span data-ttu-id="61320-107">可以在以下位置中声明和调用本地函数：</span><span class="sxs-lookup"><span data-stu-id="61320-107">Local functions can be declared in and called from:</span></span>

- <span data-ttu-id="61320-108">方法（尤其是迭代器方法和异步方法）</span><span class="sxs-lookup"><span data-stu-id="61320-108">Methods, especially iterator methods and async methods</span></span>
- <span data-ttu-id="61320-109">构造函数</span><span class="sxs-lookup"><span data-stu-id="61320-109">Constructors</span></span>
- <span data-ttu-id="61320-110">属性访问器</span><span class="sxs-lookup"><span data-stu-id="61320-110">Property accessors</span></span>
- <span data-ttu-id="61320-111">事件访问器</span><span class="sxs-lookup"><span data-stu-id="61320-111">Event accessors</span></span>
- <span data-ttu-id="61320-112">匿名方法</span><span class="sxs-lookup"><span data-stu-id="61320-112">Anonymous methods</span></span>
- <span data-ttu-id="61320-113">Lambda 表达式</span><span class="sxs-lookup"><span data-stu-id="61320-113">Lambda expressions</span></span>
- <span data-ttu-id="61320-114">终结器</span><span class="sxs-lookup"><span data-stu-id="61320-114">Finalizers</span></span>
- <span data-ttu-id="61320-115">其他本地函数</span><span class="sxs-lookup"><span data-stu-id="61320-115">Other local functions</span></span>

<span data-ttu-id="61320-116">但是，不能在 expression-bodied 成员中声明本地函数。</span><span class="sxs-lookup"><span data-stu-id="61320-116">However, local functions can't be declared inside an expression-bodied member.</span></span>

> [!NOTE]
> <span data-ttu-id="61320-117">在某些情况下，可以使用 lambda 表达式实现本地函数也支持的功能。</span><span class="sxs-lookup"><span data-stu-id="61320-117">In some cases, you can use a lambda expression to implement functionality also supported by a local function.</span></span> <span data-ttu-id="61320-118">有关比较，请参阅[本地函数与 lambda 表达式](#local-functions-vs-lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="61320-118">For a comparison, see [Local functions vs. lambda expressions](#local-functions-vs-lambda-expressions).</span></span>

<span data-ttu-id="61320-119">本地函数可使代码意图明确。</span><span class="sxs-lookup"><span data-stu-id="61320-119">Local functions make the intent of your code clear.</span></span> <span data-ttu-id="61320-120">任何读取代码的人都可以看到，此方法不可调用，包含方法除外。</span><span class="sxs-lookup"><span data-stu-id="61320-120">Anyone reading your code can see that the method is not callable except by the containing method.</span></span> <span data-ttu-id="61320-121">对于团队项目，它们也使得其他开发人员无法直接从类或结构中的其他位置错误调用此方法。</span><span class="sxs-lookup"><span data-stu-id="61320-121">For team projects, they also make it impossible for another developer to mistakenly call the method directly from elsewhere in the class or struct.</span></span>

## <a name="local-function-syntax"></a><span data-ttu-id="61320-122">本地函数语法</span><span class="sxs-lookup"><span data-stu-id="61320-122">Local function syntax</span></span>

<span data-ttu-id="61320-123">本地函数被定义为包含成员中的嵌套方法。</span><span class="sxs-lookup"><span data-stu-id="61320-123">A local function is defined as a nested method inside a containing member.</span></span> <span data-ttu-id="61320-124">其定义具有以下语法：</span><span class="sxs-lookup"><span data-stu-id="61320-124">Its definition has the following syntax:</span></span>

```csharp
<modifiers> <return-type> <method-name> <parameter-list>
```

<span data-ttu-id="61320-125">可以将以下修饰符用于本地函数：</span><span class="sxs-lookup"><span data-stu-id="61320-125">You can use the following modifiers with a local function:</span></span>

- [`async`](../../language-reference/keywords/async.md)
- [`unsafe`](../../language-reference/keywords/unsafe.md)
- <span data-ttu-id="61320-126">[`static`](../../language-reference/keywords/static.md)（在 C# 8.0 和更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="61320-126">[`static`](../../language-reference/keywords/static.md) (in C# 8.0 and later).</span></span> <span data-ttu-id="61320-127">静态本地函数无法捕获局部变量或实例状态。</span><span class="sxs-lookup"><span data-stu-id="61320-127">A static local function can't capture local variables or instance state.</span></span>
- <span data-ttu-id="61320-128">[`extern`](../../language-reference/keywords/extern.md)（在 C# 9.0 和更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="61320-128">[`extern`](../../language-reference/keywords/extern.md) (in C# 9.0 and later).</span></span> <span data-ttu-id="61320-129">外部本地函数必须为 `static`。</span><span class="sxs-lookup"><span data-stu-id="61320-129">An external local function must be `static`.</span></span>

<span data-ttu-id="61320-130">在包含成员中定义的所有本地变量（包括其方法参数）都可在非静态本地函数中访问。</span><span class="sxs-lookup"><span data-stu-id="61320-130">All local variables that are defined in the containing member, including its method parameters, are accessible in a non-static local function.</span></span>

<span data-ttu-id="61320-131">与方法定义不同，本地函数定义不能包含成员访问修饰符。</span><span class="sxs-lookup"><span data-stu-id="61320-131">Unlike a method definition, a local function definition cannot include the member access modifier.</span></span> <span data-ttu-id="61320-132">因为所有本地函数都是私有的，包括访问修饰符（如 `private` 关键字）会生成编译器错误 CS0106“修饰符‘private’对于此项无效”。</span><span class="sxs-lookup"><span data-stu-id="61320-132">Because all local functions are private, including an access modifier, such as the `private` keyword, generates compiler error CS0106, "The modifier 'private' is not valid for this item."</span></span>

<span data-ttu-id="61320-133">以下示例定义了一个名为 `AppendPathSeparator` 的本地函数，该函数对于名为 `GetText` 的方法是私有的：</span><span class="sxs-lookup"><span data-stu-id="61320-133">The following example defines a local function named `AppendPathSeparator` that is private to a method named `GetText`:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="Basic" :::

<span data-ttu-id="61320-134">从 C# 9.0 开始，你可以将属性应用于本地函数、其参数和类型参数，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="61320-134">Beginning with C# 9.0, you can apply attributes to a local function, its parameters and type parameters, as the following example shows:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="WithAttributes" :::

<span data-ttu-id="61320-135">前面的示例使用[特殊属性](../../language-reference/attributes/nullable-analysis.md)来帮助编译器在可为空的上下文中进行静态分析。</span><span class="sxs-lookup"><span data-stu-id="61320-135">The preceding example uses a [special attribute](../../language-reference/attributes/nullable-analysis.md) to assist the compiler in static analysis in a nullable context.</span></span>

## <a name="local-functions-and-exceptions"></a><span data-ttu-id="61320-136">本地函数和异常</span><span class="sxs-lookup"><span data-stu-id="61320-136">Local functions and exceptions</span></span>

<span data-ttu-id="61320-137">本地函数的一个实用功能是可以允许立即显示异常。</span><span class="sxs-lookup"><span data-stu-id="61320-137">One of the useful features of local functions is that they can allow exceptions to surface immediately.</span></span> <span data-ttu-id="61320-138">对于方法迭代器，仅在枚举返回的序列时才显示异常，而非在检索迭代器时。</span><span class="sxs-lookup"><span data-stu-id="61320-138">For method iterators, exceptions are surfaced only when the returned sequence is enumerated, and not when the iterator is retrieved.</span></span> <span data-ttu-id="61320-139">对于异步方法，在等待返回的任务时，将观察到异步方法中引发的任何异常。</span><span class="sxs-lookup"><span data-stu-id="61320-139">For async methods, any exceptions thrown in an async method are observed when the returned task is awaited.</span></span>

<span data-ttu-id="61320-140">以下示例定义 `OddSequence` 方法，用于枚举指定范围中的奇数。</span><span class="sxs-lookup"><span data-stu-id="61320-140">The following example defines an `OddSequence` method that enumerates odd numbers in a specified range.</span></span> <span data-ttu-id="61320-141">因为它会将一个大于 100 的数字传递到 `OddSequence` 迭代器方法，该方法将引发 <xref:System.ArgumentOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="61320-141">Because it passes a number greater than 100 to the `OddSequence` enumerator method, the method throws an <xref:System.ArgumentOutOfRangeException>.</span></span> <span data-ttu-id="61320-142">如示例中的输出所示，仅当循环访问数字时才显示异常，而非检索迭代器时。</span><span class="sxs-lookup"><span data-stu-id="61320-142">As the output from the example shows, the exception surfaces only when you iterate the numbers, and not when you retrieve the enumerator.</span></span>

:::code language="csharp" source="snippets/local-functions/IteratorWithoutLocal.cs" :::

<span data-ttu-id="61320-143">如果将迭代器逻辑放入本地函数，则在检索枚举器时会引发参数验证异常，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="61320-143">If you put iterator logic into a local function, argument validation exceptions are thrown when you retrieve the enumerator, as the following example shows:</span></span>

:::code language="csharp" source="snippets/local-functions/IteratorWithLocal.cs" :::

<span data-ttu-id="61320-144">你可以通过类似于异步操作的方式来使用本地函数。</span><span class="sxs-lookup"><span data-stu-id="61320-144">You can use local functions in a similar way with asynchronous operations.</span></span> <span data-ttu-id="61320-145">等待相应的任务时，异步方法图面中引发的异常。</span><span class="sxs-lookup"><span data-stu-id="61320-145">Exceptions thrown in an async method surface when the corresponding task is awaited.</span></span> <span data-ttu-id="61320-146">本地函数允许代码快速失败，并允许同步引发和观察异常。</span><span class="sxs-lookup"><span data-stu-id="61320-146">Local functions allow your code to fail fast and allow your exception to be both thrown and observed synchronously.</span></span>

<span data-ttu-id="61320-147">以下示例使用名为 `GetMultipleAsync` 的异步方法暂停指定的秒数并返回一个值，该值是该秒数的任意倍数。</span><span class="sxs-lookup"><span data-stu-id="61320-147">The following example uses an asynchronous method named `GetMultipleAsync` to pause for a specified number of seconds and return a value that is a random multiple of that number of seconds.</span></span> <span data-ttu-id="61320-148">最大延迟为 5 秒；如果该值大于 5，则结果为 <xref:System.ArgumentOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="61320-148">The maximum delay is 5 seconds; an <xref:System.ArgumentOutOfRangeException> results if the value is greater than 5.</span></span> <span data-ttu-id="61320-149">如下面的示例所示，仅当任务处于等待状态时，才会观察到将值 6 传递到 `GetMultipleAsync` 方法时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="61320-149">As the following example shows, the exception that is thrown when a value of 6 is passed to the `GetMultipleAsync` method is observed only when the task is awaited.</span></span>

:::code language="csharp" source="snippets/local-functions/AsyncWithoutLocal.cs" :::

<span data-ttu-id="61320-150">与方法迭代器类似，你可以重构前面的示例，将异步操作的代码放入本地函数。</span><span class="sxs-lookup"><span data-stu-id="61320-150">Like with the method iterator, you can refactor the preceding example and put the code of asynchronous operation in a local function.</span></span> <span data-ttu-id="61320-151">如以下示例中的输出所示，调用 `GetMultiple` 方法后，会引发 <xref:System.ArgumentOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="61320-151">As the output from the following example shows, the <xref:System.ArgumentOutOfRangeException> is thrown as soon as the `GetMultiple` method is called.</span></span>

:::code language="csharp" source="snippets/local-functions/AsyncWithLocal.cs" :::

## <a name="local-functions-vs-lambda-expressions"></a><span data-ttu-id="61320-152">本地函数与 Lambda 表达式</span><span class="sxs-lookup"><span data-stu-id="61320-152">Local functions vs. lambda expressions</span></span>

<span data-ttu-id="61320-153">乍看之下，本地函数和 [lambda 表达式](../../language-reference/operators/lambda-expressions.md)非常相似。</span><span class="sxs-lookup"><span data-stu-id="61320-153">At first glance, local functions and [lambda expressions](../../language-reference/operators/lambda-expressions.md) are very similar.</span></span> <span data-ttu-id="61320-154">在许多情况下，选择使用 Lambda 表达式还是本地函数是风格和个人偏好的问题。</span><span class="sxs-lookup"><span data-stu-id="61320-154">In many cases, the choice between using lambda expressions and local functions is a matter of style and personal preference.</span></span> <span data-ttu-id="61320-155">但是，应该注意，从两者中选用一种的时机和条件其实是存在差别的。</span><span class="sxs-lookup"><span data-stu-id="61320-155">However, there are real differences in where you can use one or the other that you should be aware of.</span></span>

<span data-ttu-id="61320-156">让我们检查一下阶乘算法的本地函数实现和 lambda 表达式实现之间的差异。</span><span class="sxs-lookup"><span data-stu-id="61320-156">Let's examine the differences between the local function and lambda expression implementations of the factorial algorithm.</span></span> <span data-ttu-id="61320-157">下面是使用本地函数的版本：</span><span class="sxs-lookup"><span data-stu-id="61320-157">Here's the version using a local function:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="FactorialWithLocal" :::

<span data-ttu-id="61320-158">此版本使用 Lambda 表达式：</span><span class="sxs-lookup"><span data-stu-id="61320-158">This version uses lambda expressions:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="FactorialWithLambda" :::

### <a name="naming"></a><span data-ttu-id="61320-159">命名</span><span class="sxs-lookup"><span data-stu-id="61320-159">Naming</span></span>

<span data-ttu-id="61320-160">本地函数的命名方式与方法相同。</span><span class="sxs-lookup"><span data-stu-id="61320-160">Local functions are explicitly named like methods.</span></span> <span data-ttu-id="61320-161">Lambda 表达式是一种匿名方法，需要分配给 `delegate` 类型的变量，通常是 `Action` 或 `Func` 类型。</span><span class="sxs-lookup"><span data-stu-id="61320-161">Lambda expressions are anonymous methods and need to be assigned to variables of a `delegate` type, typically either `Action` or `Func` types.</span></span> <span data-ttu-id="61320-162">声明本地函数时，此过程类似于编写普通方法；声明一个返回类型和一个函数签名。</span><span class="sxs-lookup"><span data-stu-id="61320-162">When you declare a local function, the process is like writing a normal method; you declare a return type and a function signature.</span></span>

### <a name="function-signatures-and-lambda-expression-types"></a><span data-ttu-id="61320-163">函数签名和 Lambda 表达式类型</span><span class="sxs-lookup"><span data-stu-id="61320-163">Function signatures and lambda expression types</span></span>

<span data-ttu-id="61320-164">Lambda 表达式依赖于为其分配的 `Action`/`Func` 变量的类型来确定参数和返回类型。</span><span class="sxs-lookup"><span data-stu-id="61320-164">Lambda expressions rely on the type of the `Action`/`Func` variable that they're assigned to determine the argument and return types.</span></span> <span data-ttu-id="61320-165">在本地函数中，因为语法非常类似于编写常规方法，所以参数类型和返回类型已经是函数声明的一部分。</span><span class="sxs-lookup"><span data-stu-id="61320-165">In local functions, since the syntax is much like writing a normal method, argument types and return type are already part of the function declaration.</span></span>

### <a name="definite-assignment"></a><span data-ttu-id="61320-166">明确赋值</span><span class="sxs-lookup"><span data-stu-id="61320-166">Definite assignment</span></span>

<span data-ttu-id="61320-167">Lambda 表达式是在运行时声明和分配的对象。</span><span class="sxs-lookup"><span data-stu-id="61320-167">Lambda expressions are objects that are declared and assigned at runtime.</span></span> <span data-ttu-id="61320-168">若要使用 Lambda 表达式，需要对其进行明确赋值：必须声明要分配给它的 `Action`/`Func` 变量，并为其分配 Lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="61320-168">In order for a lambda expression to be used, it needs to be definitely assigned: the `Action`/`Func` variable that it will be assigned to must be declared and the lambda expression assigned to it.</span></span> <span data-ttu-id="61320-169">请注意，`LambdaFactorial` 必须先声明和初始化 Lambda 表达式 `nthFactorial`，然后再对其进行定义。</span><span class="sxs-lookup"><span data-stu-id="61320-169">Notice that `LambdaFactorial` must declare and initialize the lambda expression `nthFactorial` before defining it.</span></span> <span data-ttu-id="61320-170">否则，会导致分配前引用 `nthFactorial` 时出现编译时错误。</span><span class="sxs-lookup"><span data-stu-id="61320-170">Not doing so results in a compile time error for referencing `nthFactorial` before assigning it.</span></span>

<span data-ttu-id="61320-171">本地函数在编译时定义。</span><span class="sxs-lookup"><span data-stu-id="61320-171">Local functions are defined at compile time.</span></span> <span data-ttu-id="61320-172">由于未将它们分配给变量，因此可以从范围内的任意代码位置引用它们；在第一个示例 `LocalFunctionFactorial` 中，我们可以在 `return` 语句的上方或下方声明本地函数，而不会触发任何编译器错误。</span><span class="sxs-lookup"><span data-stu-id="61320-172">As they're not assigned to variables, they can be referenced from any code location **where it is in scope** ; in our first example `LocalFunctionFactorial`, we could declare our local function either above or below the `return` statement and not trigger any compiler errors.</span></span>

<span data-ttu-id="61320-173">这些区别意味着使用本地函数创建递归算法会更轻松。</span><span class="sxs-lookup"><span data-stu-id="61320-173">These differences mean that recursive algorithms are easier to create using local functions.</span></span> <span data-ttu-id="61320-174">你可以声明和定义一个调用自身的本地函数。</span><span class="sxs-lookup"><span data-stu-id="61320-174">You can declare and define a local function that calls itself.</span></span> <span data-ttu-id="61320-175">必须声明 Lambda 表达式，赋给默认值，然后才能将其重新赋给引用相同 Lambda 表达式的主体。</span><span class="sxs-lookup"><span data-stu-id="61320-175">Lambda expressions must be declared, and assigned a default value before they can be re-assigned to a body that references the same lambda expression.</span></span>

### <a name="implementation-as-a-delegate"></a><span data-ttu-id="61320-176">实现为委托</span><span class="sxs-lookup"><span data-stu-id="61320-176">Implementation as a delegate</span></span>

<span data-ttu-id="61320-177">Lambda 表达式在声明时转换为委托。</span><span class="sxs-lookup"><span data-stu-id="61320-177">Lambda expressions are converted to delegates when they're declared.</span></span> <span data-ttu-id="61320-178">本地函数更加灵活，可以像传统方法一样编写，也可以作为委托编写。</span><span class="sxs-lookup"><span data-stu-id="61320-178">Local functions are more flexible in that they can be written like a traditional method *or* as a delegate.</span></span> <span data-ttu-id="61320-179">只有在用作委托时，本地函数才转换为委托。</span><span class="sxs-lookup"><span data-stu-id="61320-179">Local functions are only converted to delegates when ***used*** as a delegate.</span></span>

<span data-ttu-id="61320-180">如果声明了本地函数，但只是通过像调用方法一样调用该函数来引用该函数，它将不会转换成委托。</span><span class="sxs-lookup"><span data-stu-id="61320-180">If you declare a local function and only reference it by calling it like a method, it will not be converted to a delegate.</span></span>

### <a name="variable-capture"></a><span data-ttu-id="61320-181">变量捕获</span><span class="sxs-lookup"><span data-stu-id="61320-181">Variable capture</span></span>

<span data-ttu-id="61320-182">[明确分配](../../../../_csharplang/spec/variables.md#definite-assignment)的规则也会影响本地函数或 Lambda 表达式捕获的任何变量。</span><span class="sxs-lookup"><span data-stu-id="61320-182">The rules of [definite assignment](../../../../_csharplang/spec/variables.md#definite-assignment) also affect any variables that are captured by the local function or lambda expression.</span></span> <span data-ttu-id="61320-183">编译器可以执行静态分析，因此本地函数能够在封闭范围内明确分配捕获的变量。</span><span class="sxs-lookup"><span data-stu-id="61320-183">The compiler can perform static analysis that enables local functions to definitely assign captured variables in the enclosing scope.</span></span> <span data-ttu-id="61320-184">请看以下示例：</span><span class="sxs-lookup"><span data-stu-id="61320-184">Consider this example:</span></span>

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

<span data-ttu-id="61320-185">编译器可以确定 `LocalFunction` 在调用时明确分配 `y`。</span><span class="sxs-lookup"><span data-stu-id="61320-185">The compiler can determine that `LocalFunction` definitely assigns `y` when called.</span></span> <span data-ttu-id="61320-186">因为在 `return` 语句之前调用了 `LocalFunction`，所以在 `return` 语句中明确分配了 `y`。</span><span class="sxs-lookup"><span data-stu-id="61320-186">Because `LocalFunction` is called before the `return` statement, `y` is definitely assigned at the `return` statement.</span></span>

<span data-ttu-id="61320-187">请注意，当本地函数捕获封闭范围中的变量时，本地函数将作为委托类型实现。</span><span class="sxs-lookup"><span data-stu-id="61320-187">Note that when a local function captures variables in the enclosing scope, the local function is implemented as a delegate type.</span></span>

### <a name="heap-allocations"></a><span data-ttu-id="61320-188">堆分配</span><span class="sxs-lookup"><span data-stu-id="61320-188">Heap allocations</span></span>

<span data-ttu-id="61320-189">根据它们的用途，本地函数可以避免 Lambda 表达式始终需要的堆分配。</span><span class="sxs-lookup"><span data-stu-id="61320-189">Depending on their use, local functions can avoid heap allocations that are always necessary for lambda expressions.</span></span> <span data-ttu-id="61320-190">如果本地函数永远不会转换为委托，并且本地函数捕获的变量都不会被其他转换为委托的 lambda 或本地函数捕获，则编译器可以避免堆分配。</span><span class="sxs-lookup"><span data-stu-id="61320-190">If a local function is never converted to a delegate, and none of the variables captured by the local function are captured by other lambdas or local functions that are converted to delegates, the compiler can avoid heap allocations.</span></span>

<span data-ttu-id="61320-191">请看以下异步示例：</span><span class="sxs-lookup"><span data-stu-id="61320-191">Consider this async example:</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="AsyncWithLambda" :::

<span data-ttu-id="61320-192">该 lambda 表达式的闭包包含 `address`、`index` 和 `name` 变量。</span><span class="sxs-lookup"><span data-stu-id="61320-192">The closure for this lambda expression contains the `address`, `index` and `name` variables.</span></span> <span data-ttu-id="61320-193">就本地函数而言，实现闭包的对象可能为 `struct` 类型。</span><span class="sxs-lookup"><span data-stu-id="61320-193">In the case of local functions, the object that implements the closure may be a `struct` type.</span></span> <span data-ttu-id="61320-194">该结构类型将通过引用传递给本地函数。</span><span class="sxs-lookup"><span data-stu-id="61320-194">That struct type would be passed by reference to the local function.</span></span> <span data-ttu-id="61320-195">实现中的这个差异将保存在分配上。</span><span class="sxs-lookup"><span data-stu-id="61320-195">This difference in implementation would save on an allocation.</span></span>

<span data-ttu-id="61320-196">Lambda 表达式所需的实例化意味着额外的内存分配，后者可能是时间关键代码路径中的性能因素。</span><span class="sxs-lookup"><span data-stu-id="61320-196">The instantiation necessary for lambda expressions means extra memory allocations, which may be a performance factor in time-critical code paths.</span></span> <span data-ttu-id="61320-197">本地函数不会产生这种开销。</span><span class="sxs-lookup"><span data-stu-id="61320-197">Local functions do not incur this overhead.</span></span> <span data-ttu-id="61320-198">在以上示例中，本地函数版本具有的分配比 Lambda 表达式版本少 2 个。</span><span class="sxs-lookup"><span data-stu-id="61320-198">In the example above, the local functions version has two fewer allocations than the lambda expression version.</span></span>

<span data-ttu-id="61320-199">如果你知道本地函数不会转换为委托，并且本地函数捕获的变量都不会被其他转换为委托的 lambda 或本地函数捕获，则可以通过将本地函数声明为 `static` 本地函数来确保避免在堆上对其进行分配。</span><span class="sxs-lookup"><span data-stu-id="61320-199">If you know that your local function won't be converted to a delegate and none of the variables captured by it are captured by other lambdas or local functions that are converted to delegates, you can guarantee that your local function avoids being allocated on the heap by declaring it as a `static` local function.</span></span> <span data-ttu-id="61320-200">请注意，此功能在 C# 8.0 及更高版本中提供。</span><span class="sxs-lookup"><span data-stu-id="61320-200">Note that this feature is available in C# 8.0 and newer.</span></span>

> [!NOTE]
> <span data-ttu-id="61320-201">等效于此方法的本地函数还将类用于闭包。</span><span class="sxs-lookup"><span data-stu-id="61320-201">The local function equivalent of this method also uses a class for the closure.</span></span> <span data-ttu-id="61320-202">实现详细信息包括本地函数的闭包是作为 `class` 还是 `struct` 实现。</span><span class="sxs-lookup"><span data-stu-id="61320-202">Whether the closure for a local function is implemented as a `class` or a `struct` is an implementation detail.</span></span> <span data-ttu-id="61320-203">本地函数可能使用 `struct`，而 lambda 将始终使用 `class`。</span><span class="sxs-lookup"><span data-stu-id="61320-203">A local function may use a `struct` whereas a lambda will always use a `class`.</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="AsyncWithLocal" :::

### <a name="usage-of-the-yield-keyword"></a><span data-ttu-id="61320-204">`yield` 关键字的用法</span><span class="sxs-lookup"><span data-stu-id="61320-204">Usage of the `yield` keyword</span></span>

<span data-ttu-id="61320-205">在本示例中尚未演示的最后一个优点是，可将本地函数作为迭代器实现，使用 `yield return` 语法生成一系列值。</span><span class="sxs-lookup"><span data-stu-id="61320-205">One final advantage not demonstrated in this sample is that local functions can be implemented as iterators, using the `yield return` syntax to produce a sequence of values.</span></span>

:::code language="csharp" source="snippets/local-functions/Program.cs" id="YieldReturn" :::

<span data-ttu-id="61320-206">Lambda 表达式中不允许使用 `yield return` 语句，请参阅[编译器错误 CS1621](../../misc/cs1621.md)。</span><span class="sxs-lookup"><span data-stu-id="61320-206">The `yield return` statement is not allowed in lambda expressions, see [compiler error CS1621](../../misc/cs1621.md).</span></span>

<span data-ttu-id="61320-207">虽然本地函数对 lambda 表达式可能有点冗余，但实际上它们的目的和用法都不一样。</span><span class="sxs-lookup"><span data-stu-id="61320-207">While local functions may seem redundant to lambda expressions, they actually serve different purposes and have different uses.</span></span> <span data-ttu-id="61320-208">如果想要编写仅从上下文或其他方法中调用的函数，则使用本地函数更高效。</span><span class="sxs-lookup"><span data-stu-id="61320-208">Local functions are more efficient for the case when you want to write a function that is called only from the context of another method.</span></span>

## <a name="see-also"></a><span data-ttu-id="61320-209">请参阅</span><span class="sxs-lookup"><span data-stu-id="61320-209">See also</span></span>

- [<span data-ttu-id="61320-210">方法</span><span class="sxs-lookup"><span data-stu-id="61320-210">Methods</span></span>](methods.md)
