---
title: C# 保留的特性：可为空的静态分析
ms.date: 04/14/2020
description: 编译器会解释这些属性，以便为可为 null 和不可为 null 的引用类型提供更好的静态分析。
ms.openlocfilehash: 6678cd21de23d4ed391eff089e33939b5adff0fa
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955598"
---
# <a name="reserved-attributes-contribute-to-the-compilers-null-state-static-analysis"></a><span data-ttu-id="b5ba5-103">保留的特性有助于编译器的 null 状态静态分析</span><span class="sxs-lookup"><span data-stu-id="b5ba5-103">Reserved attributes contribute to the compiler's null state static analysis</span></span>

<span data-ttu-id="b5ba5-104">在可为 null 的上下文中，编译器对代码执行静态分析，以确定所有引用类型变量的 null 状态：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-104">In a nullable context, the compiler performs static analysis of code to determine the null state of all reference type variables:</span></span>

- <span data-ttu-id="b5ba5-105">非 null：静态分析确定将变量分配给非 null 值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-105">*not null*: Static analysis determines that a variable is assigned a non-null value.</span></span>
- <span data-ttu-id="b5ba5-106">可能为 null  ：静态分析无法确定为变量分配非 null 值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-106">*maybe null*: Static analysis cannot determine that a variable is assigned a non-null value.</span></span>

<span data-ttu-id="b5ba5-107">可以应用多个特性，以向编译器提供有关 API 语义的信息。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-107">You can apply a number of attributes that provide information to the compiler about the semantics of your APIs.</span></span> <span data-ttu-id="b5ba5-108">这些信息有助于编译器执行静态分析并确定变量何时不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-108">That information helps the compiler perform static analysis and determine when a variable is not null.</span></span> <span data-ttu-id="b5ba5-109">本文提供每个特性的简要说明以及它们的使用方法。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-109">This article provides a brief description of each of those attributes and how to use them.</span></span> <span data-ttu-id="b5ba5-110">所有示例都假设使用 C# 8.0 或更高版本，并且代码处于可为 null 的上下文中。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-110">All the examples assume C# 8.0 or newer, and the code is in a nullable context.</span></span>

<span data-ttu-id="b5ba5-111">首先，让我们看一个熟悉的示例。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-111">Let's start with a familiar example.</span></span> <span data-ttu-id="b5ba5-112">假设你的库具有以下用于检索资源字符串的 API：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-112">Imagine your library has the following API to retrieve a resource string:</span></span>

```csharp
bool TryGetMessage(string key, out string message)
```

<span data-ttu-id="b5ba5-113">前面的示例遵循 .NET 中熟悉的 `Try*` 模式。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-113">The preceding example follows the familiar `Try*` pattern in .NET.</span></span> <span data-ttu-id="b5ba5-114">此 API 有两个引用参数：`key` 和 `message` 参数。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-114">There are two reference arguments for this API: the `key` and the `message` parameter.</span></span> <span data-ttu-id="b5ba5-115">此 API 具有与这些参数的是否为 null 相关的以下规则：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-115">This API has the following rules relating to the nullness of these arguments:</span></span>

- <span data-ttu-id="b5ba5-116">调用方不应将 `null` 作为 `key` 的参数传递。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-116">Callers shouldn't pass `null` as the argument for `key`.</span></span>
- <span data-ttu-id="b5ba5-117">调用方可以传递值为 `null` 的变量作为 `message` 的参数。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-117">Callers can pass a variable whose value is `null` as the argument for `message`.</span></span>
- <span data-ttu-id="b5ba5-118">如果 `TryGetMessage` 方法返回 `true`，则 `message` 的值不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-118">If the `TryGetMessage` method returns `true`, the value of `message` isn't null.</span></span> <span data-ttu-id="b5ba5-119">如果返回值是 `false,`，则 `message`（及其 null 状态）的值为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-119">If the return value is `false,` the value of `message` (and its null state) is null.</span></span>

<span data-ttu-id="b5ba5-120">`key` 的规则可以用变量类型表示：`key` 应是不可为 null 的引用类型。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-120">The rule for `key` can be expressed by the variable type: `key` should be a non-nullable reference type.</span></span> <span data-ttu-id="b5ba5-121">`message` 参数更复杂。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-121">The `message` parameter is more complex.</span></span> <span data-ttu-id="b5ba5-122">它允许 `null` 作为参数，但保证成功时，`out` 参数不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-122">It allows `null` as the argument, but guarantees that, on success, that `out` argument isn't null.</span></span> <span data-ttu-id="b5ba5-123">对于这些情况，需要使用更丰富的词汇来描述期望。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-123">For these scenarios, you need a richer vocabulary to describe the expectations.</span></span>

<span data-ttu-id="b5ba5-124">为表示有关变量的 null 状态的附加信息，已添加多个特性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-124">Several attributes have been added to express additional information about the null state of variables.</span></span> <span data-ttu-id="b5ba5-125">在 C# 8 引入可为 null 的引用类型之前编写的所有代码都是忽略 null 的  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-125">All code you wrote before C# 8 introduced nullable reference types was *null oblivious*.</span></span> <span data-ttu-id="b5ba5-126">这意味着任何引用类型变量都可以为 null，但不需要进行 null 检查。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-126">That means any reference type variable may be null, but null checks aren't required.</span></span> <span data-ttu-id="b5ba5-127">代码“可识别为 null”后，这些规则就会改变  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-127">Once your code is *nullable aware*, those rules change.</span></span> <span data-ttu-id="b5ba5-128">引用类型不应该是 `null` 值，在取消引用之前，必须对照 `null` 检查可为 null 的引用类型。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-128">Reference types should never be the `null` value, and nullable reference types must be checked against `null` before being dereferenced.</span></span>

<span data-ttu-id="b5ba5-129">API 的规则可能更复杂，正如你在 `TryGetValue` API 方案中看到的那样。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-129">The rules for your APIs are likely more complicated, as you saw with the `TryGetValue` API scenario.</span></span> <span data-ttu-id="b5ba5-130">许多 API 对于变量何时可以或不可以为 `null` 有更复杂的规则。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-130">Many of your APIs have more complex rules for when variables can or can't be `null`.</span></span> <span data-ttu-id="b5ba5-131">在这些情况下，可使用以下属性之一来表示这些规则：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-131">In these cases, you'll use one of the following attributes to express those rules:</span></span>

- <span data-ttu-id="b5ba5-132">[AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute)：不可为 null 的输入参数可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-132">[AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute): A non-nullable input argument may be null.</span></span>
- <span data-ttu-id="b5ba5-133">[DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute)：可为 null 的输入参数不应为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-133">[DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute): A nullable input argument should never be null.</span></span>
- <span data-ttu-id="b5ba5-134">[MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute)：不可为 null 的返回值可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-134">[MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute): A non-nullable return value may be null.</span></span>
- <span data-ttu-id="b5ba5-135">[NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute)：可为 null 的返回值永远不会为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-135">[NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute): A nullable return value will never be null.</span></span>
- <span data-ttu-id="b5ba5-136">[MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute)：当方法返回指定的 `bool` 值时，不可为 null 的输入参数可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-136">[MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute): A non-nullable input argument may be null when the method returns the specified `bool` value.</span></span>
- <span data-ttu-id="b5ba5-137">[NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute)：当方法返回指定的 `bool` 值时，可为 null 的输入参数将不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-137">[NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute): A nullable input argument will not be null when the method returns the specified `bool` value.</span></span>
- <span data-ttu-id="b5ba5-138">[NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute)：如果指定参数的参数不为 null，则返回值不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-138">[NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute): A return value isn't null if the argument for the specified parameter isn't null.</span></span>
- <span data-ttu-id="b5ba5-139">[DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute)：方法从不返回。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-139">[DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute): A method never returns.</span></span> <span data-ttu-id="b5ba5-140">换句话说，它总是引发异常。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-140">In other words, it always throws an exception.</span></span>
- <span data-ttu-id="b5ba5-141">[DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute)：如果关联的 `bool` 参数具有指定值，则此方法永远不会返回。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-141">[DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute): This method never returns if the associated `bool` parameter has the specified value.</span></span>

<span data-ttu-id="b5ba5-142">上述说明是对每个特性的快速参考。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-142">The preceding descriptions are a quick reference to what each attribute does.</span></span> <span data-ttu-id="b5ba5-143">以下各节介绍了行为和含义。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-143">Each following section describes the behavior and meaning more thoroughly.</span></span>

<span data-ttu-id="b5ba5-144">添加这些特性将为编译器提供有关 API 规则的更多信息。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-144">Adding these attributes gives the compiler more information about the rules for your API.</span></span> <span data-ttu-id="b5ba5-145">当调用代码在可为 null 的上下文中编译时，编译器将在调用方违反这些规则时发出警告。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-145">When calling code is compiled in a nullable enabled context, the compiler will warn callers when they violate those rules.</span></span> <span data-ttu-id="b5ba5-146">这些特性不会对实现启用其他检查。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-146">These attributes don't enable additional checks on your implementation.</span></span>

## <a name="specify-preconditions-allownull-and-disallownull"></a><span data-ttu-id="b5ba5-147">指定前提条件：`AllowNull` 和 `DisallowNull`</span><span class="sxs-lookup"><span data-stu-id="b5ba5-147">Specify preconditions: `AllowNull` and `DisallowNull`</span></span>

<span data-ttu-id="b5ba5-148">请考虑一个从不返回 `null` 的读/写属性，因为它具有合理的默认值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-148">Consider a read/write property that never returns `null` because it has a reasonable default value.</span></span> <span data-ttu-id="b5ba5-149">调用方在将 `null` 设置为该默认值时将其传递给 set 访问器。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-149">Callers pass `null` to the set accessor when setting it to that default value.</span></span> <span data-ttu-id="b5ba5-150">例如，假设一个消息系统要求在聊天室中输入一个屏幕名称。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-150">For example, consider a messaging system that asks for a screen name in a chat room.</span></span> <span data-ttu-id="b5ba5-151">如果未提供任何内容，系统将生成一个随机名称：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-151">If none is provided, the system generates a random name:</span></span>

```csharp
public string ScreenName
{
   get => _screenName;
   set => _screenName = value ?? GenerateRandomScreenName();
}
private string _screenName;
```

<span data-ttu-id="b5ba5-152">当你在忽略可为 null 的上下文中编译前面的代码时，一切都是正常的。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-152">When you compile the preceding code in a nullable oblivious context, everything is fine.</span></span> <span data-ttu-id="b5ba5-153">启用可为 null 的引用类型后，`ScreenName` 属性将成为不可为 null 的引用。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-153">Once you enable nullable reference types, the `ScreenName` property becomes a non-nullable reference.</span></span> <span data-ttu-id="b5ba5-154">这对于 `get` 访问器是正确的：它从不返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-154">That's correct for the `get` accessor: it never returns `null`.</span></span> <span data-ttu-id="b5ba5-155">调用方不需要检查返回的 `null` 属性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-155">Callers don't need to check the returned property for `null`.</span></span> <span data-ttu-id="b5ba5-156">但现在将属性设置为 `null` 将生成警告。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-156">But now setting the property to `null` generates a warning.</span></span> <span data-ttu-id="b5ba5-157">为了继续支持这种类型的代码，请将 <xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute?displayProperty=nameWithType> 特性添加到该属性，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-157">In order to continue to support this type of code, you add the <xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute?displayProperty=nameWithType> attribute to the property, as shown in the following code:</span></span>

```csharp
[AllowNull]
public string ScreenName
{
   get => _screenName;
   set => _screenName = value ?? GenerateRandomScreenName();
}
private string _screenName = GenerateRandomScreenName();
```

<span data-ttu-id="b5ba5-158">可能需要为 <xref:System.Diagnostics.CodeAnalysis> 添加一个 `using` 指令才能使用本文中讨论的特性和其他特性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-158">You may need to add a `using` directive for <xref:System.Diagnostics.CodeAnalysis> to use this and other attributes discussed in this article.</span></span> <span data-ttu-id="b5ba5-159">特性应用于属性，而不是 `set` 访问器。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-159">The attribute is applied to the property, not the `set` accessor.</span></span> <span data-ttu-id="b5ba5-160">`AllowNull` 特性指定前置条件，并且仅适用于输入  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-160">The `AllowNull` attribute specifies *pre-conditions*, and only applies to inputs.</span></span> <span data-ttu-id="b5ba5-161">`get` 访问器有一个返回值，但没有输入参数。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-161">The `get` accessor has a return value, but no input arguments.</span></span> <span data-ttu-id="b5ba5-162">因此，`AllowNull` 特性只适用于 `set` 访问器。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-162">Therefore, the `AllowNull` attribute only applies to the `set` accessor.</span></span>

<span data-ttu-id="b5ba5-163">前面的示例演示了在参数上添加 `AllowNull` 特性时要查找的内容：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-163">The preceding example demonstrates what to look for when adding the `AllowNull` attribute on an argument:</span></span>

1. <span data-ttu-id="b5ba5-164">该变量的一般约定是它不应为 `null`，因此需要一个不可为 null 的引用类型。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-164">The general contract for that variable is that it shouldn't be `null`, so you want a non-nullable reference type.</span></span>
1. <span data-ttu-id="b5ba5-165">虽然输入变量不是最常见的用法，但仍有一些方案需要 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-165">There are scenarios for the input variable to be `null`, though they aren't the most common usage.</span></span>

<span data-ttu-id="b5ba5-166">大多数情况下，属性或 `in`、`out` 和 `ref` 参数需要此特性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-166">Most often you'll need this attribute for properties, or `in`, `out`, and `ref` arguments.</span></span> <span data-ttu-id="b5ba5-167">当变量通常为非 null 时，`AllowNull` 属性是最佳选择，但需要允许 `null` 作为前提条件。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-167">The `AllowNull` attribute is the best choice when a variable is typically non-null, but you need to allow `null` as a precondition.</span></span>

<span data-ttu-id="b5ba5-168">将此情况与使用 `DisallowNull` 方案相比：使用此特性可以指定可为 null 引用类型的输入变量不应为 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-168">Contrast that with scenarios for using `DisallowNull`: You use this attribute to specify that an input variable of a nullable reference type shouldn't be `null`.</span></span> <span data-ttu-id="b5ba5-169">请考虑一个特性，其中 `null` 是默认值，但客户端只能将其设置为非 null 值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-169">Consider a property where `null` is the default value, but clients can only set it to a non-null value.</span></span> <span data-ttu-id="b5ba5-170">考虑下列代码：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-170">Consider the following code:</span></span>

```csharp
public string ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string _comment;
```

<span data-ttu-id="b5ba5-171">前面的代码是表达设计的最佳方式，`ReviewComment` 可以是 `null`，但不能设置为 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-171">The preceding code is the best way to express your design that the `ReviewComment` could be `null`, but can't be set to `null`.</span></span> <span data-ttu-id="b5ba5-172">代码可识别为 null 后，你就可以使用 <xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute?displayProperty=nameWithType> 向调用方更清楚地表达此概念：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-172">Once this code is nullable aware, you can express this concept more clearly to callers using the <xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute?displayProperty=nameWithType>:</span></span>

```csharp
[DisallowNull]
public string? ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string? _comment;
```

<span data-ttu-id="b5ba5-173">在可为 null 的上下文中，`ReviewComment` `get` 访问器可以返回默认值 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-173">In a nullable context, the `ReviewComment` `get` accessor could return the default value of `null`.</span></span> <span data-ttu-id="b5ba5-174">编译器会警告在访问之前必须进行检查。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-174">The compiler warns that it must be checked before access.</span></span> <span data-ttu-id="b5ba5-175">此外，它警告调用方，即使它可能是 `null`，调用方也不应显式地将其设置为 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-175">Furthermore, it warns callers that, even though it could be `null`, callers shouldn't explicitly set it to `null`.</span></span> <span data-ttu-id="b5ba5-176">`DisallowNull` 特性还指定了前置条件，它不会影响 `get` 访问器  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-176">The `DisallowNull` attribute also specifies a *pre-condition*, it does not affect the `get` accessor.</span></span> <span data-ttu-id="b5ba5-177">当你观察到以下特征时，可以使用 `DisallowNull` 特性：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-177">You use the `DisallowNull` attribute when you observe these characteristics about:</span></span>

1. <span data-ttu-id="b5ba5-178">在核心方案中（通常是在首次实例化时），变量可以是 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-178">The variable could be `null` in core scenarios, often when first instantiated.</span></span>
1. <span data-ttu-id="b5ba5-179">变量不应显式设置为 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-179">The variable shouldn't be explicitly set to `null`.</span></span>

<span data-ttu-id="b5ba5-180">这些情况在忽略 null 的代码中很常见  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-180">These situations are common in code that was originally *null oblivious*.</span></span> <span data-ttu-id="b5ba5-181">可能是在两个不同的初始化操作中设置了对象属性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-181">It may be that object properties are set in two distinct initialization operations.</span></span> <span data-ttu-id="b5ba5-182">可能只有在某些异步工作完成后才能设置某些属性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-182">It may be that some properties are set only after some asynchronous work has completed.</span></span>

<span data-ttu-id="b5ba5-183">可使用 `AllowNull` 和 `DisallowNull` 特性指定变量上的前置条件可能与这些变量上的可为 null 注释不匹配。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-183">The `AllowNull` and `DisallowNull` attributes enable you to specify that preconditions on variables may not match the nullable annotations on those variables.</span></span> <span data-ttu-id="b5ba5-184">这两个特性提供了关于 API 特征的更多细节。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-184">These provide more detail about the characteristics of your API.</span></span> <span data-ttu-id="b5ba5-185">此附加信息有助于调用方正确使用 API。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-185">This additional information helps callers use your API correctly.</span></span> <span data-ttu-id="b5ba5-186">请记住，可使用以下特性指定前提条件：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-186">Remember you specify preconditions using the following attributes:</span></span>

- <span data-ttu-id="b5ba5-187">[AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute)：不可为 null 的输入参数可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-187">[AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute): A non-nullable input argument may be null.</span></span>
- <span data-ttu-id="b5ba5-188">[DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute)：可为 null 的输入参数不应为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-188">[DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute): A nullable input argument should never be null.</span></span>

## <a name="specify-post-conditions-maybenull-and-notnull"></a><span data-ttu-id="b5ba5-189">指定后置条件：`MaybeNull` 和 `NotNull`</span><span class="sxs-lookup"><span data-stu-id="b5ba5-189">Specify post-conditions: `MaybeNull` and `NotNull`</span></span>

<span data-ttu-id="b5ba5-190">假设你有使用以下签名的方法：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-190">Suppose you have a method with the following signature:</span></span>

```csharp
public Customer FindCustomer(string lastName, string firstName)
```

<span data-ttu-id="b5ba5-191">你可能已经编写了类似的方法，以便在未找到所查找的名称时返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-191">You've likely written a method like this to return `null` when the name sought wasn't found.</span></span> <span data-ttu-id="b5ba5-192">`null` 清楚地表明未找到记录。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-192">The `null` clearly indicates that the record wasn't found.</span></span> <span data-ttu-id="b5ba5-193">在本例中，你可能会将返回类型从 `Customer` 更改为 `Customer?`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-193">In this example, you'd likely change the return type from `Customer` to `Customer?`.</span></span> <span data-ttu-id="b5ba5-194">将返回值声明为可为 null 的引用类型可以清楚地指定此 API 的意图。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-194">Declaring the return value as a nullable reference type specifies the intent of this API clearly.</span></span>

<span data-ttu-id="b5ba5-195">基于[泛型定义和为 null 性](../../nullable-migration-strategies.md#generic-definitions-and-nullability)中所述的原因，该技术不适用于泛型方法。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-195">For reasons covered under [Generic definitions and nullability](../../nullable-migration-strategies.md#generic-definitions-and-nullability) that technique does not work with generic methods.</span></span> <span data-ttu-id="b5ba5-196">你可能具有遵循类似模式的泛型方法：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-196">You may have a generic method that follows a similar pattern:</span></span>

```csharp
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> predicate)
```

<span data-ttu-id="b5ba5-197">不能指定返回值为 `T?`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-197">You can't specify that the return value is `T?`.</span></span> <span data-ttu-id="b5ba5-198">当找不到所需项时，此方法返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-198">The method returns `null` when the sought item isn't found.</span></span> <span data-ttu-id="b5ba5-199">由于无法声明 `T?` 返回类型，因此需要将 `MaybeNull` 注释添加到方法返回：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-199">Since you can't declare a `T?` return type, you add the `MaybeNull` annotation to the method return:</span></span>

```csharp
[return: MaybeNull]
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> predicate)
```

<span data-ttu-id="b5ba5-200">前面的代码通知调用方，协定暗示了一个不可为 null 的类型，但是返回值可能实际上为 null  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-200">The preceding code informs callers that the contract implies a non-nullable type, but the return value *may* actually be null.</span></span>  <span data-ttu-id="b5ba5-201">当 API 应为不可为 null 的类型（通常是泛型类型参数）时，请使用 `MaybeNull` 特性，但可能会有返回 `null` 的情况。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-201">Use the `MaybeNull` attribute when your API should be a non-nullable type, typically a generic type parameter, but there may be instances where `null` would be returned.</span></span>

<span data-ttu-id="b5ba5-202">还可以指定返回值或者 `out` 或 `ref` 参数不为 null，即使该类型是可为 null 的引用类型。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-202">You can also specify that a return value or an `out` or `ref` argument isn't null even though the type is a nullable reference type.</span></span> <span data-ttu-id="b5ba5-203">请考虑一种确保数组足以容纳多个元素的方法。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-203">Consider a method that ensures an array is large enough to hold a number of elements.</span></span> <span data-ttu-id="b5ba5-204">如果输入参数没有容量，例程将分配新数组并将所有现有元素复制到其中。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-204">If the input argument doesn't have capacity, the routine would allocate a new array and copy all the existing elements into it.</span></span> <span data-ttu-id="b5ba5-205">如果输入参数是 `null`，则例程将分配新存储。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-205">If the input argument is `null`, the routine would allocate new storage.</span></span> <span data-ttu-id="b5ba5-206">如果有足够的容量，例程将不执行任何操作：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-206">If there's sufficient capacity, the routine does nothing:</span></span>

```csharp
public void EnsureCapacity<T>(ref T[] storage, int size)
```

<span data-ttu-id="b5ba5-207">可以按如下方式调用此例程：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-207">You could call this routine as follows:</span></span>

```csharp
// messages has the default value (null) when EnsureCapacity is called:
EnsureCapacity<string>(ref messages, 10);
// messages is not null.
EnsureCapacity<string>(messages, 50);
```

<span data-ttu-id="b5ba5-208">启用 null 引用类型后，需要确保前面的代码在编译时没有警告。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-208">After enabling null reference types, you want to ensure that the preceding code compiles without warnings.</span></span> <span data-ttu-id="b5ba5-209">当方法返回时，`storage` 参数保证不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-209">When the method returns, the `storage` argument is guaranteed to be not null.</span></span> <span data-ttu-id="b5ba5-210">但是，可以使用 null 引用调用 `EnsureCapacity`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-210">However, it's acceptable to call `EnsureCapacity` with a null reference.</span></span> <span data-ttu-id="b5ba5-211">可以将 `storage` 设为可为 null 的引用类型，并将 `NotNull` 后置条件添加到参数声明中：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-211">You can make `storage` a nullable reference type, and add the `NotNull` post-condition to the parameter declaration:</span></span>

```csharp
public void EnsureCapacity<T>([NotNull] ref T[]? storage, int size)
```

<span data-ttu-id="b5ba5-212">前面的代码清楚地表达了现有协定：调用方可以传递具有 `null` 值的变量，但返回值保证永远不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-212">The preceding code expresses the existing contract clearly: Callers can pass a variable with the `null` value, but the return value is guaranteed to never be null.</span></span> <span data-ttu-id="b5ba5-213">`NotNull` 特性对于 `ref` 和 `out` 参数最有用，其中 `null` 可以作为参数传递，但当方法返回时，该参数保证不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-213">The `NotNull` attribute is most useful for `ref` and `out` arguments where `null` may be passed as an argument, but that argument is guaranteed to be not null when the method returns.</span></span>

<span data-ttu-id="b5ba5-214">可以使用以下特性指定无条件后置条件：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-214">You specify unconditional postconditions using the following attributes:</span></span>

- <span data-ttu-id="b5ba5-215">[MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute)：不可为 null 的返回值可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-215">[MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute): A non-nullable return value may be null.</span></span>
- <span data-ttu-id="b5ba5-216">[NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute)：可为 null 的返回值永远不会为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-216">[NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute): A nullable return value will never be null.</span></span>

## <a name="specify-conditional-post-conditions-notnullwhen-maybenullwhen-and-notnullifnotnull"></a><span data-ttu-id="b5ba5-217">指定有条件后置条件：`NotNullWhen`、`MaybeNullWhen` 和 `NotNullIfNotNull`</span><span class="sxs-lookup"><span data-stu-id="b5ba5-217">Specify conditional post-conditions: `NotNullWhen`, `MaybeNullWhen`, and `NotNullIfNotNull`</span></span>

<span data-ttu-id="b5ba5-218">你可能很熟悉 `string` 方法 <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-218">You're likely familiar with the `string` method <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType>.</span></span> <span data-ttu-id="b5ba5-219">当参数为 null 或为空字符串时，此方法返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-219">This method returns `true` when the argument is null or an empty string.</span></span> <span data-ttu-id="b5ba5-220">这是一种 null 检查格式：如果方法返回 `false`，调用方不需要 null 检查参数。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-220">It's a form of null-check: Callers don't need to null-check the argument if the method returns `false`.</span></span> <span data-ttu-id="b5ba5-221">若要使这样的方法可识别为 null，需要将参数设置为可为 null 的引用类型，并添加 `NotNullWhen` 特性：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-221">To make a method like this nullable aware, you'd set the argument to a nullable reference type, and add the `NotNullWhen` attribute:</span></span>

```csharp
bool IsNullOrEmpty([NotNullWhen(false)] string? value);
```

<span data-ttu-id="b5ba5-222">该特性通知编译器返回值为 `false` 的任何代码都不需要进行 null 检查。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-222">That informs the compiler that any code where the return value is `false` need not be null-checked.</span></span> <span data-ttu-id="b5ba5-223">添加特性通知编译器的静态分析，`IsNullOrEmpty` 执行必要的 null 检查：当它返回 `false` 时，输入参数不是 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-223">The addition of the attribute informs the compiler's static analysis that `IsNullOrEmpty` performs the necessary null check: when it returns `false`, the input argument is not `null`.</span></span>

```csharp
string? userInput = GetUserInput();
if (!string.IsNullOrEmpty(userInput))
{
   int messageLength = userInput.Length; // no null check needed.
}
// null check needed on userInput here.
```

<span data-ttu-id="b5ba5-224">对于 .NET Core 3.0，将对 <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType> 方法进行注释，如上面所示。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-224">The <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType> method will be annotated as shown above for .NET Core 3.0.</span></span> <span data-ttu-id="b5ba5-225">代码库中可能有类似的方法来检查对象的状态是否为 null 值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-225">You may have similar methods in your codebase that check the state of objects for null values.</span></span> <span data-ttu-id="b5ba5-226">编译器无法识别自定义的 null 检查方法，你需要自己添加注释。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-226">The compiler won't recognize custom null check methods, and you'll need to add the annotations yourself.</span></span> <span data-ttu-id="b5ba5-227">添加特性时，编译器的静态分析将知道何时对测试变量进行了 null 检查。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-227">When you add the attribute, the compiler's static analysis knows when the tested variable has been null checked.</span></span>

<span data-ttu-id="b5ba5-228">这些特性的另一个用途是 `Try*` 模式。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-228">Another use for these attributes is the `Try*` pattern.</span></span> <span data-ttu-id="b5ba5-229">`ref` 和 `out` 变量的后置条件通过返回值进行通信。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-229">The postconditions for `ref` and `out` variables are communicated through the return value.</span></span> <span data-ttu-id="b5ba5-230">请考虑前面所示的方法：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-230">Consider this method shown earlier:</span></span>

```csharp
bool TryGetMessage(string key, out string message)
```

<span data-ttu-id="b5ba5-231">前面的方法遵循典型的 .NET 习惯用法：返回值指示是否将 `message` 设置为已找到的值，或者，如果未找到消息，则为默认值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-231">The preceding method follows a typical .NET idiom: the return value indicates if `message` was set to the found value or, if no message is found, to the default value.</span></span> <span data-ttu-id="b5ba5-232">如果方法返回 `true`，`message` 的值不为 null；否则，该方法将 `message` 设置为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-232">If the method returns `true`, the value of `message` isn't null; otherwise, the method sets `message` to null.</span></span>

<span data-ttu-id="b5ba5-233">你可以使用 `NotNullWhen` 特性来传达这个习惯用法。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-233">You can communicate that idiom using the `NotNullWhen` attribute.</span></span> <span data-ttu-id="b5ba5-234">更新可为 null 的引用类型的签名时，需要将 `message` 设为 `string?` 并添加一个特性：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-234">When you update the signature for nullable reference types, make `message` a `string?` and add an attribute:</span></span>

```csharp
bool TryGetMessage(string key, [NotNullWhen(true)] out string? message)
```

<span data-ttu-id="b5ba5-235">在前面的示例中，`message` 的值在 `TryGetMessage` 返回 `true` 时不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-235">In the preceding example, the value of `message` is known to be not null when `TryGetMessage` returns `true`.</span></span> <span data-ttu-id="b5ba5-236">你应以相同的方式在代码库中注释类似的方法：参数可以是 `null`，并且已知在方法返回 `true` 时不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-236">You should annotate similar methods in your codebase in the same way: the arguments could be `null`, and are known to be not null when the method returns `true`.</span></span>

<span data-ttu-id="b5ba5-237">还可能需要一个最终特性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-237">There's one final attribute you may also need.</span></span> <span data-ttu-id="b5ba5-238">有时，返回值的 null 状态取决于一个或多个输入参数的 null 状态。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-238">Sometimes the null state of a return value depends on the null state of one or more input arguments.</span></span> <span data-ttu-id="b5ba5-239">当某些输入参数不是 `null` 时，这些方法将返回非 null 值。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-239">These methods will return a non-null value whenever certain input arguments aren't `null`.</span></span> <span data-ttu-id="b5ba5-240">若要正确地注释这些方法，可以使用 `NotNullIfNotNull` 特性。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-240">To correctly annotate these methods, you use the `NotNullIfNotNull` attribute.</span></span> <span data-ttu-id="b5ba5-241">请考虑以下方法：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-241">Consider the following method:</span></span>

```csharp
string GetTopLevelDomainFromFullUrl(string url);
```

<span data-ttu-id="b5ba5-242">如果 `url` 参数不为 null，则输出不是 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-242">If the `url` argument isn't null, the output isn't `null`.</span></span> <span data-ttu-id="b5ba5-243">启用可为 null 的引用后，只要 API 永不接受 null 输入，该签名就能正常运行。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-243">Once nullable references are enabled, that signature works correctly, provided your API never accepts a null input.</span></span> <span data-ttu-id="b5ba5-244">但是，如果输入可以为 null，那么返回值也可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-244">However, if the input could be null, then return value could also be null.</span></span> <span data-ttu-id="b5ba5-245">因此，你可以将签名更改为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-245">Therefore, you could change the signature to the following code:</span></span>

```csharp
string? GetTopLevelDomainFromFullUrl(string? url);
```

<span data-ttu-id="b5ba5-246">这也是可行的，但通常会强制调用方实现额外的 `null` 检查。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-246">That also works, but will often force callers to implement extra `null` checks.</span></span> <span data-ttu-id="b5ba5-247">协定是，只有当输入参数 `url` 是 `null` 时，返回值才会是 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-247">The contract is that the return value would be `null` only when the input argument `url` is `null`.</span></span> <span data-ttu-id="b5ba5-248">若要表达该协定，你需要注释此方法，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-248">To express that contract, you would annotate this method as shown in the following code:</span></span>

```csharp
[return: NotNullIfNotNull("url")]
string? GetTopLevelDomainFromFullUrl(string? url);
```

<span data-ttu-id="b5ba5-249">返回值和参数都用 `?` 进行了注释，这表明两者都可以是 `null`。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-249">The return value and the argument have both been annotated with the `?` indicating that either could be `null`.</span></span> <span data-ttu-id="b5ba5-250">该特性进一步阐明了当 `url` 参数不是 `null` 时，返回值不会为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-250">The attribute further clarifies that the return value won't be null when the `url` argument isn't `null`.</span></span>

<span data-ttu-id="b5ba5-251">可以使用以下特性指定条件的后置条件：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-251">You specify conditional postconditions using these attributes:</span></span>

- <span data-ttu-id="b5ba5-252">[MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute)：当方法返回指定的 `bool` 值时，不可为 null 的输入参数可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-252">[MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute): A non-nullable input argument may be null when the method returns the specified `bool` value.</span></span>
- <span data-ttu-id="b5ba5-253">[NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute)：当方法返回指定的 `bool` 值时，可为 null 的输入参数将不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-253">[NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute): A nullable input argument will not be null when the method returns the specified `bool` value.</span></span>
- <span data-ttu-id="b5ba5-254">[NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute)：如果指定参数的输入参数不为 null，则返回值不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-254">[NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute): A return value isn't null if the input argument for the specified parameter isn't null.</span></span>

## <a name="verify-unreachable-code"></a><span data-ttu-id="b5ba5-255">验证无法访问的代码</span><span class="sxs-lookup"><span data-stu-id="b5ba5-255">Verify unreachable code</span></span>

<span data-ttu-id="b5ba5-256">某些方法（通常是异常帮助程序或其他实用工具方法）始终通过引发异常来退出。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-256">Some methods, typically exception helpers or other utility methods, always exit by throwing an exception.</span></span> <span data-ttu-id="b5ba5-257">或者，帮助程序可以基于布尔参数的值引发异常。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-257">Or, a helper may throw an exception based on the value of a Boolean argument.</span></span>

<span data-ttu-id="b5ba5-258">在第一种情况下，可以将 `DoesNotReturn` 特性添加到方法声明中。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-258">In the first case, you can add the `DoesNotReturn` attribute to the method declaration.</span></span> <span data-ttu-id="b5ba5-259">编译器通过三种方式为你提供帮助。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-259">The compiler helps you in three ways.</span></span> <span data-ttu-id="b5ba5-260">首先，如果存在方法可以退出而不引发异常的路径，编译器将发出警告。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-260">First, the compiler issues a warning if there is a path where the method can exit without throwing an exception.</span></span> <span data-ttu-id="b5ba5-261">其次，编译器会将调用该方法后的任何代码标记为不可访问，直到遇到适当的 `catch` 子句  。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-261">Second, the compiler marks any code after a call to that method as *unreachable*, until an appropriate `catch` clause is encountered.</span></span> <span data-ttu-id="b5ba5-262">第三，无法访问的代码不会影响任何 null 状态。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-262">Third, the unreachable code won't affect any null states.</span></span> <span data-ttu-id="b5ba5-263">请考虑此方法：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-263">Consider this method:</span></span>

```csharp
[DoesNotReturn]
private void FailFast()
{
    throw new InvalidOperationException();
}

public void SetState(object containedField)
{
    if (!isInitialized)
    {
        FailFast();
    }

    // unreachable code:
    _field = containedField;
}
```

<span data-ttu-id="b5ba5-264">在第二种情况下，需将 `DoesNotReturnIf` 特性添加到方法的布尔参数中。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-264">In the second case, you add the `DoesNotReturnIf` attribute to a Boolean parameter of the method.</span></span> <span data-ttu-id="b5ba5-265">你可以修改前面的示例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-265">You can modify the previous example as follows:</span></span>

```csharp
private void FailFast([DoesNotReturnIf(false)] bool isValid)
{
    if (!isValid)
    {
        throw new InvalidOperationException();
    }
}

public void SetState(object containedField)
{
    FailFast(isInitialized);

    // unreachable code when "isInitialized" is false:
    _field = containedField;
}
```

## <a name="summary"></a><span data-ttu-id="b5ba5-266">总结</span><span class="sxs-lookup"><span data-stu-id="b5ba5-266">Summary</span></span>

[!INCLUDE [C# version alert](../../includes/csharp-version-alert.md)]

<span data-ttu-id="b5ba5-267">添加可为 null 的引用类型提供了一个初始词汇表，用于描述 API 对可能为 `null` 的变量的期望。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-267">Adding nullable reference types provides an initial vocabulary to describe your APIs expectations for variables that could be `null`.</span></span> <span data-ttu-id="b5ba5-268">其他特性使用更丰富的词汇表来描述变量作为前置条件和后置条件的 null 状态。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-268">The additional attributes provide a richer vocabulary to describe the null state of variables as preconditions and postconditions.</span></span> <span data-ttu-id="b5ba5-269">这些特性更清楚地描述了你的期望，并为使用 API 的开发人员提供了更好的体验。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-269">These attributes more clearly describe your expectations and provide a better experience for the developers using your APIs.</span></span>

<span data-ttu-id="b5ba5-270">在为可为 null 的上下文中更新库时，添加这些特性可指导用户正确使用 API。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-270">As you update libraries for a nullable context, add these attributes to guide users of your APIs to the correct usage.</span></span> <span data-ttu-id="b5ba5-271">这些特性有助于你完全描述输入参数和返回值的 null 状态：</span><span class="sxs-lookup"><span data-stu-id="b5ba5-271">These attributes help you fully describe the null-state of input arguments and return values:</span></span>

- <span data-ttu-id="b5ba5-272">[AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute)：不可为 null 的输入参数可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-272">[AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute): A non-nullable input argument may be null.</span></span>
- <span data-ttu-id="b5ba5-273">[DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute)：可为 null 的输入参数不应为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-273">[DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute): A nullable input argument should never be null.</span></span>
- <span data-ttu-id="b5ba5-274">[MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute)：不可为 null 的返回值可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-274">[MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute): A non-nullable return value may be null.</span></span>
- <span data-ttu-id="b5ba5-275">[NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute)：可为 null 的返回值永远不会为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-275">[NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute): A nullable return value will never be null.</span></span>
- <span data-ttu-id="b5ba5-276">[MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute)：当方法返回指定的 `bool` 值时，不可为 null 的输入参数可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-276">[MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute): A non-nullable input argument may be null when the method returns the specified `bool` value.</span></span>
- <span data-ttu-id="b5ba5-277">[NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute)：当方法返回指定的 `bool` 值时，可为 null 的输入参数将不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-277">[NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute): A nullable input argument will not be null when the method returns the specified `bool` value.</span></span>
- <span data-ttu-id="b5ba5-278">[NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute)：如果指定参数的输入参数不为 null，则返回值不为 null。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-278">[NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute): A return value isn't null if the input argument for the specified parameter isn't null.</span></span>
- <span data-ttu-id="b5ba5-279">[DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute)：方法从不返回。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-279">[DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute): A method never returns.</span></span> <span data-ttu-id="b5ba5-280">换句话说，它总是引发异常。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-280">In other words, it always throws an exception.</span></span>
- <span data-ttu-id="b5ba5-281">[DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute)：如果关联的 `bool` 参数具有指定值，则此方法永远不会返回。</span><span class="sxs-lookup"><span data-stu-id="b5ba5-281">[DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute): This method never returns if the associated `bool` parameter has the specified value.</span></span>
