---
title: 如何：实现提供程序
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- observer design pattern [.NET], implementing providers
- providers [.NET], in observer design pattern
- observables [.NET], in observer design pattern
ms.assetid: 790b5d8b-d546-40a6-beeb-151b574e5ee5
ms.openlocfilehash: b57b595a40494ba0cf6c38b6a13688dece602584
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064218"
---
# <a name="how-to-implement-a-provider"></a><span data-ttu-id="d8e3e-102">如何：实现提供程序</span><span class="sxs-lookup"><span data-stu-id="d8e3e-102">How to: Implement a Provider</span></span>
<span data-ttu-id="d8e3e-103">观察程序设计模式要求区分提供程序（监视数据并发送通知）和一个或多个观察程序（通过提供程序接收通知（回调））。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-103">The observer design pattern requires a division between a provider, which monitors data and sends notifications, and one or more observers, which receive notifications (callbacks) from the provider.</span></span> <span data-ttu-id="d8e3e-104">本主题介绍了如何创建提供程序。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-104">This topic discusses how to create a provider.</span></span> <span data-ttu-id="d8e3e-105">相关主题[如何：实现观察程序](how-to-implement-an-observer.md)介绍了如何创建观察程序。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-105">A related topic, [How to: Implement an Observer](how-to-implement-an-observer.md), discusses how to create an observer.</span></span>  
  
### <a name="to-create-a-provider"></a><span data-ttu-id="d8e3e-106">创建提供程序的具体步骤</span><span class="sxs-lookup"><span data-stu-id="d8e3e-106">To create a provider</span></span>  
  
1. <span data-ttu-id="d8e3e-107">定义提供程序负责发送给观察程序的数据。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-107">Define the data that the provider is responsible for sending to observers.</span></span> <span data-ttu-id="d8e3e-108">尽管提供程序和发送给观察程序的数据可能是一种类型，但它们通常由不同类型表示。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-108">Although the provider and the data that it sends to observers can be a single type, they are generally represented by different types.</span></span> <span data-ttu-id="d8e3e-109">例如，在温度监视应用中，`Temperature` 结构定义提供程序（由下一步中定义的 `TemperatureMonitor` 类表示）监视和观察程序订阅的数据。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-109">For example, in a temperature monitoring application, the `Temperature` structure defines the data that the provider (which is represented by the `TemperatureMonitor` class defined in the next step) monitors and to which observers subscribe.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/data.cs#1)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/data.vb#1)]  
  
2. <span data-ttu-id="d8e3e-110">定义数据提供程序，即实现 <xref:System.IObservable%601?displayProperty=nameWithType> 接口的类型。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-110">Define the data provider, which is a type that implements the <xref:System.IObservable%601?displayProperty=nameWithType> interface.</span></span> <span data-ttu-id="d8e3e-111">提供程序的泛型类型参数是提供程序发送给观察程序的类型。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-111">The provider's generic type argument is the type that the provider sends to observers.</span></span> <span data-ttu-id="d8e3e-112">下面的示例定义了 `TemperatureMonitor` 类，即使用 `Temperature` 泛型类型参数的构造 <xref:System.IObservable%601?displayProperty=nameWithType> 实现。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-112">The following example defines a `TemperatureMonitor` class, which is a constructed <xref:System.IObservable%601?displayProperty=nameWithType> implementation with a generic type argument of `Temperature`.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#2)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#2)]  
  
3. <span data-ttu-id="d8e3e-113">确定提供程序如何存储对观察程序的引用，以便视情况通知每个观察程序。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-113">Determine how the provider will store references to observers so that each observer can be notified when appropriate.</span></span> <span data-ttu-id="d8e3e-114">最常见的情况是，集合对象（如泛型 <xref:System.Collections.Generic.List%601> 对象）用于实现此目的。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-114">Most commonly, a collection object such as a generic <xref:System.Collections.Generic.List%601> object is used for this purpose.</span></span> <span data-ttu-id="d8e3e-115">下面的示例定义了在 `TemperatureMonitor` 类构造函数中实例化的专用 <xref:System.Collections.Generic.List%601> 对象。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-115">The following example defines a private <xref:System.Collections.Generic.List%601> object that is instantiated in the `TemperatureMonitor` class constructor.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#3)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#3)]  
  
4. <span data-ttu-id="d8e3e-116">定义提供程序可以返回给订阅者的 <xref:System.IDisposable> 实现，以便订阅者能够随时停止接收通知。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-116">Define an <xref:System.IDisposable> implementation that the provider can return to subscribers so that they can stop receiving notifications at any time.</span></span> <span data-ttu-id="d8e3e-117">下面的示例定义了嵌套类 `Unsubscriber`，在类实例化时向其中传递对订阅者集合和订阅者的引用。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-117">The following example defines a nested `Unsubscriber` class that is passed a reference to the subscribers collection and to the subscriber when the class is instantiated.</span></span> <span data-ttu-id="d8e3e-118">使用此代码，订阅者可以调用对象的 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 实现，将自身从订阅者集合中删除。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-118">This code enables the subscriber to call the object's <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> implementation to remove itself from the subscribers collection.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#4)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#4)]  
  
5. <span data-ttu-id="d8e3e-119">实现 <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-119">Implement the <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="d8e3e-120">向此方法传递对 <xref:System.IObserver%601?displayProperty=nameWithType> 接口的引用，此方法应存储在第 3 步中为实现相应目的而设计的对象中。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-120">The method is passed a reference to the <xref:System.IObserver%601?displayProperty=nameWithType> interface and should be stored in the object designed for that purpose in step 3.</span></span> <span data-ttu-id="d8e3e-121">然后，此方法应返回在第 4 步中开发的 <xref:System.IDisposable> 实现。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-121">The method should then return the <xref:System.IDisposable> implementation developed in step 4.</span></span> <span data-ttu-id="d8e3e-122">下面的示例展示了 `TemperatureMonitor` 类中 <xref:System.IObservable%601.Subscribe%2A> 方法的实现。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-122">The following example shows the implementation of the <xref:System.IObservable%601.Subscribe%2A> method in the `TemperatureMonitor` class.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#5)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#5)]  
  
6. <span data-ttu-id="d8e3e-123">通过调用 <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>、<xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType> 和 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 实现，视情况通知观察程序。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-123">Notify observers as appropriate by calling their <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>, <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType>, and <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> implementations.</span></span> <span data-ttu-id="d8e3e-124">在某些情况下，如果出错，提供程序可能不会调用 <xref:System.IObserver%601.OnError%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-124">In some cases, a provider may not call the <xref:System.IObserver%601.OnError%2A> method when an error occurs.</span></span> <span data-ttu-id="d8e3e-125">例如，下面的 `GetTemperature` 方法模拟监视器，每 5 秒读取一次温度数据，如果温度自从上一次读数以来出现至少 0.1 度的变化，就会通知观察程序。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-125">For example, the following `GetTemperature` method simulates a monitor that reads temperature data every five seconds and notifies observers if the temperature has changed by at least .1 degree since the previous reading.</span></span> <span data-ttu-id="d8e3e-126">如果设备不报告温度（即如果值为 null），提供程序便会通知观察程序传输已完成。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-126">If the device does not report a temperature (that is, if its value is null), the provider notifies observers that the transmission is complete.</span></span> <span data-ttu-id="d8e3e-127">请注意，除了调用每个观察程序的 <xref:System.IObserver%601.OnCompleted%2A> 方法外，`GetTemperature` 方法还可以清除 <xref:System.Collections.Generic.List%601> 集合。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-127">Note that, in addition to calling each observer's <xref:System.IObserver%601.OnCompleted%2A> method, the `GetTemperature` method clears the <xref:System.Collections.Generic.List%601> collection.</span></span> <span data-ttu-id="d8e3e-128">在这种情况下，提供程序不调用观察程序的 <xref:System.IObserver%601.OnError%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-128">In this case, the provider makes no calls to the <xref:System.IObserver%601.OnError%2A> method of its observers.</span></span>  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#6)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#6)]  
  
## <a name="example"></a><span data-ttu-id="d8e3e-129">示例</span><span class="sxs-lookup"><span data-stu-id="d8e3e-129">Example</span></span>  
 <span data-ttu-id="d8e3e-130">下面的示例包含完整的源代码，用于定义温度监视应用的 <xref:System.IObservable%601> 实现。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-130">The following example contains the complete source code for defining an <xref:System.IObservable%601> implementation for a temperature monitoring application.</span></span> <span data-ttu-id="d8e3e-131">它包括 `Temperature` 结构（即发送给观察程序的数据）和 `TemperatureMonitor` 类（即 <xref:System.IObservable%601> 实现）。</span><span class="sxs-lookup"><span data-stu-id="d8e3e-131">It includes the `Temperature` structure, which is the data sent to observers, and the `TemperatureMonitor` class, which is the <xref:System.IObservable%601> implementation.</span></span>  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#7)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#7)]  
  
## <a name="see-also"></a><span data-ttu-id="d8e3e-132">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d8e3e-132">See also</span></span>

- <xref:System.IObservable%601>
- [<span data-ttu-id="d8e3e-133">观察程序设计模式</span><span class="sxs-lookup"><span data-stu-id="d8e3e-133">Observer Design Pattern</span></span>](observer-design-pattern.md)
- [<span data-ttu-id="d8e3e-134">如何：实现监视程序</span><span class="sxs-lookup"><span data-stu-id="d8e3e-134">How to: Implement an Observer</span></span>](how-to-implement-an-observer.md)
- [<span data-ttu-id="d8e3e-135">监视程序设计模式最佳做法</span><span class="sxs-lookup"><span data-stu-id="d8e3e-135">Observer Design Pattern Best Practices</span></span>](observer-design-pattern-best-practices.md)
