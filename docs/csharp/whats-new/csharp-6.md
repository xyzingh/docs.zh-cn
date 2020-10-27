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
# <a name="whats-new-in-c-6"></a>C# 6 中的新增功能

C# 6.0 版本包含许多可提高开发人员工作效率的功能。 这些功能的总体效果是让你编写的代码更简洁、更具可读性。 该语法不像许多常见做法那样繁琐。 可以更轻松地看出设计意图。 好好了解这些功能可以帮助你提高生产力，编写更具可读性的代码。 你可以更专注于功能，而不是语言的构造。

本文的其余部分是对每个功能的概述，并提供用于探索每个功能的链接。 还可以在教程部分的 [C# 6 交互式探索](../tutorials/exploration/csharp-6.yml)中探索这些功能。

## <a name="read-only-auto-properties"></a>只读自动属性

只读自动属性  提供了更简洁的语法来创建不可变类型。 你声明仅具有 get 访问器的自动属性：

[!code-csharp[ReadOnlyAutoProperty](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoProperty)]

`FirstName` 和 `LastName` 属性只能在同一个类的构造函数的主体中设置：

[!code-csharp[ReadOnlyAutoPropertyConstructor](../../../samples/snippets/csharp/new-in-6/newcode.cs#ReadOnlyAutoPropertyConstructor)]

尝试在另一种方法中设置 `LastName` 会生成 `CS0200` 编译错误：

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

此功能实现用于创建不可变类型的真正语言支持且使用更简洁和方便的自动属性语法。

如果添加此语法不会删除可访问的方法，则为[二进制兼容的更改](version-update-considerations.md#binary-compatible-changes)。

## <a name="auto-property-initializers"></a>自动属性初始化表达式

自动属性初始值设定项  可让你在属性声明中声明自动属性的初始值。

[!code-csharp[Initialization](../../../samples/snippets/csharp/new-in-6/newcode.cs#Initialization)]

`Grades` 成员在声明它的位置处被初始化。 这样，就能更容易地仅执行一次初始化。 初始化是属性声明的一部分，可更轻松地将存储分配等同于 `Student` 对象的公用接口。

## <a name="expression-bodied-function-members"></a>Expression-bodied 函数成员

你编写的许多成员是可以作为单个表达式的单个语句。 改为编写 expression-bodied 成员。 这适用于方法和只读属性。 例如，重写 `ToString()` 通常是理想之选：

[!code-csharp[ToStringExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#ToStringExpressionMember)]

也可以将此语法用于只读属性：

[!code-csharp[FullNameExpressionMember](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

将现有成员更改为 expression bodied 成员是[二进制兼容的更改](version-update-considerations.md#binary-compatible-changes)。

## <a name="using-static"></a>using static

using static  增强功能可用于导入单个类的静态方法。 指定要使用的类：

[!code-csharp[UsingStaticMath](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStaticMath)]

<xref:System.Math> 不包含任何实例方法。 还可以使用 `using static` 为具有静态和实例方法的类导入类的静态方法。 最有用的示例之一是 <xref:System.String>：

[!code-csharp[UsingStatic](../../../samples/snippets/csharp/new-in-6/newcode.cs#UsingStatic)]

> [!NOTE]
> 在 static using 语句中必须使用完全限定的类名 `System.String`。  而不能使用 `string` 关键字。

从 `static using` 语句导入时，仅在使用扩展方法调用语法调用扩展方法时，扩展方法才在范围内。 作为静态方法调用时，扩展方法不在范围内。 你在 LINQ 查询中会经常看到这种情况。 可以通过导入 <xref:System.Linq.Enumerable> 或 <xref:System.Linq.Queryable> 来导入 LINQ 模式。

[!code-csharp[UsingStaticLinq](../../../samples/snippets/csharp/new-in-6/newcode.cs#usingStaticLinq)]

通常使用扩展方法调用表达式调用扩展方法。 在使用静态方法调用语法对其进行调用的罕见情况下，添加类名称可以解决歧义。

`static using` 指令还可以导入任何嵌套的类型。 可以引用任何嵌套的类型，而无需限定。

## <a name="null-conditional-operators"></a>Null 条件运算符

Null 条件运算符使 null 检查更轻松、更流畅  。 将成员访问 `.` 替换为 `?.`：

[!code-csharp[NullConditional](../../../samples/snippets/csharp/new-in-6/program.cs#NullConditional)]

在前面的示例中，如果 Person 对象是 `null`，则将变量 `first` 赋值为 `null`。 否则，将 `FirstName` 属性的值分配给该变量。 最重要的是，`?.` 意味着当 `person` 变量为 `null` 时，此行代码不会生成 `NullReferenceException`。 它会短路并返回 `null`。 还可以将 null 条件运算符用于数组或索引器访问。 将索引表达式中的 `[]` 替换为 `?[]`。

无论 `person` 的值是什么，以下表达式均返回 `string`。 通常，将此构造与“null 合并”运算符一起使用，以在其中一个属性为 `null` 时分配默认值。 表达式短路时，键入返回的 `null` 值以匹配整个表达式。

[!code-csharp[NullCoalescing](../../../samples/snippets/csharp/new-in-6/program.cs#NullCoalescing)]

还可以将 `?.` 用于有条件地调用方法。 具有 null 条件运算符的成员函数的最常见用法是用于安全地调用可能为 `null` 的委托（或事件处理程序）。  通过使用 `?.` 运算符调用该委托的 `Invoke` 方法来访问成员。 可以在[委托模式](../delegates-patterns.md#handling-null-delegates)一文中看到示例。

`?.` 运算符的规则确保运算符的左侧仅计算一次。 它支持许多语法，包括使用事件处理程序的以下示例：

```csharp
// preferred in C# 6:
this.SomethingHappened?.Invoke(this, eventArgs);
```

确保左侧只计算一次，这使得你可以在 `?.` 的左侧使用任何表达式（包括方法调用）

## <a name="string-interpolation"></a>字符串内插

使用 C# 6，新的[字符串内插](../language-reference/tokens/interpolated.md)功能可以在字符串中嵌入表达式。 使用 `$` 作为字符串的开头，并使用 `{` 和 `}` 之间的表达式代替序号：

[!code-csharp[stringInterpolation](../../../samples/snippets/csharp/new-in-6/newcode.cs#FullNameExpressionMember)]

本示例使用替代表达式的属性。 可以使用任何表达式。 例如，可以在内插过程中计算学生的成绩平均值：

[!code-csharp[stringInterpolationFormat](../../../samples/snippets/csharp/new-in-6/newcode.cs#stringInterpolationFormat)]

上一行代码将 `Grades.Average()` 的值格式设置为具有两位小数的浮点数。

通常，可能需要使用特定区域性设置生成的字符串的格式。 请利用通过字符串内插生成的对象可以隐式转换为 <xref:System.FormattableString?displayProperty=nameWithType> 这一事实。 <xref:System.FormattableString> 实例包含组合格式字符串，以及在将其转换为字符串之前评估表达式的结果。 在设置字符串的格式时，可以使用 <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> 方法指定区域性。 下面的示例使用德语 (de-DE) 区域性生成字符串。 （德语区域性默认使用“,”字符作为小数分隔符，使用“.”字符作为千位分隔符。）

```csharp
FormattableString str = $"Average grade is {s.Grades.Average()}";
var gradeStr = str.ToString(new System.Globalization.CultureInfo("de-DE"));
```

要开始使用字符串内插，请参阅 [C# 中的字符串内插](../tutorials/exploration/interpolated-strings.yml)交互式教程、[字符串内插](../language-reference/tokens/interpolated.md)一文和 [C# 中字符串内插](../tutorials/string-interpolation.md)教程。

## <a name="exception-filters"></a>异常筛选器

“异常筛选器”是确定何时应该应用给定的 catch 子句的子句  。 如果用于异常筛选器的表达式计算结果为 `true`，则 catch 子句将对异常执行正常处理。 如果表达式计算结果为 `false`，则将跳过 `catch` 子句。 一种用途是检查有关异常的信息，以确定 `catch` 子句是否可以处理该异常：

[!code-csharp[ExceptionFilter](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#ExceptionFilter)]

## <a name="the-nameof-expression"></a>`nameof` 表达式

[nameof](../language-reference/operators/nameof.md) 表达式的计算结果为符号的名称。 每当需要变量、属性或成员字段的名称时，这是让工具正常运行的好办法。 `nameof` 的其中一个最常见的用途是提供引起异常的符号的名称：

[!code-csharp[nameof](../../../samples/snippets/csharp/new-in-6/NewCode.cs#UsingStaticString)]

另一个用途是用于实现 `INotifyPropertyChanged` 接口的基于 XAML 的应用程序：

[!code-csharp[nameofNotify](../../../samples/snippets/csharp/new-in-6/viewmodel.cs#nameofNotify)]

## <a name="await-in-catch-and-finally-blocks"></a>Catch 和 Finally 块中的 Await

C# 5 对于可放置 `await` 表达式的位置有若干限制。 使用 C# 6，现在可以在 `catch` 或 `finally` 表达式中使用 `await`。 这通常用于日志记录方案：

[!code-csharp[AwaitFinally](../../../samples/snippets/csharp/new-in-6/NetworkClient.cs#AwaitFinally)]

在 `catch` 和 `finally` 子句中添加 `await` 支持的实现细节可确保该行为与同步代码的行为一致。 当在 `catch` 或 `finally` 子句中执行的代码引发异常时，执行将在下一个外层块中查找合适的 `catch` 子句。 如果存在当前异常，则该异常将丢失。 `catch` 和 `finally` 子句中的 awaited 表达式也会发生同样的情况：搜索合适的 `catch`，并且当前异常（如果有）将丢失。  

> [!NOTE]
> 鉴于此行为，建议仔细编写 `catch` 和 `finally` 子句，避免引入新的异常。

## <a name="initialize-associative-collections-using-indexers"></a>使用索引器初始化关联集合

索引初始值设定项  是提高集合初始值设定项与索引用途一致性的两个功能之一。 在早期版本的 C# 中，可以将集合初始值设定项用于序列样式集合，包括在键值对周围添加括号而得到 <xref:System.Collections.Generic.Dictionary%602>：

[!code-csharp[ListInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#CollectionInitializer)]

可以将集合初始值设定项与 <xref:System.Collections.Generic.Dictionary%602> 集合和其他类型一起使用，在这种情况下，可访问的 `Add` 方法接受多个参数。 新语法支持使用索引分配到集合中：

[!code-csharp[DictionaryInitializer](../../../samples/snippets/csharp/new-in-6/initializers.cs#DictionaryInitializer)]

此功能意味着，可以使用与多个版本中已有的序列容器语法类似的语法初始化关联容器。

## <a name="extension-add-methods-in-collection-initializers"></a>集合初始值设定项中的扩展 `Add` 方法

使集合初始化更容易的另一个功能是对 `Add` 方法使用扩展方法。 添加此功能的目的是进行 Visual Basic 的奇偶校验。 如果自定义集合类的方法具有通过语义方式添加新项的名称，则此功能非常有用。

## <a name="improved-overload-resolution"></a>改进了重载解析

你可能不会注意到这最后一项功能。 在以前的一些构造中，以前版本的 C# 编译器可能会发现涉及 lambda 表达式的一些方法不明确。 请考虑此方法：

[!code-csharp[AsyncMethod](../../../samples/snippets/csharp/new-in-6/overloads.cs#AsyncMethod)]

在早期版本的 C# 中，使用方法组语法调用该方法将失败：

[!code-csharp[MethodGroup](../../../samples/snippets/csharp/new-in-6/overloads.cs#MethodGroup)]

早期的编译器无法正确区分 `Task.Run(Action)` 和 `Task.Run(Func<Task>())`。 在早期版本中，需要使用 lambda 表达式作为参数：

[!code-csharp[Lambda](../../../samples/snippets/csharp/new-in-6/overloads.cs#Lambda)]

C# 6 编译器正确地确定 `Task.Run(Func<Task>())` 是更好的选择。

### <a name="deterministic-compiler-output"></a>确定性的编译器选项

`-deterministic` 选项指示编译器为同一源文件的后续编译生成完全相同的输出程序集。

默认情况下，每个编译都生成唯一的输出内容。 编译器添加一个时间戳和一个随机生成的 GUID。 如果想按字节比较输出以确保各项生成之间的一致性，请使用此选项。

有关详细信息，请参阅 [-deterministic 编译器选项](../language-reference/compiler-options/deterministic-compiler-option.md)文章。
