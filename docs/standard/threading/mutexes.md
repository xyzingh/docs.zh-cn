---
title: Mutexes
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- wait handles
- threading [.NET], Mutex class
- Mutex class, about Mutex class
- threading [.NET], cross-process synchronization
ms.assetid: 9dd06e25-12c0-4a9e-855a-452dc83803e2
ms.openlocfilehash: ba31fff03cfffda7cf2a40a3a82b2222e8951035
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188986"
---
# <a name="mutexes"></a><span data-ttu-id="74e14-102">Mutexes</span><span class="sxs-lookup"><span data-stu-id="74e14-102">Mutexes</span></span>

<span data-ttu-id="74e14-103"><xref:System.Threading.Mutex> 对象可用于提供对资源的独占访问权限。</span><span class="sxs-lookup"><span data-stu-id="74e14-103">You can use a <xref:System.Threading.Mutex> object to provide exclusive access to a resource.</span></span> <span data-ttu-id="74e14-104">虽然 <xref:System.Threading.Mutex> 类使用的系统资源比 <xref:System.Threading.Monitor> 类更多，但它可以跨应用域边界进行封送，可用于多个等待操作以及同步不同进程中的线程。</span><span class="sxs-lookup"><span data-stu-id="74e14-104">The <xref:System.Threading.Mutex> class uses more system resources than the <xref:System.Threading.Monitor> class, but it can be marshaled across application domain boundaries, it can be used with multiple waits, and it can be used to synchronize threads in different processes.</span></span> <span data-ttu-id="74e14-105">有关托管同步机制的比较，请参阅[同步基元概述](overview-of-synchronization-primitives.md)。</span><span class="sxs-lookup"><span data-stu-id="74e14-105">For a comparison of managed synchronization mechanisms, see [Overview of Synchronization Primitives](overview-of-synchronization-primitives.md).</span></span>  
  
 <span data-ttu-id="74e14-106">有关代码示例，请参阅 <xref:System.Threading.Mutex.%23ctor%2A> 构造函数的参考文档。</span><span class="sxs-lookup"><span data-stu-id="74e14-106">For code examples, see the reference documentation for the <xref:System.Threading.Mutex.%23ctor%2A> constructors.</span></span>  
  
## <a name="using-mutexes"></a><span data-ttu-id="74e14-107">使用 Mutex</span><span class="sxs-lookup"><span data-stu-id="74e14-107">Using Mutexes</span></span>  
 <span data-ttu-id="74e14-108">线程调用 mutex 的 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法来请求获取所有权。</span><span class="sxs-lookup"><span data-stu-id="74e14-108">A thread calls the <xref:System.Threading.WaitHandle.WaitOne%2A> method of a mutex to request ownership.</span></span> <span data-ttu-id="74e14-109">在 mutex 可用或可选超时间隔结束前，该调用会一直处于阻止状态。</span><span class="sxs-lookup"><span data-stu-id="74e14-109">The call blocks until the mutex is available, or until the optional timeout interval elapses.</span></span> <span data-ttu-id="74e14-110">如果没有任何线程拥有它，则 mutex 将处于已发出信号状态。</span><span class="sxs-lookup"><span data-stu-id="74e14-110">The state of a mutex is signaled if no thread owns it.</span></span>  
  
 <span data-ttu-id="74e14-111">线程通过调用 <xref:System.Threading.Mutex.ReleaseMutex%2A> 方法来释放 mutex。</span><span class="sxs-lookup"><span data-stu-id="74e14-111">A thread releases a mutex by calling its <xref:System.Threading.Mutex.ReleaseMutex%2A> method.</span></span> <span data-ttu-id="74e14-112">Mutex 具有线程关联；即 mutex 只能由拥有它的线程释放。</span><span class="sxs-lookup"><span data-stu-id="74e14-112">Mutexes have thread affinity; that is, the mutex can be released only by the thread that owns it.</span></span> <span data-ttu-id="74e14-113">如果线程释放的 mutex 不是它拥有的，就会在线程中抛出 <xref:System.ApplicationException>。</span><span class="sxs-lookup"><span data-stu-id="74e14-113">If a thread releases a mutex it does not own, an <xref:System.ApplicationException> is thrown in the thread.</span></span>  
  
 <span data-ttu-id="74e14-114">由于 <xref:System.Threading.Mutex> 类派生自 <xref:System.Threading.WaitHandle>，因此还可以调用 <xref:System.Threading.WaitHandle> 的静态 <xref:System.Threading.WaitHandle.WaitAll%2A> 或 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法，以请求获取 <xref:System.Threading.Mutex> 的所有权以及其他等待句柄。</span><span class="sxs-lookup"><span data-stu-id="74e14-114">Because the <xref:System.Threading.Mutex> class derives from <xref:System.Threading.WaitHandle>, you can also call the static <xref:System.Threading.WaitHandle.WaitAll%2A> or <xref:System.Threading.WaitHandle.WaitAny%2A> methods of <xref:System.Threading.WaitHandle> to request ownership of a <xref:System.Threading.Mutex> in combination with other wait handles.</span></span>  
  
 <span data-ttu-id="74e14-115">如果线程拥有 <xref:System.Threading.Mutex>，此线程可以在重复的等待-请求调用中指定相同的 <xref:System.Threading.Mutex>，而不会阻止执行；不过，它必须释放 <xref:System.Threading.Mutex>，次数与释放所有权一样多。</span><span class="sxs-lookup"><span data-stu-id="74e14-115">If a thread owns a <xref:System.Threading.Mutex>, that thread can specify the same <xref:System.Threading.Mutex> in repeated wait-request calls without blocking its execution; however, it must release the <xref:System.Threading.Mutex> as many times to release ownership.</span></span>  
  
## <a name="abandoned-mutexes"></a><span data-ttu-id="74e14-116">放弃的 mutex</span><span class="sxs-lookup"><span data-stu-id="74e14-116">Abandoned Mutexes</span></span>  
 <span data-ttu-id="74e14-117">如果线程终止而未释放 <xref:System.Threading.Mutex>，则认为已放弃 mutex。</span><span class="sxs-lookup"><span data-stu-id="74e14-117">If a thread terminates without releasing a <xref:System.Threading.Mutex>, the mutex is said to be abandoned.</span></span> <span data-ttu-id="74e14-118">这通常指示存在严重的编程错误，因为该 mutex 正在保护的资源可能会处于不一致状态。</span><span class="sxs-lookup"><span data-stu-id="74e14-118">This often indicates a serious programming error because the resource the mutex is protecting might be left in an inconsistent state.</span></span> <span data-ttu-id="74e14-119">在下一个获取 mutex 的线程中引发 <xref:System.Threading.AbandonedMutexException>。</span><span class="sxs-lookup"><span data-stu-id="74e14-119">An <xref:System.Threading.AbandonedMutexException> is thrown in the next thread that acquires the mutex.</span></span>
  
 <span data-ttu-id="74e14-120">对于系统范围的 mutex，放弃的 mutex 可能指示应用程序已突然终止（例如，通过使用 Windows 任务管理器终止）。</span><span class="sxs-lookup"><span data-stu-id="74e14-120">In the case of a system-wide mutex, an abandoned mutex might indicate that an application has been terminated abruptly (for example, by using Windows Task Manager).</span></span>  
  
## <a name="local-and-system-mutexes"></a><span data-ttu-id="74e14-121">本地 mutex 和系统 mutex</span><span class="sxs-lookup"><span data-stu-id="74e14-121">Local and System Mutexes</span></span>  
 <span data-ttu-id="74e14-122">Mutex 有两种类型：本地 mutex 和命名系统 mutex。</span><span class="sxs-lookup"><span data-stu-id="74e14-122">Mutexes are of two types: local mutexes and named system mutexes.</span></span> <span data-ttu-id="74e14-123">如果使用接受名称的构造函数创建 <xref:System.Threading.Mutex> 对象，此对象与同名的操作系统对象相关联。</span><span class="sxs-lookup"><span data-stu-id="74e14-123">If you create a <xref:System.Threading.Mutex> object using a constructor that accepts a name, it is associated with an operating-system object of that name.</span></span> <span data-ttu-id="74e14-124">命名系统 mutex 在整个操作系统中都可见，并且可用于同步进程活动。</span><span class="sxs-lookup"><span data-stu-id="74e14-124">Named system mutexes are visible throughout the operating system and can be used to synchronize the activities of processes.</span></span> <span data-ttu-id="74e14-125">可以创建多个表示同一命名系统 mutex 的 <xref:System.Threading.Mutex> 对象，还能使用 <xref:System.Threading.Mutex.OpenExisting%2A> 方法打开现有的命名系统 mutex。</span><span class="sxs-lookup"><span data-stu-id="74e14-125">You can create multiple <xref:System.Threading.Mutex> objects that represent the same named system mutex, and you can use the <xref:System.Threading.Mutex.OpenExisting%2A> method to open an existing named system mutex.</span></span>  
  
 <span data-ttu-id="74e14-126">本地 mutex 仅存在于进程中。</span><span class="sxs-lookup"><span data-stu-id="74e14-126">A local mutex exists only within your process.</span></span> <span data-ttu-id="74e14-127">进程中引用本地 <xref:System.Threading.Mutex> 对象的所有线程都可以使用本地 mutex。</span><span class="sxs-lookup"><span data-stu-id="74e14-127">It can be used by any thread in your process that has a reference to the local <xref:System.Threading.Mutex> object.</span></span> <span data-ttu-id="74e14-128">每个 <xref:System.Threading.Mutex> 对象都是单独的本地 mutex。</span><span class="sxs-lookup"><span data-stu-id="74e14-128">Each <xref:System.Threading.Mutex> object is a separate local mutex.</span></span>  
  
### <a name="access-control-security-for-system-mutexes"></a><span data-ttu-id="74e14-129">系统 mutex 的访问控制安全性</span><span class="sxs-lookup"><span data-stu-id="74e14-129">Access Control Security for System Mutexes</span></span>  

<span data-ttu-id="74e14-130">可借助 .NET 进行查询和设置命名系统对象的 Windows 访问控制安全性。</span><span class="sxs-lookup"><span data-stu-id="74e14-130">.NET provides the ability to query and set Windows access control security for named system objects.</span></span> <span data-ttu-id="74e14-131">建议从创建起立刻开始保护系统 mutex，因为系统对象是全局对象，因此可能被不是你自己的代码锁定。</span><span class="sxs-lookup"><span data-stu-id="74e14-131">Protecting system mutexes from the moment of creation is recommended because system objects are global and therefore can be locked by code other than your own.</span></span>  
  
 <span data-ttu-id="74e14-132">若要了解 mutex 访问控制安全性，请参阅 <xref:System.Security.AccessControl.MutexSecurity> 和 <xref:System.Security.AccessControl.MutexAccessRule> 类、<xref:System.Security.AccessControl.MutexRights> 枚举、<xref:System.Threading.Mutex> 类的 <xref:System.Threading.Mutex.GetAccessControl%2A>、<xref:System.Threading.Mutex.SetAccessControl%2A> 和 <xref:System.Threading.Mutex.OpenExisting%2A> 方法，以及 <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29> 构造函数。</span><span class="sxs-lookup"><span data-stu-id="74e14-132">For information on access control security for mutexes, see the <xref:System.Security.AccessControl.MutexSecurity> and <xref:System.Security.AccessControl.MutexAccessRule> classes, the <xref:System.Security.AccessControl.MutexRights> enumeration, the <xref:System.Threading.Mutex.GetAccessControl%2A>, <xref:System.Threading.Mutex.SetAccessControl%2A>, and <xref:System.Threading.Mutex.OpenExisting%2A> methods of the <xref:System.Threading.Mutex> class, and the <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29> constructor.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="74e14-133">请参阅</span><span class="sxs-lookup"><span data-stu-id="74e14-133">See also</span></span>

- <xref:System.Threading.Mutex?displayProperty=nameWithType>
- <xref:System.Threading.Mutex.%23ctor%2A>
- <xref:System.Security.AccessControl.MutexSecurity?displayProperty=nameWithType>
- <xref:System.Security.AccessControl.MutexAccessRule?displayProperty=nameWithType>
- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- [<span data-ttu-id="74e14-134">线程处理对象和功能</span><span class="sxs-lookup"><span data-stu-id="74e14-134">Threading objects and features</span></span>](threading-objects-and-features.md)
- [<span data-ttu-id="74e14-135">线程与线程处理</span><span class="sxs-lookup"><span data-stu-id="74e14-135">Threads and threading</span></span>](threads-and-threading.md)
- [<span data-ttu-id="74e14-136">线程处理</span><span class="sxs-lookup"><span data-stu-id="74e14-136">Threading</span></span>](index.md)
