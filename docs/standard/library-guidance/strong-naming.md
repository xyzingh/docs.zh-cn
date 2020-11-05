---
title: 强命名和 .NET 库
description: 强命名 .NET 库的最佳实践建议。
ms.date: 10/16/2018
ms.openlocfilehash: 6f9533d768331964a8e640243536b12ddde158e5
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189207"
---
# <a name="strong-naming"></a><span data-ttu-id="346df-103">强命名</span><span class="sxs-lookup"><span data-stu-id="346df-103">Strong naming</span></span>

<span data-ttu-id="346df-104">强命名指使用密钥对程序集进行签名，从而生成[强名称程序集](../assembly/strong-named.md)。</span><span class="sxs-lookup"><span data-stu-id="346df-104">Strong naming refers to signing an assembly with a key, producing a [strong-named assembly](../assembly/strong-named.md).</span></span> <span data-ttu-id="346df-105">程序集具有强名称时，将基于名称和程序集版本号创建唯一标识，并有助于防止发生程序集冲突。</span><span class="sxs-lookup"><span data-stu-id="346df-105">When an assembly is strong-named, it creates a unique identity based on the name and assembly version number, and it can help prevent assembly conflicts.</span></span>

<span data-ttu-id="346df-106">强命名的缺点是，一旦程序集具有强名称，Windows 上的 .NET Framework 就会严格加载程序集。</span><span class="sxs-lookup"><span data-stu-id="346df-106">The downside to strong naming is that .NET Framework on Windows enables strict loading of assemblies once an assembly is strong named.</span></span> <span data-ttu-id="346df-107">强名称程序集引用必须与已加载的程序集版本完全匹配，强制开发人员在使用程序集时[配置绑定重定向](../../framework/configure-apps/redirect-assembly-versions.md)：</span><span class="sxs-lookup"><span data-stu-id="346df-107">A strong-named assembly reference must exactly match the version of the loaded assembly, forcing developers to [configure binding redirects](../../framework/configure-apps/redirect-assembly-versions.md) when using the assembly:</span></span>

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="neutral" />
            <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

<span data-ttu-id="346df-108">当 .NET 开发人员抱怨强命名时，通常抱怨的是严格的程序集加载。</span><span class="sxs-lookup"><span data-stu-id="346df-108">When .NET developers complain about strong naming, what they're usually complaining about is strict assembly loading.</span></span> <span data-ttu-id="346df-109">幸运的是，此问题独立于 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="346df-109">Fortunately, this issue is isolated to .NET Framework.</span></span> <span data-ttu-id="346df-110">.NET 5+、.NET Core、Xamarin、UWP 和大多数其他 .NET 实现没有严格的程序集加载（强命名的主要缺点）。</span><span class="sxs-lookup"><span data-stu-id="346df-110">.NET 5+, .NET Core, Xamarin, UWP, and most other .NET implementations don't have strict assembly loading, which is the main downside of strong naming.</span></span>

<span data-ttu-id="346df-111">强命名的一个重要方面是它已迅速传播开了：某个强名称程序集只能引用其他强名称程序集。</span><span class="sxs-lookup"><span data-stu-id="346df-111">One important aspect of strong naming is that it's viral: a strong named assembly can only reference other strong named assemblies.</span></span> <span data-ttu-id="346df-112">如果你的库未强命名，则会阻止生成需要强命名的应用程序或库的开发人员使用该库。</span><span class="sxs-lookup"><span data-stu-id="346df-112">If your library isn't strong named, then you have excluded developers who are building an application or library that needs strong naming from using it.</span></span>

<span data-ttu-id="346df-113">强命名的优点包括：</span><span class="sxs-lookup"><span data-stu-id="346df-113">The benefits of strong naming are:</span></span>

1. <span data-ttu-id="346df-114">程序集可以被引用并由其他强名称程序集使用。</span><span class="sxs-lookup"><span data-stu-id="346df-114">The assembly can be referenced and used by other strong-named assemblies.</span></span>
2. <span data-ttu-id="346df-115">程序集可以存储在全局程序集缓存 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="346df-115">The assembly can be stored in the Global Assembly Cache (GAC).</span></span>
3. <span data-ttu-id="346df-116">程序集可以与其他版本的程序集并行加载。</span><span class="sxs-lookup"><span data-stu-id="346df-116">The assembly can be loaded side by side with other versions of the assembly.</span></span> <span data-ttu-id="346df-117">具有插件体系结构的应用程序通常需要并行程序集加载。</span><span class="sxs-lookup"><span data-stu-id="346df-117">Side-by-side assembly loading is commonly required by applications with plug-in architectures.</span></span>

## <a name="create-strong-named-net-libraries"></a><span data-ttu-id="346df-118">创建强名称 .NET 库</span><span class="sxs-lookup"><span data-stu-id="346df-118">Create strong named .NET libraries</span></span>

<span data-ttu-id="346df-119">应强命名开放源代码 .NET 库。</span><span class="sxs-lookup"><span data-stu-id="346df-119">You should strong name your open-source .NET libraries.</span></span> <span data-ttu-id="346df-120">强命名程序集可确保大多数人可以使用它，并且严格的程序集加载仅影响 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="346df-120">Strong naming an assembly ensures the most people can use it, and strict assembly loading only affects .NET Framework.</span></span>

> [!NOTE]
> <span data-ttu-id="346df-121">本指南特定于公开分布的 .NET 库，如 NuGet.org 上发布的 .NET 库。强命名不是大多数 .NET 应用程序所必需的，默认情况下不得执行强命名。</span><span class="sxs-lookup"><span data-stu-id="346df-121">This guidance is specific to publicly distributed .NET libraries, such as .NET libraries published on NuGet.org. Strong naming is not required by most .NET applications and should not be done by default.</span></span>

<span data-ttu-id="346df-122">✔️ 请考虑强命名库的程序集。</span><span class="sxs-lookup"><span data-stu-id="346df-122">✔️ CONSIDER strong naming your library's assemblies.</span></span>

<span data-ttu-id="346df-123">✔️ 请考虑将强命名密钥添加到源代码管理系统。</span><span class="sxs-lookup"><span data-stu-id="346df-123">✔️ CONSIDER adding the strong naming key to your source control system.</span></span>

> <span data-ttu-id="346df-124">公开提供的密钥可让开发人员修改库源代码并使用相同的密钥进行重新编译。</span><span class="sxs-lookup"><span data-stu-id="346df-124">A publicly available key lets developers modify and recompile your library source code with the same key.</span></span>
>
> <span data-ttu-id="346df-125">如果强命名密钥过去用于在[部分信任的方案](../../framework/misc/using-libraries-from-partially-trusted-code.md)中授予特殊权限，则不得公开该强命名密钥。</span><span class="sxs-lookup"><span data-stu-id="346df-125">You shouldn't make the strong naming key public if it has been used in the past to give special permissions in [partial-trust scenarios](../../framework/misc/using-libraries-from-partially-trusted-code.md).</span></span> <span data-ttu-id="346df-126">或者，可能会破坏现有环境。</span><span class="sxs-lookup"><span data-stu-id="346df-126">Otherwise, you might compromise existing environments.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="346df-127">需要了解代码发布者的身份时，建议使用[验证码](/windows-hardware/drivers/install/authenticode)和 [NuGet 包签名](/nuget/create-packages/sign-a-package)。</span><span class="sxs-lookup"><span data-stu-id="346df-127">When the identity of the publisher of the code is desired, [Authenticode](/windows-hardware/drivers/install/authenticode) and [NuGet Package Signing](/nuget/create-packages/sign-a-package) are recommended.</span></span> <span data-ttu-id="346df-128">代码访问安全性 (CAS) 不得用作安全缓解。</span><span class="sxs-lookup"><span data-stu-id="346df-128">Code Access Security (CAS) should not be used as a security mitigation.</span></span>

<span data-ttu-id="346df-129">✔️ 请考虑仅在主版本发生更改时递增程序集版本，以帮助用户减少绑定重定向和更新频率。</span><span class="sxs-lookup"><span data-stu-id="346df-129">✔️ CONSIDER incrementing the assembly version on only major version changes to help users reduce binding redirects, and how often they're updated.</span></span>

> <span data-ttu-id="346df-130">详细了解[版本控制和程序集版本](./versioning.md#assembly-version)。</span><span class="sxs-lookup"><span data-stu-id="346df-130">Read more about [versioning and the assembly version](./versioning.md#assembly-version).</span></span>

<span data-ttu-id="346df-131">❌ 请勿添加、删除或更改强命名密钥。</span><span class="sxs-lookup"><span data-stu-id="346df-131">❌ DO NOT add, remove, or change the strong naming key.</span></span>

> <span data-ttu-id="346df-132">修改程序集的强命名密钥会更改程序集的标识并破坏使用该标识的已编译代码。</span><span class="sxs-lookup"><span data-stu-id="346df-132">Modifying an assembly's strong naming key changes the assembly's identity and breaks compiled code that uses it.</span></span> <span data-ttu-id="346df-133">有关详细信息，请参阅[二进制重大更改](./breaking-changes.md#binary-breaking-change)。</span><span class="sxs-lookup"><span data-stu-id="346df-133">For more information, see [binary breaking changes](./breaking-changes.md#binary-breaking-change).</span></span>

<span data-ttu-id="346df-134">❌ 请勿发布库的强名称和非强名称版本。</span><span class="sxs-lookup"><span data-stu-id="346df-134">❌ DO NOT publish strong-named and non-strong-named versions of your library.</span></span> <span data-ttu-id="346df-135">例如，`Contoso.Api` 和 `Contoso.Api.StrongNamed`。</span><span class="sxs-lookup"><span data-stu-id="346df-135">For example, `Contoso.Api` and `Contoso.Api.StrongNamed`.</span></span>

> <span data-ttu-id="346df-136">发布两个包会为开发人员生态系统创建分支。</span><span class="sxs-lookup"><span data-stu-id="346df-136">Publishing two packages forks your developer eco-system.</span></span> <span data-ttu-id="346df-137">此外，如果应用程序依赖于这两个包，则开发人员可能会遇到类型名称冲突。</span><span class="sxs-lookup"><span data-stu-id="346df-137">Also, if an application ends up depending on both packages the developer can encounter type name conflicts.</span></span> <span data-ttu-id="346df-138">就 .NET 而言，它们是不同程序集中的不同类型。</span><span class="sxs-lookup"><span data-stu-id="346df-138">As far as .NET is concerned they are different types in different assemblies.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="346df-139">[上一页](cross-platform-targeting.md)
>[下一页](nuget.md)</span><span class="sxs-lookup"><span data-stu-id="346df-139">[Previous](cross-platform-targeting.md)
[Next](nuget.md)</span></span>
