---
title: 如何：实现监视程序
description: 在 .NET 中实现监视程序。 观察程序设计模式要求区分观察程序（注册获取通知）和提供程序。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- observers [.NET], observer design pattern
- observer design pattern [.NET], implementing observers
ms.assetid: 8ecfa9f5-b500-473d-bcf0-5652ffb1e53d
ms.openlocfilehash: 71df673b580f711ad692454d12beea991810f508
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064205"
---
# <a name="how-to-implement-an-observer"></a><span data-ttu-id="bf8fe-104">如何：实现监视程序</span><span class="sxs-lookup"><span data-stu-id="bf8fe-104">How to: Implement an Observer</span></span>
<span data-ttu-id="bf8fe-105">观察程序设计模式要求区分观察程序（注册获取通知）和提供程序（监视数据并将通知发送到一个或多个观察程序）。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-105">The observer design pattern requires a division between an observer, which registers for notifications, and a provider, which monitors data and sends notifications to one or more observers.</span></span> <span data-ttu-id="bf8fe-106">本主题介绍了如何创建观察程序。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-106">This topic discusses how to create an observer.</span></span> <span data-ttu-id="bf8fe-107">相关主题[如何：实现提供程序](how-to-implement-a-provider.md)介绍了如何创建提供程序。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-107">A related topic, [How to: Implement a Provider](how-to-implement-a-provider.md), discusses how to create an provider.</span></span>  
  
### <a name="to-create-an-observer"></a><span data-ttu-id="bf8fe-108">创建观察程序的具体步骤</span><span class="sxs-lookup"><span data-stu-id="bf8fe-108">To create an observer</span></span>  
  
1. <span data-ttu-id="bf8fe-109">定义观察程序，即实现 <xref:System.IObserver%601?displayProperty=nameWithType> 接口的类型。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-109">Define the observer, which is a type that implements the <xref:System.IObserver%601?displayProperty=nameWithType> interface.</span></span> <span data-ttu-id="bf8fe-110">例如，下面的代码定义了 `TemperatureReporter` 类型，即使用 `Temperature` 泛型类型参数的构造 <xref:System.IObserver%601?displayProperty=nameWithType> 实现。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-110">For example, the following code defines a type named `TemperatureReporter` that is a constructed <xref:System.IObserver%601?displayProperty=nameWithType> implementation with a generic type argument of `Temperature`.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#8)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#8)]  
  
2. <span data-ttu-id="bf8fe-111">如果观察程序可以在提供程序调用 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 实现前停止接收通知，请定义专用变量，用于保留提供程序 <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> 方法返回的 <xref:System.IDisposable> 实现。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-111">If the observer can stop receiving notifications before the provider calls its <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementation, define a private variable that will hold the <xref:System.IDisposable> implementation returned by the provider's <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="bf8fe-112">还应定义订阅方法，用于调用提供程序的 <xref:System.IObservable%601.Subscribe%2A> 方法，并存储返回的 <xref:System.IDisposable> 对象。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-112">You should also define a subscription method that calls the provider's <xref:System.IObservable%601.Subscribe%2A> method and stores the returned <xref:System.IDisposable> object.</span></span> <span data-ttu-id="bf8fe-113">例如，下面的代码定义 `unsubscriber` 专用变量，并定义 `Subscribe` 方法，用于调用提供程序的 <xref:System.IObservable%601.Subscribe%2A> 方法，并将返回的对象分配给 `unsubscriber` 变量。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-113">For example, the following code defines a private variable named `unsubscriber` and defines a `Subscribe` method that calls the provider's <xref:System.IObservable%601.Subscribe%2A> method and assigns the returned object to the `unsubscriber` variable.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#9)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#9)]  
  
3. <span data-ttu-id="bf8fe-114">定义一个方法，以便观察程序可以在提供程序调用 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 实现前停止接收通知（如果需要此功能的话）。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-114">Define a method that enables the observer to stop receiving notifications before the provider calls its <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementation, if this feature is required.</span></span> <span data-ttu-id="bf8fe-115">下面的示例定义了 `Unsubscribe` 方法。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-115">The following example defines an `Unsubscribe` method.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#10)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#10)]  
  
4. <span data-ttu-id="bf8fe-116">实现 <xref:System.IObserver%601> 接口定义的三个方法：<xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>、<xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType> 和 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-116">Provide implementations of the three methods defined by the <xref:System.IObserver%601> interface: <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>, <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType>, and <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="bf8fe-117">根据提供程序和应用需求，<xref:System.IObserver%601.OnError%2A> 和 <xref:System.IObserver%601.OnCompleted%2A> 方法可以是存根实现。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-117">Depending on the provider and the needs of the application, the <xref:System.IObserver%601.OnError%2A> and <xref:System.IObserver%601.OnCompleted%2A> methods can be stub implementations.</span></span> <span data-ttu-id="bf8fe-118">请注意，<xref:System.IObserver%601.OnError%2A> 方法不得将传入的 <xref:System.Exception> 对象处理为异常，<xref:System.IObserver%601.OnCompleted%2A> 方法可以随意调用提供程序的 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 实现。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-118">Note that the <xref:System.IObserver%601.OnError%2A> method should not handle the passed <xref:System.Exception> object as an exception, and the <xref:System.IObserver%601.OnCompleted%2A> method is free to call the provider's <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> implementation.</span></span> <span data-ttu-id="bf8fe-119">下面的示例展示了 `TemperatureReporter` 类的 <xref:System.IObserver%601> 实现。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-119">The following example shows the <xref:System.IObserver%601> implementation of the `TemperatureReporter` class.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#11)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#11)]  
  
## <a name="example"></a><span data-ttu-id="bf8fe-120">示例</span><span class="sxs-lookup"><span data-stu-id="bf8fe-120">Example</span></span>  
 <span data-ttu-id="bf8fe-121">下面的示例包含 `TemperatureReporter` 类的完整源代码，提供了温度监视应用的 <xref:System.IObserver%601> 实现。</span><span class="sxs-lookup"><span data-stu-id="bf8fe-121">The following example contains the complete source code for the `TemperatureReporter` class, which provides the <xref:System.IObserver%601> implementation for a temperature monitoring application.</span></span>  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#12)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#12)]  
  
## <a name="see-also"></a><span data-ttu-id="bf8fe-122">请参阅</span><span class="sxs-lookup"><span data-stu-id="bf8fe-122">See also</span></span>

- <xref:System.IObserver%601>
- [<span data-ttu-id="bf8fe-123">观察程序设计模式</span><span class="sxs-lookup"><span data-stu-id="bf8fe-123">Observer Design Pattern</span></span>](observer-design-pattern.md)
- [<span data-ttu-id="bf8fe-124">如何：实现提供程序</span><span class="sxs-lookup"><span data-stu-id="bf8fe-124">How to: Implement a Provider</span></span>](how-to-implement-a-provider.md)
- [<span data-ttu-id="bf8fe-125">监视程序设计模式最佳做法</span><span class="sxs-lookup"><span data-stu-id="bf8fe-125">Observer Design Pattern Best Practices</span></span>](observer-design-pattern-best-practices.md)
