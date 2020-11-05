---
title: 公共语言运行时 (CLR) 概述 - .NET
titleSuffix: ''
description: 公共语言运行时 (CLR)（.NET 的运行时环境）入门。 CLR 运行代码并提供服务，使开发过程更轻松。
ms.date: 10/22/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- compiling source code, runtime functionality
- code, execution
- managed data
- runtime
- common language runtime
- metadata, runtime functionality
- .NET, common language runtime
- language compilers
- managed code
- source code execution
- code, runtime functionality
ms.assetid: 059a624e-f7db-4134-ba9f-08b676050482
ms.custom: updateeachrelease
ms.openlocfilehash: 39543a511e8f405d9205df2697bcf4fd1194bd7a
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687516"
---
# <a name="common-language-runtime-clr-overview"></a><span data-ttu-id="24f66-104">公共语言运行时 (CLR) 概述</span><span class="sxs-lookup"><span data-stu-id="24f66-104">Common Language Runtime (CLR) overview</span></span>

<span data-ttu-id="24f66-105">.NET 提供了一个称为公共语言运行时的运行时环境，它运行代码并提供使开发过程更轻松的服务。</span><span class="sxs-lookup"><span data-stu-id="24f66-105">.NET provides a run-time environment, called the common language runtime, that runs the code and provides services that make the development process easier.</span></span>

<span data-ttu-id="24f66-106">公共语言运行时的功能通过编译器和工具公开，你可以编写利用此托管执行环境的代码。</span><span class="sxs-lookup"><span data-stu-id="24f66-106">Compilers and tools expose the common language runtime's functionality and enable you to write code that benefits from this managed execution environment.</span></span> <span data-ttu-id="24f66-107">使用面向运行时的语言编译器开发的代码称为托管代码。</span><span class="sxs-lookup"><span data-stu-id="24f66-107">Code that you develop with a language compiler that targets the runtime is called managed code.</span></span> <span data-ttu-id="24f66-108">托管代码具有许多优点，例如：跨语言集成、跨语言异常处理、增强的安全性、版本控制和部署支持、简化的组件交互模型、调试和分析服务等。</span><span class="sxs-lookup"><span data-stu-id="24f66-108">Managed code benefits from features such as cross-language integration, cross-language exception handling, enhanced security, versioning and deployment support, a simplified model for component interaction, and debugging and profiling services.</span></span>

> [!NOTE]
> <span data-ttu-id="24f66-109">编译器和工具可以产生公共语言运行时可以使用的输出，因为类型系统、元数据格式和该运行时环境（虚拟执行系统）都由公共标准（ECMA 公共语言基础结构规范）定义。</span><span class="sxs-lookup"><span data-stu-id="24f66-109">Compilers and tools are able to produce output that the common language runtime can consume because the type system, the format of metadata, and the run-time environment (the virtual execution system) are all defined by a public standard, the ECMA Common Language Infrastructure specification.</span></span> <span data-ttu-id="24f66-110">有关详细信息，请参阅 [ECMA C# 和公共语言基础结构规范](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/)。</span><span class="sxs-lookup"><span data-stu-id="24f66-110">For more information, see [ECMA C# and Common Language Infrastructure Specifications](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/).</span></span>

<span data-ttu-id="24f66-111">若要使公共语言运行时能够向托管代码提供服务，语言编译器必须生成一些元数据来描述代码中的类型、成员和引用。</span><span class="sxs-lookup"><span data-stu-id="24f66-111">To enable the runtime to provide services to managed code, language compilers must emit metadata that describes the types, members, and references in your code.</span></span> <span data-ttu-id="24f66-112">元数据与代码一起存储；每个可加载的公共语言运行时可迁移执行 (PE) 文件都包含元数据。</span><span class="sxs-lookup"><span data-stu-id="24f66-112">Metadata is stored with the code; every loadable common language runtime portable executable (PE) file contains metadata.</span></span> <span data-ttu-id="24f66-113">公共语言运行时使用元数据来完成以下任务：查找和加载类，在内存中安排实例，解析方法调用，生成本机代码，强制安全性，以及设置运行时上下文边界。</span><span class="sxs-lookup"><span data-stu-id="24f66-113">The runtime uses metadata to locate and load classes, lay out instances in memory, resolve method invocations, generate native code, enforce security, and set run-time context boundaries.</span></span>

<span data-ttu-id="24f66-114">公共语言运行时自动处理对象布局并管理对象引用，当不再使用对象时释放它们。</span><span class="sxs-lookup"><span data-stu-id="24f66-114">The runtime automatically handles object layout and manages references to objects, releasing them when they are no longer being used.</span></span> <span data-ttu-id="24f66-115">按这种方式实现生存期管理的对象称为托管数据。</span><span class="sxs-lookup"><span data-stu-id="24f66-115">Objects whose lifetimes are managed in this way are called managed data.</span></span> <span data-ttu-id="24f66-116">垃圾回收消除了内存泄漏以及其他一些常见的编程错误。</span><span class="sxs-lookup"><span data-stu-id="24f66-116">Garbage collection eliminates memory leaks as well as some other common programming errors.</span></span> <span data-ttu-id="24f66-117">如果你编写的代码是托管代码，则可以在 .NET 应用程序中使用托管数据、非托管数据或者同时使用这两种数据。</span><span class="sxs-lookup"><span data-stu-id="24f66-117">If your code is managed, you can use managed data, unmanaged data, or both managed and unmanaged data in your .NET application.</span></span> <span data-ttu-id="24f66-118">由于语言编译器会提供自己的类型（如基元类型），因此你可能并不总是知道（或需要知道）这些数据是否是托管的。</span><span class="sxs-lookup"><span data-stu-id="24f66-118">Because language compilers supply their own types, such as primitive types, you might not always know (or need to know) whether your data is being managed.</span></span>

<span data-ttu-id="24f66-119">有了公共语言运行时，就可以很容易地设计出对象能够跨语言交互的组件和应用程序。</span><span class="sxs-lookup"><span data-stu-id="24f66-119">The common language runtime makes it easy to design components and applications whose objects interact across languages.</span></span> <span data-ttu-id="24f66-120">也就是说，用不同语言编写的对象可以互相通信，并且它们的行为可以紧密集成。</span><span class="sxs-lookup"><span data-stu-id="24f66-120">Objects written in different languages can communicate with each other, and their behaviors can be tightly integrated.</span></span> <span data-ttu-id="24f66-121">例如，可以定义一个类，然后使用不同的语言从原始类派生出另一个类或调用原始类的方法。</span><span class="sxs-lookup"><span data-stu-id="24f66-121">For example, you can define a class and then use a different language to derive a class from your original class or call a method on the original class.</span></span> <span data-ttu-id="24f66-122">还可以将一个类的实例传递到用不同的语言编写的另一个类的方法。</span><span class="sxs-lookup"><span data-stu-id="24f66-122">You can also pass an instance of a class to a method of a class written in a different language.</span></span> <span data-ttu-id="24f66-123">这种跨语言集成之所以成为可能，是因为基于公共语言运行时的语言编译器和工具使用由公共语言运行时定义的常规类型系统，而且它们遵循公共语言运行时关于定义新类型以及创建、使用、保持和绑定到类型的规则。</span><span class="sxs-lookup"><span data-stu-id="24f66-123">This cross-language integration is possible because language compilers and tools that target the runtime use a common type system defined by the runtime, and they follow the runtime's rules for defining new types, as well as for creating, using, persisting, and binding to types.</span></span>

<span data-ttu-id="24f66-124">所有托管组件都带有生成它们所基于的组件和资源的信息，这些信息构成了元数据的一部分。</span><span class="sxs-lookup"><span data-stu-id="24f66-124">As part of their metadata, all managed components carry information about the components and resources they were built against.</span></span> <span data-ttu-id="24f66-125">公共语言运行时使用这些信息确保组件或应用程序具有它需要的所有内容的指定版本，这样就使代码不太可能由于某些未满足的依赖项而发生中断。</span><span class="sxs-lookup"><span data-stu-id="24f66-125">The runtime uses this information to ensure that your component or application has the specified versions of everything it needs, which makes your code less likely to break because of some unmet dependency.</span></span> <span data-ttu-id="24f66-126">注册信息和状态数据不再保存在注册表中（因为在注册表中建立和维护这些信息很困难）。</span><span class="sxs-lookup"><span data-stu-id="24f66-126">Registration information and state data are no longer stored in the registry where they can be difficult to establish and maintain.</span></span> <span data-ttu-id="24f66-127">取而代之的是，有关你定义的类型（及其依赖项）的信息作为元数据与代码存储在一起，这样大大降低了组件复制和移除任务的复杂性。</span><span class="sxs-lookup"><span data-stu-id="24f66-127">Instead, information about the types you define (and their dependencies) is stored with the code as metadata, making the tasks of component replication and removal much less complicated.</span></span>

<span data-ttu-id="24f66-128">语言编译器和工具公开公共语言运行时的功能的方式对于开发人员来说不仅很有用，而且很直观。</span><span class="sxs-lookup"><span data-stu-id="24f66-128">Language compilers and tools expose the runtime's functionality in ways that are intended to be useful and intuitive to developers.</span></span> <span data-ttu-id="24f66-129">这意味着，公共语言运行时的某些功能可能在一个环境中比在另一个环境中更突出。</span><span class="sxs-lookup"><span data-stu-id="24f66-129">This means that some features of the runtime might be more noticeable in one environment than in another.</span></span> <span data-ttu-id="24f66-130">你对公共语言运行时的体验取决于所使用的语言编译器或工具。</span><span class="sxs-lookup"><span data-stu-id="24f66-130">How you experience the runtime depends on which language compilers or tools you use.</span></span> <span data-ttu-id="24f66-131">例如，如果你是一位 Visual Basic 开发人员，你可能会注意到：有了公共语言运行时，Visual Basic 语言的面向对象的功能比以前多了。</span><span class="sxs-lookup"><span data-stu-id="24f66-131">For example, if you are a Visual Basic developer, you might notice that with the common language runtime, the Visual Basic language has more object-oriented features than before.</span></span> <span data-ttu-id="24f66-132">运行时提供如下优点：</span><span class="sxs-lookup"><span data-stu-id="24f66-132">The runtime provides the following benefits:</span></span>

- <span data-ttu-id="24f66-133">性能得到了改进。</span><span class="sxs-lookup"><span data-stu-id="24f66-133">Performance improvements.</span></span>

- <span data-ttu-id="24f66-134">能够轻松使用用其他语言开发的组件。</span><span class="sxs-lookup"><span data-stu-id="24f66-134">The ability to easily use components developed in other languages.</span></span>

- <span data-ttu-id="24f66-135">类库提供的可扩展类型。</span><span class="sxs-lookup"><span data-stu-id="24f66-135">Extensible types provided by a class library.</span></span>

- <span data-ttu-id="24f66-136">语言功能，如面向对象的编程的继承、接口和重载。</span><span class="sxs-lookup"><span data-stu-id="24f66-136">Language features such as inheritance, interfaces, and overloading for object-oriented programming.</span></span>

- <span data-ttu-id="24f66-137">允许创建多线程的可缩放应用程序的显式自由线程处理支持。</span><span class="sxs-lookup"><span data-stu-id="24f66-137">Support for explicit free threading that allows creation of multithreaded, scalable applications.</span></span>

- <span data-ttu-id="24f66-138">结构化异常处理支持。</span><span class="sxs-lookup"><span data-stu-id="24f66-138">Support for structured exception handling.</span></span>

- <span data-ttu-id="24f66-139">自定义特性支持。</span><span class="sxs-lookup"><span data-stu-id="24f66-139">Support for custom attributes.</span></span>

- <span data-ttu-id="24f66-140">垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="24f66-140">Garbage collection.</span></span>

- <span data-ttu-id="24f66-141">使用委托取代函数指针，从而增强了类型安全和安全性。</span><span class="sxs-lookup"><span data-stu-id="24f66-141">Use of delegates instead of function pointers for increased type safety and security.</span></span> <span data-ttu-id="24f66-142">有关委派的详细信息，请参阅[通用类型系统](base-types/common-type-system.md)。</span><span class="sxs-lookup"><span data-stu-id="24f66-142">For more information about delegates, see [Common Type System](base-types/common-type-system.md).</span></span>

## <a name="clr-versions"></a><span data-ttu-id="24f66-143">CLR 版本</span><span class="sxs-lookup"><span data-stu-id="24f66-143">CLR versions</span></span>

<span data-ttu-id="24f66-144">.NET Core 和 .NET 5+ 版本具有一个产品版本，即没有单独的 CLR 版本。</span><span class="sxs-lookup"><span data-stu-id="24f66-144">.NET Core and .NET 5+ releases have a single product version, that is, there is no separate CLR version.</span></span> <span data-ttu-id="24f66-145">有关 .NET Core 版本的列表，请参阅[下载 .NET Core](https://dotnet.microsoft.com/download/dotnet-core)。</span><span class="sxs-lookup"><span data-stu-id="24f66-145">For a list of .NET Core versions, see [Download .NET Core](https://dotnet.microsoft.com/download/dotnet-core).</span></span>

<span data-ttu-id="24f66-146">但是，.NET Framework 版本号并非一定要与其包含的 CLR 的版本号相对应。</span><span class="sxs-lookup"><span data-stu-id="24f66-146">However, the .NET Framework version number doesn't necessarily correspond to the version number of the CLR it includes.</span></span> <span data-ttu-id="24f66-147">有关 .NET Framework 版本及其相应 CLR 版本的列表，请参阅 [.NET Framework 版本及依赖项](../framework/migration-guide/versions-and-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="24f66-147">For a list of .NET Framework versions and their corresponding CLR versions, see [.NET Framework versions and dependencies](../framework/migration-guide/versions-and-dependencies.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="24f66-148">相关主题</span><span class="sxs-lookup"><span data-stu-id="24f66-148">Related topics</span></span>

|<span data-ttu-id="24f66-149">Title</span><span class="sxs-lookup"><span data-stu-id="24f66-149">Title</span></span>|<span data-ttu-id="24f66-150">描述</span><span class="sxs-lookup"><span data-stu-id="24f66-150">Description</span></span>|
|-----------|-----------------|
|[<span data-ttu-id="24f66-151">托管执行过程</span><span class="sxs-lookup"><span data-stu-id="24f66-151">Managed Execution Process</span></span>](managed-execution-process.md)|<span data-ttu-id="24f66-152">描述使用公共语言运行时所需要的步骤。</span><span class="sxs-lookup"><span data-stu-id="24f66-152">Describes the steps required to take advantage of the common language runtime.</span></span>|
|[<span data-ttu-id="24f66-153">自动内存管理</span><span class="sxs-lookup"><span data-stu-id="24f66-153">Automatic Memory Management</span></span>](automatic-memory-management.md)|<span data-ttu-id="24f66-154">描述垃圾回收器如何分配和释放内存。</span><span class="sxs-lookup"><span data-stu-id="24f66-154">Describes how the garbage collector allocates and releases memory.</span></span>|
|[<span data-ttu-id="24f66-155">.NET Framework 概述</span><span class="sxs-lookup"><span data-stu-id="24f66-155">Overview of .NET Framework</span></span>](../framework/get-started/overview.md)|<span data-ttu-id="24f66-156">描述关键的 .NET Framework 概念，例如通用类型系统、跨语言互操作性、托管执行、应用程序域和程序集。</span><span class="sxs-lookup"><span data-stu-id="24f66-156">Describes key .NET Framework concepts, such as the common type system, cross-language interoperability, managed execution, application domains, and assemblies.</span></span>|
|[<span data-ttu-id="24f66-157">常规类型系统</span><span class="sxs-lookup"><span data-stu-id="24f66-157">Common Type System</span></span>](./base-types/common-type-system.md)|<span data-ttu-id="24f66-158">描述在运行时中如何声明、使用和管理类型以支持跨语言集成。</span><span class="sxs-lookup"><span data-stu-id="24f66-158">Describes how types are declared, used, and managed in the runtime in support of cross-language integration.</span></span>|
