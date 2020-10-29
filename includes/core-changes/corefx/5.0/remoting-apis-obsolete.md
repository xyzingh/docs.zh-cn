---
ms.openlocfilehash: 35041a035041fd4ad5402e1bc0dd137a74d4f949
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434963"
---
### <a name="remoting-apis-are-obsolete"></a><span data-ttu-id="82816-101">远程处理 API 已过时</span><span class="sxs-lookup"><span data-stu-id="82816-101">Remoting APIs are obsolete</span></span>

<span data-ttu-id="82816-102">某些与远程处理相关的 API 标记为已过时，并在编译时生成 `SYSLIB0010` 警告。</span><span class="sxs-lookup"><span data-stu-id="82816-102">Some remoting-related APIs are marked as obsolete and generate a `SYSLIB0010` warning at compile time.</span></span> <span data-ttu-id="82816-103">.NET 的未来版本中将删除这些 API。</span><span class="sxs-lookup"><span data-stu-id="82816-103">These APIs may be removed in a future version of .NET.</span></span>

#### <a name="change-description"></a><span data-ttu-id="82816-104">更改描述</span><span class="sxs-lookup"><span data-stu-id="82816-104">Change description</span></span>

<span data-ttu-id="82816-105">以下远程处理 API 标记为已过时。</span><span class="sxs-lookup"><span data-stu-id="82816-105">The following remoting APIs are marked obsolete.</span></span>

| <span data-ttu-id="82816-106">API</span><span class="sxs-lookup"><span data-stu-id="82816-106">API</span></span> | <span data-ttu-id="82816-107">在以下版本中标记为已过时…</span><span class="sxs-lookup"><span data-stu-id="82816-107">Marked obsolete in...</span></span> |
| - | - |
| <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType> | <span data-ttu-id="82816-108">5.0 RC1</span><span class="sxs-lookup"><span data-stu-id="82816-108">5.0 RC1</span></span> |
| <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType> | <span data-ttu-id="82816-109">5.0 RC1</span><span class="sxs-lookup"><span data-stu-id="82816-109">5.0 RC1</span></span> |

<span data-ttu-id="82816-110">在 .NET Framework 2.x - 4.x 中，<xref:System.MarshalByRefObject.GetLifetimeService> 和 <xref:System.MarshalByRefObject.InitializeLifetimeService> 方法控制与 .NET 远程处理有关的实例的生存期。</span><span class="sxs-lookup"><span data-stu-id="82816-110">In .NET Framework 2.x - 4.x, the <xref:System.MarshalByRefObject.GetLifetimeService> and <xref:System.MarshalByRefObject.InitializeLifetimeService> methods control the lifetime of instances involved with .NET remoting.</span></span> <span data-ttu-id="82816-111">在 .NET Core 2.x- 3.x 中，这些方法始终会在运行时引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="82816-111">In .NET Core 2.x- 3.x, these methods always throw a <xref:System.PlatformNotSupportedException> at run time.</span></span>

<span data-ttu-id="82816-112">在 .NET 5.0 和更高版本中，<xref:System.MarshalByRefObject.GetLifetimeService> 和 <xref:System.MarshalByRefObject.InitializeLifetimeService> 方法以警告的形式标记为已过时，但仍在运行时引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="82816-112">In .NET 5.0 and later versions, the <xref:System.MarshalByRefObject.GetLifetimeService> and <xref:System.MarshalByRefObject.InitializeLifetimeService> methods are marked obsolete as warning, but continue to throw a <xref:System.PlatformNotSupportedException> at run time.</span></span>

```csharp
// MemoryStream, like all Stream instances, subclasses MarshalByRefObject.
MemoryStream stream = new MemoryStream();
// Throws PlatformNotSupportedException; also produces warning SYSLIB0010.
obj.InitializeLifetimeService();
```

<span data-ttu-id="82816-113">这是仅在编译时进行的更改。</span><span class="sxs-lookup"><span data-stu-id="82816-113">This is a compile-time only change.</span></span> <span data-ttu-id="82816-114">以前版本的 .NET Core 没有运行时更改。</span><span class="sxs-lookup"><span data-stu-id="82816-114">There is no run-time change from previous versions of .NET Core.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="82816-115">更改原因</span><span class="sxs-lookup"><span data-stu-id="82816-115">Reason for change</span></span>

<span data-ttu-id="82816-116">[.NET 远程处理](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71))是一项传统技术。</span><span class="sxs-lookup"><span data-stu-id="82816-116">[.NET remoting](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) is a legacy technology.</span></span> <span data-ttu-id="82816-117">它允许实例化另一个进程中的对象（甚至可能在不同的计算机上），并与该对象进行交互，就好像它是普通的进程内 .NET 对象实例一样。</span><span class="sxs-lookup"><span data-stu-id="82816-117">It allows instantiating an object in another process (potentially even on a different machine) and interacting with that object as if it were an ordinary, in-process .NET object instance.</span></span> <span data-ttu-id="82816-118">.NET 远程处理基础结构仅存在于 .NET Framework 2.x - 4.x 中。</span><span class="sxs-lookup"><span data-stu-id="82816-118">The .NET remoting infrastructure only exists in .NET Framework 2.x - 4.x.</span></span> <span data-ttu-id="82816-119">.NET Core 和 .NET 5.0 及更高版本不支持 .NET 远程处理，远程处理 API 要么不存在，要么始终在这些运行时引发异常。</span><span class="sxs-lookup"><span data-stu-id="82816-119">.NET Core and .NET 5.0 and later versions don't have support for .NET remoting, and the remoting APIs either don't exist or always throw exceptions on these runtimes.</span></span>

<span data-ttu-id="82816-120">为帮助开发人员摒弃这些 API，我们正在淘汰选定的远程处理相关 API。</span><span class="sxs-lookup"><span data-stu-id="82816-120">To help steer developers away from these APIs, we are obsoleting selected remoting-related APIs.</span></span> <span data-ttu-id="82816-121">.NET 的未来版本中可能完全删除这些 API。</span><span class="sxs-lookup"><span data-stu-id="82816-121">These APIs may be removed entirely in a future version of .NET.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="82816-122">引入的版本</span><span class="sxs-lookup"><span data-stu-id="82816-122">Version introduced</span></span>

<span data-ttu-id="82816-123">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="82816-123">.NET 5.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="82816-124">建议操作</span><span class="sxs-lookup"><span data-stu-id="82816-124">Recommended action</span></span>

- <span data-ttu-id="82816-125">请考虑使用 WCF 或基于 HTTP 的 REST 服务与其他应用程序的对象或跨计算机进行通信。</span><span class="sxs-lookup"><span data-stu-id="82816-125">Consider using WCF or HTTP-based REST services to communicate with objects in other applications or across machines.</span></span> <span data-ttu-id="82816-126">有关详细信息，请参阅 [.NET Framework 技术在 .NET Core 上不可用](../../../../docs/core/porting/net-framework-tech-unavailable.md)。</span><span class="sxs-lookup"><span data-stu-id="82816-126">For more information, see [.NET Framework technologies unavailable on .NET Core](../../../../docs/core/porting/net-framework-tech-unavailable.md).</span></span>

- <span data-ttu-id="82816-127">如果必须继续使用已过时的 API，可在代码中取消 `SYSLIB0010` 警告。</span><span class="sxs-lookup"><span data-stu-id="82816-127">If you must continue to use the obsolete APIs, you can suppress the `SYSLIB0010` warning in code.</span></span>

  ```csharp
  MarshalByRefObject obj = GetMarshalByRefObj();
  #pragma warning disable SYSLIB0010 // Disable the warning.
  obj.InitializeLifetimeService(); // Still throws PNSE.
  obj.GetLifetimeService(); // Still throws PNSE.
  #pragma warning restore SYSLIB0010 // Reenable the warning.
  ```

  <span data-ttu-id="82816-128">还可以在项目文件中取消警告，这将对项目中的所有源文件禁用警告。</span><span class="sxs-lookup"><span data-stu-id="82816-128">You can also suppress the warning in your project file, which disables the warning for all source files in the project.</span></span>

  ```xml
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
     <TargetFramework>net5.0</TargetFramework>
     <!-- NoWarn below will suppress SYSLIB0010 project-wide -->
     <NoWarn>$(NoWarn);SYSLIB0010</NoWarn>
    </PropertyGroup>
  </Project>
  ```

  <span data-ttu-id="82816-129">取消 `SYSLIB0010` 仅禁用远程处理 API 过时警告。</span><span class="sxs-lookup"><span data-stu-id="82816-129">Suppressing `SYSLIB0010` disables only the remoting API obsoletion warnings.</span></span> <span data-ttu-id="82816-130">它不会禁用任何其他警告。</span><span class="sxs-lookup"><span data-stu-id="82816-130">It does not disable any other warnings.</span></span> <span data-ttu-id="82816-131">此外，它不会更改此硬编码运行时行为（即始终引发 <xref:System.PlatformNotSupportedException>）。</span><span class="sxs-lookup"><span data-stu-id="82816-131">Additionally, it doesn't change the hardcoded run-time behavior of always throwing <xref:System.PlatformNotSupportedException>.</span></span>

#### <a name="category"></a><span data-ttu-id="82816-132">类别</span><span class="sxs-lookup"><span data-stu-id="82816-132">Category</span></span>

<span data-ttu-id="82816-133">Core .NET 库</span><span class="sxs-lookup"><span data-stu-id="82816-133">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="82816-134">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="82816-134">Affected APIs</span></span>

- <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=fullName>
- <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.MarshalByRefObject.GetLifetimeService`
- `M:System.MarshalByRefObject.InitializeLifetimeService`

-->
