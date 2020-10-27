---
title: C# 6 中的新增功能 - C# 指南
description: 了解 C# 版本 6 中的新增功能
ms.date: 12/12/2018
ms.openlocfilehash: da40b4c9d4af0094fdd907c542e971ba55086e0f
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224231"
---
# <a name="whats-new-in-c-6"></a><span data-ttu-id="ceaee-103">C# 6 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ceaee-103">What's New in C# 6</span></span>

<span data-ttu-id="ceaee-104">C# 6.0 版本包含许多可提高开发人员工作效率的功能。</span><span class="sxs-lookup"><span data-stu-id="ceaee-104">The 6.0 release of C# contained many features that improve productivity for developers.</span></span> <span data-ttu-id="ceaee-105">这些功能的总体效果是让你编写的代码更简洁、更具可读性。</span><span class="sxs-lookup"><span data-stu-id="ceaee-105">The overall effect of these features is that you write more concise code that is also more readable.</span></span> <span data-ttu-id="ceaee-106">该语法不像许多常见做法那样繁琐。</span><span class="sxs-lookup"><span data-stu-id="ceaee-106">The syntax contains less ceremony for many common practices.</span></span> <span data-ttu-id="ceaee-107">可以更轻松地看出设计意图。</span><span class="sxs-lookup"><span data-stu-id="ceaee-107">It's easier to see the design intent with less ceremony.</span></span> <span data-ttu-id="ceaee-108">好好了解这些功能可以帮助你提高生产力，编写更具可读性的代码。</span><span class="sxs-lookup"><span data-stu-id="ceaee-108">Learn these features well, and you'll be more productive and write more readable code.</span></span> <span data-ttu-id="ceaee-109">你可以更专注于功能，而不是语言的构造。</span><span class="sxs-lookup"><span data-stu-id="ceaee-109">You can concentrate more on your features than on the constructs of the language.</span></span>

<span data-ttu-id="ceaee-110">本文的其余部分是对每个功能的概述，并提供用于探索每个功能的链接。</span><span class="sxs-lookup"><span data-stu-id="ceaee-110">The rest of this article provides an overview of each of these features, with a link to explore each feature.</span></span> <span data-ttu-id="ceaee-111">还可以在教程部分的 [C# 6 交互式探索](../tutorials/exploration/csharp-6.yml)中探索这些功能。</span><span class="sxs-lookup"><span data-stu-id="ceaee-111">You can also explore the features in an [interactive exploration on C# 6](../tutorials/exploration/csharp-6.yml) in the tutorials section.</span></span>

## <a name="read-only-auto-properties"></a><span data-ttu-id="ceaee-112">只读自动属性</span><span class="sxs-lookup"><span data-stu-id="ceaee-112">Read-only auto-properties</span></span>

<span data-ttu-id="ceaee-113">只读自动属性  提供了更简洁的语法来创建不可变类型。</span><span class="sxs-lookup"><span data-stu-id="ceaee-113">*Read-only auto-properties* provide a more concise syntax to create immutable types.</span></span> <span data-ttu-id="ceaee-114">你声明仅具有 get 访问器的自动属性：</span><span class="sxs-lookup"><span data-stu-id="ceaee-114">You declare the auto-property with only a get accessor:</span></span>

[!code-csharp[ReadOnlyAutoProperty](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoProperty)]

<span data-ttu-id="ceaee-115">`FirstName` 和 `LastName` 属性只能在同一个类的构造函数的主体中设置：</span><span class="sxs-lookup"><span data-stu-id="ceaee-115">The `FirstName` and `LastName` properties can be set only in the body of the constructor of the same class:</span></span>

[!code-csharp[ReadOnlyAutoPropertyConstructor](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoPropertyConstructor)]

<span data-ttu-id="ceaee-116">尝试在另一种方法中设置 `LastName` 会生成 `CS0200` 编译错误：</span><span class="sxs-lookup"><span data-stu-id="ceaee-116">Trying to set `LastName` in another method generates a `CS0200` compilation error:</span></span>

```csharp
public class Student
{
    public string LastName { get;  }

    public void ChangeName(string newLastName)
    {
        // Generates CS0200: Property or indexer cannot be assigned to -- it is read only
        LastName = newLastName;
    }
}
```

<span data-ttu-id="ceaee-117">此功能实现用于创建不可变类型的真正语言支持且使用更简洁和方便的自动属性语法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-117">This feature enables true language support for creating immutable types and uses the more concise and convenient auto-property syntax.</span></span>

<span data-ttu-id="ceaee-118">如果添加此语法不会删除可访问的方法，则为[二进制兼容的更改](version-update-considerations.md#binary-compatible-changes)。</span><span class="sxs-lookup"><span data-stu-id="ceaee-118">If adding this syntax doesn't remove an accessible method, it's a [binary compatible change](version-update-considerations.md#binary-compatible-changes).</span></span>

## <a name="auto-property-initializers"></a><span data-ttu-id="ceaee-119">自动属性初始化表达式</span><span class="sxs-lookup"><span data-stu-id="ceaee-119">Auto-property initializers</span></span>

<span data-ttu-id="ceaee-120">自动属性初始值设定项  可让你在属性声明中声明自动属性的初始值。</span><span class="sxs-lookup"><span data-stu-id="ceaee-120">*Auto-property initializers* let you declare the initial value for an auto-property as part of the property declaration.</span></span>

[!code-csharp[Initialization](../../../samples/snippets/csharp/new-in-6/newcode.cs#Initialization)]

<span data-ttu-id="ceaee-121">`Grades` 成员在声明它的位置处被初始化。</span><span class="sxs-lookup"><span data-stu-id="ceaee-121">The `Grades` member is initialized where it's declared.</span></span> <span data-ttu-id="ceaee-122">这样，就能更容易地仅执行一次初始化。</span><span class="sxs-lookup"><span data-stu-id="ceaee-122">That makes it easier to perform the initialization exactly once.</span></span> <span data-ttu-id="ceaee-123">初始化是属性声明的一部分，可更轻松地将存储分配等同于 `Student` 对象的公用接口。</span><span class="sxs-lookup"><span data-stu-id="ceaee-123">The initialization is part of the property declaration, making it easier to equate the storage allocation with the public interface for `Student` objects.</span></span>

## <a name="expression-bodied-function-members"></a><span data-ttu-id="ceaee-124">Expression-bodied 函数成员</span><span class="sxs-lookup"><span data-stu-id="ceaee-124">Expression-bodied function members</span></span>

<span data-ttu-id="ceaee-125">你编写的许多成员是可以作为单个表达式的单个语句。</span><span class="sxs-lookup"><span data-stu-id="ceaee-125">Many members that you write are single statements that could be single expressions.</span></span> <span data-ttu-id="ceaee-126">改为编写 expression-bodied 成员。</span><span class="sxs-lookup"><span data-stu-id="ceaee-126">Write an expression-bodied member instead.</span></span> <span data-ttu-id="ceaee-127">这适用于方法和只读属性。</span><span class="sxs-lookup"><span data-stu-id="ceaee-127">It works for methods and read-only properties.</span></span> <span data-ttu-id="ceaee-128">例如，重写 `ToString()` 通常是理想之选：</span><span class="sxs-lookup"><span data-stu-id="ceaee-128">For example, an override of `ToString()` is often a great candidate:</span></span>

[!code-csharp[ToStringExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#ToStringExpressionMember)]

<span data-ttu-id="ceaee-129">也可以将此语法用于只读属性：</span><span class="sxs-lookup"><span data-stu-id="ceaee-129">You can also use this syntax for read-only properties:</span></span>

[!code-csharp[FullNameExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

<span data-ttu-id="ceaee-130">将现有成员更改为 expression bodied 成员是[二进制兼容的更改](version-update-considerations.md#binary-compatible-changes)。</span><span class="sxs-lookup"><span data-stu-id="ceaee-130">Changing an existing member to an expression bodied member is a [binary compatible change](version-update-considerations.md#binary-compatible-changes).</span></span>

## <a name="using-static"></a><span data-ttu-id="ceaee-131">using static</span><span class="sxs-lookup"><span data-stu-id="ceaee-131">using static</span></span>

<span data-ttu-id="ceaee-132">using static  增强功能可用于导入单个类的静态方法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-132">The *using static* enhancement enables you to import the static methods of a single class.</span></span> <span data-ttu-id="ceaee-133">指定要使用的类：</span><span class="sxs-lookup"><span data-stu-id="ceaee-133">You specify the class you're using:</span></span>

[!code-csharp[UsingStaticMath](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStaticMath)]

<span data-ttu-id="ceaee-134"><xref:System.Math> 不包含任何实例方法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-134">The <xref:System.Math> does not contain any instance methods.</span></span> <span data-ttu-id="ceaee-135">还可以使用 `using static` 为具有静态和实例方法的类导入类的静态方法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-135">You can also use `using static` to import a class' static methods for a class that has both static and instance methods.</span></span> <span data-ttu-id="ceaee-136">最有用的示例之一是 <xref:System.String>：</span><span class="sxs-lookup"><span data-stu-id="ceaee-136">One of the most useful examples is <xref:System.String>:</span></span>

[!code-csharp[UsingStatic](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStatic)]

> [!NOTE]
> <span data-ttu-id="ceaee-137">在 static using 语句中必须使用完全限定的类名 `System.String`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-137">You must use the fully qualified class name, `System.String`  in a static using statement.</span></span>  <span data-ttu-id="ceaee-138">而不能使用 `string` 关键字。</span><span class="sxs-lookup"><span data-stu-id="ceaee-138">You cannot use the `string` keyword instead.</span></span>

<span data-ttu-id="ceaee-139">从 `static using` 语句导入时，仅在使用扩展方法调用语法调用扩展方法时，扩展方法才在范围内。</span><span class="sxs-lookup"><span data-stu-id="ceaee-139">When imported from a `static using` statement, extension methods are only in scope when called using the extension method invocation syntax.</span></span> <span data-ttu-id="ceaee-140">作为静态方法调用时，扩展方法不在范围内。</span><span class="sxs-lookup"><span data-stu-id="ceaee-140">They aren't in scope when called as a static method.</span></span> <span data-ttu-id="ceaee-141">你在 LINQ 查询中会经常看到这种情况。</span><span class="sxs-lookup"><span data-stu-id="ceaee-141">You'll often see this in LINQ queries.</span></span> <span data-ttu-id="ceaee-142">可以通过导入 <xref:System.Linq.Enumerable> 或 <xref:System.Linq.Queryable> 来导入 LINQ 模式。</span><span class="sxs-lookup"><span data-stu-id="ceaee-142">You can import the LINQ pattern by importing <xref:System.Linq.Enumerable>, or <xref:System.Linq.Queryable>.</span></span>

[!code-csharp[UsingStaticLinq](../../../samples/snippets/csharp/new-in-6/newcode.cs#usingStaticLinq)]

<span data-ttu-id="ceaee-143">通常使用扩展方法调用表达式调用扩展方法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-143">You typically call extension methods using extension method invocation expressions.</span></span> <span data-ttu-id="ceaee-144">在使用静态方法调用语法对其进行调用的罕见情况下，添加类名称可以解决歧义。</span><span class="sxs-lookup"><span data-stu-id="ceaee-144">Adding the class name in the rare case where you call them using static method call syntax resolves ambiguity.</span></span>

<span data-ttu-id="ceaee-145">`static using` 指令还可以导入任何嵌套的类型。</span><span class="sxs-lookup"><span data-stu-id="ceaee-145">The `static using` directive also imports any nested types.</span></span> <span data-ttu-id="ceaee-146">可以引用任何嵌套的类型，而无需限定。</span><span class="sxs-lookup"><span data-stu-id="ceaee-146">You can reference any nested types without qualification.</span></span>

## <a name="null-conditional-operators"></a><span data-ttu-id="ceaee-147">Null 条件运算符</span><span class="sxs-lookup"><span data-stu-id="ceaee-147">Null-conditional operators</span></span>

<span data-ttu-id="ceaee-148">Null 条件运算符使 null 检查更轻松、更流畅  。</span><span class="sxs-lookup"><span data-stu-id="ceaee-148">The *null conditional operator* makes null checks much easier and fluid.</span></span> <span data-ttu-id="ceaee-149">将成员访问 `.` 替换为 `?.`：</span><span class="sxs-lookup"><span data-stu-id="ceaee-149">Replace the member access `.` with `?.`:</span></span>

[!code-csharp[NullConditional](../../../samples/snippets/csharp/new-in-6/program.cs#NullConditional)]

<span data-ttu-id="ceaee-150">在前面的示例中，如果 Person 对象是 `null`，则将变量 `first` 赋值为 `null`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-150">In the preceding example, the variable `first` is assigned `null` if the person object is `null`.</span></span> <span data-ttu-id="ceaee-151">否则，将 `FirstName` 属性的值分配给该变量。</span><span class="sxs-lookup"><span data-stu-id="ceaee-151">Otherwise, it is assigned the value of the `FirstName` property.</span></span> <span data-ttu-id="ceaee-152">最重要的是，`?.` 意味着当 `person` 变量为 `null` 时，此行代码不会生成 `NullReferenceException`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-152">Most importantly, the `?.` means that this line of code doesn't generate a `NullReferenceException` if the `person` variable is `null`.</span></span> <span data-ttu-id="ceaee-153">它会短路并返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-153">Instead, it short-circuits and returns `null`.</span></span> <span data-ttu-id="ceaee-154">还可以将 null 条件运算符用于数组或索引器访问。</span><span class="sxs-lookup"><span data-stu-id="ceaee-154">You can also use a null conditional operator for array or indexer access.</span></span> <span data-ttu-id="ceaee-155">将索引表达式中的 `[]` 替换为 `?[]`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-155">Replace `[]` with `?[]` in the index expression.</span></span>

<span data-ttu-id="ceaee-156">无论 `person` 的值是什么，以下表达式均返回 `string`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-156">The following expression returns a `string`, regardless of the value of `person`.</span></span> <span data-ttu-id="ceaee-157">通常，将此构造与“null 合并”运算符一起使用，以在其中一个属性为 `null` 时分配默认值。</span><span class="sxs-lookup"><span data-stu-id="ceaee-157">You often use this construct with the *null coalescing* operator to assign default values when one of the properties is `null`.</span></span> <span data-ttu-id="ceaee-158">表达式短路时，键入返回的 `null` 值以匹配整个表达式。</span><span class="sxs-lookup"><span data-stu-id="ceaee-158">When the expression short-circuits, the `null` value returned is typed to match the full expression.</span></span>

[!code-csharp[NullCoalescing](../../../samples/snippets/csharp/new-in-6/program.cs#NullCoalescing)]

<span data-ttu-id="ceaee-159">还可以将 `?.` 用于有条件地调用方法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-159">You can also use `?.` to conditionally invoke methods.</span></span> <span data-ttu-id="ceaee-160">具有 null 条件运算符的成员函数的最常见用法是用于安全地调用可能为 `null` 的委托（或事件处理程序）。</span><span class="sxs-lookup"><span data-stu-id="ceaee-160">The most common use of member functions  with the null conditional operator is to safely invoke delegates (or event handlers) that may be `null`.</span></span>  <span data-ttu-id="ceaee-161">通过使用 `?.` 运算符调用该委托的 `Invoke` 方法来访问成员。</span><span class="sxs-lookup"><span data-stu-id="ceaee-161">You'll call the delegate's `Invoke` method using the `?.` operator to access the member.</span></span> <span data-ttu-id="ceaee-162">可以在[委托模式](../delegates-patterns.md#handling-null-delegates)一文中看到示例。</span><span class="sxs-lookup"><span data-stu-id="ceaee-162">You can see an example in the [delegate patterns](../delegates-patterns.md#handling-null-delegates) article.</span></span>

<span data-ttu-id="ceaee-163">`?.` 运算符的规则确保运算符的左侧仅计算一次。</span><span class="sxs-lookup"><span data-stu-id="ceaee-163">The rules of the `?.` operator ensure that the left-hand side of the operator is evaluated only once.</span></span> <span data-ttu-id="ceaee-164">它支持许多语法，包括使用事件处理程序的以下示例：</span><span class="sxs-lookup"><span data-stu-id="ceaee-164">It enables many idioms, including the following example using event handlers:</span></span>

```csharp
// preferred in C# 6:
this.SomethingHappened?.Invoke(this, eventArgs);
```

<span data-ttu-id="ceaee-165">确保左侧只计算一次，这使得你可以在 `?.` 的左侧使用任何表达式（包括方法调用）</span><span class="sxs-lookup"><span data-stu-id="ceaee-165">Ensuring that the left side is evaluated only once also enables you to use any expression, including method calls, on the left side of the `?.`</span></span>

## <a name="string-interpolation"></a><span data-ttu-id="ceaee-166">字符串内插</span><span class="sxs-lookup"><span data-stu-id="ceaee-166">String interpolation</span></span>

<span data-ttu-id="ceaee-167">使用 C# 6，新的[字符串内插](../language-reference/tokens/interpolated.md)功能可以在字符串中嵌入表达式。</span><span class="sxs-lookup"><span data-stu-id="ceaee-167">With C# 6, the new [string interpolation](../language-reference/tokens/interpolated.md) feature enables you to embed expressions in a string.</span></span> <span data-ttu-id="ceaee-168">使用 `$` 作为字符串的开头，并使用 `{` 和 `}` 之间的表达式代替序号：</span><span class="sxs-lookup"><span data-stu-id="ceaee-168">Simply preface the string with `$`and use expressions between `{` and `}` instead of ordinals:</span></span>

[!code-csharp[stringInterpolation](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

<span data-ttu-id="ceaee-169">本示例使用替代表达式的属性。</span><span class="sxs-lookup"><span data-stu-id="ceaee-169">This example uses properties for the substituted expressions.</span></span> <span data-ttu-id="ceaee-170">可以使用任何表达式。</span><span class="sxs-lookup"><span data-stu-id="ceaee-170">You can use any expression.</span></span> <span data-ttu-id="ceaee-171">例如，可以在内插过程中计算学生的成绩平均值：</span><span class="sxs-lookup"><span data-stu-id="ceaee-171">For example, you could compute a student's grade point average as part of the interpolation:</span></span>

[!code-csharp[stringInterpolationFormat](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationFormat)]

<span data-ttu-id="ceaee-172">上一行代码将 `Grades.Average()` 的值格式设置为具有两位小数的浮点数。</span><span class="sxs-lookup"><span data-stu-id="ceaee-172">The preceding line of code formats the value for `Grades.Average()` as a floating-point number with two decimal places.</span></span>

<span data-ttu-id="ceaee-173">通常，可能需要使用特定区域性设置生成的字符串的格式。</span><span class="sxs-lookup"><span data-stu-id="ceaee-173">Often, you may need to format the string produced using a specific culture.</span></span> <span data-ttu-id="ceaee-174">请利用通过字符串内插生成的对象可以隐式转换为 <xref:System.FormattableString?displayProperty=nameWithType> 这一事实。</span><span class="sxs-lookup"><span data-stu-id="ceaee-174">You use the fact that the object produced by a string interpolation can be implicitly converted to <xref:System.FormattableString?displayProperty=nameWithType>.</span></span> <span data-ttu-id="ceaee-175"><xref:System.FormattableString> 实例包含组合格式字符串，以及在将其转换为字符串之前评估表达式的结果。</span><span class="sxs-lookup"><span data-stu-id="ceaee-175">The <xref:System.FormattableString> instance contains the composite format string and the results of evaluating the expressions before converting them to strings.</span></span> <span data-ttu-id="ceaee-176">在设置字符串的格式时，可以使用 <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> 方法指定区域性。</span><span class="sxs-lookup"><span data-stu-id="ceaee-176">Use the <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> method to specify the culture when formatting a string.</span></span> <span data-ttu-id="ceaee-177">下面的示例使用德语 (de-DE) 区域性生成字符串。</span><span class="sxs-lookup"><span data-stu-id="ceaee-177">The following example produces a string using the German (de-DE) culture.</span></span> <span data-ttu-id="ceaee-178">（德语区域性默认使用“,”字符作为小数分隔符，使用“.”字符作为千位分隔符。）</span><span class="sxs-lookup"><span data-stu-id="ceaee-178">(By default, the German culture uses the ',' character for the decimal separator, and the '.' character as the thousands separator.)</span></span>

```csharp
FormattableString str = $"Average grade is {s.Grades.Average()}";
var gradeStr = str.ToString(new System.Globalization.CultureInfo("de-DE"));
```

<span data-ttu-id="ceaee-179">要开始使用字符串内插，请参阅 [C# 中的字符串内插](../tutorials/exploration/interpolated-strings.yml)交互式教程、[字符串内插](../language-reference/tokens/interpolated.md)一文和 [C# 中字符串内插](../tutorials/string-interpolation.md)教程。</span><span class="sxs-lookup"><span data-stu-id="ceaee-179">To get started with string interpolation, see the [String interpolation in C#](../tutorials/exploration/interpolated-strings.yml) interactive tutorial, the [String interpolation](../language-reference/tokens/interpolated.md) article, and the [String interpolation in C#](../tutorials/string-interpolation.md) tutorial.</span></span>

## <a name="exception-filters"></a><span data-ttu-id="ceaee-180">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="ceaee-180">Exception filters</span></span>

<span data-ttu-id="ceaee-181">“异常筛选器”是确定何时应该应用给定的 catch 子句的子句  。</span><span class="sxs-lookup"><span data-stu-id="ceaee-181">*Exception Filters* are clauses that determine when a given catch clause should be applied.</span></span> <span data-ttu-id="ceaee-182">如果用于异常筛选器的表达式计算结果为 `true`，则 catch 子句将对异常执行正常处理。</span><span class="sxs-lookup"><span data-stu-id="ceaee-182">If the expression used for an exception filter evaluates to `true`, the catch clause performs its normal processing on an exception.</span></span> <span data-ttu-id="ceaee-183">如果表达式计算结果为 `false`，则将跳过 `catch` 子句。</span><span class="sxs-lookup"><span data-stu-id="ceaee-183">If the expression evaluates to `false`, then the `catch` clause is skipped.</span></span> <span data-ttu-id="ceaee-184">一种用途是检查有关异常的信息，以确定 `catch` 子句是否可以处理该异常：</span><span class="sxs-lookup"><span data-stu-id="ceaee-184">One use is to examine information about an exception to determine if a `catch` clause can process the exception:</span></span>

[!code-csharp[ExceptionFilter](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#ExceptionFilter)]

## <a name="the-nameof-expression"></a><span data-ttu-id="ceaee-185">`nameof` 表达式</span><span class="sxs-lookup"><span data-stu-id="ceaee-185">The `nameof` expression</span></span>

<span data-ttu-id="ceaee-186">[nameof](../language-reference/operators/nameof.md) 表达式的计算结果为符号的名称。</span><span class="sxs-lookup"><span data-stu-id="ceaee-186">The [nameof](../language-reference/operators/nameof.md) expression evaluates to the name of a symbol.</span></span> <span data-ttu-id="ceaee-187">每当需要变量、属性或成员字段的名称时，这是让工具正常运行的好办法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-187">It's a great way to get tools working whenever you need the name of a variable, a property, or a member field.</span></span> <span data-ttu-id="ceaee-188">`nameof` 的其中一个最常见的用途是提供引起异常的符号的名称：</span><span class="sxs-lookup"><span data-stu-id="ceaee-188">One of the most common uses for `nameof` is to provide the name of a symbol that caused an exception:</span></span>

[!code-csharp[nameof](../../../samples/snippets/csharp/new-in-6/NewCode.cs#UsingStaticString)]

<span data-ttu-id="ceaee-189">另一个用途是用于实现 `INotifyPropertyChanged` 接口的基于 XAML 的应用程序：</span><span class="sxs-lookup"><span data-stu-id="ceaee-189">Another use is with XAML-based applications that implement the `INotifyPropertyChanged` interface:</span></span>

[!code-csharp[nameofNotify](../../../samples/snippets/csharp/new-in-6/viewmodel.cs#nameofNotify)]

## <a name="await-in-catch-and-finally-blocks"></a><span data-ttu-id="ceaee-190">Catch 和 Finally 块中的 Await</span><span class="sxs-lookup"><span data-stu-id="ceaee-190">Await in Catch and Finally blocks</span></span>

<span data-ttu-id="ceaee-191">C# 5 对于可放置 `await` 表达式的位置有若干限制。</span><span class="sxs-lookup"><span data-stu-id="ceaee-191">C# 5 had several limitations around where you could place `await` expressions.</span></span> <span data-ttu-id="ceaee-192">使用 C# 6，现在可以在 `catch` 或 `finally` 表达式中使用 `await`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-192">With C# 6, you can now use `await` in `catch` or `finally` expressions.</span></span> <span data-ttu-id="ceaee-193">这通常用于日志记录方案：</span><span class="sxs-lookup"><span data-stu-id="ceaee-193">This is most often used with logging scenarios:</span></span>

[!code-csharp[AwaitFinally](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#AwaitFinally)]

<span data-ttu-id="ceaee-194">在 `catch` 和 `finally` 子句中添加 `await` 支持的实现细节可确保该行为与同步代码的行为一致。</span><span class="sxs-lookup"><span data-stu-id="ceaee-194">The implementation details for adding `await` support inside `catch` and `finally` clauses ensure that the behavior is consistent with the behavior for synchronous code.</span></span> <span data-ttu-id="ceaee-195">当在 `catch` 或 `finally` 子句中执行的代码引发异常时，执行将在下一个外层块中查找合适的 `catch` 子句。</span><span class="sxs-lookup"><span data-stu-id="ceaee-195">When code executed in a `catch` or `finally` clause throws, execution looks for a suitable `catch` clause in the next surrounding block.</span></span> <span data-ttu-id="ceaee-196">如果存在当前异常，则该异常将丢失。</span><span class="sxs-lookup"><span data-stu-id="ceaee-196">If there was a current exception, that exception is lost.</span></span> <span data-ttu-id="ceaee-197">`catch` 和 `finally` 子句中的 awaited 表达式也会发生同样的情况：搜索合适的 `catch`，并且当前异常（如果有）将丢失。</span><span class="sxs-lookup"><span data-stu-id="ceaee-197">The same happens with awaited expressions in `catch` and `finally` clauses: a suitable `catch` is searched for, and the current exception, if any, is lost.</span></span>  

> [!NOTE]
> <span data-ttu-id="ceaee-198">鉴于此行为，建议仔细编写 `catch` 和 `finally` 子句，避免引入新的异常。</span><span class="sxs-lookup"><span data-stu-id="ceaee-198">This behavior is the reason it's recommended to write `catch` and `finally` clauses carefully, to avoid introducing new exceptions.</span></span>

## <a name="initialize-associative-collections-using-indexers"></a><span data-ttu-id="ceaee-199">使用索引器初始化关联集合</span><span class="sxs-lookup"><span data-stu-id="ceaee-199">Initialize associative collections using indexers</span></span>

<span data-ttu-id="ceaee-200">索引初始值设定项  是提高集合初始值设定项与索引用途一致性的两个功能之一。</span><span class="sxs-lookup"><span data-stu-id="ceaee-200">*Index Initializers* is one of two features that make collection initializers more consistent with index usage.</span></span> <span data-ttu-id="ceaee-201">在早期版本的 C# 中，可以将集合初始值设定项用于序列样式集合，包括在键值对周围添加括号而得到 <xref:System.Collections.Generic.Dictionary%602>：</span><span class="sxs-lookup"><span data-stu-id="ceaee-201">In earlier releases of C#, you could use *collection initializers* with sequence style collections, including <xref:System.Collections.Generic.Dictionary%602>, by adding braces around key and value pairs:</span></span>

[!code-csharp[ListInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#CollectionInitializer)]

<span data-ttu-id="ceaee-202">可以将集合初始值设定项与 <xref:System.Collections.Generic.Dictionary%602> 集合和其他类型一起使用，在这种情况下，可访问的 `Add` 方法接受多个参数。</span><span class="sxs-lookup"><span data-stu-id="ceaee-202">You can use them with <xref:System.Collections.Generic.Dictionary%602> collections and other types where the accessible `Add` method accepts more than one argument.</span></span> <span data-ttu-id="ceaee-203">新语法支持使用索引分配到集合中：</span><span class="sxs-lookup"><span data-stu-id="ceaee-203">The new syntax supports assignment using an index into the collection:</span></span>

[!code-csharp[DictionaryInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#DictionaryInitializer)]

<span data-ttu-id="ceaee-204">此功能意味着，可以使用与多个版本中已有的序列容器语法类似的语法初始化关联容器。</span><span class="sxs-lookup"><span data-stu-id="ceaee-204">This feature means that associative containers can be initialized using syntax similar to what's been in place for sequence containers for several versions.</span></span>

## <a name="extension-add-methods-in-collection-initializers"></a><span data-ttu-id="ceaee-205">集合初始值设定项中的扩展 `Add` 方法</span><span class="sxs-lookup"><span data-stu-id="ceaee-205">Extension `Add` methods in collection initializers</span></span>

<span data-ttu-id="ceaee-206">使集合初始化更容易的另一个功能是对 `Add` 方法使用扩展方法。</span><span class="sxs-lookup"><span data-stu-id="ceaee-206">Another feature that makes collection initialization easier is the ability to use an *extension method* for the `Add` method.</span></span> <span data-ttu-id="ceaee-207">添加此功能的目的是进行 Visual Basic 的奇偶校验。</span><span class="sxs-lookup"><span data-stu-id="ceaee-207">This feature was added for parity with Visual Basic.</span></span> <span data-ttu-id="ceaee-208">如果自定义集合类的方法具有通过语义方式添加新项的名称，则此功能非常有用。</span><span class="sxs-lookup"><span data-stu-id="ceaee-208">The feature is most useful when you have a custom collection class that has a method with a different name to semantically add new items.</span></span>

## <a name="improved-overload-resolution"></a><span data-ttu-id="ceaee-209">改进了重载解析</span><span class="sxs-lookup"><span data-stu-id="ceaee-209">Improved overload resolution</span></span>

<span data-ttu-id="ceaee-210">你可能不会注意到这最后一项功能。</span><span class="sxs-lookup"><span data-stu-id="ceaee-210">This last feature is one you probably won't notice.</span></span> <span data-ttu-id="ceaee-211">在以前的一些构造中，以前版本的 C# 编译器可能会发现涉及 lambda 表达式的一些方法不明确。</span><span class="sxs-lookup"><span data-stu-id="ceaee-211">There were constructs where the previous version of the C# compiler may have found some method calls involving lambda expressions ambiguous.</span></span> <span data-ttu-id="ceaee-212">请考虑此方法：</span><span class="sxs-lookup"><span data-stu-id="ceaee-212">Consider this method:</span></span>

[!code-csharp[AsyncMethod](../../../samples/snippets/csharp/new-in-6/overloads.cs#AsyncMethod)]

<span data-ttu-id="ceaee-213">在早期版本的 C# 中，使用方法组语法调用该方法将失败：</span><span class="sxs-lookup"><span data-stu-id="ceaee-213">In earlier versions of C#, calling that method using the method group syntax would fail:</span></span>

[!code-csharp[MethodGroup](../../../samples/snippets/csharp/new-in-6/overloads.cs#MethodGroup)]

<span data-ttu-id="ceaee-214">早期的编译器无法正确区分 `Task.Run(Action)` 和 `Task.Run(Func<Task>())`。</span><span class="sxs-lookup"><span data-stu-id="ceaee-214">The earlier compiler couldn't distinguish correctly between `Task.Run(Action)` and `Task.Run(Func<Task>())`.</span></span> <span data-ttu-id="ceaee-215">在早期版本中，需要使用 lambda 表达式作为参数：</span><span class="sxs-lookup"><span data-stu-id="ceaee-215">In previous versions, you'd need to use a lambda expression as an argument:</span></span>

[!code-csharp[Lambda](../../../samples/snippets/csharp/new-in-6/overloads.cs#Lambda)]

<span data-ttu-id="ceaee-216">C# 6 编译器正确地确定 `Task.Run(Func<Task>())` 是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="ceaee-216">The C# 6 compiler correctly determines that `Task.Run(Func<Task>())` is a better choice.</span></span>

### <a name="deterministic-compiler-output"></a><span data-ttu-id="ceaee-217">确定性的编译器选项</span><span class="sxs-lookup"><span data-stu-id="ceaee-217">Deterministic compiler output</span></span>

<span data-ttu-id="ceaee-218">`-deterministic` 选项指示编译器为同一源文件的后续编译生成完全相同的输出程序集。</span><span class="sxs-lookup"><span data-stu-id="ceaee-218">The `-deterministic` option instructs the compiler to produce a byte-for-byte identical output assembly for successive compilations of the same source files.</span></span>

<span data-ttu-id="ceaee-219">默认情况下，每个编译都生成唯一的输出内容。</span><span class="sxs-lookup"><span data-stu-id="ceaee-219">By default, every compilation produces unique output on each compilation.</span></span> <span data-ttu-id="ceaee-220">编译器添加一个时间戳和一个随机生成的 GUID。</span><span class="sxs-lookup"><span data-stu-id="ceaee-220">The compiler adds a timestamp, and a GUID generated from random numbers.</span></span> <span data-ttu-id="ceaee-221">如果想按字节比较输出以确保各项生成之间的一致性，请使用此选项。</span><span class="sxs-lookup"><span data-stu-id="ceaee-221">You use this option if you want to compare the byte-for-byte output to ensure consistency across builds.</span></span>

<span data-ttu-id="ceaee-222">有关详细信息，请参阅 [-deterministic 编译器选项](../language-reference/compiler-options/deterministic-compiler-option.md)文章。</span><span class="sxs-lookup"><span data-stu-id="ceaee-222">For more information, see the [-deterministic compiler option](../language-reference/compiler-options/deterministic-compiler-option.md) article.</span></span>
