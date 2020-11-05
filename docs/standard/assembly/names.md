---
title: 程序集名称
description: 了解 .NET 程序集名称及其对程序集范围的影响并将其用于应用程序，并了解 FullName 属性。
ms.date: 08/19/2019
helpviewer_keywords:
- names [.NET], assemblies
- assemblies [.NET], names
ms.assetid: 8f8c2c90-f15d-400e-87e7-a757e4f04d0e
ms.openlocfilehash: 136c3b7a06ce72be02e00bcc4d2354160178468c
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687579"
---
# <a name="assembly-names"></a><span data-ttu-id="2bb79-103">程序集名称</span><span class="sxs-lookup"><span data-stu-id="2bb79-103">Assembly names</span></span>

<span data-ttu-id="2bb79-104">程序集的名称存储在元数据中，它对程序集的范围及应用程序对程序集的使用有重要影响。</span><span class="sxs-lookup"><span data-stu-id="2bb79-104">An assembly's name is stored in metadata and has a significant impact on the assembly's scope and use by an application.</span></span> <span data-ttu-id="2bb79-105">强名称程序集有一个完全限定的名称，由程序集的名称、区域性、公钥、版本号以及（可选）处理器体系结构组成。</span><span class="sxs-lookup"><span data-stu-id="2bb79-105">A strong-named assembly has a fully qualified name that includes the assembly's name, culture, public key, version number, and, optionally, processor architecture.</span></span> <span data-ttu-id="2bb79-106">使用 <xref:System.Reflection.Assembly.FullName%2A> 属性来获取已加载程序集的完全限定名称，该名称通常称为显示名称。</span><span class="sxs-lookup"><span data-stu-id="2bb79-106">Use the <xref:System.Reflection.Assembly.FullName%2A> property to obtain the fully qualified name, frequently referred to as the display name, for loaded assemblies.</span></span>

<span data-ttu-id="2bb79-107">运行时使用此名称信息来定位程序集并将其同其他同名的程序集区分开。</span><span class="sxs-lookup"><span data-stu-id="2bb79-107">The runtime uses the name information to locate the assembly and differentiate it from other assemblies with the same name.</span></span> <span data-ttu-id="2bb79-108">例如，名为 `myTypes` 的强名称程序集可以具有下列完全限定名：</span><span class="sxs-lookup"><span data-stu-id="2bb79-108">For example, a strong-named assembly called `myTypes` could have the following fully qualified name:</span></span>

```
myTypes, Version=1.0.1234.0, Culture=en-US, PublicKeyToken=b77a5c561934e089c, ProcessorArchitecture=msil
```

<span data-ttu-id="2bb79-109">在此例中，完全限定名称表明 `myTypes` 程序集的强名称具有公钥标记、区域性值为美国英语、版本号为 1.0.1234.0。</span><span class="sxs-lookup"><span data-stu-id="2bb79-109">In this example, the fully qualified name indicates that the `myTypes` assembly has a strong name with a public key token, has the culture value for United States English, and has a version number of 1.0.1234.0.</span></span> <span data-ttu-id="2bb79-110">它的处理器体系结构为 `msil`，表示程序集将以实时 (JIT) 方式编译为 32 位代码或 64 位代码（具体取决于操作系统和处理器）。</span><span class="sxs-lookup"><span data-stu-id="2bb79-110">Its processor architecture is `msil`, which means that it will be just-in-time (JIT)-compiled to 32-bit code or 64-bit code depending on the operating system and processor.</span></span>

> [!TIP]
> <span data-ttu-id="2bb79-111">`ProcessorArchitecture` 信息允许特定于处理器的程序集版本。</span><span class="sxs-lookup"><span data-stu-id="2bb79-111">The `ProcessorArchitecture` information allows processor-specific versions of assemblies.</span></span> <span data-ttu-id="2bb79-112">可以创建某程序集的多个版本，其标识的差异仅在于处理器体系结构不同，例如特定于 32 位和 64 位处理器的版本。</span><span class="sxs-lookup"><span data-stu-id="2bb79-112">You can create versions of an assembly whose identity differs only by processor architecture, for example 32-bit and 64-bit processor-specific versions.</span></span> <span data-ttu-id="2bb79-113">处理器体系结构对于强名称不是必需的。</span><span class="sxs-lookup"><span data-stu-id="2bb79-113">Processor architecture is not required for strong names.</span></span> <span data-ttu-id="2bb79-114">有关详细信息，请参阅 <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="2bb79-114">For more information, see <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A?displayProperty=nameWithType>.</span></span>

 <span data-ttu-id="2bb79-115">请求程序集中的类型的代码必须使用完全限定的程序集名称。</span><span class="sxs-lookup"><span data-stu-id="2bb79-115">Code that requests types in an assembly must use a fully qualified assembly name.</span></span> <span data-ttu-id="2bb79-116">这称为完全限定绑定。</span><span class="sxs-lookup"><span data-stu-id="2bb79-116">This is called fully qualified binding.</span></span> <span data-ttu-id="2bb79-117">在 .NET Framework 中引用程序集时不允许使用部分绑定，因为它只指定一个程序集名称。</span><span class="sxs-lookup"><span data-stu-id="2bb79-117">Partial binding, which specifies only an assembly name, is not permitted when referencing assemblies in .NET Framework.</span></span>

 <span data-ttu-id="2bb79-118">对组成 .NET Framework 的程序集的所有程序集引用也必须包含程序集的完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="2bb79-118">All assembly references to assemblies that make up .NET Framework must also contain the fully qualified name of the assembly.</span></span> <span data-ttu-id="2bb79-119">例如，若要引用 1.0 版的 System.Data .NET Framework 程序集，需要包括：</span><span class="sxs-lookup"><span data-stu-id="2bb79-119">For example, a reference to the System.Data .NET Framework assembly for version 1.0 would include:</span></span>

```
System.data, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
```

<span data-ttu-id="2bb79-120">该版本与随 .NET Framework 1.0 版一起提供的所有 .NET Framework 程序集的版本号相对应。</span><span class="sxs-lookup"><span data-stu-id="2bb79-120">The version corresponds to the version number of all .NET Framework assemblies that shipped with .NET Framework version 1.0.</span></span> <span data-ttu-id="2bb79-121">对于 .NET Framework 程序集，区域性值始终不是特定的，公钥与上例中所示公钥相同。</span><span class="sxs-lookup"><span data-stu-id="2bb79-121">For .NET Framework assemblies, the culture value is always neutral, and the public key is the same as shown in the above example.</span></span>

 <span data-ttu-id="2bb79-122">例如，若要在配置文件中添加程序集引用以设置跟踪侦听器，需要包括系统 .NET Framework 程序集的完全限定名：</span><span class="sxs-lookup"><span data-stu-id="2bb79-122">For example, to add an assembly reference in a configuration file to set up a trace listener, you would include the fully qualified name of the system .NET Framework assembly:</span></span>

```xml
<add name="myListener" type="System.Diagnostics.TextWriterTraceListener, System, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />
```

> [!NOTE]
> <span data-ttu-id="2bb79-123">绑定到程序集时，运行时不区分程序集名称的大小写，但会保留程序集名称中使用的大小写。</span><span class="sxs-lookup"><span data-stu-id="2bb79-123">The runtime treats assembly names as case-insensitive when binding to an assembly, but preserves whatever case is used in an assembly name.</span></span> <span data-ttu-id="2bb79-124">Windows SDK 中的几个工具会区分程序集名称的大小写。</span><span class="sxs-lookup"><span data-stu-id="2bb79-124">Several tools in the Windows SDK handle assembly names as case-sensitive.</span></span> <span data-ttu-id="2bb79-125">为获得最佳效果，管理程序集名称时请按区分大小写的方式来处理。</span><span class="sxs-lookup"><span data-stu-id="2bb79-125">For best results, manage assembly names as though they were case-sensitive.</span></span>

## <a name="name-application-components"></a><span data-ttu-id="2bb79-126">命名应用程序组件</span><span class="sxs-lookup"><span data-stu-id="2bb79-126">Name application components</span></span>
 <span data-ttu-id="2bb79-127">运行时在确定程序集的标识时不考虑文件名。</span><span class="sxs-lookup"><span data-stu-id="2bb79-127">The runtime does not consider the file name when determining an assembly's identity.</span></span> <span data-ttu-id="2bb79-128">程序集标识（由程序集名称、版本、区域性和强名称组成）对运行时必须清楚明了。</span><span class="sxs-lookup"><span data-stu-id="2bb79-128">The assembly identity, which consists of the assembly name, version, culture, and strong name, must be clear to the runtime.</span></span>

 <span data-ttu-id="2bb79-129">例如，如果一个名为 myAssembly.exe 的程序集引用一个名为 myAssembly.dll 的程序集，则在执行 myAssembly.exe 时会正确进行绑定  。</span><span class="sxs-lookup"><span data-stu-id="2bb79-129">For example, if you have an assembly called *myAssembly.exe* that references an assembly called *myAssembly.dll* , binding occurs correctly if you execute *myAssembly.exe*.</span></span> <span data-ttu-id="2bb79-130">但是，如果另一个应用程序使用 <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=nameWithType> 方法执行 myAssembly.exe，则当 myAssembly.exe 请求绑定到 `myAssembly` 时，运行时会确定 `myAssembly` 已经加载 。</span><span class="sxs-lookup"><span data-stu-id="2bb79-130">However, if another application executes *myAssembly.exe* using the method <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=nameWithType>, the runtime determines that `myAssembly` is already loaded when *myAssembly.exe* requests binding to `myAssembly`.</span></span> <span data-ttu-id="2bb79-131">在这种情况下，不会加载 myAssembly.dll。</span><span class="sxs-lookup"><span data-stu-id="2bb79-131">In this case, *myAssembly.dll* is never loaded.</span></span> <span data-ttu-id="2bb79-132">由于 myAssembly.exe 不包含请求的类型，因此会发生 <xref:System.TypeLoadException>。</span><span class="sxs-lookup"><span data-stu-id="2bb79-132">Because *myAssembly.exe* does not contain the requested type, a <xref:System.TypeLoadException> occurs.</span></span>

 <span data-ttu-id="2bb79-133">为避免这个问题，请确保组成应用程序的程序集具有不同的程序集名称，或者将名称相同的程序集放在不同的目录中。</span><span class="sxs-lookup"><span data-stu-id="2bb79-133">To avoid this problem, make sure the assemblies that make up your application do not have the same assembly name or place assemblies with the same name in different directories.</span></span>

> [!NOTE]
> <span data-ttu-id="2bb79-134">在 .NET Framework 中，如果将强名称程序集置于全局程序集缓存中，则程序集的文件名必须与程序集名称相匹配，不包括文件扩展名，如 .exe 或 .dll 。</span><span class="sxs-lookup"><span data-stu-id="2bb79-134">In .NET Framework, if you put a strong-named assembly in the global assembly cache, the assembly's file name must match the assembly name, not including the file name extension, such as *.exe* or *.dll*.</span></span> <span data-ttu-id="2bb79-135">例如，如果程序集的文件名为 myAssembly.dll，则程序集名称必须为 `myAssembly`。</span><span class="sxs-lookup"><span data-stu-id="2bb79-135">For example, if the file name of an assembly is *myAssembly.dll* , the assembly name must be `myAssembly`.</span></span> <span data-ttu-id="2bb79-136">只有在根应用程序目录中部署的专用程序集的程序集名称可以不同于文件名。</span><span class="sxs-lookup"><span data-stu-id="2bb79-136">Private assemblies deployed only in the root application directory can have an assembly name that is different from the file name.</span></span>

## <a name="see-also"></a><span data-ttu-id="2bb79-137">请参阅</span><span class="sxs-lookup"><span data-stu-id="2bb79-137">See also</span></span>

- [<span data-ttu-id="2bb79-138">如何：确定程序集的完全限定名称</span><span class="sxs-lookup"><span data-stu-id="2bb79-138">How to: Determine an assembly's fully qualified name</span></span>](find-fully-qualified-name.md)
- [<span data-ttu-id="2bb79-139">创建程序集</span><span class="sxs-lookup"><span data-stu-id="2bb79-139">Create assemblies</span></span>](create.md)
- [<span data-ttu-id="2bb79-140">具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="2bb79-140">Strong-named assemblies</span></span>](strong-named.md)
- [<span data-ttu-id="2bb79-141">全局程序集缓存</span><span class="sxs-lookup"><span data-stu-id="2bb79-141">Global assembly cache</span></span>](../../framework/app-domains/gac.md)
- [<span data-ttu-id="2bb79-142">运行时如何定位程序集</span><span class="sxs-lookup"><span data-stu-id="2bb79-142">How the runtime locates assemblies</span></span>](../../framework/deployment/how-the-runtime-locates-assemblies.md)
