---
title: 实现 DisposeAsync 方法
description: 了解如何实现 DisposeAsync 和 DisposeAsyncCore 方法来执行异步资源清理。
author: IEvangelist
ms.author: dapine
ms.date: 10/26/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
helpviewer_keywords:
- DisposeAsync method
- garbage collection, DisposeAsync method
ms.openlocfilehash: 5aa82c507c22a4795f39267ac8f435599fb9cd92
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687724"
---
# <a name="implement-a-disposeasync-method"></a><span data-ttu-id="a5a90-103">实现 DisposeAsync 方法</span><span class="sxs-lookup"><span data-stu-id="a5a90-103">Implement a DisposeAsync method</span></span>

<span data-ttu-id="a5a90-104">已将 <xref:System.IAsyncDisposable?displayProperty=nameWithType> 接口作为 C# 8.0 的一部分引入。</span><span class="sxs-lookup"><span data-stu-id="a5a90-104">The <xref:System.IAsyncDisposable?displayProperty=nameWithType> interface was introduced as part of C# 8.0.</span></span> <span data-ttu-id="a5a90-105">需要执行资源清理时，可以实现 <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> 方法，就像[实现 Dispose 方法](implementing-dispose.md)一样。</span><span class="sxs-lookup"><span data-stu-id="a5a90-105">You implement the <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> method when you need to perform resource cleanup, just as you would when [implementing a Dispose method](implementing-dispose.md).</span></span> <span data-ttu-id="a5a90-106">但是，其中一个主要区别是，此实现允许异步清理操作。</span><span class="sxs-lookup"><span data-stu-id="a5a90-106">One of the key differences however, is that this implementation allows for asynchronous cleanup operations.</span></span> <span data-ttu-id="a5a90-107"><xref:System.IAsyncDisposable.DisposeAsync> 返回表示异步释放操作的 <xref:System.Threading.Tasks.ValueTask>。</span><span class="sxs-lookup"><span data-stu-id="a5a90-107">The <xref:System.IAsyncDisposable.DisposeAsync> returns a <xref:System.Threading.Tasks.ValueTask> that represents the asynchronous dispose operation.</span></span>

<span data-ttu-id="a5a90-108">通常，当实现 <xref:System.IAsyncDisposable> 接口时，类还将实现 <xref:System.IDisposable> 接口。</span><span class="sxs-lookup"><span data-stu-id="a5a90-108">It is typical when implementing the <xref:System.IAsyncDisposable> interface that classes will also implement the <xref:System.IDisposable> interface.</span></span> <span data-ttu-id="a5a90-109"><xref:System.IAsyncDisposable> 接口的一种良好实现模式是为同步或异步释放做好准备。</span><span class="sxs-lookup"><span data-stu-id="a5a90-109">A good implementation pattern of the <xref:System.IAsyncDisposable> interface is to be prepared for either synchronous or asynchronous dispose.</span></span> <span data-ttu-id="a5a90-110">用于实现释放模式的所有指南也适用于异步实现。</span><span class="sxs-lookup"><span data-stu-id="a5a90-110">All of the guidance for implementing the dispose pattern also applies to the asynchronous implementation.</span></span> <span data-ttu-id="a5a90-111">本文假设你已熟悉如何[实现 Dispose 方法](implementing-dispose.md)。</span><span class="sxs-lookup"><span data-stu-id="a5a90-111">This article assumes that you're already familiar with how to [implement a Dispose method](implementing-dispose.md).</span></span>

## <a name="disposeasync-and-disposeasynccore"></a><span data-ttu-id="a5a90-112">DisposeAsync() 和 DisposeAsyncCore()</span><span class="sxs-lookup"><span data-stu-id="a5a90-112">DisposeAsync() and DisposeAsyncCore()</span></span>

<span data-ttu-id="a5a90-113"><xref:System.IAsyncDisposable> 接口声明单个无参数方法 <xref:System.IAsyncDisposable.DisposeAsync>。</span><span class="sxs-lookup"><span data-stu-id="a5a90-113">The <xref:System.IAsyncDisposable> interface declares a single parameterless method, <xref:System.IAsyncDisposable.DisposeAsync>.</span></span> <span data-ttu-id="a5a90-114">任何非密封类都应具有另外一个也返回 <xref:System.Threading.Tasks.ValueTask> 的 `DisposeAsyncCore()` 方法。</span><span class="sxs-lookup"><span data-stu-id="a5a90-114">Any non-sealed class should have an additional `DisposeAsyncCore()` method that also returns a <xref:System.Threading.Tasks.ValueTask>.</span></span>

- <span data-ttu-id="a5a90-115">没有参数的 `public` <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> 实现。</span><span class="sxs-lookup"><span data-stu-id="a5a90-115">A `public` <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> implementation that has no parameters.</span></span>
- <span data-ttu-id="a5a90-116">一个 `protected virtual ValueTask DisposeAsyncCore()` 方法，其签名为：</span><span class="sxs-lookup"><span data-stu-id="a5a90-116">A `protected virtual ValueTask DisposeAsyncCore()` method whose signature is:</span></span>

  ```csharp
  protected virtual ValueTask DisposeAsyncCore()
  {
  }
  ```

### <a name="the-disposeasync-method"></a><span data-ttu-id="a5a90-117">DisposeAsync() 方法</span><span class="sxs-lookup"><span data-stu-id="a5a90-117">The DisposeAsync() method</span></span>

<span data-ttu-id="a5a90-118">`public` 无参数的 `DisposeAsync()` 方法在 `await using` 语句中隐式调用，其用途是释放非托管资源，执行常规清理，以及指示终结器（如果存在）不必运行。</span><span class="sxs-lookup"><span data-stu-id="a5a90-118">The `public` parameterless `DisposeAsync()` method is called implicitly in an `await using` statement, and its purpose is to free unmanaged resources, perform general cleanup, and to indicate that the finalizer, if one is present, need not run.</span></span> <span data-ttu-id="a5a90-119">释放与托管对象关联的内存始终是[垃圾回收器](index.md)的域。</span><span class="sxs-lookup"><span data-stu-id="a5a90-119">Freeing the memory associated with a managed object is always the domain of the [garbage collector](index.md).</span></span> <span data-ttu-id="a5a90-120">因此，它具有标准实现：</span><span class="sxs-lookup"><span data-stu-id="a5a90-120">Because of this, it has a standard implementation:</span></span>

```csharp
public async ValueTask DisposeAsync()
{
    // Perform async cleanup.
    await DisposeAsyncCore();

    // Dispose of unmanaged resources.
    Dispose(false);
    // Suppress finalization.
    GC.SuppressFinalize(this);
}
```

> [!NOTE]
> <span data-ttu-id="a5a90-121">与释放模式相比，异步释放模式的主要差异在于，从 <xref:System.IAsyncDisposable.DisposeAsync> 到 `Dispose(bool)` 重载方法的调用被赋予 `false` 作为参数。</span><span class="sxs-lookup"><span data-stu-id="a5a90-121">One primary difference in the async dispose pattern compared to the dispose pattern, is that the call from <xref:System.IAsyncDisposable.DisposeAsync> to the `Dispose(bool)` overload method is given `false` as an argument.</span></span> <span data-ttu-id="a5a90-122">但实现 <xref:System.IDisposable.Dispose?displayProperty=nameWithType> 方法时，改为传递 `true`。</span><span class="sxs-lookup"><span data-stu-id="a5a90-122">When implementing the <xref:System.IDisposable.Dispose?displayProperty=nameWithType> method, however, `true` is passed instead.</span></span> <span data-ttu-id="a5a90-123">这有助于确保与同步释放模式的功能等效性，并进一步确保仍调用终结器代码路径。</span><span class="sxs-lookup"><span data-stu-id="a5a90-123">This helps ensure functional equivalence with the synchronous dispose pattern, and further ensures that finalizer code paths still get invoked.</span></span> <span data-ttu-id="a5a90-124">换句话说，`DisposeAsyncCore()` 方法将异步释放托管资源，因此不希望也同步释放这些资源。</span><span class="sxs-lookup"><span data-stu-id="a5a90-124">In other words, the `DisposeAsyncCore()` method will dispose of managed resources asynchronously, so you don't want to dispose of them synchronously as well.</span></span> <span data-ttu-id="a5a90-125">因此，调用 `Dispose(false)` 而非 `Dispose(true)`。</span><span class="sxs-lookup"><span data-stu-id="a5a90-125">Therefore, call `Dispose(false)` instead of `Dispose(true)`.</span></span>

### <a name="the-disposeasynccore-method"></a><span data-ttu-id="a5a90-126">DisposeAsyncCore() 方法</span><span class="sxs-lookup"><span data-stu-id="a5a90-126">The DisposeAsyncCore() method</span></span>

<span data-ttu-id="a5a90-127">`DisposeAsyncCore()` 方法旨在执行受管理资源的异步清理，或对 `DisposeAsync()` 执行级联调用。</span><span class="sxs-lookup"><span data-stu-id="a5a90-127">The `DisposeAsyncCore()` method is intended to perform the asynchronous cleanup of managed resources or for cascading calls to `DisposeAsync()`.</span></span> <span data-ttu-id="a5a90-128">当子类继承作为 <xref:System.IAsyncDisposable> 的实现的基类时，它会封装常见的异步清理操作。</span><span class="sxs-lookup"><span data-stu-id="a5a90-128">It encapsulates the common asynchronous cleanup operations when a subclass inherits a base class that is an implementation of <xref:System.IAsyncDisposable>.</span></span> <span data-ttu-id="a5a90-129">`DisposeAsyncCore()` 方法是 `virtual`，以便派生类可以在其重写中定义其他清理。</span><span class="sxs-lookup"><span data-stu-id="a5a90-129">The `DisposeAsyncCore()` method is `virtual` so that derived classes can define additional cleanup in their overrides.</span></span>

> [!TIP]
> <span data-ttu-id="a5a90-130">如果 <xref:System.IAsyncDisposable> 的实现是 `sealed`，则不需要 `DisposeAsyncCore()` 方法，异步清理可直接在 <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> 方法中执行。</span><span class="sxs-lookup"><span data-stu-id="a5a90-130">If an implementation of <xref:System.IAsyncDisposable> is `sealed`, the `DisposeAsyncCore()` method is not needed, and the asynchronous cleanup can be performed directly in the <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> method.</span></span>

## <a name="implement-the-async-dispose-pattern"></a><span data-ttu-id="a5a90-131">实现异步释放模式</span><span class="sxs-lookup"><span data-stu-id="a5a90-131">Implement the async dispose pattern</span></span>

<span data-ttu-id="a5a90-132">所有非密封类都应被视为潜在的基类，因为它们可以被继承。</span><span class="sxs-lookup"><span data-stu-id="a5a90-132">All non-sealed classes should be considered a potential base class, because they could be inherited.</span></span> <span data-ttu-id="a5a90-133">如果为任何潜在基类实现异步释放模式，则必须提供 `protected virtual ValueTask DisposeAsyncCore()` 方法。</span><span class="sxs-lookup"><span data-stu-id="a5a90-133">If you implement the async dispose pattern for any potential base class, you must provide the `protected virtual ValueTask DisposeAsyncCore()` method.</span></span> <span data-ttu-id="a5a90-134">下面是使用 <xref:System.Text.Json.Utf8JsonWriter?displayProperty=nameWithType> 的异步释放模式的实现示例。</span><span class="sxs-lookup"><span data-stu-id="a5a90-134">Here is an example implementation of the async dispose pattern that uses a <xref:System.Text.Json.Utf8JsonWriter?displayProperty=nameWithType>.</span></span>

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/disposeasync.cs":::

<span data-ttu-id="a5a90-135">前面的示例使用 <xref:System.Text.Json.Utf8JsonWriter>。</span><span class="sxs-lookup"><span data-stu-id="a5a90-135">The preceding example uses the <xref:System.Text.Json.Utf8JsonWriter>.</span></span> <span data-ttu-id="a5a90-136">有关 `System.Text.Json` 的详细信息，请参阅[如何从 Newtonsoft.Json 迁移到 System.Text.Json](../serialization/system-text-json-migrate-from-newtonsoft-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="a5a90-136">For more information about `System.Text.Json`, see [How to migrate from Newtonsoft.Json to System.Text.Json](../serialization/system-text-json-migrate-from-newtonsoft-how-to.md).</span></span>

## <a name="implement-both-dispose-and-async-dispose-patterns"></a><span data-ttu-id="a5a90-137">同时实现释放模式和异步释放模式</span><span class="sxs-lookup"><span data-stu-id="a5a90-137">Implement both dispose and async dispose patterns</span></span>

<span data-ttu-id="a5a90-138">可能需要同时实现 <xref:System.IDisposable> 和 <xref:System.IAsyncDisposable> 接口，尤其是当类范围包含这些实现的实例时。</span><span class="sxs-lookup"><span data-stu-id="a5a90-138">You may need to implement both the <xref:System.IDisposable> and <xref:System.IAsyncDisposable> interfaces, especially when your class scope contains instances of these implementations.</span></span> <span data-ttu-id="a5a90-139">这样做可确保你可以正确地级联清理调用。</span><span class="sxs-lookup"><span data-stu-id="a5a90-139">Doing so ensures that you can properly cascade clean up calls.</span></span> <span data-ttu-id="a5a90-140">下面是一个示例类，它实现两个接口并演示清理的正确指导。</span><span class="sxs-lookup"><span data-stu-id="a5a90-140">Here is an example class that implements both interfaces and demonstrates the proper guidance for cleanup.</span></span>

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/dispose-and-disposeasync.cs":::

<span data-ttu-id="a5a90-141"><xref:System.IDisposable.Dispose?displayProperty=nameWithType> 和 <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> 实现都是简单的样板代码。</span><span class="sxs-lookup"><span data-stu-id="a5a90-141">The <xref:System.IDisposable.Dispose?displayProperty=nameWithType> and <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> implementations are both simple boilerplate code.</span></span>

<span data-ttu-id="a5a90-142">在 `Dispose(bool)` 重载方法中，如果 <xref:System.IDisposable> 实例不为 `null`，则有条件地将其释放。</span><span class="sxs-lookup"><span data-stu-id="a5a90-142">In the `Dispose(bool)` overload method, the <xref:System.IDisposable> instance is conditionally disposed of if it is not `null`.</span></span> <span data-ttu-id="a5a90-143"><xref:System.IAsyncDisposable> 实例被强制转换为 <xref:System.IDisposable>，如果该实例也不为 `null`，也将被释放。</span><span class="sxs-lookup"><span data-stu-id="a5a90-143">The <xref:System.IAsyncDisposable> instance is cast as <xref:System.IDisposable>, and if it is also not `null`, it is disposed of as well.</span></span> <span data-ttu-id="a5a90-144">然后，将这两个实例都分配给 `null`。</span><span class="sxs-lookup"><span data-stu-id="a5a90-144">Both instances are then assigned to `null`.</span></span>

<span data-ttu-id="a5a90-145">使用 `DisposeAsyncCore()` 方法时，遵循相同的逻辑方法。</span><span class="sxs-lookup"><span data-stu-id="a5a90-145">With the `DisposeAsyncCore()` method, the same logical approach is followed.</span></span> <span data-ttu-id="a5a90-146">如果 <xref:System.IAsyncDisposable> 实例不为 `null`，则等待其对 `DisposeAsync().ConfigureAwait(false)` 的调用。</span><span class="sxs-lookup"><span data-stu-id="a5a90-146">If the <xref:System.IAsyncDisposable> instance is not `null`, its call to `DisposeAsync().ConfigureAwait(false)` is awaited.</span></span> <span data-ttu-id="a5a90-147">如果 <xref:System.IDisposable> 实例也是 <xref:System.IAsyncDisposable> 的实现，也将其异步释放。</span><span class="sxs-lookup"><span data-stu-id="a5a90-147">If the <xref:System.IDisposable> instance is also an implementation of <xref:System.IAsyncDisposable>, it's also disposed of asynchronously.</span></span> <span data-ttu-id="a5a90-148">然后，将这两个实例都分配给 `null`。</span><span class="sxs-lookup"><span data-stu-id="a5a90-148">Both instances are then assigned to `null`.</span></span>

## <a name="using-async-disposable"></a><span data-ttu-id="a5a90-149">使用异步释放</span><span class="sxs-lookup"><span data-stu-id="a5a90-149">Using async disposable</span></span>

<span data-ttu-id="a5a90-150">要正确使用实现 <xref:System.IAsyncDisposable> 接口的对象，请将 [await](../../csharp/language-reference/operators/await.md)和 [using](../../csharp/language-reference/keywords/using-statement.md) 关键字结合使用。</span><span class="sxs-lookup"><span data-stu-id="a5a90-150">To properly consume an object that implements the <xref:System.IAsyncDisposable> interface, you use the [await](../../csharp/language-reference/operators/await.md) and [using](../../csharp/language-reference/keywords/using-statement.md) keywords together.</span></span> <span data-ttu-id="a5a90-151">请考虑以下示例，其中 `ExampleAsyncDisposable` 类进行了实例化，然后包装在 `await using` 语句中。</span><span class="sxs-lookup"><span data-stu-id="a5a90-151">Consider the following example, where the `ExampleAsyncDisposable` class is instantiated and then wrapped in an `await using` statement.</span></span>

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/proper-await-using.cs":::

> [!IMPORTANT]
> <span data-ttu-id="a5a90-152">使用 <xref:System.IAsyncDisposable> 接口的 <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)> 扩展方法配置延续任务在其原始上下文或计划程序上的封送方式。</span><span class="sxs-lookup"><span data-stu-id="a5a90-152">Use the <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)> extension method of the <xref:System.IAsyncDisposable> interface to configure how the continuation of the task is marshalled on its original context or scheduler.</span></span> <span data-ttu-id="a5a90-153">有关 `ConfigureAwait` 的详细信息，请参阅 [ConfigureAwait FAQ](https://devblogs.microsoft.com/dotnet/configureawait-faq/)。</span><span class="sxs-lookup"><span data-stu-id="a5a90-153">For more information on `ConfigureAwait`, see [ConfigureAwait FAQ](https://devblogs.microsoft.com/dotnet/configureawait-faq/).</span></span>

<span data-ttu-id="a5a90-154">对于不需要使用 `ConfigureAwait` 的情况，可以按如下所示简化 `await using` 语句：</span><span class="sxs-lookup"><span data-stu-id="a5a90-154">For situations where the usage of `ConfigureAwait` is not needed, the `await using` statement could be simplified as follows:</span></span>

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-non-configureawait.cs":::

<span data-ttu-id="a5a90-155">此外，它还可以编写为使用 [using 声明](../../csharp/whats-new/csharp-8.md#using-declarations)的隐式范围。</span><span class="sxs-lookup"><span data-stu-id="a5a90-155">Furthermore, it could be written to use the implicit scoping of a [using declaration](../../csharp/whats-new/csharp-8.md#using-declarations).</span></span>

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-declaration.cs":::

## <a name="stacked-usings"></a><span data-ttu-id="a5a90-156">堆叠的 using</span><span class="sxs-lookup"><span data-stu-id="a5a90-156">Stacked usings</span></span>

<span data-ttu-id="a5a90-157">在创建和使用实现 <xref:System.IAsyncDisposable> 的多个对象的情况下，残存错误条件中具有 <xref:System.Threading.Tasks.ValueTask.ConfigureAwait%2A> 的堆叠 `await using` 语句可能会阻止调用 <xref:System.IAsyncDisposable.DisposeAsync>。</span><span class="sxs-lookup"><span data-stu-id="a5a90-157">In situations where you create and use multiple objects that implement <xref:System.IAsyncDisposable>, it's possible that stacking `await using` statements with <xref:System.Threading.Tasks.ValueTask.ConfigureAwait%2A> could prevent calls to <xref:System.IAsyncDisposable.DisposeAsync> in errant conditions.</span></span> <span data-ttu-id="a5a90-158">若要确保始终调用 <xref:System.IAsyncDisposable.DisposeAsync>，应避免堆叠。</span><span class="sxs-lookup"><span data-stu-id="a5a90-158">To ensure that <xref:System.IAsyncDisposable.DisposeAsync> is always called, you should avoid stacking.</span></span> <span data-ttu-id="a5a90-159">下面的三个代码示例显示要改用的可接受模式。</span><span class="sxs-lookup"><span data-stu-id="a5a90-159">The following three code examples show acceptable patterns to use instead.</span></span>

### <a name="acceptable-pattern-one"></a><span data-ttu-id="a5a90-160">可接受的模式一</span><span class="sxs-lookup"><span data-stu-id="a5a90-160">Acceptable pattern one</span></span>

:::code language="csharp" id="one" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

<span data-ttu-id="a5a90-161">在前面的示例中，每个异步清理操作的范围都显式地限定在 `await using` 块下。</span><span class="sxs-lookup"><span data-stu-id="a5a90-161">In the preceding example, each asynchronous clean up operation is explicitly scoped under the `await using` block.</span></span> <span data-ttu-id="a5a90-162">外部范围由 `objOne` 设置其大括号的方法来定义；若将 `objTwo` 括起来，这样就会先处理 `objTwo`，然后处理 `objOne`。</span><span class="sxs-lookup"><span data-stu-id="a5a90-162">The outer scope is defined by how `objOne` sets its braces, enclosing `objTwo`, as such `objTwo` is disposed first, followed by `objOne`.</span></span> <span data-ttu-id="a5a90-163">这两个 `IAsyncDisposable` 实例都使三种 <xref:System.IAsyncDisposable.DisposeAsync> 方法等待，从而执行其异步清理操作。</span><span class="sxs-lookup"><span data-stu-id="a5a90-163">Both `IAsyncDisposable` instances have there <xref:System.IAsyncDisposable.DisposeAsync> methods awaited, thus performing its asynchronous clean up operation.</span></span> <span data-ttu-id="a5a90-164">嵌套调用，而不是堆叠调用。</span><span class="sxs-lookup"><span data-stu-id="a5a90-164">The calls are nested, not stacked.</span></span>

### <a name="acceptable-pattern-two"></a><span data-ttu-id="a5a90-165">可接受的模式二</span><span class="sxs-lookup"><span data-stu-id="a5a90-165">Acceptable pattern two</span></span>

:::code language="csharp" id="two" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

<span data-ttu-id="a5a90-166">在前面的示例中，每个异步清理操作的范围都显式地限定在 `await using` 块下。</span><span class="sxs-lookup"><span data-stu-id="a5a90-166">In the preceding example, each asynchronous clean up operation is explicitly scoped under the `await using` block.</span></span> <span data-ttu-id="a5a90-167">在每个块的末尾，相应的 `IAsyncDisposable` 实例使其 <xref:System.IAsyncDisposable.DisposeAsync> 方法等待，从而执行其异步清理操作。</span><span class="sxs-lookup"><span data-stu-id="a5a90-167">At the end of each block, the corresponding `IAsyncDisposable` instance has its <xref:System.IAsyncDisposable.DisposeAsync> method awaited, thus performing its asynchronous clean up operation.</span></span> <span data-ttu-id="a5a90-168">按顺序排列调用，而不是堆叠调用。</span><span class="sxs-lookup"><span data-stu-id="a5a90-168">The calls are sequential, not stacked.</span></span> <span data-ttu-id="a5a90-169">在此场景中，首先处理 `objOne`，然后处理 `objTwo`。</span><span class="sxs-lookup"><span data-stu-id="a5a90-169">In this scenario `objOne` is disposed first, then `objTwo` is disposed.</span></span>

### <a name="acceptable-pattern-three"></a><span data-ttu-id="a5a90-170">可接受的模式三</span><span class="sxs-lookup"><span data-stu-id="a5a90-170">Acceptable pattern three</span></span>

:::code language="csharp" id="three" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

<span data-ttu-id="a5a90-171">在前面的示例中，每个异步清理操作都通过包含的方法主体隐式限定了范围。</span><span class="sxs-lookup"><span data-stu-id="a5a90-171">In the preceding example, each asynchronous clean up operation is implicitly scoped with the containing method body.</span></span> <span data-ttu-id="a5a90-172">在封闭块的末尾，`IAsyncDisposable` 实例执行其异步清理操作。</span><span class="sxs-lookup"><span data-stu-id="a5a90-172">At the end of the enclosing block, the `IAsyncDisposable` instances perform their asynchronous clean up operations.</span></span> <span data-ttu-id="a5a90-173">此运行顺序与它们声明的顺序相反，这意味着 `objTwo` 在 `objOne` 之前被处理。</span><span class="sxs-lookup"><span data-stu-id="a5a90-173">This runs in reverse order from which they were declared, meaning that `objTwo` is disposed before `objOne`.</span></span>

### <a name="unacceptable-pattern"></a><span data-ttu-id="a5a90-174">无法接受的模式</span><span class="sxs-lookup"><span data-stu-id="a5a90-174">Unacceptable pattern</span></span>

<span data-ttu-id="a5a90-175">如果从 `AnotherAsyncDisposable` 构造函数引发异常，则 `objOne` 不会得到正确处理：</span><span class="sxs-lookup"><span data-stu-id="a5a90-175">If an exception is thrown from the `AnotherAsyncDisposable` constructor, then `objOne` does not get properly disposed:</span></span>

:::code language="csharp" id="dontdothis" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

> [!TIP]
> <span data-ttu-id="a5a90-176">避免此模式，因为它可能导致意外行为。</span><span class="sxs-lookup"><span data-stu-id="a5a90-176">Avoid this pattern as it could lead to unexpected behavior.</span></span>

## <a name="see-also"></a><span data-ttu-id="a5a90-177">请参阅</span><span class="sxs-lookup"><span data-stu-id="a5a90-177">See also</span></span>

- <xref:System.IAsyncDisposable>
- <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)>
