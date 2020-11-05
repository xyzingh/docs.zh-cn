---
title: 线程本地存储区：线程相关的静态字段和数据槽
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET], local storage
- threading [.NET], thread-relative static fields
- local thread storage
- TLS
ms.assetid: c633a4dc-a790-4ed1-96b5-f72bd968b284
ms.openlocfilehash: f80cc09d87116d3daff8047c1d1398c5e6104178
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188154"
---
# <a name="thread-local-storage-thread-relative-static-fields-and-data-slots"></a><span data-ttu-id="5cb1b-102">线程本地存储区：线程相关的静态字段和数据槽</span><span class="sxs-lookup"><span data-stu-id="5cb1b-102">Thread Local Storage: Thread-Relative Static Fields and Data Slots</span></span>

<span data-ttu-id="5cb1b-103">托管线程本地存储 (TLS) 可用于存储对线程和应用程序域唯一的数据。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-103">You can use managed thread local storage (TLS) to store data that's unique to a thread and application domain.</span></span> <span data-ttu-id="5cb1b-104">.NET 提供了下面两种托管 TLS 使用方式：线程相对静态字段和数据槽。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-104">.NET provides two ways to use managed TLS: thread-relative static fields and data slots.</span></span>  
  
- <span data-ttu-id="5cb1b-105">如果可以在编译时预测确切需求，请使用线程相对静态字段（Visual Basic 中的线程相对 `Shared` 字段）。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-105">Use thread-relative static fields (thread-relative `Shared` fields in Visual Basic) if you can anticipate your exact needs at compile time.</span></span> <span data-ttu-id="5cb1b-106">线程相对静态字段的性能最佳。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-106">Thread-relative static fields provide the best performance.</span></span> <span data-ttu-id="5cb1b-107">它们还支持编译时类型检查。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-107">They also give you the benefits of compile-time type checking.</span></span>  
  
- <span data-ttu-id="5cb1b-108">如果只能在运行时发现实际需求，请使用数据槽。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-108">Use data slots when your actual requirements might be discovered only at run time.</span></span> <span data-ttu-id="5cb1b-109">数据槽使用起来比线程相对静态字段更慢、更加棘手。由于数据存储为类型 <xref:System.Object>，因此使用前必须将它强制转换为正确类型。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-109">Data slots are slower and more awkward to use than thread-relative static fields, and data is stored as type <xref:System.Object>, so you must cast it to the correct type before you use it.</span></span>  
  
 <span data-ttu-id="5cb1b-110">在非托管 C++ 中，使用 `TlsAlloc` 动态分配槽，使用 `__declspec(thread)` 声明应在线程相对存储中分配变量。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-110">In unmanaged C++, you use `TlsAlloc` to allocate slots dynamically and `__declspec(thread)` to declare that a variable should be allocated in thread-relative storage.</span></span> <span data-ttu-id="5cb1b-111">线程相对静态字段和数据槽提供了此行为的托管版本。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-111">Thread-relative static fields and data slots provide the managed version of this behavior.</span></span>  
  
<span data-ttu-id="5cb1b-112">可以使用 <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> 类来创建在首次使用对象时迟缓初始化的线程本地对象。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-112">You can use the <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> class to create thread-local objects that are initialized lazily when the object is first consumed.</span></span> <span data-ttu-id="5cb1b-113">若要了解详细信息，请参阅[迟缓初始化](../../framework/performance/lazy-initialization.md)</span><span class="sxs-lookup"><span data-stu-id="5cb1b-113">For more information, see [Lazy Initialization](../../framework/performance/lazy-initialization.md).</span></span>  
  
## <a name="uniqueness-of-data-in-managed-tls"></a><span data-ttu-id="5cb1b-114">托管 TLS 中数据的唯一性</span><span class="sxs-lookup"><span data-stu-id="5cb1b-114">Uniqueness of Data in Managed TLS</span></span>  
 <span data-ttu-id="5cb1b-115">无论使用线程相对静态字段，还是使用数据槽，托管 TLS 中的数据都是对线程和应用域唯一的数据。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-115">Whether you use thread-relative static fields or data slots, data in managed TLS is unique to the combination of thread and application domain.</span></span>  
  
- <span data-ttu-id="5cb1b-116">在应用域内，一个线程无法修改另一个线程的数据，即使两个线程使用相同的字段或槽，也不例外。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-116">Within an application domain, one thread cannot modify data from another thread, even when both threads use the same field or slot.</span></span>  
  
- <span data-ttu-id="5cb1b-117">如果线程访问多个应用域中的相同字段或槽，每个应用域中都会保留单独的值。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-117">When a thread accesses the same field or slot from multiple application domains, a separate value is maintained in each application domain.</span></span>  
  
 <span data-ttu-id="5cb1b-118">例如，如果线程设置线程相对静态字段值，并在进入另一个应用域后检索此字段的值，那么在第二个应用域中检索到的值与第一个应用域中的值不同。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-118">For example, if a thread sets the value of a thread-relative static field, enters another application domain, and then retrieves the value of the field, the value retrieved in the second application domain differs from the value in the first application domain.</span></span> <span data-ttu-id="5cb1b-119">对第二个应用域中的字段设置新值不会影响第一个应用域中的字段值。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-119">Setting a new value for the field in the second application domain does not affect the field's value in the first application domain.</span></span>  
  
 <span data-ttu-id="5cb1b-120">同样，如果线程在两个不同的应用域中有同名数据槽，第一个应用域中的数据不受第二个应用域中数据的影响。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-120">Similarly, when a thread gets the same named data slot in two different application domains, the data in the first application domain remains independent of the data in the second application domain.</span></span>  
  
## <a name="thread-relative-static-fields"></a><span data-ttu-id="5cb1b-121">线程相对静态字段</span><span class="sxs-lookup"><span data-stu-id="5cb1b-121">Thread-Relative Static Fields</span></span>  
 <span data-ttu-id="5cb1b-122">如果确定一条数据始终对线程和应用域是唯一的，请向静态字段应用 <xref:System.ThreadStaticAttribute> 属性。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-122">If you know that a piece of data is always unique to a thread and application-domain combination, apply the <xref:System.ThreadStaticAttribute> attribute to the static field.</span></span> <span data-ttu-id="5cb1b-123">此字段的使用方法与其他任何静态字段一样。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-123">Use the field as you would use any other static field.</span></span> <span data-ttu-id="5cb1b-124">此字段中的数据对使用它的每个线程都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-124">The data in the field is unique to each thread that uses it.</span></span>  
  
 <span data-ttu-id="5cb1b-125">线程相对静态字段的性能优于数据槽，并支持编译时类型检查。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-125">Thread-relative static fields provide better performance than data slots and have the benefit of compile-time type checking.</span></span>  
  
 <span data-ttu-id="5cb1b-126">请注意，任何类构造函数代码都会在访问此字段的首个上下文中的第一个线程上运行。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-126">Be aware that any class constructor code will run on the first thread in the first context that accesses the field.</span></span> <span data-ttu-id="5cb1b-127">在同一应用域中的其他所有线程或上下文中，如果字段是引用类型，便会初始化为 `null`（Visual Basic 中的 `Nothing`）；如果字段是值类型，便会初始化为默认值。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-127">In all other threads or contexts in the same application domain, the fields will be initialized to `null` (`Nothing` in Visual Basic) if they are reference types, or to their default values if they are value types.</span></span> <span data-ttu-id="5cb1b-128">因此，不得依赖类构造函数来初始化线程相对静态字段。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-128">Therefore, you should not rely on class constructors to initialize thread-relative static fields.</span></span> <span data-ttu-id="5cb1b-129">相反，请避免初始化线程相对静态字段，而是假设它们初始化为 `null` (`Nothing`) 或默认值。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-129">Instead, avoid initializing thread-relative static fields and assume that they are initialized to `null` (`Nothing`) or to their default values.</span></span>  
  
## <a name="data-slots"></a><span data-ttu-id="5cb1b-130">数据槽</span><span class="sxs-lookup"><span data-stu-id="5cb1b-130">Data Slots</span></span>  

<span data-ttu-id="5cb1b-131">.NET 提供了对于线程和应用程序域都是唯一的动态数据槽。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-131">.NET provides dynamic data slots that are unique to a combination of thread and application domain.</span></span> <span data-ttu-id="5cb1b-132">数据槽分为下列两种类型：命名槽和未命名槽。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-132">There are two types of data slots: named slots and unnamed slots.</span></span> <span data-ttu-id="5cb1b-133">两种类型都是使用 <xref:System.LocalDataStoreSlot> 结构实现。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-133">Both are implemented by using the <xref:System.LocalDataStoreSlot> structure.</span></span>  
  
- <span data-ttu-id="5cb1b-134">若要创建命名数据槽，请使用 <xref:System.Threading.Thread.AllocateNamedDataSlot%2A?displayProperty=nameWithType> 或 <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-134">To create a named data slot, use the <xref:System.Threading.Thread.AllocateNamedDataSlot%2A?displayProperty=nameWithType> or <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="5cb1b-135">若要获取对现有命名槽的引用，请将它的名称传递给 <xref:System.Threading.Thread.GetNamedDataSlot%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-135">To get a reference to an existing named slot, pass its name to the <xref:System.Threading.Thread.GetNamedDataSlot%2A> method.</span></span>  
  
- <span data-ttu-id="5cb1b-136">若要创建未命名数据槽，请使用 <xref:System.Threading.Thread.AllocateDataSlot%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-136">To create an unnamed data slot, use the <xref:System.Threading.Thread.AllocateDataSlot%2A?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="5cb1b-137">对于命名槽和未命名槽，请使用 <xref:System.Threading.Thread.SetData%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Thread.GetData%2A?displayProperty=nameWithType> 方法设置和检索槽中的信息。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-137">For both named and unnamed slots, use the <xref:System.Threading.Thread.SetData%2A?displayProperty=nameWithType> and <xref:System.Threading.Thread.GetData%2A?displayProperty=nameWithType> methods to set and retrieve the information in the slot.</span></span> <span data-ttu-id="5cb1b-138">这些静态方法始终处理当前正在执行它们的线程的数据。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-138">These are static methods that always act on the data for the thread that is currently executing them.</span></span>  
  
 <span data-ttu-id="5cb1b-139">命名槽非常便捷，因为可以在需要时检索槽，具体操作是将它的名称传递给 <xref:System.Threading.Thread.GetNamedDataSlot%2A> 方法，而不用维护对未命名槽的引用。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-139">Named slots can be convenient, because you can retrieve the slot when you need it by passing its name to the <xref:System.Threading.Thread.GetNamedDataSlot%2A> method, instead of maintaining a reference to an unnamed slot.</span></span> <span data-ttu-id="5cb1b-140">不过，如果另一个组件对线程相对存储使用相同的名称，并且线程同时执行你的组件和另一个组件的代码，这两个组件可能会相互损坏数据。</span><span class="sxs-lookup"><span data-stu-id="5cb1b-140">However, if another component uses the same name for its thread-relative storage and a thread executes code from both your component and the other component, the two components might corrupt each other's data.</span></span> <span data-ttu-id="5cb1b-141">（此方案假定这两个组件都在同一个应用域中运行，并不旨在共享相同的数据。）</span><span class="sxs-lookup"><span data-stu-id="5cb1b-141">(This scenario assumes that both components are running in the same application domain, and that they are not designed to share the same data.)</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5cb1b-142">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5cb1b-142">See also</span></span>

- <xref:System.ContextStaticAttribute>
- <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType>
- <xref:System.ThreadStaticAttribute>
- <xref:System.Runtime.Remoting.Messaging.CallContext>
- [<span data-ttu-id="5cb1b-143">线程处理</span><span class="sxs-lookup"><span data-stu-id="5cb1b-143">Threading</span></span>](index.md)
