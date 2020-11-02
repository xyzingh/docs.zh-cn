---
title: 轮询异步操作的状态
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous programming, status polling
- polling asynchronous operation status
- status information [.NET], asynchronous operations
ms.assetid: b541af31-dacb-4e20-8847-1b1ff7c35363
ms.openlocfilehash: c73ee50c67034feed07a4869deb0a32342bb45e5
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888732"
---
# <a name="polling-for-the-status-of-an-asynchronous-operation"></a><span data-ttu-id="aeb79-102">轮询异步操作的状态</span><span class="sxs-lookup"><span data-stu-id="aeb79-102">Polling for the Status of an Asynchronous Operation</span></span>
<span data-ttu-id="aeb79-103">如果应用可以在等待异步操作结果期间继续执行其他工作，不得阻止应用一直到操作完成。</span><span class="sxs-lookup"><span data-stu-id="aeb79-103">Applications that can do other work while waiting for the results of an asynchronous operation should not block waiting until the operation completes.</span></span> <span data-ttu-id="aeb79-104">请使用下列方法之一，在应用等待异步操作完成期间继续执行指令：</span><span class="sxs-lookup"><span data-stu-id="aeb79-104">Use one of the following options to continue executing instructions while waiting for an asynchronous operation to complete:</span></span>  
  
- <span data-ttu-id="aeb79-105">使用异步操作的 **Begin**_OperationName_ 方法返回的 <xref:System.IAsyncResult> 的 <xref:System.IAsyncResult.IsCompleted%2A> 属性，确定操作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="aeb79-105">Use the <xref:System.IAsyncResult.IsCompleted%2A> property of the <xref:System.IAsyncResult> returned by the asynchronous operation's **Begin**_OperationName_ method to determine whether the operation has completed.</span></span> <span data-ttu-id="aeb79-106">这种方法称为“轮询”，本主题介绍的就是它。</span><span class="sxs-lookup"><span data-stu-id="aeb79-106">This approach is known as polling and is demonstrated in this topic.</span></span>  
  
- <span data-ttu-id="aeb79-107">使用 <xref:System.AsyncCallback> 委托，在单独的线程中处理异步操作结果。</span><span class="sxs-lookup"><span data-stu-id="aeb79-107">Use an <xref:System.AsyncCallback> delegate to process the results of the asynchronous operation in a separate thread.</span></span> <span data-ttu-id="aeb79-108">有关展示这种方法的示例，请参阅[使用 AsyncCallback 委托结束异步操作](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)。</span><span class="sxs-lookup"><span data-stu-id="aeb79-108">For an example that demonstrates this approach, see [Using an AsyncCallback Delegate to End an Asynchronous Operation](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="aeb79-109">示例</span><span class="sxs-lookup"><span data-stu-id="aeb79-109">Example</span></span>  
 <span data-ttu-id="aeb79-110">下面的代码示例展示了如何使用 <xref:System.Net.Dns> 类中的异步方法，检索用户指定计算机的域名系统信息。</span><span class="sxs-lookup"><span data-stu-id="aeb79-110">The following code example demonstrates using asynchronous methods in the <xref:System.Net.Dns> class to retrieve Domain Name System information for a user-specified computer.</span></span> <span data-ttu-id="aeb79-111">此示例启动异步操作，然后在控制台打印句点 (".")，直到操作完成。</span><span class="sxs-lookup"><span data-stu-id="aeb79-111">This example starts the asynchronous operation and then prints periods (".") at the console until the operation is complete.</span></span> <span data-ttu-id="aeb79-112">请注意，对 <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.AsyncCallback> 和 <xref:System.Object> 参数传递的是 null（Visual Basic 中的 Nothing），因为使用这种方法时这些是可选参数。</span><span class="sxs-lookup"><span data-stu-id="aeb79-112">Note that **null** ( **Nothing** in Visual Basic) is passed for the <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.AsyncCallback> and <xref:System.Object> parameters because these arguments are not required when using this approach.</span></span>  
  
 [!code-csharp[AsyncDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_Poll.cs#3)]
 [!code-vb[AsyncDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_Poll.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="aeb79-113">另请参阅</span><span class="sxs-lookup"><span data-stu-id="aeb79-113">See also</span></span>

- [<span data-ttu-id="aeb79-114">基于事件的异步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="aeb79-114">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
- [<span data-ttu-id="aeb79-115">基于事件的异步模式概述</span><span class="sxs-lookup"><span data-stu-id="aeb79-115">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
