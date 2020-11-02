---
title: 解析程序集加载
description: 本文介绍 .NET AppDomain.AssemblyResolve 事件。 将此事件用于需要对程序集加载进行控制的应用程序。
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 16f2f61a2a36e4189e98c85b3d3ce706a52e2938
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687274"
---
# <a name="resolve-assembly-loads"></a><span data-ttu-id="264ea-104">解析程序集加载</span><span class="sxs-lookup"><span data-stu-id="264ea-104">Resolve assembly loads</span></span>

<span data-ttu-id="264ea-105">.NET 为对程序集加载需要更强控制的应用程序提供了 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件。</span><span class="sxs-lookup"><span data-stu-id="264ea-105">.NET provides the <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> event for applications that require greater control over assembly loading.</span></span> <span data-ttu-id="264ea-106">通过处理此事件，应用程序可从常规探测路径外部将程序集加载到加载上下文、从几个程序集版本中选择要加载的版本、发出动态程序集并返回此程序集，等等。</span><span class="sxs-lookup"><span data-stu-id="264ea-106">By handling this event, your application can load an assembly into the load context from outside the normal probing paths, select which of several assembly versions to load, emit a dynamic assembly and return it, and so on.</span></span> <span data-ttu-id="264ea-107">本主题指导如何处理 <xref:System.AppDomain.AssemblyResolve> 事件。</span><span class="sxs-lookup"><span data-stu-id="264ea-107">This topic provides guidance for handling the <xref:System.AppDomain.AssemblyResolve> event.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="264ea-108">若要在仅限反射的上下文中解决程序集加载问题，请改用 <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> 事件。</span><span class="sxs-lookup"><span data-stu-id="264ea-108">For resolving assembly loads in the reflection-only context, use the <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> event instead.</span></span>  
  
## <a name="how-the-assemblyresolve-event-works"></a><span data-ttu-id="264ea-109">AssemblyResolve 事件的工作原理</span><span class="sxs-lookup"><span data-stu-id="264ea-109">How the AssemblyResolve event works</span></span>  
 <span data-ttu-id="264ea-110">注册 <xref:System.AppDomain.AssemblyResolve> 事件的处理程序后，每当运行时无法按名称绑定到程序集时，此处理程序都将被调用。</span><span class="sxs-lookup"><span data-stu-id="264ea-110">When you register a handler for the <xref:System.AppDomain.AssemblyResolve> event, the handler is invoked whenever the runtime fails to bind to an assembly by name.</span></span> <span data-ttu-id="264ea-111">例如，从用户代码中调用以下方法可能导致引发 <xref:System.AppDomain.AssemblyResolve> 事件：</span><span class="sxs-lookup"><span data-stu-id="264ea-111">For example, calling the following methods from user code can cause the <xref:System.AppDomain.AssemblyResolve> event to be raised:</span></span>  
  
- <span data-ttu-id="264ea-112"><xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 方法重载或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法重载，其第一个参数是表示要加载的程序集的显示名称的字符串（即，<xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> 属性返回的字符串）。</span><span class="sxs-lookup"><span data-stu-id="264ea-112">An <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method overload or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overload whose first argument is a string that represents the display name of the assembly to load (that is, the string returned by the <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> property).</span></span>  
  
- <span data-ttu-id="264ea-113"><xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 方法重载或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法重载，其第一个参数是标识要加载的程序集的 <xref:System.Reflection.AssemblyName> 对象。</span><span class="sxs-lookup"><span data-stu-id="264ea-113">An <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method overload or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overload whose first argument is an <xref:System.Reflection.AssemblyName> object that identifies the assembly to load.</span></span>  
  
- <span data-ttu-id="264ea-114"><xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 方法重载。</span><span class="sxs-lookup"><span data-stu-id="264ea-114">An <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> method overload.</span></span>  
  
- <span data-ttu-id="264ea-115"><xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> 或 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> 方法重载，实例化另一个应用程序域中的对象。</span><span class="sxs-lookup"><span data-stu-id="264ea-115">An <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> or <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> method overload that instantiates an object in another application domain.</span></span>  
  
### <a name="what-the-event-handler-does"></a><span data-ttu-id="264ea-116">事件处理程序的功能</span><span class="sxs-lookup"><span data-stu-id="264ea-116">What the event handler does</span></span>  
 <span data-ttu-id="264ea-117"><xref:System.AppDomain.AssemblyResolve> 事件的处理程序接收要加载的程序集的显示名称（在 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 属性中）。</span><span class="sxs-lookup"><span data-stu-id="264ea-117">The handler for the <xref:System.AppDomain.AssemblyResolve> event receives the display name of the assembly to be loaded, in the <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="264ea-118">如果处理程序无法识别程序集名称，则返回 `null` (C#)、`Nothing` (Visual Basic) 或 `nullptr` (Visual C++)。</span><span class="sxs-lookup"><span data-stu-id="264ea-118">If the handler does not recognize the assembly name, it returns `null` (C#), `Nothing` (Visual Basic), or `nullptr` (Visual C++).</span></span>  
  
 <span data-ttu-id="264ea-119">如果处理程序识别了程序集名称，它可以加载并返回满足此请求的程序集。</span><span class="sxs-lookup"><span data-stu-id="264ea-119">If the handler recognizes the assembly name, it can load and return an assembly that satisfies the request.</span></span> <span data-ttu-id="264ea-120">下面的列表介绍了一些示例方案。</span><span class="sxs-lookup"><span data-stu-id="264ea-120">The following list describes some sample scenarios.</span></span>  
  
- <span data-ttu-id="264ea-121">如果处理程序知道某一版本程序集的位置，它可以使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> 方法加载程序集，然后返回已加载的程序集（如果成功）。</span><span class="sxs-lookup"><span data-stu-id="264ea-121">If the handler knows the location of a version of the assembly, it can load the assembly by using the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> method, and can return the loaded assembly if successful.</span></span>  
  
- <span data-ttu-id="264ea-122">如果处理程序有权访问以字节数组形式存储的程序集的数据库，则它可以通过使用可采用字节数组的一种 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法重载来加载字节数组。</span><span class="sxs-lookup"><span data-stu-id="264ea-122">If the handler has access to a database of assemblies stored as byte arrays, it can load a byte array by using one of the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overloads that take a byte array.</span></span>  
  
- <span data-ttu-id="264ea-123">处理程序可以生成动态程序集并将其返回。</span><span class="sxs-lookup"><span data-stu-id="264ea-123">The handler can generate a dynamic assembly and return it.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="264ea-124">处理程序必须将程序集加载到加载源上下文或加载上下文，或加载不具有上下文的程序集。如果处理程序使用 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> 方法将程序集加载到仅限反射的上下文，则引发 <xref:System.AppDomain.AssemblyResolve> 事件的加载尝试将失败。</span><span class="sxs-lookup"><span data-stu-id="264ea-124">The handler must load the assembly into the load-from context, into the load context, or without context.If the handler loads the assembly into the reflection-only context by using the <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> or the <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> method, the load attempt that raised the <xref:System.AppDomain.AssemblyResolve> event fails.</span></span>  
  
 <span data-ttu-id="264ea-125">事件处理程序负责返回适当的程序集。</span><span class="sxs-lookup"><span data-stu-id="264ea-125">It is the responsibility of the event handler to return a suitable assembly.</span></span> <span data-ttu-id="264ea-126">通过将 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 属性值传递到 <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> 构造函数，处理程序可以解析所请求程序集的显示名称。</span><span class="sxs-lookup"><span data-stu-id="264ea-126">The handler can parse the display name of the requested assembly by passing the <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> property value to the <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> constructor.</span></span> <span data-ttu-id="264ea-127">从 .NET Framework 4 开始，处理程序可使用 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 属性确定当前请求是否是另一程序集的依赖项。</span><span class="sxs-lookup"><span data-stu-id="264ea-127">Beginning with the .NET Framework 4, the handler can use the <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property to determine whether the current request is a dependency of another assembly.</span></span> <span data-ttu-id="264ea-128">此信息有助于识别满足依赖关系的程序集。</span><span class="sxs-lookup"><span data-stu-id="264ea-128">This information can help identify an assembly that will satisfy the dependency.</span></span>  
  
 <span data-ttu-id="264ea-129">事件处理程序返回的程序集版本可能与请求的版本不同。</span><span class="sxs-lookup"><span data-stu-id="264ea-129">The event handler can return a different version of the assembly than the version that was requested.</span></span>  
  
 <span data-ttu-id="264ea-130">大多数情况下，处理程序返回的程序集在加载上下文中显示，与处理程序将其加载到的上下文无关。</span><span class="sxs-lookup"><span data-stu-id="264ea-130">In most cases, the assembly that is returned by the handler appears in the load context, regardless of the context the handler loads it into.</span></span> <span data-ttu-id="264ea-131">例如，如果处理程序使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法将程序集加载到加载源上下文，当处理程序返回此程序集时，它将在加载上下文中显示。</span><span class="sxs-lookup"><span data-stu-id="264ea-131">For example, if the handler uses the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> method to load an assembly into the load-from context, the assembly appears in the load context when the handler returns it.</span></span> <span data-ttu-id="264ea-132">但在以下情况，处理程序返回程序集时将不会显示其上下文：</span><span class="sxs-lookup"><span data-stu-id="264ea-132">However, in the following case the assembly appears without context when the handler returns it:</span></span>  
  
- <span data-ttu-id="264ea-133">处理程序加载了不具有上下文的程序集。</span><span class="sxs-lookup"><span data-stu-id="264ea-133">The handler loads an assembly without context.</span></span>  
  
- <span data-ttu-id="264ea-134"><xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 属性不为 null。</span><span class="sxs-lookup"><span data-stu-id="264ea-134">The <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property is not null.</span></span>  
  
- <span data-ttu-id="264ea-135">加载请求的程序集（即 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 属性返回的程序集）时未加载上下文。</span><span class="sxs-lookup"><span data-stu-id="264ea-135">The requesting assembly (that is, the assembly that is returned by the <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property) was loaded without context.</span></span>  
  
 <span data-ttu-id="264ea-136">有关上下文的信息，请参阅 <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> 方法重载。</span><span class="sxs-lookup"><span data-stu-id="264ea-136">For information about contexts, see the <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> method overload.</span></span>  
  
 <span data-ttu-id="264ea-137">可将同一程序集的多个版本加载到同一应用程序域中。</span><span class="sxs-lookup"><span data-stu-id="264ea-137">Multiple versions of the same assembly can be loaded into the same application domain.</span></span> <span data-ttu-id="264ea-138">不推荐此做法，因为可能导致类型分配问题。</span><span class="sxs-lookup"><span data-stu-id="264ea-138">This practice is not recommended, because it can lead to type assignment problems.</span></span> <span data-ttu-id="264ea-139">请参阅[适用于程序集加载的最佳做法](../../framework/deployment/best-practices-for-assembly-loading.md)。</span><span class="sxs-lookup"><span data-stu-id="264ea-139">See [Best practices for assembly loading](../../framework/deployment/best-practices-for-assembly-loading.md).</span></span>  
  
### <a name="what-the-event-handler-should-not-do"></a><span data-ttu-id="264ea-140">事件处理程序的禁忌操作</span><span class="sxs-lookup"><span data-stu-id="264ea-140">What the event handler should not do</span></span>  
<span data-ttu-id="264ea-141">处理 <xref:System.AppDomain.AssemblyResolve> 事件的主要规则是不应试图返回无法识别的程序集。</span><span class="sxs-lookup"><span data-stu-id="264ea-141">The primary rule for handling the <xref:System.AppDomain.AssemblyResolve> event is that you should not try to return an assembly you do not recognize.</span></span> <span data-ttu-id="264ea-142">编写处理程序时应了解哪些程序集可能会导致引发该事件。</span><span class="sxs-lookup"><span data-stu-id="264ea-142">When you write the handler, you should know which assemblies might cause the event to be raised.</span></span> <span data-ttu-id="264ea-143">处理程序集应对其他程序集返回 null。</span><span class="sxs-lookup"><span data-stu-id="264ea-143">Your handler should return null for other assemblies.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="264ea-144">从 .NET Framework 4 开始，<xref:System.AppDomain.AssemblyResolve> 事件针对附属程序集引发。</span><span class="sxs-lookup"><span data-stu-id="264ea-144">Beginning with the .NET Framework 4, the <xref:System.AppDomain.AssemblyResolve> event is raised for satellite assemblies.</span></span> <span data-ttu-id="264ea-145">此更改会影响为早期版本的 .NET Framework 编写的事件处理程序（如果此类事件处理程序尝试解决所有程序集加载请求）。</span><span class="sxs-lookup"><span data-stu-id="264ea-145">This change affects an event handler that was written for an earlier version of the .NET Framework, if the handler tries to resolve all assembly load requests.</span></span> <span data-ttu-id="264ea-146">忽略无法识别的程序集的事件处理程序不受此更改的影响：这些程序会返回 NULL，并遵循正常的回退机制。</span><span class="sxs-lookup"><span data-stu-id="264ea-146">Event handlers that ignore assemblies they do not recognize are not affected by this change: They return null, and normal fallback mechanisms are followed.</span></span>  

<span data-ttu-id="264ea-147">加载程序集时，事件处理程序禁止使用可导致递归引发 <xref:System.AppDomain.AssemblyResolve> 事件的任何 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法重载，因为可能导致堆栈溢出。</span><span class="sxs-lookup"><span data-stu-id="264ea-147">When loading an assembly, the event handler must not use any of the <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overloads that can cause the <xref:System.AppDomain.AssemblyResolve> event to be raised recursively, because this can lead to a stack overflow.</span></span> <span data-ttu-id="264ea-148">（请参阅本主题前面部分提供的列表。）即使为加载请求提供异常处理也会发生此情况，因为异常都是在所有事件处理程序返回后引发的。</span><span class="sxs-lookup"><span data-stu-id="264ea-148">(See the list provided earlier in this topic.) This happens even if you provide exception handling for the load request, because no exception is thrown until all event handlers have returned.</span></span> <span data-ttu-id="264ea-149">因此，如果未找到 `MyAssembly`，下面的代码将导致堆栈溢出：</span><span class="sxs-lookup"><span data-stu-id="264ea-149">Thus, the following code results in a stack overflow if `MyAssembly` is not found:</span></span>  

```cpp
using namespace System;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);
        return Assembly::Load(e->Name);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
 */
```

```csharp
using System;
using System.Reflection;

class BadExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);
        return Assembly.Load(e.Name);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
 */
```

```vb
Imports System.Reflection

Class BadExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object, _
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)
        Return Assembly.Load(e.Name)
    End Function
End Class

' This example produces output similar to the following:
'
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'...
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'
'Process is terminated due to StackOverflowException.
```

## <a name="see-also"></a><span data-ttu-id="264ea-150">请参阅</span><span class="sxs-lookup"><span data-stu-id="264ea-150">See also</span></span>

- [<span data-ttu-id="264ea-151">适用于程序集加载的最佳做法</span><span class="sxs-lookup"><span data-stu-id="264ea-151">Best practices for assembly loading</span></span>](../../framework/deployment/best-practices-for-assembly-loading.md)
- [<span data-ttu-id="264ea-152">使用应用程序域</span><span class="sxs-lookup"><span data-stu-id="264ea-152">Use application domains</span></span>](../../framework/app-domains/use.md)
