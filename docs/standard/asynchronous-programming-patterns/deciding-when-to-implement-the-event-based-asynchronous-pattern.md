---
title: 确定何时实现基于事件的异步模式
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET], asynchronous
- AsyncOperationManager class
- threading [.NET], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: a00046aa-785d-4f7f-a8e5-d06475ea50da
ms.openlocfilehash: b9c3edeb468445e6f7a58ead194559bed5636579
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888849"
---
# <a name="deciding-when-to-implement-the-event-based-asynchronous-pattern"></a><span data-ttu-id="f4afe-102">确定何时实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="f4afe-102">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>

<span data-ttu-id="f4afe-103">基于事件的异步模式可用于公开类的异步行为。</span><span class="sxs-lookup"><span data-stu-id="f4afe-103">The Event-based Asynchronous Pattern provides a pattern for exposing the asynchronous behavior of a class.</span></span> <span data-ttu-id="f4afe-104">通过引入此模式，.NET 定义了下面两种用于公开异步行为的模式：基于 <xref:System.IAsyncResult?displayProperty=nameWithType> 接口的异步模式和基于事件的模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-104">With the introduction of this pattern, .NET defines two patterns for exposing asynchronous behavior: the Asynchronous Pattern based on the <xref:System.IAsyncResult?displayProperty=nameWithType> interface, and the event-based pattern.</span></span> <span data-ttu-id="f4afe-105">本文介绍了何时适合实现这两种模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-105">This article describes when it's appropriate for you to implement both patterns.</span></span>

<span data-ttu-id="f4afe-106">若要详细了解如何使用 <xref:System.IAsyncResult> 接口进行异步编程，请参阅[异步编程模型 (APM)](asynchronous-programming-model-apm.md)。</span><span class="sxs-lookup"><span data-stu-id="f4afe-106">For more information about asynchronous programming with the <xref:System.IAsyncResult> interface, see [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md).</span></span>

## <a name="general-principles"></a><span data-ttu-id="f4afe-107">一般原则</span><span class="sxs-lookup"><span data-stu-id="f4afe-107">General Principles</span></span>

<span data-ttu-id="f4afe-108">一般来说，应尽量使用基于事件的异步模式公开异步功能。</span><span class="sxs-lookup"><span data-stu-id="f4afe-108">In general, you should expose asynchronous features using the Event-based Asynchronous Pattern whenever possible.</span></span> <span data-ttu-id="f4afe-109">不过，基于事件的模式无法满足一些要求。</span><span class="sxs-lookup"><span data-stu-id="f4afe-109">However, there are some requirements that the event-based pattern cannot meet.</span></span> <span data-ttu-id="f4afe-110">在这种情况下，除了基于事件的模式外，可能还需要实现 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-110">In those cases, you may need to implement the <xref:System.IAsyncResult> pattern in addition to the event-based pattern.</span></span>

> [!NOTE]
> <span data-ttu-id="f4afe-111">实现了 <xref:System.IAsyncResult> 模式但没有实现基于事件的模式，这种情况很少见。</span><span class="sxs-lookup"><span data-stu-id="f4afe-111">It is rare for the <xref:System.IAsyncResult> pattern to be implemented without the event-based pattern also being implemented.</span></span>

## <a name="guidelines"></a><span data-ttu-id="f4afe-112">准则</span><span class="sxs-lookup"><span data-stu-id="f4afe-112">Guidelines</span></span>

<span data-ttu-id="f4afe-113">下面列出了应在何时实现基于事件的异步模式的相关指南：</span><span class="sxs-lookup"><span data-stu-id="f4afe-113">The following list describes the guidelines for when you should implement Event-based Asynchronous Pattern:</span></span>

- <span data-ttu-id="f4afe-114">将基于事件的模式用作公开类的异步行为的默认 API。</span><span class="sxs-lookup"><span data-stu-id="f4afe-114">Use the event-based pattern as the default API to expose asynchronous behavior for your class.</span></span>

- <span data-ttu-id="f4afe-115">如果类主要用于客户端应用（例如，Windows 窗体），请勿公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-115">Do not expose the <xref:System.IAsyncResult> pattern when your class is primarily used in a client application, for example Windows Forms.</span></span>

- <span data-ttu-id="f4afe-116">仅在需要满足特定要求时，才公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-116">Only expose the <xref:System.IAsyncResult> pattern when it is necessary for meeting your requirements.</span></span> <span data-ttu-id="f4afe-117">例如，为了与现有 API 兼容，可能需要公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-117">For example, compatibility with an existing API may require you to expose the <xref:System.IAsyncResult> pattern.</span></span>

- <span data-ttu-id="f4afe-118">请勿在不公开基于事件的模式的情况下公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-118">Do not expose the <xref:System.IAsyncResult> pattern without also exposing the event-based pattern.</span></span>

- <span data-ttu-id="f4afe-119">如果必须公开 <xref:System.IAsyncResult> 模式，请以高级选项的形式这样做。</span><span class="sxs-lookup"><span data-stu-id="f4afe-119">If you must expose the <xref:System.IAsyncResult> pattern, do so as an advanced option.</span></span> <span data-ttu-id="f4afe-120">例如，如果生成代理对象，默认生成的是基于事件的模式，并含用于生成 <xref:System.IAsyncResult> 模式的选项。</span><span class="sxs-lookup"><span data-stu-id="f4afe-120">For example, if you generate a proxy object, generate the event-based pattern by default, with an option to generate the <xref:System.IAsyncResult> pattern.</span></span>

- <span data-ttu-id="f4afe-121">在 <xref:System.IAsyncResult> 模式实现的基础之上生成基于事件的模式实现。</span><span class="sxs-lookup"><span data-stu-id="f4afe-121">Build your event-based pattern implementation on your <xref:System.IAsyncResult> pattern implementation.</span></span>

- <span data-ttu-id="f4afe-122">避免对相同的类公开基于事件的模式和 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-122">Avoid exposing both the event-based pattern and the <xref:System.IAsyncResult> pattern on the same class.</span></span> <span data-ttu-id="f4afe-123">请对“高级”类公开基于事件的模式，并对“低级”类公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-123">Expose the event-based pattern on "higher level" classes and the <xref:System.IAsyncResult> pattern on "lower level" classes.</span></span> <span data-ttu-id="f4afe-124">例如，比较 <xref:System.Net.WebClient> 组件上基于事件的模式与 <xref:System.Web.HttpRequest> 类上的 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-124">For example, compare the event-based pattern on the <xref:System.Net.WebClient> component with the <xref:System.IAsyncResult> pattern on the <xref:System.Web.HttpRequest> class.</span></span>

  - <span data-ttu-id="f4afe-125">出于兼容性需要，可以对相同的类公开基于事件的模式和 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-125">Expose the event-based pattern and the <xref:System.IAsyncResult> pattern on the same class when compatibility requires it.</span></span> <span data-ttu-id="f4afe-126">例如，如果已释放使用 <xref:System.IAsyncResult> 模式的 API，需要保留 <xref:System.IAsyncResult> 模式，以实现向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="f4afe-126">For example, if you have already released an API that uses the <xref:System.IAsyncResult> pattern, you would need to retain the <xref:System.IAsyncResult> pattern for backward compatibility.</span></span>

  - <span data-ttu-id="f4afe-127">如果生成的对象模型复杂性远远超过分离实现的好处，请对相同的类公开基于事件的模式和 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-127">Expose the event-based pattern and the <xref:System.IAsyncResult> pattern on the same class if the resulting object model complexity outweighs the benefit of separating the implementations.</span></span> <span data-ttu-id="f4afe-128">对一个类公开两种模式优于避免公开基于事件的模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-128">It is better to expose both patterns on a single class than to avoid exposing the event-based pattern.</span></span>

  - <span data-ttu-id="f4afe-129">如果必须对一个类公开基于事件的模式和 <xref:System.IAsyncResult> 模式，请将 <xref:System.ComponentModel.EditorBrowsableAttribute> 设置为 <xref:System.ComponentModel.EditorBrowsableState.Advanced>，以将 <xref:System.IAsyncResult> 模式实现标记为高级功能。</span><span class="sxs-lookup"><span data-stu-id="f4afe-129">If you must expose both the event-based pattern and <xref:System.IAsyncResult> pattern on a single class, use <xref:System.ComponentModel.EditorBrowsableAttribute> set to <xref:System.ComponentModel.EditorBrowsableState.Advanced> to mark the <xref:System.IAsyncResult> pattern implementation as an advanced feature.</span></span> <span data-ttu-id="f4afe-130">这会指示设计环境（如 Visual Studio IntelliSense）不显示 <xref:System.IAsyncResult> 属性和方法。</span><span class="sxs-lookup"><span data-stu-id="f4afe-130">This indicates to design environments, such as Visual Studio IntelliSense, not to display the <xref:System.IAsyncResult> properties and methods.</span></span> <span data-ttu-id="f4afe-131">这些属性和方法仍完全可用，这样做只是为了让使用 IntelliSense 的开发人员对 API 更加明确。</span><span class="sxs-lookup"><span data-stu-id="f4afe-131">These properties and methods are still fully usable, but the developer working through IntelliSense has a clearer view of the API.</span></span>

## <a name="criteria-for-exposing-the-iasyncresult-pattern-in-addition-to-the-event-based-pattern"></a><span data-ttu-id="f4afe-132">除了基于事件的模式外还公开 IAsyncResult 模式的条件</span><span class="sxs-lookup"><span data-stu-id="f4afe-132">Criteria for Exposing the IAsyncResult Pattern in Addition to the Event-based Pattern</span></span>

<span data-ttu-id="f4afe-133">虽然基于事件的异步模式在上述情况下有许多优点，但也有一些缺点。如果性能是最重要的要求，应注意这些缺点。</span><span class="sxs-lookup"><span data-stu-id="f4afe-133">While the Event-based Asynchronous Pattern has many benefits under the previously mentioned scenarios, it does have some drawbacks, which you should be aware of if performance is your most important requirement.</span></span>

<span data-ttu-id="f4afe-134"><xref:System.IAsyncResult> 模式比基于事件的模式更适用 的情况有三种：</span><span class="sxs-lookup"><span data-stu-id="f4afe-134">There are three scenarios that the event-based pattern does not address as well as the <xref:System.IAsyncResult> pattern:</span></span>

- <span data-ttu-id="f4afe-135">对 <xref:System.IAsyncResult> 阻止等待操作</span><span class="sxs-lookup"><span data-stu-id="f4afe-135">Blocking wait on one <xref:System.IAsyncResult></span></span>

- <span data-ttu-id="f4afe-136">对多个 <xref:System.IAsyncResult> 对象阻止等待操作</span><span class="sxs-lookup"><span data-stu-id="f4afe-136">Blocking wait on many <xref:System.IAsyncResult> objects</span></span>

- <span data-ttu-id="f4afe-137">对 <xref:System.IAsyncResult> 轮询完成状态</span><span class="sxs-lookup"><span data-stu-id="f4afe-137">Polling for completion on the <xref:System.IAsyncResult></span></span>

<span data-ttu-id="f4afe-138">虽然可以使用基于事件的模式来处理这些情况，但这样做比使用 <xref:System.IAsyncResult> 模式更不方便。</span><span class="sxs-lookup"><span data-stu-id="f4afe-138">You can address these scenarios by using the event-based pattern, but doing so is more cumbersome than using the <xref:System.IAsyncResult> pattern.</span></span>

<span data-ttu-id="f4afe-139">开发人员经常对性能要求通常很高的服务使用 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-139">Developers often use the <xref:System.IAsyncResult> pattern for services that typically have very high performance requirements.</span></span> <span data-ttu-id="f4afe-140">例如，轮询完成状态就是一种高性能服务器技术。</span><span class="sxs-lookup"><span data-stu-id="f4afe-140">For example, the polling for completion scenario is a high-performance server technique.</span></span>

<span data-ttu-id="f4afe-141">此外，基于事件的模式的效率低于 <xref:System.IAsyncResult> 模式，因为前者创建的对象更多（尤其是 <xref:System.EventArgs>），并且跨线程同步。</span><span class="sxs-lookup"><span data-stu-id="f4afe-141">Additionally, the event-based pattern is less efficient than the <xref:System.IAsyncResult> pattern because it creates more objects, especially <xref:System.EventArgs>, and because it synchronizes across threads.</span></span>

<span data-ttu-id="f4afe-142">下面列出了一些在决定使用 <xref:System.IAsyncResult> 模式时要遵循的建议：</span><span class="sxs-lookup"><span data-stu-id="f4afe-142">The following list shows some recommendations to follow if you decide to use the <xref:System.IAsyncResult> pattern:</span></span>

- <span data-ttu-id="f4afe-143">仅在特别需要对 <xref:System.Threading.WaitHandle> 或<xref:System.IAsyncResult> 对象的支持时，才公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-143">Only expose the <xref:System.IAsyncResult> pattern when you specifically require support for <xref:System.Threading.WaitHandle> or <xref:System.IAsyncResult> objects.</span></span>

- <span data-ttu-id="f4afe-144">仅在有使用 <xref:System.IAsyncResult> 模式的现有 API 时，才公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-144">Only expose the <xref:System.IAsyncResult> pattern when you have an existing API that uses the <xref:System.IAsyncResult> pattern.</span></span>

- <span data-ttu-id="f4afe-145">如果有基于 <xref:System.IAsyncResult> 模式的现有 API，还请考虑在下一个版本中公开基于事件的模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-145">If you have an existing API based on the <xref:System.IAsyncResult> pattern, consider also exposing the event-based pattern in your next release.</span></span>

- <span data-ttu-id="f4afe-146">仅在有高性能要求，且已验证无法通过基于事件的模式满足这些要求，但可以通过 <xref:System.IAsyncResult> 模式满足时，才公开 <xref:System.IAsyncResult> 模式。</span><span class="sxs-lookup"><span data-stu-id="f4afe-146">Only expose <xref:System.IAsyncResult> pattern if you have high performance requirements which you have verified cannot be met by the event-based pattern but can be met by the <xref:System.IAsyncResult> pattern.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4afe-147">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f4afe-147">See also</span></span>

- [<span data-ttu-id="f4afe-148">如何：实现支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="f4afe-148">How to: Implement a Component That Supports the Event-based Asynchronous Pattern</span></span>](component-that-supports-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="f4afe-149">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="f4afe-149">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
- [<span data-ttu-id="f4afe-150">实现基于事件的异步模式</span><span class="sxs-lookup"><span data-stu-id="f4afe-150">Implementing the Event-based Asynchronous Pattern</span></span>](implementing-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="f4afe-151">实现基于事件的异步模式的最佳做法</span><span class="sxs-lookup"><span data-stu-id="f4afe-151">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="f4afe-152">基于事件的异步模式概述</span><span class="sxs-lookup"><span data-stu-id="f4afe-152">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
