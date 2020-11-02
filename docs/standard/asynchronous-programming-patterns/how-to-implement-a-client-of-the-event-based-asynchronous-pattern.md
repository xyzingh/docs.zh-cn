---
title: 如何：实现基于事件的异步模式的客户端
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET], asynchronous features
- components [.NET], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
ms.openlocfilehash: 95997f219a08c131905cfc86b78e94c36f3ec851
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888810"
---
# <a name="how-to-implement-a-client-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="14167-102">如何：实现基于事件的异步模式的客户端</span><span class="sxs-lookup"><span data-stu-id="14167-102">How to: Implement a Client of the Event-based Asynchronous Pattern</span></span>
<span data-ttu-id="14167-103">下面的代码示例展示了如何使用符合[基于事件的异步模式概述](event-based-asynchronous-pattern-overview.md)要求的组件。</span><span class="sxs-lookup"><span data-stu-id="14167-103">The following code example demonstrates how to use a component that adheres to the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md).</span></span> <span data-ttu-id="14167-104">此示例的窗体使用[如何：实现支持基于事件的异步模式的组件](component-that-supports-the-event-based-asynchronous-pattern.md)中介绍的 `PrimeNumberCalculator` 组件。</span><span class="sxs-lookup"><span data-stu-id="14167-104">The form for this example uses the `PrimeNumberCalculator` component described in [How to: Implement a Component That Supports the Event-based Asynchronous Pattern](component-that-supports-the-event-based-asynchronous-pattern.md).</span></span>  
  
 <span data-ttu-id="14167-105">运行使用此示例的项目时，将会看到包含一个网格和两个按钮（“启动新任务”  和“取消”  ）的“质数计算器”窗体。</span><span class="sxs-lookup"><span data-stu-id="14167-105">When you run a project that uses this example, you will see a "Prime Number Calculator" form with a grid and two buttons: **Start New Task** and **Cancel** .</span></span> <span data-ttu-id="14167-106">可以连续多次单击“启动新任务”  按钮。每次单击后，异步操作都会开始计算，以确定随机生成的测试数字是否为质数。</span><span class="sxs-lookup"><span data-stu-id="14167-106">You can click the **Start New Task** button several times in succession, and for each click, an asynchronous operation will begin a computation to determine if a randomly generated test number is prime.</span></span> <span data-ttu-id="14167-107">窗体会定期显示进度和增量结果。</span><span class="sxs-lookup"><span data-stu-id="14167-107">The form will periodically display progress and incremental results.</span></span> <span data-ttu-id="14167-108">每个操作都分配有唯一的任务 ID。</span><span class="sxs-lookup"><span data-stu-id="14167-108">Each operation is assigned a unique task ID.</span></span> <span data-ttu-id="14167-109">计算结果显示在“结果”  列中；如果测试数字不是质数，将会把它标记为“复合”  ，并显示第一个除数。</span><span class="sxs-lookup"><span data-stu-id="14167-109">The result of the computation is displayed in the **Result** column; if the test number is not prime, it is labeled as **Composite,** and its first divisor is displayed.</span></span>  
  
 <span data-ttu-id="14167-110">可使用“取消”  按钮，取消任意挂起的操作。</span><span class="sxs-lookup"><span data-stu-id="14167-110">Any pending operation can be canceled with the **Cancel** button.</span></span> <span data-ttu-id="14167-111">可以多选。</span><span class="sxs-lookup"><span data-stu-id="14167-111">Multiple selections can be made.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="14167-112">数字大多不是质数。</span><span class="sxs-lookup"><span data-stu-id="14167-112">Most numbers will not be prime.</span></span> <span data-ttu-id="14167-113">如果在多个操作已完成后找不到质数，只需启动更多任务，最终会找到一些质数。</span><span class="sxs-lookup"><span data-stu-id="14167-113">If you have not found a prime number after several completed operations, simply start more tasks, and eventually you will find some prime numbers.</span></span>  
  
## <a name="example"></a><span data-ttu-id="14167-114">示例</span><span class="sxs-lookup"><span data-stu-id="14167-114">Example</span></span>  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#10)]  
  
## <a name="see-also"></a><span data-ttu-id="14167-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="14167-115">See also</span></span>

- <xref:System.ComponentModel.AsyncOperation>
- <xref:System.ComponentModel.AsyncOperationManager>
- <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>
