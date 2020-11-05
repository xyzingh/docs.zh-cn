---
title: 启动时创建线程并传递数据
description: 了解如何在 .NET 中的操作系统进程开始时创建线程并传递数据。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [.NET], creating
- threading [.NET], passing data to threads
- threading [.NET], retrieving data from threads
ms.assetid: 52b32222-e185-4f42-91a7-eaca65c0ab6d
ms.openlocfilehash: a1e8f8f6e017d29f352d79ea08c09b2d97041bba
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188375"
---
# <a name="creating-threads-and-passing-data-at-start-time"></a><span data-ttu-id="72370-103">启动时创建线程并传递数据</span><span class="sxs-lookup"><span data-stu-id="72370-103">Creating threads and passing data at start time</span></span>

<span data-ttu-id="72370-104">在操作系统进程创建后，操作系统会注入线程，用于执行相应进程中的代码，包括所有原始应用域。</span><span class="sxs-lookup"><span data-stu-id="72370-104">When an operating-system process is created, the operating system injects a thread to execute code in that process, including any original application domain.</span></span> <span data-ttu-id="72370-105">自此时起，可以创建和销毁应用域，而无需创建或销毁任何操作系统线程。</span><span class="sxs-lookup"><span data-stu-id="72370-105">From that point on, application domains can be created and destroyed without any operating system threads necessarily being created or destroyed.</span></span> <span data-ttu-id="72370-106">如果要执行的代码是托管代码，可以检索 <xref:System.Threading.Thread> 类型的静态 <xref:System.Threading.Thread.CurrentThread%2A> 属性，以获取在当前应用域中执行的线程的 <xref:System.Threading.Thread> 对象。</span><span class="sxs-lookup"><span data-stu-id="72370-106">If the code being executed is managed code, then a <xref:System.Threading.Thread> object for the thread executing in the current application domain can be obtained by retrieving the static <xref:System.Threading.Thread.CurrentThread%2A> property of type <xref:System.Threading.Thread>.</span></span> <span data-ttu-id="72370-107">本主题介绍了如何创建线程，以及向线程过程传递数据的替换方法。</span><span class="sxs-lookup"><span data-stu-id="72370-107">This topic describes thread creation and discusses alternatives for passing data to the thread procedure.</span></span>  
  
## <a name="creating-a-thread"></a><span data-ttu-id="72370-108">创建线程</span><span class="sxs-lookup"><span data-stu-id="72370-108">Creating a thread</span></span>

 <span data-ttu-id="72370-109">新建 <xref:System.Threading.Thread> 对象会新建托管线程。</span><span class="sxs-lookup"><span data-stu-id="72370-109">Creating a new <xref:System.Threading.Thread> object creates a new managed thread.</span></span> <span data-ttu-id="72370-110"><xref:System.Threading.Thread> 类包含需要使用 <xref:System.Threading.ThreadStart> 委托或 <xref:System.Threading.ParameterizedThreadStart> 委托的构造函数；委托包装在调用 <xref:System.Threading.Thread.Start%2A> 方法时由新线程调用的方法。</span><span class="sxs-lookup"><span data-stu-id="72370-110">The <xref:System.Threading.Thread> class has constructors that take a <xref:System.Threading.ThreadStart> delegate or a <xref:System.Threading.ParameterizedThreadStart> delegate; the delegate wraps the method that is invoked by the new thread when you call the <xref:System.Threading.Thread.Start%2A> method.</span></span> <span data-ttu-id="72370-111">多次调用 <xref:System.Threading.Thread.Start%2A> 会导致 <xref:System.Threading.ThreadStateException> 抛出。</span><span class="sxs-lookup"><span data-stu-id="72370-111">Calling <xref:System.Threading.Thread.Start%2A> more than once causes a <xref:System.Threading.ThreadStateException> to be thrown.</span></span>  
  
 <span data-ttu-id="72370-112">通常情况下，在 <xref:System.Threading.Thread.Start%2A> 方法返回结果后，新线程其实紧接着启动。</span><span class="sxs-lookup"><span data-stu-id="72370-112">The <xref:System.Threading.Thread.Start%2A> method returns immediately, often before the new thread has actually started.</span></span> <span data-ttu-id="72370-113">可以使用 <xref:System.Threading.Thread.ThreadState%2A> 和 <xref:System.Threading.Thread.IsAlive%2A> 属性，以确定任意时刻的线程状态，但不得将这些属性用于同步线程活动。</span><span class="sxs-lookup"><span data-stu-id="72370-113">You can use the <xref:System.Threading.Thread.ThreadState%2A> and <xref:System.Threading.Thread.IsAlive%2A> properties to determine the state of the thread at any one moment, but these properties should never be used for synchronizing the activities of threads.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="72370-114">线程一旦启动，就无需保留对 <xref:System.Threading.Thread> 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="72370-114">Once a thread is started, it is not necessary to retain a reference to the <xref:System.Threading.Thread> object.</span></span> <span data-ttu-id="72370-115">线程可以继续执行到线程过程结束。</span><span class="sxs-lookup"><span data-stu-id="72370-115">The thread continues to execute until the thread procedure ends.</span></span>  
  
 <span data-ttu-id="72370-116">下面的代码示例新建两个线程，以对另一个对象调用实例和静态方法。</span><span class="sxs-lookup"><span data-stu-id="72370-116">The following code example creates two new threads to call instance and static methods on another object.</span></span>  
  
 [!code-cpp[System.Threading.ThreadStart2#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source2.cpp#2)]
 [!code-csharp[System.Threading.ThreadStart2#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source2.cs#2)]
 [!code-vb[System.Threading.ThreadStart2#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source2.vb#2)]  
  
## <a name="passing-data-to-threads"></a><span data-ttu-id="72370-117">将数据传递到线程</span><span class="sxs-lookup"><span data-stu-id="72370-117">Passing data to threads</span></span>

<span data-ttu-id="72370-118">调用 <xref:System.Threading.Thread.Start(System.Object)?displayProperty=nameWithType> 时，使用 <xref:System.Threading.ParameterizedThreadStart> 委托可将包含数据的对象轻松传递给线程。</span><span class="sxs-lookup"><span data-stu-id="72370-118">The <xref:System.Threading.ParameterizedThreadStart> delegate provides an easy way to pass an object containing data to a thread when you call <xref:System.Threading.Thread.Start(System.Object)?displayProperty=nameWithType>.</span></span> <span data-ttu-id="72370-119">有关代码示例，请参阅 <xref:System.Threading.ParameterizedThreadStart>。</span><span class="sxs-lookup"><span data-stu-id="72370-119">See <xref:System.Threading.ParameterizedThreadStart> for a code example.</span></span>
  
 <span data-ttu-id="72370-120">使用 <xref:System.Threading.ParameterizedThreadStart> 委托不是传递数据的类型安全方式，因为 <xref:System.Threading.Thread.Start(System.Object)?displayProperty=nameWithType> 方法接受任何对象。</span><span class="sxs-lookup"><span data-stu-id="72370-120">Using the <xref:System.Threading.ParameterizedThreadStart> delegate is not a type-safe way to pass data, because the <xref:System.Threading.Thread.Start(System.Object)?displayProperty=nameWithType> method accepts any object.</span></span> <span data-ttu-id="72370-121">替换方法是，将线程过程和数据封装到帮助程序类中，并使用 <xref:System.Threading.ThreadStart> 委托执行线程过程。</span><span class="sxs-lookup"><span data-stu-id="72370-121">An alternative is to encapsulate the thread procedure and the data in a helper class and use the <xref:System.Threading.ThreadStart> delegate to execute the thread procedure.</span></span> <span data-ttu-id="72370-122">下面的示例演示这一方法：</span><span class="sxs-lookup"><span data-stu-id="72370-122">The following example demonstrates this technique:</span></span>

 [!code-cpp[System.Threading.ThreadStart2#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source3.cpp#3)]
 [!code-csharp[System.Threading.ThreadStart2#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source3.cs#3)]
 [!code-vb[System.Threading.ThreadStart2#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source3.vb#3)]  

<span data-ttu-id="72370-123"><xref:System.Threading.ThreadStart> 和 <xref:System.Threading.ParameterizedThreadStart> 委托都没有返回值，因为没有从异步调用返回数据的位置。</span><span class="sxs-lookup"><span data-stu-id="72370-123">Neither <xref:System.Threading.ThreadStart> nor <xref:System.Threading.ParameterizedThreadStart> delegate has a return value, because there is no place to return the data from an asynchronous call.</span></span> <span data-ttu-id="72370-124">若要检索线程方法的结果，可以使用回叫方法，如下一节所示。</span><span class="sxs-lookup"><span data-stu-id="72370-124">To retrieve the results of a thread method, you can use a callback method, as shown in the next section.</span></span>
  
## <a name="retrieving-data-from-threads-with-callback-methods"></a><span data-ttu-id="72370-125">使用回叫方法检索线程中的数据</span><span class="sxs-lookup"><span data-stu-id="72370-125">Retrieving data from threads with callback methods</span></span>

 <span data-ttu-id="72370-126">下面的示例展示了从线程检索数据的回调方法。</span><span class="sxs-lookup"><span data-stu-id="72370-126">The following example demonstrates a callback method that retrieves data from a thread.</span></span> <span data-ttu-id="72370-127">包含数据和线程方法的类构造函数还接受表示回调方法的委托；在线程方法结束前，它调用回调委托。</span><span class="sxs-lookup"><span data-stu-id="72370-127">The constructor for the class that contains the data and the thread method also accepts a delegate representing the callback method; before the thread method ends, it invokes the callback delegate.</span></span>  
  
 [!code-cpp[System.Threading.ThreadStart2#4](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source4.cpp#4)]
 [!code-csharp[System.Threading.ThreadStart2#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source4.cs#4)]
 [!code-vb[System.Threading.ThreadStart2#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source4.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="72370-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="72370-128">See also</span></span>

- <xref:System.Threading.Thread>
- <xref:System.Threading.ThreadStart>
- <xref:System.Threading.ParameterizedThreadStart>
- <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType>
- [<span data-ttu-id="72370-129">线程处理</span><span class="sxs-lookup"><span data-stu-id="72370-129">Threading</span></span>](index.md)
- [<span data-ttu-id="72370-130">使用线程和线程处理</span><span class="sxs-lookup"><span data-stu-id="72370-130">Using Threads and Threading</span></span>](using-threads-and-threading.md)
