---
ms.openlocfilehash: 959d8cb6d3e52916f6777054f3e9b327dc8edb4e
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434960"
---
### <a name="global-assembly-cache-apis-are-obsolete"></a><span data-ttu-id="20e58-101">全局程序集缓存 API 已过时</span><span class="sxs-lookup"><span data-stu-id="20e58-101">Global assembly cache APIs are obsolete</span></span>

<span data-ttu-id="20e58-102">.NET Core 和 .NET 5.0 及更高版本消除了 .NET Framework 中存在的全局程序集缓存 (GAC) 这一概念。</span><span class="sxs-lookup"><span data-stu-id="20e58-102">.NET Core and .NET 5.0 and later versions eliminate the concept of the global assembly cache (GAC) that was present in .NET Framework.</span></span> <span data-ttu-id="20e58-103">因此，所有处理 GAC 的 .NETCore 和 .NET 5+ API 要么失败，要么不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="20e58-103">As such, all .NET Core and .NET 5+ APIs that deal with the GAC either fail or perform no operation.</span></span>

<span data-ttu-id="20e58-104">为帮助开发人员摒弃这些 API，一些 GAC 相关的 API 标记为已过时，并在编译时生成 `SYSLIB0005` 警告。</span><span class="sxs-lookup"><span data-stu-id="20e58-104">To help steer developers away from these APIs, some GAC-related APIs are marked as obsolete, and generate a `SYSLIB0005` warning at compile time.</span></span> <span data-ttu-id="20e58-105">.NET 的未来版本中将删除这些 API。</span><span class="sxs-lookup"><span data-stu-id="20e58-105">These APIs may be removed in a future version of .NET.</span></span>

#### <a name="change-description"></a><span data-ttu-id="20e58-106">更改描述</span><span class="sxs-lookup"><span data-stu-id="20e58-106">Change description</span></span>

<span data-ttu-id="20e58-107">以下 API 标记为已过时。</span><span class="sxs-lookup"><span data-stu-id="20e58-107">The following APIs are marked obsolete.</span></span>

| <span data-ttu-id="20e58-108">API</span><span class="sxs-lookup"><span data-stu-id="20e58-108">API</span></span> | <span data-ttu-id="20e58-109">在以下版本中标记为已过时…</span><span class="sxs-lookup"><span data-stu-id="20e58-109">Marked obsolete in...</span></span> |
| - | - |
| <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=nameWithType> | <span data-ttu-id="20e58-110">5.0 RC1</span><span class="sxs-lookup"><span data-stu-id="20e58-110">5.0 RC1</span></span> |

<span data-ttu-id="20e58-111">在 .NET Framework 2.x - 4.x 中，如果从 GAC 加载了查询的程序集，则 <xref:System.Reflection.Assembly.GlobalAssemblyCache> 属性返回 `true`，如果从磁盘的不同位置加载了该程序集，则返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="20e58-111">In .NET Framework 2.x - 4.x, the <xref:System.Reflection.Assembly.GlobalAssemblyCache> property returns `true` if the queried assembly was loaded from the GAC, and `false` if it was loaded from a different location on disk.</span></span> <span data-ttu-id="20e58-112">在 .NET Core 2.x - 3.x 中，<xref:System.Reflection.Assembly.GlobalAssemblyCache> 始终返回 `false`，这表明 GAC 在 .NET Core 中不存在。</span><span class="sxs-lookup"><span data-stu-id="20e58-112">In .NET Core 2.x - 3.x, the <xref:System.Reflection.Assembly.GlobalAssemblyCache> always returns `false`, reflecting that the GAC does not exist in .NET Core.</span></span>

```csharp
Assembly asm = typeof(object).Assembly;
// Prints 'True' on .NET Framework, 'False' on .NET Core.
Console.WriteLine(asm.GlobalAssemblyCache);
```

<span data-ttu-id="20e58-113">在 .NET 5.0 和更高版本中，<xref:System.Reflection.Assembly.GlobalAssemblyCache> 属性仍始终返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="20e58-113">In .NET 5.0 and later versions, the <xref:System.Reflection.Assembly.GlobalAssemblyCache> property continues to always return `false`.</span></span> <span data-ttu-id="20e58-114">然而，属性 Getter 也标记为已过时，以指示调用方应停止访问该属性。</span><span class="sxs-lookup"><span data-stu-id="20e58-114">However, the property getter is also marked as obsolete to indicate to callers that they should stop accessing the property.</span></span> <span data-ttu-id="20e58-115">库和应用不应使用 <xref:System.Reflection.Assembly.GlobalAssemblyCache> API 来确定运行时行为，因为它在 .NET Core 和 .NET 5.0 及更高版本中始终返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="20e58-115">Libraries and apps should not use the <xref:System.Reflection.Assembly.GlobalAssemblyCache> API to make determinations about run-time behavior, as it always returns `false` in .NET Core and .NET 5.0 and later versions.</span></span>

```csharp
Assembly asm = typeof(object).Assembly;
// Prints 'False' on .NET 5.0+; also produces warning SYSLIB0005 at compile time.
Console.WriteLine(asm.GlobalAssemblyCache);
```

<span data-ttu-id="20e58-116">这是仅在编译时进行的更改。</span><span class="sxs-lookup"><span data-stu-id="20e58-116">This is a compile-time only change.</span></span> <span data-ttu-id="20e58-117">以前版本的 .NET Core 没有运行时更改。</span><span class="sxs-lookup"><span data-stu-id="20e58-117">There is no run-time change from previous versions of .NET Core.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="20e58-118">更改原因</span><span class="sxs-lookup"><span data-stu-id="20e58-118">Reason for change</span></span>

<span data-ttu-id="20e58-119">全局程序集缓存 (GAC) 这一概念不存在于 .NET Core 和 .NET 5.0 及更高版本中。</span><span class="sxs-lookup"><span data-stu-id="20e58-119">The global assembly cache (GAC) does not exist as a concept in .NET Core and .NET 5.0 and later versions.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="20e58-120">引入的版本</span><span class="sxs-lookup"><span data-stu-id="20e58-120">Version introduced</span></span>

<span data-ttu-id="20e58-121">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="20e58-121">.NET 5.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="20e58-122">建议操作</span><span class="sxs-lookup"><span data-stu-id="20e58-122">Recommended action</span></span>

- <span data-ttu-id="20e58-123">如果你的应用程序查询 <xref:System.Reflection.Assembly.GlobalAssemblyCache> 属性，请考虑删除该调用。</span><span class="sxs-lookup"><span data-stu-id="20e58-123">If your application queries the <xref:System.Reflection.Assembly.GlobalAssemblyCache> property, consider removing the call.</span></span> <span data-ttu-id="20e58-124">如果在运行时使用 <xref:System.Reflection.Assembly.GlobalAssemblyCache> 值在“GAC 中的程序集”流与“不在 GAC 中的程序集”流之间进行选择，请重新考虑流对于.NET Core 或 .NET 5.0+ 应用程序是否仍然有意义。</span><span class="sxs-lookup"><span data-stu-id="20e58-124">If you use the <xref:System.Reflection.Assembly.GlobalAssemblyCache> value to choose between an "assembly in the GAC"-flow vs. an "assembly not in the GAC"-flow at run time, reconsider whether the flow still makes sense for a .NET Core or .NET 5.0+ application.</span></span>

- <span data-ttu-id="20e58-125">如果必须继续使用已过时的 API，可在代码中取消 `SYSLIB0005` 警告。</span><span class="sxs-lookup"><span data-stu-id="20e58-125">If you must continue to use the obsolete APIs, you can suppress the `SYSLIB0005` warning in code.</span></span>

  ```csharp
  Assembly asm = typeof(object).Assembly;
  #pragma warning disable SYSLIB0005 // Disable the warning.
  // Prints 'False' on .NET 5.0+.
  Console.WriteLine(asm.GlobalAssemblyCache);
  #pragma warning restore SYSLIB0005 // Re-enable the warning.
  ```

  <span data-ttu-id="20e58-126">还可以在项目文件中取消警告，这将对项目中的所有源文件禁用警告。</span><span class="sxs-lookup"><span data-stu-id="20e58-126">You can also suppress the warning in your project file, which disables the warning for all source files in the project.</span></span>

  ```xml
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
     <TargetFramework>net5.0</TargetFramework>
     <!-- NoWarn below will suppress SYSLIB0005 project-wide -->
     <NoWarn>$(NoWarn);SYSLIB0005</NoWarn>
    </PropertyGroup>
  </Project>
  ```

  <span data-ttu-id="20e58-127">取消 `SYSLIB0005` 仅禁用 <xref:System.Reflection.Assembly.GlobalAssemblyCache> 过时警告。</span><span class="sxs-lookup"><span data-stu-id="20e58-127">Suppressing `SYSLIB0005` disables only the <xref:System.Reflection.Assembly.GlobalAssemblyCache> obsoletion warning.</span></span> <span data-ttu-id="20e58-128">它不会禁用任何其他警告。</span><span class="sxs-lookup"><span data-stu-id="20e58-128">It does not disable any other warnings.</span></span>

#### <a name="category"></a><span data-ttu-id="20e58-129">类别</span><span class="sxs-lookup"><span data-stu-id="20e58-129">Category</span></span>

<span data-ttu-id="20e58-130">Core .NET 库</span><span class="sxs-lookup"><span data-stu-id="20e58-130">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="20e58-131">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="20e58-131">Affected APIs</span></span>

- <xref:System.Reflection.Assembly.GlobalAssemblyCache?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Reflection.Assembly.GlobalAssemblyCache`

-->
