---
title: 程序集和并行执行
description: 了解并行执行，它是在同一台计算机上存储和运行应用程序或组件的多个版本的能力。
ms.date: 08/20/2019
helpviewer_keywords:
- side-by-side execution [.NET]
- assemblies [.NET], side-by-side execution
ms.assetid: e42036ee-7590-47d1-b884-cc856e39bd5d
ms.openlocfilehash: 7bedd5a384ceace014412eb894adad5c92c00b05
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687977"
---
# <a name="assemblies-and-side-by-side-execution"></a><span data-ttu-id="9a6ab-103">程序集和并行执行</span><span class="sxs-lookup"><span data-stu-id="9a6ab-103">Assemblies and side-by-side execution</span></span>

<span data-ttu-id="9a6ab-104">并行执行是在同一台计算机上存储和执行应用程序或组件的多个版本的能力。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-104">Side-by-side execution is the ability to store and execute multiple versions of an application or component on the same computer.</span></span> <span data-ttu-id="9a6ab-105">这意味着在同一台计算机上可以同时有运行时的多个版本，并且可以有使用其中某个运行时版本的应用程序和组件的多个版本。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-105">This means that you can have multiple versions of the runtime, and multiple versions of applications and components that use a version of the runtime, on the same computer at the same time.</span></span> <span data-ttu-id="9a6ab-106">并行执行使您能够更多地控制应用程序绑定到的组件版本和应用程序使用的运行时版本。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-106">Side-by-side execution gives you more control over what versions of a component an application binds to, and more control over what version of the runtime an application uses.</span></span>  
  
<span data-ttu-id="9a6ab-107">支持并行存储和执行同一程序集的不同版本是强命名中不可缺少的部分，这种支持内置于运行时基础结构中。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-107">Support for side-by-side storage and execution of different versions of the same assembly is an integral part of strong naming and is built into the infrastructure of the runtime.</span></span> <span data-ttu-id="9a6ab-108">因为强名称程序集的版本号是其标识的一部分，所以运行时能够在全局程序集缓存中存储同一程序集的多个版本，并且在运行时加载这些程序集。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-108">Because the strong-named assembly's version number is part of its identity, the runtime can store multiple versions of the same assembly in the global assembly cache and load those assemblies at run time.</span></span>  
  
<span data-ttu-id="9a6ab-109">尽管运行时使您能够创建并行应用程序，但并行执行并不是自动进行的。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-109">Although the runtime provides you with the ability to create side-by-side applications, side-by-side execution is not automatic.</span></span> <span data-ttu-id="9a6ab-110">有关创建并行执行的应用程序的详细信息，请参阅[并行执行的组件的创建指南](../../framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="9a6ab-110">For more information on creating applications for side-by-side execution, see [Guidelines for creating components for side-by-side execution](../../framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9a6ab-111">请参阅</span><span class="sxs-lookup"><span data-stu-id="9a6ab-111">See also</span></span>

- [<span data-ttu-id="9a6ab-112">运行时如何定位程序集</span><span class="sxs-lookup"><span data-stu-id="9a6ab-112">How the runtime locates assemblies</span></span>](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [<span data-ttu-id="9a6ab-113">.NET 中的程序集</span><span class="sxs-lookup"><span data-stu-id="9a6ab-113">Assemblies in .NET</span></span>](index.md)
