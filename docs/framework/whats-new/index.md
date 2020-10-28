---
title: .NET Framework 中的新增功能
description: 了解不同版本 .NET Framework 中的新变化。 阅读每个版本的主要新功能和改进的摘要。
ms.date: 10/21/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
ms.assetid: 1d971dd7-10fc-4692-8dac-30ca308fc0fa
ms.openlocfilehash: 13346836b6cc1c9db4a1b6fd93a11615c2a843c0
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687566"
---
# <a name="whats-new-in-net-framework"></a><span data-ttu-id="4d376-104">.NET Framework 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-104">What's new in .NET Framework</span></span>

[!INCLUDE [net-framework-future](../../../includes/net-framework-future.md)]

<span data-ttu-id="4d376-105">本文总结了以下版本的 .NET Framework 中的主要新功能和改进：</span><span class="sxs-lookup"><span data-stu-id="4d376-105">This article summarizes key new features and improvements in the following versions of .NET Framework:</span></span>

- [<span data-ttu-id="4d376-106">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="4d376-106">.NET Framework 4.8</span></span>](#v48)
- [<span data-ttu-id="4d376-107">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="4d376-107">.NET Framework 4.7.2</span></span>](#v472)
- [<span data-ttu-id="4d376-108">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="4d376-108">.NET Framework 4.7.1</span></span>](#v471)
- [<span data-ttu-id="4d376-109">.NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="4d376-109">.NET Framework 4.7</span></span>](#v47)
- [<span data-ttu-id="4d376-110">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="4d376-110">.NET Framework 4.6.2</span></span>](#v462)
- [<span data-ttu-id="4d376-111">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="4d376-111">.NET Framework 4.6.1</span></span>](#v461)
- [<span data-ttu-id="4d376-112">.NET 2015 和 .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="4d376-112">.NET 2015 and .NET Framework 4.6</span></span>](#v46)
- [<span data-ttu-id="4d376-113">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="4d376-113">.NET Framework 4.5.2</span></span>](#v452)
- [<span data-ttu-id="4d376-114">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="4d376-114">.NET Framework 4.5.1</span></span>](#v451)
- [<span data-ttu-id="4d376-115">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="4d376-115">.NET Framework 4.5</span></span>](#v45)

<span data-ttu-id="4d376-116">本文不提供有关每项新增功能的完整信息，并有可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="4d376-116">This article does not provide comprehensive information about each new feature and is subject to change.</span></span> <span data-ttu-id="4d376-117">有关 .NET Framework 的常规信息，请参阅[入门](../get-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-117">For general information about .NET Framework, see [Getting Started](../get-started/index.md).</span></span> <span data-ttu-id="4d376-118">有关支持的平台，请参阅[系统要求](../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-118">For supported platforms, see [System Requirements](../get-started/system-requirements.md).</span></span> <span data-ttu-id="4d376-119">有关下载链接和安装说明，请参阅[安装指南](../install/guide-for-developers.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-119">For download links and installation instructions, see [Installation Guide](../install/guide-for-developers.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4d376-120">.NET Framework 团队还发布 NuGet 带外功能以扩展平台支持并引入新功能，如不可变集合和启用了 SIMD 的矢量类型。</span><span class="sxs-lookup"><span data-stu-id="4d376-120">The .NET Framework team also releases features out of band, using NuGet, to expand platform support and introduce new functionality, such as immutable collections and SIMD-enabled vector types.</span></span> <span data-ttu-id="4d376-121">有关详细信息，请参阅[其他类库和 API](../additional-apis/index.md) 以及 [.NET Framework 和带外版本](../get-started/the-net-framework-and-out-of-band-releases.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-121">For more information, see [Additional Class Libraries and APIs](../additional-apis/index.md) and [.NET Framework and Out-of-Band Releases](../get-started/the-net-framework-and-out-of-band-releases.md).</span></span>
> <span data-ttu-id="4d376-122">请参阅用于 .NET Framework 的 [完整 NuGet 包列表](https://www.nuget.org/profiles/dotnetframework)。</span><span class="sxs-lookup"><span data-stu-id="4d376-122">See a [complete list of NuGet packages](https://www.nuget.org/profiles/dotnetframework) for .NET Framework.</span></span>

<a name="v48"></a>

## <a name="introducing-net-framework-48"></a><span data-ttu-id="4d376-123">.NET Framework 4.8 简介</span><span class="sxs-lookup"><span data-stu-id="4d376-123">Introducing .NET Framework 4.8</span></span>

<span data-ttu-id="4d376-124">.NET Framework 4.8 在 .NET Framework 4.x 早期版本的基础之上构建而成，新增了许多修补程序和功能，同时很好地保持了产品的稳定性。</span><span class="sxs-lookup"><span data-stu-id="4d376-124">.NET Framework 4.8 builds on previous versions of .NET Framework 4.x by adding many new fixes and several new features while remaining a very stable product.</span></span>

### <a name="download-and-install-net-framework-48"></a><span data-ttu-id="4d376-125">下载和安装 .NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="4d376-125">Download and install .NET Framework 4.8</span></span>

<span data-ttu-id="4d376-126">可以从下列位置下载 .NET Framework 4.8：</span><span class="sxs-lookup"><span data-stu-id="4d376-126">You can download .NET Framework 4.8 from the following locations:</span></span>

- [<span data-ttu-id="4d376-127">.NET Framework 4.8 Web 安装程序</span><span class="sxs-lookup"><span data-stu-id="4d376-127">.NET Framework 4.8 Web Installer</span></span>](https://dotnet.microsoft.com/download/dotnet-framework/net48)

- [<span data-ttu-id="4d376-128">NET Framework 4.8 脱机安装程序</span><span class="sxs-lookup"><span data-stu-id="4d376-128">NET Framework 4.8 Offline Installer</span></span>](https://dotnet.microsoft.com/download/dotnet-framework/net48)

<span data-ttu-id="4d376-129">可以在 Windows 10、Windows 8.1、Windows 7 SP1 和对应的服务器平台（版本不低于 Windows Server 2008 R2 SP1）上安装 .NET Framework 4.8。</span><span class="sxs-lookup"><span data-stu-id="4d376-129">.NET Framework 4.8 can be installed on Windows 10, Windows 8.1, Windows 7 SP1, and the corresponding server platforms starting with Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="4d376-130">可以使用 Web 安装程序或脱机安装程序来安装 .NET Framework 4.8。</span><span class="sxs-lookup"><span data-stu-id="4d376-130">You can install .NET Framework 4.8 by using either the web installer or the offline installer.</span></span> <span data-ttu-id="4d376-131">适用于大多数用户的建议方法是使用 Web 安装程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-131">The recommended way for most users is to use the web installer.</span></span>

<span data-ttu-id="4d376-132">可以通过安装 [.NET Framework 4.8 开发人员工具包](https://go.microsoft.com/fwlink/?LinkId=2085167)，在 Visual Studio 2012 或更高版本中定位 .NET Framework 4.8。</span><span class="sxs-lookup"><span data-stu-id="4d376-132">You can target .NET Framework 4.8 in Visual Studio 2012 or later by installing the [.NET Framework 4.8 Developer Pack](https://go.microsoft.com/fwlink/?LinkId=2085167).</span></span>

### <a name="whats-new-in-net-framework-48"></a><span data-ttu-id="4d376-133">.NET Framework 4.8 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-133">What's new in .NET Framework 4.8</span></span>

<span data-ttu-id="4d376-134">.NET Framework 4.8 在以下几个领域引入了新功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-134">.NET Framework 4.8 introduces new features in the following areas:</span></span>

- [<span data-ttu-id="4d376-135">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-135">Base classes</span></span>](#core48)
- [<span data-ttu-id="4d376-136">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="4d376-136">Windows Communication Foundation (WCF)</span></span>](#wcf48)
- [<span data-ttu-id="4d376-137">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-137">Windows Presentation Foundation (WPF)</span></span>](#wpf48)
- [<span data-ttu-id="4d376-138">公共语言运行时</span><span class="sxs-lookup"><span data-stu-id="4d376-138">Common language runtime</span></span>](#clr48)

<span data-ttu-id="4d376-139">改进了辅助功能，使应用程序能为辅助技术的用户提供最佳体验，这仍是 .NET Framework 4.8 的重点。</span><span class="sxs-lookup"><span data-stu-id="4d376-139">Improved accessibility, which allows an application to provide an appropriate experience for users of Assistive Technology, continues to be a major focus of .NET Framework 4.8.</span></span> <span data-ttu-id="4d376-140">有关 .NET Framework 4.8 中辅助功能改进的信息，请参阅 [.NET Framework 中辅助功能的新增功能](whats-new-in-accessibility.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-140">For information on accessibility improvements in .NET Framework 4.8, see [What's new in accessibility in .NET Framework](whats-new-in-accessibility.md).</span></span>

<a name="core48"></a>

#### <a name="base-classes"></a><span data-ttu-id="4d376-141">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-141">Base classes</span></span>

<span data-ttu-id="4d376-142">**减少 FIPS 对加密的影响** 。</span><span class="sxs-lookup"><span data-stu-id="4d376-142">**Reduced FIPS impact on Cryptography** .</span></span> <span data-ttu-id="4d376-143">在 .NET framework 的早期版本中，当在“FIPS 模式”下配置系统加密库时，<xref:System.Security.Cryptography.SHA256Managed> 等托管加密提供程序类会引发 <xref:System.Security.Cryptography.CryptographicException>。</span><span class="sxs-lookup"><span data-stu-id="4d376-143">In previous versions of .NET Framework, managed cryptographic provider classes such as <xref:System.Security.Cryptography.SHA256Managed> throw a <xref:System.Security.Cryptography.CryptographicException> when the system cryptographic libraries are configured in "FIPS mode".</span></span> <span data-ttu-id="4d376-144">引发这些异常的原因是加密提供程序类的托管版本尚未进行 FIPS（联邦信息处理标准）140-2 认证，这与系统加密库不同。</span><span class="sxs-lookup"><span data-stu-id="4d376-144">These exceptions are thrown because the managed versions of the cryptographic provider classes, unlike the system cryptographic libraries, have not undergone FIPS (Federal Information Processing Standards) 140-2 certification.</span></span> <span data-ttu-id="4d376-145">由于几个开发人员使其开发计算机处于 FIPS 模式，因此通常会在生产系统中引发异常。</span><span class="sxs-lookup"><span data-stu-id="4d376-145">Because few developers have their development machines in FIPS mode, the exceptions are commonly thrown in production systems.</span></span>

<span data-ttu-id="4d376-146">默认情况下，在面向 .NET Framework 4.8 的应用程序中，以下托管加密类在这种情况下不再引发 <xref:System.Security.Cryptography.CryptographicException>：</span><span class="sxs-lookup"><span data-stu-id="4d376-146">By default in applications that target .NET Framework 4.8, the following managed cryptography classes no longer throw a <xref:System.Security.Cryptography.CryptographicException> in this case:</span></span>

- <xref:System.Security.Cryptography.MD5Cng>
- <xref:System.Security.Cryptography.MD5CryptoServiceProvider>
- <xref:System.Security.Cryptography.RC2CryptoServiceProvider>
- <xref:System.Security.Cryptography.RijndaelManaged>
- <xref:System.Security.Cryptography.RIPEMD160Managed>
- <xref:System.Security.Cryptography.SHA256Managed>

<span data-ttu-id="4d376-147">相反，这些类会将加密操作重定向到系统加密库。</span><span class="sxs-lookup"><span data-stu-id="4d376-147">Instead, these classes redirect cryptographic operations to a system cryptography library.</span></span> <span data-ttu-id="4d376-148">此更改可有效地删除开发人员环境和生产环境之间可能令人混淆的差异，并使本机组件和托管组件采用相同的加密策略运行。</span><span class="sxs-lookup"><span data-stu-id="4d376-148">This change effectively removes a potentially confusing difference between developer environments and production environments and makes native components and managed components operate under the same cryptographic policy.</span></span> <span data-ttu-id="4d376-149">依赖于这些异常的应用程序可以通过将 AppContext 开关 `Switch.System.Security.Cryptography.UseLegacyFipsThrow` 设置为 `true` 来还原以前的行为。</span><span class="sxs-lookup"><span data-stu-id="4d376-149">Applications that depend on these exceptions can restore the previous behavior by setting the AppContext switch `Switch.System.Security.Cryptography.UseLegacyFipsThrow` to `true`.</span></span> <span data-ttu-id="4d376-150">有关详细信息，请参阅[托管加密类不会在 FIPS 模式下引发 CryptographyException](../migration-guide/retargeting/4.7.2-4.8.md#managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode)。</span><span class="sxs-lookup"><span data-stu-id="4d376-150">For more information, see [Managed cryptography classes do not throw a CryptographyException in FIPS mode](../migration-guide/retargeting/4.7.2-4.8.md#managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode).</span></span>

<span data-ttu-id="4d376-151">**使用 ZLib 的更新版本**</span><span class="sxs-lookup"><span data-stu-id="4d376-151">**Use of updated version of ZLib**</span></span>

<span data-ttu-id="4d376-152">从 .NET Framework 4.5 开始，clrcompression.dll 程序集使用 [ZLib](https://www.zlib.net)（即，数据压缩的本机外部库），以便提供 deflate 算法实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-152">Starting with .NET Framework 4.5, the clrcompression.dll assembly uses [ZLib](https://www.zlib.net), a native external library for data compression, in order to provide an implementation for the deflate algorithm.</span></span> <span data-ttu-id="4d376-153">在 .NET Framework 4.8 版本中，clrcompression.dll 更新为使用 ZLib 版本 1.2.11，其中包括几个主要的改进和修补程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-153">The .NET Framework 4.8 version of clrcompression.dll is updated to use ZLib Version 1.2.11, which includes several key improvements and fixes.</span></span>

<a name="wcf48"></a>

#### <a name="windows-communication-foundation-wcf"></a><span data-ttu-id="4d376-154">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="4d376-154">Windows Communication Foundation (WCF)</span></span>

<span data-ttu-id="4d376-155">**ServiceHealthBehavior 简介**</span><span class="sxs-lookup"><span data-stu-id="4d376-155">**Introduction of ServiceHealthBehavior**</span></span>

<span data-ttu-id="4d376-156">运行状况终结点由业务流程工具广泛使用以基于其运行状况状态来管理服务。</span><span class="sxs-lookup"><span data-stu-id="4d376-156">Health endpoints are widely used by orchestration tools to manage services based on their health status.</span></span> <span data-ttu-id="4d376-157">运行状况检查还可由监视工具使用以跟踪并提供有关服务的可用性和性能的通知。</span><span class="sxs-lookup"><span data-stu-id="4d376-157">Health checks can also be used by monitoring tools to track and provide notifications about the availability and performance of a service.</span></span>

<span data-ttu-id="4d376-158">ServiceHealthBehavior 是一个 WCF 服务行为，该行为可扩展 <xref:System.ServiceModel.Description.IServiceBehavior>。</span><span class="sxs-lookup"><span data-stu-id="4d376-158">**ServiceHealthBehavior** is a WCF service behavior that extends <xref:System.ServiceModel.Description.IServiceBehavior>.</span></span>  <span data-ttu-id="4d376-159">添加到 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors?displayProperty=nameWithType> 集合后，服务行为会执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="4d376-159">When added to the <xref:System.ServiceModel.Description.ServiceDescription.Behaviors?displayProperty=nameWithType> collection, a service behavior does the following:</span></span>

- <span data-ttu-id="4d376-160">返回带有 HTTP 响应代码的服务运行状况状态。</span><span class="sxs-lookup"><span data-stu-id="4d376-160">Returns service health status with HTTP response codes.</span></span> <span data-ttu-id="4d376-161">可以在查询字符串中指定 HTTP/GET 运行状况探测请求的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-161">You can specify in a query string the HTTP status code for a HTTP/GET health probe request.</span></span>

- <span data-ttu-id="4d376-162">发布有关服务运行状况的信息。</span><span class="sxs-lookup"><span data-stu-id="4d376-162">Publishes information about service health.</span></span> <span data-ttu-id="4d376-163">服务特定的详细信息，包括可以使用带有 `?health` 查询字符串的 HTTP/GET 请求显示的服务状态、限制计数和容量。</span><span class="sxs-lookup"><span data-stu-id="4d376-163">Service-specific details, including service state, throttle counts, and capacity can be displayed by using an HTTP/GET request with the `?health` query string.</span></span> <span data-ttu-id="4d376-164">对行为不正常的 WCF 服务进行故障排除时，可以轻松访问此类信息则很重要。</span><span class="sxs-lookup"><span data-stu-id="4d376-164">Ease of access to such information is important when troubleshooting a misbehaving WCF service.</span></span>

<span data-ttu-id="4d376-165">可通过两种方式公开运行状况终结点并发布 WCF 服务运行状况信息：</span><span class="sxs-lookup"><span data-stu-id="4d376-165">There are two ways to expose the health endpoint and publish WCF service health information:</span></span>

- <span data-ttu-id="4d376-166">通过代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-166">Through code.</span></span> <span data-ttu-id="4d376-167">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-167">For example:</span></span>

  ```csharp
  ServiceHost host = new ServiceHost(typeof(Service1),
                     new Uri("http://contoso:81/Service1"));
  ServiceHealthBehavior healthBehavior =
      host.Description.Behaviors.Find<ServiceHealthBehavior>();
  healthBehavior ??= new ServiceHealthBehavior();
  host.Description.Behaviors.Add(healthBehavior);
  ```

  ```vb
  Dim host As New ServiceHost(GetType(Service1),
              New Uri("http://contoso:81/Service1"))
  Dim healthBehavior As ServiceHealthBehavior =
     host.Description.Behaviors.Find(Of ServiceHealthBehavior)()
  If healthBehavior Is Nothing Then
     healthBehavior = New ServiceHealthBehavior()
  End If
  host.Description.Behaviors.Add(healthBehavior)
  ```

- <span data-ttu-id="4d376-168">通过使用配置文件。</span><span class="sxs-lookup"><span data-stu-id="4d376-168">By using a configuration file.</span></span> <span data-ttu-id="4d376-169">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-169">For example:</span></span>

  ```xml
  <behaviors>
    <serviceBehaviors>
      <behavior name="DefaultBehavior">
        <serviceHealth httpsGetEnabled="true"/>
      </behavior>
    </serviceBehaviors>
  </behaviors>
  ```

<span data-ttu-id="4d376-170">可以使用查询参数（例如，`OnServiceFailure`、`OnDispatcherFailure`、`OnListenerFailure`、`OnThrottlePercentExceeded`）查询服务的运行状况状态，并且可以为每个查询参数指定 HTTP 响应代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-170">A service's health status can be queried by using query parameters such as `OnServiceFailure`, `OnDispatcherFailure`, `OnListenerFailure`, `OnThrottlePercentExceeded`), and an HTTP response code can be specified for each query parameter.</span></span> <span data-ttu-id="4d376-171">如果省略了查询参数的 HTTP 响应代码，则默认使用 503 HTTP 响应代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-171">If the HTTP response code is omitted for a query parameter, a 503 HTTP response code is used by default.</span></span> <span data-ttu-id="4d376-172">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-172">For example:</span></span>

- <span data-ttu-id="4d376-173">OnServiceFailure：`https://contoso:81/Service1?health&OnServiceFailure=450`</span><span class="sxs-lookup"><span data-stu-id="4d376-173">OnServiceFailure: `https://contoso:81/Service1?health&OnServiceFailure=450`</span></span>

  <span data-ttu-id="4d376-174">当 [ServiceHost.State](xref:System.ServiceModel.Channels.CommunicationObject.State) 大于 <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType> 时，将返回 450 HTTP 响应状态代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-174">A 450 HTTP response status code is returned when [ServiceHost.State](xref:System.ServiceModel.Channels.CommunicationObject.State) is greater than <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="4d376-175">查询参数和示例：</span><span class="sxs-lookup"><span data-stu-id="4d376-175">Query parameters and examples:</span></span>

- <span data-ttu-id="4d376-176">OnDispatcherFailure：`https://contoso:81/Service1?health&OnDispatcherFailure=455`</span><span class="sxs-lookup"><span data-stu-id="4d376-176">OnDispatcherFailure: `https://contoso:81/Service1?health&OnDispatcherFailure=455`</span></span>

  <span data-ttu-id="4d376-177">当任意通道调度程序的状态大于 <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType> 时，将返回 455 HTTP 响应状态代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-177">A 455 HTTP response status code is returned when the state of any of the channel dispatchers is greater than <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="4d376-178">OnListenerFailure：`https://contoso:81/Service1?health&OnListenerFailure=465`</span><span class="sxs-lookup"><span data-stu-id="4d376-178">OnListenerFailure: `https://contoso:81/Service1?health&OnListenerFailure=465`</span></span>

  <span data-ttu-id="4d376-179">当任意通道侦听器的状态大于 <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType> 时，将返回 465 HTTP 响应状态代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-179">A 465 HTTP response status code is returned when the state of any of the channel listeners is greater than <xref:System.ServiceModel.CommunicationState.Opened?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="4d376-180">OnThrottlePercentExceeded：`https://contoso:81/Service1?health&OnThrottlePercentExceeded= 70:350,95:500`</span><span class="sxs-lookup"><span data-stu-id="4d376-180">OnThrottlePercentExceeded: `https://contoso:81/Service1?health&OnThrottlePercentExceeded= 70:350,95:500`</span></span>

  <span data-ttu-id="4d376-181">指定触发响应及其 HTTP 响应代码 {200 – 599} 的百分比 {1 – 100}。</span><span class="sxs-lookup"><span data-stu-id="4d376-181">Specifies the percentage {1 – 100} that triggers the response and its HTTP response code {200 – 599}.</span></span> <span data-ttu-id="4d376-182">在此示例中：</span><span class="sxs-lookup"><span data-stu-id="4d376-182">In this example:</span></span>

  - <span data-ttu-id="4d376-183">如果百分比大于 95，则返回 500 HTTP 响应代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-183">If the percentage is greater than 95, a 500 HTTP response code is returned.</span></span>

  - <span data-ttu-id="4d376-184">如果百分比介于 70 和 95 之间，则返回 350。</span><span class="sxs-lookup"><span data-stu-id="4d376-184">If the percentage or between 70 and 95, 350 is returned.</span></span>

  - <span data-ttu-id="4d376-185">否则将返回 200。</span><span class="sxs-lookup"><span data-stu-id="4d376-185">Otherwise, 200 is returned.</span></span>

<span data-ttu-id="4d376-186">服务运行状况状态可以通过指定查询字符串（如 `https://contoso:81/Service1?health`）以 HTML 格式显示，或通过指定查询字符串（如 `https://contoso:81/Service1?health&Xml`）以 XML 格式显示。</span><span class="sxs-lookup"><span data-stu-id="4d376-186">The service health status can be displayed either in HTML by specifying a query string like `https://contoso:81/Service1?health` or in XML by specifying a query string like `https://contoso:81/Service1?health&Xml`.</span></span> <span data-ttu-id="4d376-187">查询字符串（如 `https://contoso:81/Service1?health&NoContent`）返回空 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="4d376-187">A query string like `https://contoso:81/Service1?health&NoContent` returns an empty HTML page.</span></span>

<a name="wpf48"></a>

#### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="4d376-188">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-188">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="4d376-189">**高 DPI 增强功能**</span><span class="sxs-lookup"><span data-stu-id="4d376-189">**High DPI enhancements**</span></span>

<span data-ttu-id="4d376-190">在 .NET Framework 4.8 中，WPF 添加了对按监视器 V2 DPI 感知和混合模式 DPI 缩放的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-190">In .NET Framework 4.8, WPF adds support for Per-Monitor V2 DPI Awareness and Mixed-Mode DPI scaling.</span></span> <span data-ttu-id="4d376-191">有关高 DPI 开发的其他信息，请参阅[在 Windows 上开发高 DPI 桌面应用程序](/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows)。</span><span class="sxs-lookup"><span data-stu-id="4d376-191">See [High DPI Desktop Application Development on Windows](/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows) for additional information about high DPI development.</span></span>

<span data-ttu-id="4d376-192">.NET framework 4.8 改进了对支持混合模式 DPI 缩放的平台上的高 DPI WPF 应用程序中的寄宿 HWND 和 Windows 窗体互操作的支持（从 Windows 10 2018 年 4 月更新开始）。</span><span class="sxs-lookup"><span data-stu-id="4d376-192">.NET Framework 4.8 improves support for hosted HWNDs and Windows Forms interoperation in High-DPI WPF applications on platforms that support Mixed-Mode DPI scaling (starting with Windows 10 April 2018 Update).</span></span> <span data-ttu-id="4d376-193">通过调用 [SetThreadDpiHostingBehavior](/windows/desktop/api/winuser/nf-winuser-setthreaddpihostingbehavior) 和 [SetThreadDpiAwarenessContext](/windows/desktop/api/winuser/nf-winuser-setthreaddpiawarenesscontext) 将寄宿 HWND 或 Windows 窗体控件创建为混合模式 DPI 缩放窗口时，它们可以托管在按监视器 V2 WPF 应用程序中，并且相应地调整大小和缩放。</span><span class="sxs-lookup"><span data-stu-id="4d376-193">When hosted HWNDs or Windows Forms controls are created as Mixed-Mode DPI-scaled windows by calling [SetThreadDpiHostingBehavior](/windows/desktop/api/winuser/nf-winuser-setthreaddpihostingbehavior) and [SetThreadDpiAwarenessContext](/windows/desktop/api/winuser/nf-winuser-setthreaddpiawarenesscontext), they can be hosted in a Per-Monitor V2 WPF application and are sized and scaled appropriately.</span></span> <span data-ttu-id="4d376-194">此类托管内容不以本机 DPI 呈现；相反，操作系统将托管内容缩放到合适大小。</span><span class="sxs-lookup"><span data-stu-id="4d376-194">Such hosted content is not rendered at the native DPI; instead, the operating system scales the hosted content to the appropriate size.</span></span> <span data-ttu-id="4d376-195">对按监视器 v2 DPI 感知模式的支持还允许 WPF 控件托管（即，设置为父级）在高 DPI 应用程序的本机窗口中。</span><span class="sxs-lookup"><span data-stu-id="4d376-195">The support for Per-Monitor v2 DPI awareness mode also allows WPF controls to be hosted (i.e., parented) in a native window in a high-DPI application.</span></span>

<span data-ttu-id="4d376-196">若要启用对混合模式高 DPI 缩放的支持，可以设置以下 [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 切换应用程序配置文件：</span><span class="sxs-lookup"><span data-stu-id="4d376-196">To enable support for Mixed-Mode High DPI scaling, you can set the following [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) switches the application configuration file:</span></span>

```xml
<runtime>
   <AppContextSwitchOverrides value = "Switch.System.Windows.DoNotScaleForDpiChanges=false; Switch.System.Windows.DoNotUsePresentationDpiCapabilityTier2OrGreater=false"/>
</runtime>
```

<a name="clr48"></a>

#### <a name="common-language-runtime"></a><span data-ttu-id="4d376-197">公共语言运行时</span><span class="sxs-lookup"><span data-stu-id="4d376-197">Common language runtime</span></span>

<span data-ttu-id="4d376-198">.NET Framework 4.8 中的运行时包含以下更改和改进：</span><span class="sxs-lookup"><span data-stu-id="4d376-198">The runtime in .NET Framework 4.8 includes the following changes and improvements:</span></span>

<span data-ttu-id="4d376-199">**JIT 编译器的改进** 。</span><span class="sxs-lookup"><span data-stu-id="4d376-199">**Improvements to the JIT compiler** .</span></span> <span data-ttu-id="4d376-200">.NET Framework 4.8 中的实时 (JIT) 编译器基于 .NET Core 2.1 中的 JIT 编译器。</span><span class="sxs-lookup"><span data-stu-id="4d376-200">The Just-in-time (JIT) compiler in .NET Framework 4.8 is based on the JIT compiler in .NET Core 2.1.</span></span> <span data-ttu-id="4d376-201">对 .NET Core 2.1 JIT 编译器所做的多个优化和所有 bug 修复都包含在 .NET Framework 4.8 JIT 编译器中。</span><span class="sxs-lookup"><span data-stu-id="4d376-201">Many of the optimizations and all of the bug fixes made to the .NET Core 2.1 JIT compiler are included in the .NET Framework 4.8 JIT compiler.</span></span>

<span data-ttu-id="4d376-202">**NGEN 改进** 。</span><span class="sxs-lookup"><span data-stu-id="4d376-202">**NGEN improvements** .</span></span> <span data-ttu-id="4d376-203">运行时改进了[本机映像生成器](../tools/ngen-exe-native-image-generator.md) (NGEN) 映像的内存管理，以便从 NGEN 映像映射的数据不驻留在内存中。</span><span class="sxs-lookup"><span data-stu-id="4d376-203">The runtime has improved its memory management for [Native Image Generator](../tools/ngen-exe-native-image-generator.md) (NGEN) images so that data mapped from NGEN images are not memory-resident.</span></span> <span data-ttu-id="4d376-204">这将缩减可受到攻击的外围应用，攻击方法为试图通过修改将执行的内存来执行任意代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-204">This reduces the surface area available to attacks that attempt to execute arbitrary code by modifying memory that will be executed.</span></span>

<span data-ttu-id="4d376-205">**所有程序集的反恶意软件扫描** 。</span><span class="sxs-lookup"><span data-stu-id="4d376-205">**Antimalware scanning for all assemblies** .</span></span> <span data-ttu-id="4d376-206">在 .NET Framework 的早期版本中，运行时使用 Windows Defender 或第三方反恶意软件扫描从磁盘加载的所有程序集。</span><span class="sxs-lookup"><span data-stu-id="4d376-206">In previous versions of .NET Framework, the runtime scans all assemblies loaded from disk using either Windows Defender or third-party antimalware software.</span></span> <span data-ttu-id="4d376-207">但是，从其他源加载的程序集（例如，通过 <xref:System.Reflection.Assembly.Load(System.Byte[])?displayProperty=nameWithType> 方法）不会进行扫描，并且可能包含未检测到的恶意软件。</span><span class="sxs-lookup"><span data-stu-id="4d376-207">However, assemblies loaded from other sources, such as by the <xref:System.Reflection.Assembly.Load(System.Byte[])?displayProperty=nameWithType> method, are not scanned and can potentially contain undetected malware.</span></span> <span data-ttu-id="4d376-208">从 Windows 10 上运行的 .NET Framework 4.8 开始，运行时通过实现[反恶意软件扫描界面 (AMSI)](/windows/desktop/AMSI/antimalware-scan-interface-portal) 的反恶意软件解决方案来触发扫描。</span><span class="sxs-lookup"><span data-stu-id="4d376-208">Starting with .NET Framework 4.8 running on Windows 10, the runtime triggers a scan by antimalware solutions that implement the [Antimalware Scan Interface (AMSI)](/windows/desktop/AMSI/antimalware-scan-interface-portal).</span></span>

<a name="v472"></a>

## <a name="whats-new-in-net-framework-472"></a><span data-ttu-id="4d376-209">.NET Framework 4.7.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-209">What's new in .NET Framework 4.7.2</span></span>

<span data-ttu-id="4d376-210">.NET Framework 4.7.2 在以下几个领域新增了功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-210">.NET Framework 4.7.2 includes new features in the following areas:</span></span>

- [<span data-ttu-id="4d376-211">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-211">Base classes</span></span>](#core-472)
- [<span data-ttu-id="4d376-212">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-212">ASP.NET</span></span>](#asp-net472)
- [<span data-ttu-id="4d376-213">网络连接</span><span class="sxs-lookup"><span data-stu-id="4d376-213">Networking</span></span>](#net472)
- [<span data-ttu-id="4d376-214">SQL</span><span class="sxs-lookup"><span data-stu-id="4d376-214">SQL</span></span>](#sql472)
- [<span data-ttu-id="4d376-215">WPF</span><span class="sxs-lookup"><span data-stu-id="4d376-215">WPF</span></span>](#wpf472)
- [<span data-ttu-id="4d376-216">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="4d376-216">ClickOnce</span></span>](#clickonce)

<span data-ttu-id="4d376-217">.NET Framework 4.7.2 持续关注的重点是辅助功能的改进，使应用程序能为使用辅助技术的用户提供最佳体验。</span><span class="sxs-lookup"><span data-stu-id="4d376-217">A continuing focus in .NET Framework 4.7.2 is improved accessibility, which allows an application to provide an appropriate experience for users of Assistive Technology.</span></span> <span data-ttu-id="4d376-218">有关 .NET Framework 4.7.2 中辅助功能改进的信息，请参阅 [.NET Framework 中辅助功能的新增功能](whats-new-in-accessibility.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-218">For information on accessibility improvements in .NET Framework 4.7.2, see [What's new in accessibility in .NET Framework](whats-new-in-accessibility.md).</span></span>

<a name="core-472"></a>

#### <a name="base-classes"></a><span data-ttu-id="4d376-219">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-219">Base classes</span></span>

<span data-ttu-id="4d376-220">.NET Framework 4.7.2 提供大量的加密增强功能、对 ZIP 存档更好的解压缩支持以及额外的集合 API。</span><span class="sxs-lookup"><span data-stu-id="4d376-220">.NET Framework 4.7.2 features a large number of cryptographic enhancements, better decompression support for ZIP archives, and additional collection APIs.</span></span>

<span data-ttu-id="4d376-221">**RSA.Create 和 DSA.Create 的新重载**</span><span class="sxs-lookup"><span data-stu-id="4d376-221">**New overloads of RSA.Create and DSA.Create**</span></span>

<span data-ttu-id="4d376-222">利用 <xref:System.Security.Cryptography.DSA.Create(System.Security.Cryptography.DSAParameters)?displayProperty=nameWithType> 和 <xref:System.Security.Cryptography.RSA.Create(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType> 方法，可以在实例化新的 <xref:System.Security.Cryptography.DSA> 或 <xref:System.Security.Cryptography.RSA> 密钥时提供密钥参数。</span><span class="sxs-lookup"><span data-stu-id="4d376-222">The <xref:System.Security.Cryptography.DSA.Create(System.Security.Cryptography.DSAParameters)?displayProperty=nameWithType> and <xref:System.Security.Cryptography.RSA.Create(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType> methods let you supply key parameters when instantiating a new <xref:System.Security.Cryptography.DSA> or <xref:System.Security.Cryptography.RSA> key.</span></span> <span data-ttu-id="4d376-223">它们允许你替换如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="4d376-223">They allow you to replace code like the following:</span></span>

```csharp
// Before .NET Framework 4.7.2
using (RSA rsa = RSA.Create())
{
   rsa.ImportParameters(rsaParameters);
   // Other code to execute using the RSA instance.
}
```

```vb
' Before .NET Framework 4.7.2
Using rsa = RSA.Create()
   rsa.ImportParameters(rsaParameters)
   ' Other code to execute using the rsa instance.
End Using
```

<span data-ttu-id="4d376-224">采用类似如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="4d376-224">with code like this:</span></span>

```csharp
// Starting with .NET Framework 4.7.2
using (RSA rsa = RSA.Create(rsaParameters))
{
   // Other code to execute using the rsa instance.
}
```

```vb
' Starting with .NET Framework 4.7.2
Using rsa = RSA.Create(rsaParameters)
   ' Other code to execute using the rsa instance.
End Using
```

<span data-ttu-id="4d376-225"><xref:System.Security.Cryptography.DSA.Create(System.Int32)?displayProperty=nameWithType> 和 <xref:System.Security.Cryptography.RSA.Create(System.Int32)?displayProperty=nameWithType> 方法允许生成具有特定密钥大小的 <xref:System.Security.Cryptography.DSA> 或 <xref:System.Security.Cryptography.RSA> 密钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-225">The <xref:System.Security.Cryptography.DSA.Create(System.Int32)?displayProperty=nameWithType> and <xref:System.Security.Cryptography.RSA.Create(System.Int32)?displayProperty=nameWithType> methods let you generate new <xref:System.Security.Cryptography.DSA> or <xref:System.Security.Cryptography.RSA> keys with a specific key size.</span></span> <span data-ttu-id="4d376-226">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-226">For example:</span></span>

```csharp
using (DSA dsa = DSA.Create(2048))
{
   // Other code to execute using the dsa instance.
}
```

```vb
Using dsa = DSA.Create(2048)
   ' Other code to execute using the dsa instance.
End Using
```

<span data-ttu-id="4d376-227">**Rfc2898DeriveBytes 构造函数接受哈希算法名称**</span><span class="sxs-lookup"><span data-stu-id="4d376-227">**Rfc2898DeriveBytes constructors accept a hash algorithm name**</span></span>

<span data-ttu-id="4d376-228"><xref:System.Security.Cryptography.Rfc2898DeriveBytes> 类具有三个带 <xref:System.Security.Cryptography.HashAlgorithmName> 参数的构造函数，该参数标识在派生密钥时使用的 HMAC 算法。</span><span class="sxs-lookup"><span data-stu-id="4d376-228">The <xref:System.Security.Cryptography.Rfc2898DeriveBytes> class has three new constructors with a <xref:System.Security.Cryptography.HashAlgorithmName> parameter that identifies the HMAC algorithm to use when deriving keys.</span></span> <span data-ttu-id="4d376-229">与 SHA-1 相比，开发人员应使用基于 SHA-2 的 HMAC，例如 SHA-256，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-229">Instead of using SHA-1, developers should use a SHA-2-based HMAC like SHA-256, as shown in the following example:</span></span>

```csharp
private static byte[] DeriveKey(string password, out int iterations, out byte[] salt,
                                out HashAlgorithmName algorithm)
{
   iterations = 100000;
   algorithm = HashAlgorithmName.SHA256;

   const int SaltSize = 32;
   const int DerivedValueSize = 32;

   using (Rfc2898DeriveBytes pbkdf2 = new Rfc2898DeriveBytes(password, SaltSize,
                                                             iterations, algorithm))
   {
      salt = pbkdf2.Salt;
      return pbkdf2.GetBytes(DerivedValueSize);
   }
}
```

```vb
Private Shared Function DeriveKey(password As String, ByRef iterations As Integer,
                                  ByRef salt AS Byte(), ByRef algorithm As HashAlgorithmName) As Byte()
   iterations = 100000
   algorithm = HashAlgorithmName.SHA256

   Const SaltSize As Integer = 32
   Const  DerivedValueSize As Integer = 32

   Using pbkdf2 = New Rfc2898DeriveBytes(password, SaltSize, iterations, algorithm)
      salt = pbkdf2.Salt
      Return pbkdf2.GetBytes(DerivedValueSize)
   End Using
End Function
```

<span data-ttu-id="4d376-230">**临时密钥支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-230">**Support for ephemeral keys**</span></span>

<span data-ttu-id="4d376-231">PFX 导入可以选择绕过硬盘直接从内存加载私钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-231">PFX import can optionally load private keys directly from memory, bypassing the hard drive.</span></span> <span data-ttu-id="4d376-232"> 如果在 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 构造函数或 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.Import%2A?displayProperty=nameWithType> 方法的其中一个重载中指定了新的 <xref:System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.EphemeralKeySet?displayProperty=nameWithType> 标记，则私钥将加载为临时密钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-232">When the new <xref:System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.EphemeralKeySet?displayProperty=nameWithType> flag is specified in an <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> constructor or one of the overloads of the <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.Import%2A?displayProperty=nameWithType> method, the private keys will be loaded as ephemeral keys.</span></span> <span data-ttu-id="4d376-233">这能防止密钥在磁盘上可见。</span><span class="sxs-lookup"><span data-stu-id="4d376-233">This prevents the keys from being visible on the disk.</span></span> <span data-ttu-id="4d376-234">但是：</span><span class="sxs-lookup"><span data-stu-id="4d376-234">However:</span></span>

- <span data-ttu-id="4d376-235">由于密钥不会保留到磁盘，最好不要将通过此标记加载的证书添加到 X509Store。</span><span class="sxs-lookup"><span data-stu-id="4d376-235">Since the keys are not persisted to disk, certificates loaded with this flag are not good candidates to add to an X509Store.</span></span>

- <span data-ttu-id="4d376-236">以这种方式加载的密钥大多都是通过 Windows CNG 加载的。</span><span class="sxs-lookup"><span data-stu-id="4d376-236">Keys loaded in this manner are almost always loaded via Windows CNG.</span></span> <span data-ttu-id="4d376-237">因此，调用方必须通过调用扩展方法访问私钥，例如 [cert.GetRSAPrivateKey()](xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey%2A)。</span><span class="sxs-lookup"><span data-stu-id="4d376-237">Therefore, callers must access the private key by calling extension methods, such as [cert.GetRSAPrivateKey()](xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey%2A).</span></span> <span data-ttu-id="4d376-238"><xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> 属性不起作用。</span><span class="sxs-lookup"><span data-stu-id="4d376-238">The <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> property does not function.</span></span>

- <span data-ttu-id="4d376-239">由于旧的 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> 属性对证书不起作用，开发人员应在切换至临时密钥之前执行严密的测试。</span><span class="sxs-lookup"><span data-stu-id="4d376-239">Since the legacy <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> property does not work with certificates, developers should perform rigorous testing before switching to ephemeral keys.</span></span>

<span data-ttu-id="4d376-240">**PKCS#10 证书签名请求和 X.509 公钥证书的编程式创建**</span><span class="sxs-lookup"><span data-stu-id="4d376-240">**Programmatic creation of PKCS#10 certification signing requests and X.509 public key certificates**</span></span>

<span data-ttu-id="4d376-241">从 .NET Framework 4.7.2 开始，工作负载可以生成证书签名请求 (CSR)，这允许将证书请求生成分阶到现有工具中。</span><span class="sxs-lookup"><span data-stu-id="4d376-241">Starting with .NET Framework 4.7.2, workloads can generate certificate signing requests (CSRs), which allows certificate request generation to be staged into existing tooling.</span></span> <span data-ttu-id="4d376-242">这在测试方案中常常很有用。</span><span class="sxs-lookup"><span data-stu-id="4d376-242">This is frequently useful in test scenarios.</span></span>

<span data-ttu-id="4d376-243">有关详细信息和代码示例，请参阅 [.NET 博客](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/)中的“PKCS#10 证书签名请求和 X.509 公钥证书的编程式创建”。</span><span class="sxs-lookup"><span data-stu-id="4d376-243">For more information and code examples, see "Programmatic creation of PKCS#10 certification signing requests and X.509 public key certificates" in the [.NET Blog](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/).</span></span>

<span data-ttu-id="4d376-244">**新的 SignerInfo 成员**</span><span class="sxs-lookup"><span data-stu-id="4d376-244">**New SignerInfo members**</span></span>

<span data-ttu-id="4d376-245">从 .NET Framework 4.7.2 开始，<xref:System.Security.Cryptography.Pkcs.SignerInfo> 类将公开更多有关签名的信息。</span><span class="sxs-lookup"><span data-stu-id="4d376-245">Starting with .NET Framework 4.7.2, the <xref:System.Security.Cryptography.Pkcs.SignerInfo> class exposes more information about the signature.</span></span> <span data-ttu-id="4d376-246">你可以检索 <xref:System.Security.Cryptography.Pkcs.SignerInfo.SignatureAlgorithm?displayProperty=fullName> 属性的值，以确定签名者采用的签名算法。</span><span class="sxs-lookup"><span data-stu-id="4d376-246">You can retrieve the value of the <xref:System.Security.Cryptography.Pkcs.SignerInfo.SignatureAlgorithm?displayProperty=fullName> property to determine the signature algorithm used by the signer.</span></span> <span data-ttu-id="4d376-247">可以调用 <xref:System.Security.Cryptography.Pkcs.SignerInfo.GetSignature%2A?displayProperty=nameWithType> 来获取此签名者的加密签名副本。</span><span class="sxs-lookup"><span data-stu-id="4d376-247"><xref:System.Security.Cryptography.Pkcs.SignerInfo.GetSignature%2A?displayProperty=nameWithType> can be called to get a copy of the cryptographic signature for this signer.</span></span>

<span data-ttu-id="4d376-248">**在 CryptoStream 释放后保持包装流打开**</span><span class="sxs-lookup"><span data-stu-id="4d376-248">**Leaving a wrapped stream open after CryptoStream is disposed**</span></span>

<span data-ttu-id="4d376-249">从 .NET Framework 4.7.2 开始，<xref:System.Security.Cryptography.CryptoStream> 类有了一个额外的构造函数可允许 <xref:System.Security.Cryptography.CryptoStream.Dispose%2A> 不关闭包装流。</span><span class="sxs-lookup"><span data-stu-id="4d376-249">Starting with .NET Framework 4.7.2, the <xref:System.Security.Cryptography.CryptoStream> class has an additional constructor that allows <xref:System.Security.Cryptography.CryptoStream.Dispose%2A> to not close the wrapped stream.</span></span> <span data-ttu-id="4d376-250"> 若要在释放 <xref:System.Security.Cryptography.CryptoStream> 实例后保持包装流的打开状态，请调用新的 <xref:System.Security.Cryptography.CryptoStream> 构造函数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-250">To leave the wrapped stream open after the <xref:System.Security.Cryptography.CryptoStream> instance is disposed, call the new <xref:System.Security.Cryptography.CryptoStream> constructor as follows:</span></span>

```csharp
var cStream = new CryptoStream(stream, transform, mode, leaveOpen: true);
```

```vb
Dim cStream = New CryptoStream(stream, transform, mode, leaveOpen:=true)
```

<span data-ttu-id="4d376-251">**DeflateStream 中的解压缩更改**</span><span class="sxs-lookup"><span data-stu-id="4d376-251">**Decompression changes in DeflateStream**</span></span>

<span data-ttu-id="4d376-252">从 .NET Framework 4.7.2 开始，<xref:System.IO.Compression.DeflateStream> 类中的解压缩操作的实现变为默认使用本机 Windows API。</span><span class="sxs-lookup"><span data-stu-id="4d376-252">Starting with .NET Framework 4.7.2, the implementation of decompression operations in the <xref:System.IO.Compression.DeflateStream> class has changed to use native Windows APIs by default.</span></span> <span data-ttu-id="4d376-253">通常情况下，这能大大地提高性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-253">Typically, this results in a substantial performance improvement.</span></span>

<span data-ttu-id="4d376-254">对于面向 .NET Framework 4.7.2 的应用程序，默认启用通过使用 Windows API 进行解压缩的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-254">Support for decompression by using Windows APIs is enabled by default for applications that target .NET Framework 4.7.2.</span></span> <span data-ttu-id="4d376-255">对于面向旧版 .NET Framework 但在 .NET Framework 4.7.2 下运行的应用程序，可以将以下 [AppContext 开关](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)添加到应用程序配置文件，从而选择启用此行为：</span><span class="sxs-lookup"><span data-stu-id="4d376-255">Applications that target earlier versions of .NET Framework but are running under .NET Framework 4.7.2 can opt into this behavior by adding the following [AppContext switch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) to the application configuration file:</span></span>

```xml
<AppContextSwitchOverrides value="Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=false" />
```

<span data-ttu-id="4d376-256">**额外的集合 API**</span><span class="sxs-lookup"><span data-stu-id="4d376-256">**Additional collection APIs**</span></span>

<span data-ttu-id="4d376-257">.NET Framework 4.7.2 将一些新 API 添加到 <xref:System.Collections.Generic.SortedSet%601> 和 <xref:System.Collections.Generic.HashSet%601> 类型。</span><span class="sxs-lookup"><span data-stu-id="4d376-257">.NET Framework 4.7.2 adds a number of new APIs to the <xref:System.Collections.Generic.SortedSet%601> and <xref:System.Collections.Generic.HashSet%601> types.</span></span> <span data-ttu-id="4d376-258">这些方法包括：</span><span class="sxs-lookup"><span data-stu-id="4d376-258">These include:</span></span>

- <span data-ttu-id="4d376-259">`TryGetValue` 方法，将其他集合类型中使用的尝试模式扩展到了这两种类型中。</span><span class="sxs-lookup"><span data-stu-id="4d376-259">`TryGetValue` methods, which extend the try pattern used in other collection types to these two types.</span></span> <span data-ttu-id="4d376-260">这两个方法是：</span><span class="sxs-lookup"><span data-stu-id="4d376-260">The methods are:</span></span>

  - [<span data-ttu-id="4d376-261">public bool HashSet\<T>.TryGetValue(T equalValue, out T actualValue)</span><span class="sxs-lookup"><span data-stu-id="4d376-261">public bool HashSet\<T>.TryGetValue(T equalValue, out T actualValue)</span></span>](xref:System.Collections.Generic.SortedSet%601.TryGetValue%2A)
  - [<span data-ttu-id="4d376-262">public bool SortedSet\<T>.TryGetValue(T equalValue, out T actualValue)</span><span class="sxs-lookup"><span data-stu-id="4d376-262">public bool SortedSet\<T>.TryGetValue(T equalValue, out T actualValue)</span></span>](xref:System.Collections.Generic.SortedSet%601.TryGetValue%2A)

- <span data-ttu-id="4d376-263">`Enumerable.To*` 扩展方法，将集合转换为 <xref:System.Collections.Generic.HashSet%601>：</span><span class="sxs-lookup"><span data-stu-id="4d376-263">`Enumerable.To*` extension methods, which convert a collection to a <xref:System.Collections.Generic.HashSet%601>:</span></span>

  - [<span data-ttu-id="4d376-264">public static HashSet\<TSource> ToHashSet\<TSource>(this IEnumerable\<TSource> source)</span><span class="sxs-lookup"><span data-stu-id="4d376-264">public static HashSet\<TSource> ToHashSet\<TSource>(this IEnumerable\<TSource> source)</span></span>](xref:System.Linq.Enumerable.ToHashSet%2A)
  - [<span data-ttu-id="4d376-265">public static HashSet\<TSource> ToHashSet\<TSource>(this IEnumerable\<TSource> source, IEqualityComparer\<TSource> comparer)</span><span class="sxs-lookup"><span data-stu-id="4d376-265">public static HashSet\<TSource> ToHashSet\<TSource>(this IEnumerable\<TSource> source, IEqualityComparer\<TSource> comparer)</span></span>](xref:System.Linq.Enumerable.ToHashSet%2A)

- <span data-ttu-id="4d376-266">新的 <xref:System.Collections.Generic.HashSet%601> 构造函数，让你设置集合容量，可以在提前知道 <xref:System.Collections.Generic.HashSet%601> 大小的情况下提升性能：</span><span class="sxs-lookup"><span data-stu-id="4d376-266">New <xref:System.Collections.Generic.HashSet%601> constructors that let you set the collection's capacity, which yields a performance benefit when you know the size of the <xref:System.Collections.Generic.HashSet%601> in advance:</span></span>

  - <span data-ttu-id="4d376-267">[public HashSet(int capacity)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32))</span><span class="sxs-lookup"><span data-stu-id="4d376-267">[public HashSet(int capacity)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32))</span></span>
  - <span data-ttu-id="4d376-268">[public HashSet(int capacity, IEqualityComparer\<T> comparer)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32,System.Collections.Generic.IEqualityComparer%7B%600%7D))</span><span class="sxs-lookup"><span data-stu-id="4d376-268">[public HashSet(int capacity, IEqualityComparer\<T> comparer)](xref:System.Collections.Generic.HashSet%601.%23ctor(System.Int32,System.Collections.Generic.IEqualityComparer%7B%600%7D))</span></span>

<span data-ttu-id="4d376-269"><xref:System.Collections.Concurrent.ConcurrentDictionary%602> 类包含 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A> 和 <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> 方法的新重载，以便在词典中检索值或添加找不到的值，以及将值添加到词典或者更新已存在的值。</span><span class="sxs-lookup"><span data-stu-id="4d376-269">The <xref:System.Collections.Concurrent.ConcurrentDictionary%602> class includes new overloads of the <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A> and <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> methods to retrieve a value from the dictionary or to add it if it is not found, and to add a value to the dictionary or to update it if it already exists.</span></span>

```csharp
public TValue AddOrUpdate<TArg>(TKey key, Func<TKey, TArg, TValue> addValueFactory, Func<TKey, TValue, TArg, TValue> updateValueFactory, TArg factoryArgument)

public TValue GetOrAdd<TArg>(TKey key, Func<TKey, TArg, TValue> valueFactory, TArg factoryArgument)
```

```vb
Public AddOrUpdate(Of TArg)(key As TKey, addValueFactory As Func(Of TKey, TArg, TValue), updateValueFactory As Func(Of TKey, TValue, TArg, TValue), factoryArgument As TArg) As TValue

Public GetOrAdd(Of TArg)(key As TKey, valueFactory As Func(Of TKey, TArg, TValue), factoryArgument As TArg) As TValue
```

<a name="asp-net472"></a>

#### <a name="aspnet"></a><span data-ttu-id="4d376-270">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-270">ASP.NET</span></span>

<span data-ttu-id="4d376-271">**Web 窗体中的依赖项注入支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-271">**Support for dependency injection in Web Forms**</span></span>

<span data-ttu-id="4d376-272">[依赖项注入 (DI)](/aspnet/core/fundamentals/dependency-injection#overview-of-dependency-injection) 分离对象和它们的依赖项，使得对象的代码不再仅因依赖项更改而需要进行更改。</span><span class="sxs-lookup"><span data-stu-id="4d376-272">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection#overview-of-dependency-injection) decouples objects and their dependencies so that an object's code no longer needs to be changed just because a dependency has changed.</span></span> <span data-ttu-id="4d376-273">在开发面向 .NET Framework 4.7.2 的 ASP.NET 应用程序时，可以：</span><span class="sxs-lookup"><span data-stu-id="4d376-273">When developing ASP.NET applications that target .NET Framework 4.7.2, you can:</span></span>

- <span data-ttu-id="4d376-274">在[处理程序和模块](/previous-versions/aspnet/bb398986(v=vs.100))、[页面实例](xref:System.Web.UI.Page)和 ASP.NET Web 应用程序项目的[用户控件](/previous-versions/aspnet/y6wb1a0e(v=vs.100))中使用基于资源库、基于接口和基于构造函数的注入。</span><span class="sxs-lookup"><span data-stu-id="4d376-274">Use setter-based, interface-based, and constructor-based injection in [handlers and modules](/previous-versions/aspnet/bb398986(v=vs.100)), [Page instances](xref:System.Web.UI.Page), and [user controls](/previous-versions/aspnet/y6wb1a0e(v=vs.100)) of ASP.NET web application projects.</span></span>

- <span data-ttu-id="4d376-275">在[处理程序和模块](/previous-versions/aspnet/bb398986(v=vs.100))、[页面实例](xref:System.Web.UI.Page)和 ASP.NET 网站项目的[用户控件](/previous-versions/aspnet/y6wb1a0e(v=vs.100))中使用基于资源库和基于接口的注入。</span><span class="sxs-lookup"><span data-stu-id="4d376-275">Use setter-based and interface-based injection in [handlers and modules](/previous-versions/aspnet/bb398986(v=vs.100)), [Page instances](xref:System.Web.UI.Page), and [user controls](/previous-versions/aspnet/y6wb1a0e(v=vs.100)) of ASP.NET web site projects.</span></span>

- <span data-ttu-id="4d376-276">插入不同的依赖关系注入框架。</span><span class="sxs-lookup"><span data-stu-id="4d376-276">Plug in different dependency injection frameworks.</span></span>

<span data-ttu-id="4d376-277">**同站点 cookie 支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-277">**Support for same-site cookies**</span></span>

<span data-ttu-id="4d376-278">[SameSite](https://tools.ietf.org/html/draft-west-first-party-cookies-07) 防止浏览器将 cookie 和跨站点请求一起发送。</span><span class="sxs-lookup"><span data-stu-id="4d376-278">[SameSite](https://tools.ietf.org/html/draft-west-first-party-cookies-07) prevents a browser from sending a cookie along with a cross-site request.</span></span> <span data-ttu-id="4d376-279">.NET Framework 4.7.2 添加了一个值为 <xref:System.Web.SameSiteMode?displayProperty=nameWithType> 枚举成员的 <xref:System.Web.HttpCookie.SameSite?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="4d376-279">.NET Framework 4.7.2 adds a <xref:System.Web.HttpCookie.SameSite?displayProperty=nameWithType> property whose value is a <xref:System.Web.SameSiteMode?displayProperty=nameWithType> enumeration member.</span></span> <span data-ttu-id="4d376-280">如果它的值为 <xref:System.Web.SameSiteMode.Strict?displayProperty=nameWithType> 或 <xref:System.Web.SameSiteMode.Lax?displayProperty=nameWithType>，ASP.NET 将 `SameSite` 属性添加到 set-cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="4d376-280">If its value is <xref:System.Web.SameSiteMode.Strict?displayProperty=nameWithType> or <xref:System.Web.SameSiteMode.Lax?displayProperty=nameWithType>, ASP.NET adds the `SameSite` attribute to the set-cookie header.</span></span> <span data-ttu-id="4d376-281">SameSite 支持适用于 <xref:System.Web.HttpCookie> 对象，以及 <xref:System.Web.Security.FormsAuthentication> 和 <xref:System.Web.SessionState> cookie。</span><span class="sxs-lookup"><span data-stu-id="4d376-281">SameSite support applies to <xref:System.Web.HttpCookie> objects, as well as to <xref:System.Web.Security.FormsAuthentication> and <xref:System.Web.SessionState> cookies.</span></span>

<span data-ttu-id="4d376-282">可以为 <xref:System.Web.HttpCookie> 对象设置 SameSite，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-282">You can set SameSite for an <xref:System.Web.HttpCookie> object as follows:</span></span>

```csharp
var c = new HttpCookie("secureCookie", "same origin");
c.SameSite = SameSiteMode.Lax;
```

```vb
Dim c As New HttpCookie("secureCookie", "same origin")
c.SameSite = SameSiteMode.Lax
```

<span data-ttu-id="4d376-283">还可以通过修改 web.config 文件，在应用程序级别配置 SameSite cookie：</span><span class="sxs-lookup"><span data-stu-id="4d376-283">You can also configure SameSite cookies at the application level by modifying the web.config file:</span></span>

```xml
<system.web>
   <httpCookies sameSite="Strict" />
</system.web>
```

<span data-ttu-id="4d376-284">通过修改 Web 配置文件，可以为 <xref:System.Web.Security.FormsAuthentication> 和 <xref:System.Web.SessionState> cookie 添加 SameSite：</span><span class="sxs-lookup"><span data-stu-id="4d376-284">You can add SameSite for <xref:System.Web.Security.FormsAuthentication> and <xref:System.Web.SessionState> cookies by modifying the web config file:</span></span>

```xml
<system.web>
   <authentication mode="Forms">
      <forms cookieSameSite="Lax">
         <!-- ...   -->
      </forms>
   </authentication>
   <sessionState cookieSameSite="Lax"></sessionState>
</system.web>
```

<a name="net472"></a>

#### <a name="networking"></a><span data-ttu-id="4d376-285">网络</span><span class="sxs-lookup"><span data-stu-id="4d376-285">Networking</span></span>

<span data-ttu-id="4d376-286">**HttpClientHandler 属性的实现**</span><span class="sxs-lookup"><span data-stu-id="4d376-286">**Implementation of HttpClientHandler properties**</span></span>

<span data-ttu-id="4d376-287">.NET Framework 4.7.1 将八个属性添加到了 <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-287">.NET Framework 4.7.1 added eight properties to the <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> class.</span></span> <span data-ttu-id="4d376-288">不过其中有两个会引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="4d376-288">However, two threw a <xref:System.PlatformNotSupportedException>.</span></span> <span data-ttu-id="4d376-289">.NET Framework 4.7.2 现在为这些属性提供实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-289">.NET Framework 4.7.2 now provides an implementation for these properties.</span></span> <span data-ttu-id="4d376-290">这些属性为：</span><span class="sxs-lookup"><span data-stu-id="4d376-290">The properties are:</span></span>

- <xref:System.Net.Http.HttpClientHandler.CheckCertificateRevocationList>
- <xref:System.Net.Http.HttpClientHandler.SslProtocols>

<a name="sql472"></a>

#### <a name="sqlclient"></a><span data-ttu-id="4d376-291">SQLClient</span><span class="sxs-lookup"><span data-stu-id="4d376-291">SQLClient</span></span>

<span data-ttu-id="4d376-292">**对 Azure Active Directory 通用身份验证和多重身份验证的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-292">**Support for Azure Active Directory Universal Authentication and Multi-Factor authentication**</span></span>

<span data-ttu-id="4d376-293">不断增加的符合性和安全性需求让很多客户需要使用多重身份验证 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="4d376-293">Growing compliance and security demands require that many customers use multi-factor authentication (MFA).</span></span> <span data-ttu-id="4d376-294">此外，当前的最佳做法不鼓励在连接字符串中直接包含用户密码。</span><span class="sxs-lookup"><span data-stu-id="4d376-294">In addition, current best practices discourage including user passwords directly in connection strings.</span></span> <span data-ttu-id="4d376-295">为了支持这些更改，.NET Framework 4.7.2 通过添加新值“Active Directory Interactive”扩展了 [SQLClient 连接字符串](xref:System.Data.SqlClient.SqlConnection.ConnectionString)，让现有“身份验证”关键字支持 MFA 和 [Azure AD 身份验证](/azure/sql-database/sql-database-aad-authentication-configure)。</span><span class="sxs-lookup"><span data-stu-id="4d376-295">To support these changes, .NET Framework 4.7.2 extends [SQLClient connection strings](xref:System.Data.SqlClient.SqlConnection.ConnectionString) by adding a new value, "Active Directory Interactive", for the existing "Authentication" keyword to support MFA and [Azure AD Authentication](/azure/sql-database/sql-database-aad-authentication-configure).</span></span> <span data-ttu-id="4d376-296">新的交互式方法支持本机和联合 Azure AD 用户以及 Azure AD 来宾用户。</span><span class="sxs-lookup"><span data-stu-id="4d376-296">The new interactive method supports native and federated Azure AD users as well as Azure AD guest users.</span></span> <span data-ttu-id="4d376-297">使用此方法时，SQL 数据库将支持由 Azure AD 施加的 MFA 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d376-297">When this method is used, the MFA authentication imposed by Azure AD is supported for SQL databases.</span></span> <span data-ttu-id="4d376-298">此外，为了遵循安全最佳做法，身份验证流程会请求用户密码。</span><span class="sxs-lookup"><span data-stu-id="4d376-298">In addition, the authentication process requests a user password to adhere to security best practices.</span></span>

<span data-ttu-id="4d376-299">在以前版本的 .NET Framework 中，SQL 连接只支持 <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryPassword?displayProperty=nameWithType> 和 <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryIntegrated?displayProperty=nameWithType> 选项。</span><span class="sxs-lookup"><span data-stu-id="4d376-299">In previous versions of .NET Framework, SQL connectivity supported only the <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryPassword?displayProperty=nameWithType> and <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryIntegrated?displayProperty=nameWithType> options.</span></span> <span data-ttu-id="4d376-300">两者都是非交互式 [ADAL 协议](/azure/active-directory/develop/active-directory-authentication-libraries)的一部分，而该协议不支持 MFA。</span><span class="sxs-lookup"><span data-stu-id="4d376-300">Both of these are part of the non-interactive [ADAL protocol](/azure/active-directory/develop/active-directory-authentication-libraries), which does not support MFA.</span></span> <span data-ttu-id="4d376-301">利用新的 <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryInteractive?displayProperty=nameWithType> 选项，SQL 连接可支持 MFA 以及现有身份验证方法（密码和集成身份验证），让用户可以交互式地输入用户密码，而无需将密码存留在连接字符串中。</span><span class="sxs-lookup"><span data-stu-id="4d376-301">With the new <xref:System.Data.SqlClient.SqlAuthenticationMethod.ActiveDirectoryInteractive?displayProperty=nameWithType> option, SQL connectivity supports MFA as well as existing authentication methods (password and integrated authentication), which allows users to enter user passwords interactively without persisting passwords in the connection string.</span></span>

<span data-ttu-id="4d376-302">有关详细信息和示例，请参阅 [.NET 博客](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/)中的“SQL - Azure AD 通用和多重身份验证支持”。</span><span class="sxs-lookup"><span data-stu-id="4d376-302">For more information and an example, see "SQL -- Azure AD Universal and Multi-factor Authentication Support" in the [.NET Blog](https://devblogs.microsoft.com/dotnet/net-framework-4-7-2-developer-pack-early-access-build-3056-is-available/).</span></span>

<span data-ttu-id="4d376-303">**Always Encrypted 版本 2 的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-303">**Support for Always Encrypted version 2**</span></span>

<span data-ttu-id="4d376-304">NET Framework 4.7.2 为基于 enclave 的 Always Encrypted 添加支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-304">NET Framework 4.7.2 adds supports for enclave-based Always Encrypted.</span></span> <span data-ttu-id="4d376-305">Always Encrypted 的原始版本是客户端加密技术，其中的加密密钥不会离开客户端。</span><span class="sxs-lookup"><span data-stu-id="4d376-305">The original version of Always Encrypted is a client-side encryption technology in which encryption keys never leave the client.</span></span> <span data-ttu-id="4d376-306">在基于 enclave 的 Always Encrypted 中，客户端可以选择将加密密钥发送到安全的 enclave，即一个安全的计算实体，该实体可以看作是 SQL Server 的一部分，但 SQL Server 代码无法对其进行篡改。</span><span class="sxs-lookup"><span data-stu-id="4d376-306">In enclave-based Always Encrypted, the client can optionally send the encryption keys to a secure enclave, which is a secure computational entity that can be considered part of SQL Server but that SQL Server code cannot tamper with.</span></span> <span data-ttu-id="4d376-307">为了支持基于 enclave 的 Always Encrypted，NET Framework 4.7.2 将以下类型和成员添加到 <xref:System.Data.SqlClient> 命名空间：</span><span class="sxs-lookup"><span data-stu-id="4d376-307">To support enclave-based Always Encrypted, .NET Framework 4.7.2 adds the following types and members to the <xref:System.Data.SqlClient> namespace:</span></span>

- <span data-ttu-id="4d376-308"><xref:System.Data.SqlClient.SqlConnectionStringBuilder.EnclaveAttestationUrl?displayProperty=nameWithType>，为基于 enclave 的 Always Encrypted 指定 URI。</span><span class="sxs-lookup"><span data-stu-id="4d376-308"><xref:System.Data.SqlClient.SqlConnectionStringBuilder.EnclaveAttestationUrl?displayProperty=nameWithType>, which specifies the Uri for enclave-based Always Encrypted.</span></span>

- <span data-ttu-id="4d376-309"><xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider>，一个抽象类，所有 enclave 提供程序都自它派生。</span><span class="sxs-lookup"><span data-stu-id="4d376-309"><xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider>, which is an abstract class from which all enclave providers are derived.</span></span>

- <span data-ttu-id="4d376-310"><xref:System.Data.SqlClient.SqlEnclaveSession>，封装给定 enclave 会话的状态。</span><span class="sxs-lookup"><span data-stu-id="4d376-310"><xref:System.Data.SqlClient.SqlEnclaveSession>, which encapsulates the state for a given enclave session.</span></span>

- <span data-ttu-id="4d376-311"><xref:System.Data.SqlClient.SqlEnclaveAttestationParameters>，提供 SQL Server 所使用的认证参数，以获取执行特定认证协议所需的信息。</span><span class="sxs-lookup"><span data-stu-id="4d376-311"><xref:System.Data.SqlClient.SqlEnclaveAttestationParameters>, which provides the attestation parameters used by SQL Server to get information required to execute a particular Attestation Protocol.</span></span>

<span data-ttu-id="4d376-312">抽象 <xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider?displayProperty=nameWithType> 类提供了 enclave 提供程序的功能，应用程序配置文件随后会指定该类的具体实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-312">The application configuration file then specifies a concrete implementation of the abstract <xref:System.Data.SqlClient.SqlColumnEncryptionEnclaveProvider?displayProperty=nameWithType> class that provides the functionality for the enclave provider.</span></span> <span data-ttu-id="4d376-313">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-313">For example:</span></span>

```xml
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="Azure" type="Microsoft.SqlServer.Management.AlwaysEncrypted.AzureEnclaveProvider,MyApp"/>
      <add name="HGS" type="Microsoft.SqlServer.Management.AlwaysEncrypted.HGSEnclaveProvider,MyApp" />
    </providers>
  </SqlColumnEncryptionEnclaveProviders >
</configuration>
```

<span data-ttu-id="4d376-314">基于 enclave 的 Always Encrypted 的基本流是：</span><span class="sxs-lookup"><span data-stu-id="4d376-314">The basic flow of enclave-based Always Encrypted is:</span></span>

1. <span data-ttu-id="4d376-315">用户创建与 SQL Server（支持基于 enclave 的 Always Encrypted）的 AlwaysEncrypted 连接。</span><span class="sxs-lookup"><span data-stu-id="4d376-315">The user creates an AlwaysEncrypted connection to SQL Server that supported enclave-based Always Encrypted.</span></span> <span data-ttu-id="4d376-316">驱动程序联系认证服务以确保它连接到正确的 enclave。</span><span class="sxs-lookup"><span data-stu-id="4d376-316">The driver contacts the attestation service to ensure that it is connecting to right enclave.</span></span>

1. <span data-ttu-id="4d376-317">enclave 验证成功后，驱动程序将建立与托管在 SQL Server 上的安全 enclave 之间的安全信道。</span><span class="sxs-lookup"><span data-stu-id="4d376-317">Once the enclave has been attested, the driver establishes a secure channel with the secure enclave hosted on SQL Server.</span></span>

1. <span data-ttu-id="4d376-318">在 SQL 连接期间，驱动程序与安全 enclave 共享由客户端授权的加密密钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-318">The driver shares encryption keys authorized by the client with the secure enclave for the duration of the SQL connection.</span></span>

<a name="wpf472"></a>

#### <a name="windows-presentation-foundation"></a><span data-ttu-id="4d376-319">Windows Presentation Foundation</span><span class="sxs-lookup"><span data-stu-id="4d376-319">Windows Presentation Foundation</span></span>

<span data-ttu-id="4d376-320">**按源查找 ResourceDictionaries**</span><span class="sxs-lookup"><span data-stu-id="4d376-320">**Finding ResourceDictionaries by Source**</span></span>

<span data-ttu-id="4d376-321">从 .NET Framework 4.7.2 开始，诊断助手可以找到从给定源 URI 创建的 <xref:System.Windows.Xps.Packaging.IXpsFixedPageReader.ResourceDictionaries>。</span><span class="sxs-lookup"><span data-stu-id="4d376-321">Starting with .NET Framework 4.7.2, a diagnostic assistant can locate the <xref:System.Windows.Xps.Packaging.IXpsFixedPageReader.ResourceDictionaries> that have been created from a given source Uri.</span></span> <span data-ttu-id="4d376-322"> （此功能通过诊断助手使用，而非生产应用程序。）通过诊断助手（例如 Visual Studio 的“编辑并继续”），用户可编辑 ResourceDictionary，将更改应用于正在运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-322">(This feature is for use by diagnostic assistants, not by production applications.) A diagnostic assistant such as Visual Studio's "Edit-and-Continue" facility lets its user edit a ResourceDictionary with the intent that the changes be applied to the running application.</span></span> <span data-ttu-id="4d376-323">要实现这一点，其中一个步骤是从被编辑的字典中找到正在运行的应用程序创建的所有 ResourceDictionary。</span><span class="sxs-lookup"><span data-stu-id="4d376-323">One step in achieving this is finding all the ResourceDictionaries that the running application has created from the dictionary that's being edited.</span></span> <span data-ttu-id="4d376-324">例如，应用程序可以声明某个从给定源 URI 复制内容的 ResourceDictionary：</span><span class="sxs-lookup"><span data-stu-id="4d376-324">For example, an application can declare a ResourceDictionary whose content is copied from a given source URI:</span></span>

```xml
<ResourceDictionary Source="MyRD.xaml" />
```

<span data-ttu-id="4d376-325">编辑 MyRD.xaml 中的原始标记的诊断助手可以使用新功能来找到字典  。</span><span class="sxs-lookup"><span data-stu-id="4d376-325">A diagnostic assistant that edits the original markup in *MyRD.xaml* can use the new feature to locate the dictionary.</span></span> <span data-ttu-id="4d376-326"> 此功能通过新的静态方法 <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetResourceDictionariesForSource%2A?displayProperty=nameWithType> 实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-326">The feature is implemented by a new static method, <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetResourceDictionariesForSource%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="4d376-327">诊断助手使用标识原始标记的绝对 URI 调用新方法，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-327">The diagnostic assistant calls the new method using an absolute Uri that identifies the original markup, as illustrated by the following code:</span></span>

```csharp
IEnumerable<ResourceDictionary> dictionaries = ResourceDictionaryDiagnostics.GetResourceDictionariesForSource(new Uri("pack://application:,,,/MyApp;component/MyRD.xaml"));
```

```vb
Dim dictionaries As IEnumerable(Of ResourceDictionary) = ResourceDictionaryDiagnostics.GetResourceDictionariesForSource(New Uri("pack://application:,,,/MyApp;component/MyRD.xaml"))
```

<span data-ttu-id="4d376-328">该方法返回空的枚举值，除非启用了 <xref:System.Windows.Diagnostics.VisualDiagnostics> 并且设置了 [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) 环境变量。</span><span class="sxs-lookup"><span data-stu-id="4d376-328">The method returns an empty enumerable unless <xref:System.Windows.Diagnostics.VisualDiagnostics> is enabled and the [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) environment variable is set.</span></span>

<span data-ttu-id="4d376-329">**查找 ResourceDictionary 所有者**</span><span class="sxs-lookup"><span data-stu-id="4d376-329">**Finding ResourceDictionary owners**</span></span>

<span data-ttu-id="4d376-330">从 .NET Framework 4.7.2 开始，诊断助手可以找到给定 <xref:Windows.UI.Xaml.ResourceDictionary> 的所有者。</span><span class="sxs-lookup"><span data-stu-id="4d376-330">Starting with .NET Framework 4.7.2, a diagnostic assistant can locate the owners of a given <xref:Windows.UI.Xaml.ResourceDictionary>.</span></span> <span data-ttu-id="4d376-331"> （此功能供诊断助手，而非生产应用程序使用。）每当对 <xref:Windows.UI.Xaml.ResourceDictionary> 做出更改时，WPF 会自动查找所有可能会受此更改影响的 [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) 引用。</span><span class="sxs-lookup"><span data-stu-id="4d376-331">(The feature is for use by diagnostic assistants and not by production applications.) Whenever a change is made to a <xref:Windows.UI.Xaml.ResourceDictionary>, WPF automatically finds all [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) references that might be affected by the change.</span></span>

<span data-ttu-id="4d376-332">诊断助手（例如 Visual Studio 的“编辑并继续”）可能想对此进行扩展以处理 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 引用。</span><span class="sxs-lookup"><span data-stu-id="4d376-332">A diagnostic assistant such as Visual Studio's "Edit-and-Continue" facility may want to extend this to handle [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) references.</span></span> <span data-ttu-id="4d376-333">此过程的第一步是找到字典的所有者，也就是找到其 `Resources` 属性引用该字典（不管是直接引用，还是通过 <xref:System.Windows.ResourceDictionary.MergedDictionaries?displayProperty=nameWithType> 属性间接引用）的所有对象。</span><span class="sxs-lookup"><span data-stu-id="4d376-333">The first step in this process is to find the owners of the dictionary; that is, to find all the objects whose `Resources` property refers to the dictionary (either directly, or indirectly via the <xref:System.Windows.ResourceDictionary.MergedDictionaries?displayProperty=nameWithType> property).</span></span> <span data-ttu-id="4d376-334"><xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics?displayProperty=nameWithType> 类上实现的三个新的静态方法（每个对应具有 `Resources` 属性的基类型）支持此步骤：</span><span class="sxs-lookup"><span data-stu-id="4d376-334">Three new static methods implemented on the <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics?displayProperty=nameWithType> class, one for each of the base types that has a `Resources` property, support this step:</span></span>

- [`public static IEnumerable<FrameworkElement> GetFrameworkElementOwners(ResourceDictionary dictionary);`](xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetFrameworkElementOwners%2A)

- [`public static IEnumerable<FrameworkContentElement> GetFrameworkContentElementOwners(ResourceDictionary dictionary);`](xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetFrameworkContentElementOwners%2A)

- [`public static IEnumerable<Application> GetApplicationOwners(ResourceDictionary dictionary);`](xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.GetApplicationOwners%2A)

<span data-ttu-id="4d376-335">这些方法返回空的枚举值，除非启用了 <xref:System.Windows.Diagnostics.VisualDiagnostics> 并且设置了 [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) 环境变量。</span><span class="sxs-lookup"><span data-stu-id="4d376-335">These methods return an empty enumerable unless <xref:System.Windows.Diagnostics.VisualDiagnostics> is enabled and the [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) environment variable is set.</span></span>

<span data-ttu-id="4d376-336">**查找 StaticResource 引用**</span><span class="sxs-lookup"><span data-stu-id="4d376-336">**Finding StaticResource references**</span></span>

<span data-ttu-id="4d376-337">现在，每当一个 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 引用被解析时，诊断助手都能收到通知。</span><span class="sxs-lookup"><span data-stu-id="4d376-337">A diagnostic assistant can now receive a notification whenever a [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) reference is resolved.</span></span> <span data-ttu-id="4d376-338"> （此功能供诊断助手，而非生产应用程序使用。）诊断助手（例如 Visual Studio 的“编辑并继续”）可能想在 <xref:Windows.UI.Xaml.ResourceDictionary> 中某个资源的值发生更改时更新该资源的所有使用。</span><span class="sxs-lookup"><span data-stu-id="4d376-338">(The feature is for use by diagnostic assistants, not by production applications.) A diagnostic assistant such as Visual Studio's "Edit-and-Continue" facility may want to update all uses of a resource when its value in a <xref:Windows.UI.Xaml.ResourceDictionary> changes.</span></span> <span data-ttu-id="4d376-339">WPF 为 [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) 引用自动完成此操作，但不会为 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 引用有意执行该操作。</span><span class="sxs-lookup"><span data-stu-id="4d376-339">WPF does this automatically for [DynamicResource](/dotnet/desktop/wpf/advanced/dynamicresource-markup-extension) references, but it intentionally does not do so for [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) references.</span></span> <span data-ttu-id="4d376-340">从 .NET Framework 4.7.2 开始，诊断助手可以利用这些通知来查找静态资源的使用情况。</span><span class="sxs-lookup"><span data-stu-id="4d376-340">Starting with .NET Framework 4.7.2, the diagnostic assistant can use these notifications to locate those uses of the static resource.</span></span>

<span data-ttu-id="4d376-341">该通知由新的 <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.StaticResourceResolved?displayProperty=nameWithType> 事件实现：</span><span class="sxs-lookup"><span data-stu-id="4d376-341">The notification is implemented by the new <xref:System.Windows.Diagnostics.ResourceDictionaryDiagnostics.StaticResourceResolved?displayProperty=nameWithType> event:</span></span>

```csharp
public static event EventHandler<StaticResourceResolvedEventArgs> StaticResourceResolved;
```

```vb
Public Shared Event StaticResourceResolved As EventHandler(Of StaticResourceResolvedEventArgs)
```

<span data-ttu-id="4d376-342">每当运行时解析 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 引用时，都会引发此事件。</span><span class="sxs-lookup"><span data-stu-id="4d376-342">This event is raised whenever the runtime resolves a [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) reference.</span></span> <span data-ttu-id="4d376-343"><xref:System.Windows.Diagnostics.StaticResourceResolvedEventArgs> 参数描述解析，并指示托管 [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) 引用的对象和属性及用于解析的 <xref:Windows.UI.Xaml.ResourceDictionary> 和密钥：</span><span class="sxs-lookup"><span data-stu-id="4d376-343">The <xref:System.Windows.Diagnostics.StaticResourceResolvedEventArgs> arguments describe the resolution, and indicate the object and property that host the [StaticResource](/dotnet/desktop/wpf/advanced/staticresource-markup-extension) reference and the <xref:Windows.UI.Xaml.ResourceDictionary> and key used for the resolution:</span></span>

```csharp
public class StaticResourceResolvedEventArgs : EventArgs
{
   public Object TargetObject { get; }

   public Object TargetProperty { get; }

   public ResourceDictionary ResourceDictionary { get; }

   public object ResourceKey { get; }
}
```

```vb
Public Class StaticResourceResolvedEventArgs : Inherits EventArgs
   Public ReadOnly Property TargetObject As Object
   Public ReadOnly Property TargetProperty As Object
   Public ReadOnly Property ResourceDictionary As ResourceDictionary
   Public ReadOnly Property ResourceKey As Object
End Class
```

<span data-ttu-id="4d376-344">除非启用 <xref:System.Windows.Diagnostics.VisualDiagnostics> 并设置了 [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) 环境变量，否则不会引发该事件（且忽略它的 `add` 访问器）。</span><span class="sxs-lookup"><span data-stu-id="4d376-344">The event is not raised (and its `add` accessor is ignored) unless <xref:System.Windows.Diagnostics.VisualDiagnostics> is enabled and the [`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`](xref:System.Windows.Diagnostics.VisualDiagnostics.GetXamlSourceInfo%2A) environment variable is set.</span></span>

#### <a name="clickonce"></a><span data-ttu-id="4d376-345">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="4d376-345">ClickOnce</span></span>

<span data-ttu-id="4d376-346">Windows 窗体的 HDPI 感知应用程序、Windows Presentation Foundation (WPF) 以及 Visual Studio Tools for Office (VSTO) 都可以通过使用 ClickOnce 进行部署。</span><span class="sxs-lookup"><span data-stu-id="4d376-346">HDPI-aware applications for Windows Forms, Windows Presentation Foundation (WPF), and Visual Studio Tools for Office (VSTO) can all be deployed by using ClickOnce.</span></span> <span data-ttu-id="4d376-347">如果在应用程序清单中找到了以下条目，则部署将在 .NET Framework 4.7.2 下成功执行：</span><span class="sxs-lookup"><span data-stu-id="4d376-347">If the following entry is found in the application manifest, deployment will succeed under .NET Framework 4.7.2:</span></span>

```xml
<windowsSettings>
   <dpiAware xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">true</dpiAware>
</windowsSettings>
```

<span data-ttu-id="4d376-348">对于 Windows 窗体应用程序，不需要像以前那样在应用程序配置文件（而非应用程序清单）中设置 DPI 感知就可以成功完成 ClickOnce 部署。</span><span class="sxs-lookup"><span data-stu-id="4d376-348">For Windows Forms application, the previous workaround of setting DPI awareness in the application configuration file rather than the application manifest is no longer necessary for ClickOnce deployment to succeed.</span></span>

<a name="v471"></a>

## <a name="whats-new-in-net-framework-471"></a><span data-ttu-id="4d376-349">.NET Framework 4.7.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-349">What's new in .NET Framework 4.7.1</span></span>

<span data-ttu-id="4d376-350">.NET Framework 4.7.1 在以下几个领域新增了功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-350">.NET Framework 4.7.1 includes new features in the following areas:</span></span>

- [<span data-ttu-id="4d376-351">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-351">Base classes</span></span>](#core471)
- [<span data-ttu-id="4d376-352">公共语言运行时 (CLR)</span><span class="sxs-lookup"><span data-stu-id="4d376-352">Common language runtime (CLR)</span></span>](#clr)
- [<span data-ttu-id="4d376-353">网络连接</span><span class="sxs-lookup"><span data-stu-id="4d376-353">Networking</span></span>](#net471)
- [<span data-ttu-id="4d376-354">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-354">ASP.NET</span></span>](#asp-net471)

<span data-ttu-id="4d376-355">此外，.NET Framework 4.7.1 的重点是改进了辅助功能，使应用程序能为使用辅助技术的用户提供最佳体验。</span><span class="sxs-lookup"><span data-stu-id="4d376-355">In addition, a major focus in .NET Framework 4.7.1 is improved accessibility, which allows an application to provide an appropriate experience for users of Assistive Technology.</span></span> <span data-ttu-id="4d376-356">有关 .NET Framework 4.7.1 中辅助功能改进的信息，请参阅 [.NET Framework 中辅助功能的新增功能](whats-new-in-accessibility.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-356">For information on accessibility improvements in .NET Framework 4.7.1, see [What's new in accessibility in .NET Framework](whats-new-in-accessibility.md).</span></span>

<a name="core471"></a>

#### <a name="base-classes"></a><span data-ttu-id="4d376-357">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-357">Base classes</span></span>

<span data-ttu-id="4d376-358">**支持 .NET Standard 2.0**</span><span class="sxs-lookup"><span data-stu-id="4d376-358">**Support for .NET Standard 2.0**</span></span>

<span data-ttu-id="4d376-359">[.NET Standard](../../standard/net-standard.md) 定义一组 API，这些 API 必须可用于支持 Standard 版本的每个 .NET 实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-359">[.NET Standard](../../standard/net-standard.md) defines a set of APIs that must be available on each .NET implementation that supports that version of the standard.</span></span> <span data-ttu-id="4d376-360">.NET Framework 4.7.1 完全支持 .NET Standard 2.0 并增加了[ 200 个 API](https://github.com/dotnet/standard/blob/master/src/netstandard/src/ApiCompatBaseline.net461.txt)，这些 API 在 .NET Standard 2.0 中定义，.NET Framework 4.6.1、4.6.2 和 4.7 中也延续使用。</span><span class="sxs-lookup"><span data-stu-id="4d376-360">.NET Framework 4.7.1 fully supports .NET Standard 2.0 and adds [about 200 APIs](https://github.com/dotnet/standard/blob/master/src/netstandard/src/ApiCompatBaseline.net461.txt) that are defined in .NET Standard 2.0 and are missing from .NET Framework 4.6.1, 4.6.2, and 4.7.</span></span> <span data-ttu-id="4d376-361">（请注意，这些版本的 .NET Framework 只有在其他 .NET Standard 支持文件也部署在目标系统时才支持 .NET Standard 2.0。）有关详细信息，请参阅 [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)（.NET Framework 4.7.1 运行时和编译器功能）博客文章中的“BCL - .NET Standard 2.0 Support”（BCL - .NET Standard 2.0 支持）。</span><span class="sxs-lookup"><span data-stu-id="4d376-361">(Note that these versions of .NET Framework support .NET Standard 2.0 only if additional .NET Standard support files are also deployed on the target system.) For more information, see "BCL - .NET Standard 2.0 Support" in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span>

<span data-ttu-id="4d376-362">**支持配置生成器**</span><span class="sxs-lookup"><span data-stu-id="4d376-362">**Support for configuration builders**</span></span>

<span data-ttu-id="4d376-363">配置生成器允许开发者在运行时动态地插入和生成应用程序的配置设置。</span><span class="sxs-lookup"><span data-stu-id="4d376-363">Configuration builders allow developers to inject and build configuration settings for applications dynamically at run time.</span></span> <span data-ttu-id="4d376-364">自定义配置生成器可用于修改配置节中的现有数据，也可用于生成全新的配置节。</span><span class="sxs-lookup"><span data-stu-id="4d376-364">Custom configuration builders can be used to modify existing data in a configuration section or to build a configuration section entirely from scratch.</span></span> <span data-ttu-id="4d376-365">如果没有配置生成器，.config 文件将是静态的，并且其设置将在应用程序启动之前定义。</span><span class="sxs-lookup"><span data-stu-id="4d376-365">Without configuration builders, .config files are static, and their settings are defined some time before an application is launched.</span></span>

<span data-ttu-id="4d376-366">若要创建自定义配置生成器，请从抽象的 <xref:System.Configuration.ConfigurationBuilder> 类派生生成器并且替代其 <xref:System.Configuration.ConfigurationBuilder.ProcessConfigurationSection%2A?displayProperty=nameWithType> 和 <xref:System.Configuration.ConfigurationBuilder.ProcessRawXml%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="4d376-366">To create a custom configuration builder, you derive your builder from the abstract <xref:System.Configuration.ConfigurationBuilder> class and override its <xref:System.Configuration.ConfigurationBuilder.ProcessConfigurationSection%2A?displayProperty=nameWithType> and <xref:System.Configuration.ConfigurationBuilder.ProcessRawXml%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="4d376-367">也可在 .config 文件中定义生成器。</span><span class="sxs-lookup"><span data-stu-id="4d376-367">You also define your builders in your .config file.</span></span> <span data-ttu-id="4d376-368">有关详细信息，请参阅 [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)（.NET Framework 4.7.1 ASP.NET 和配置功能）博客文章中的“Configuration Builders”（配置生成器）一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-368">For more information, see the "Configuration Builders" section in the [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<span data-ttu-id="4d376-369">**运行时功能检测**</span><span class="sxs-lookup"><span data-stu-id="4d376-369">**Run-time feature detection**</span></span>

<span data-ttu-id="4d376-370"><xref:System.Runtime.CompilerServices.RuntimeFeature?displayProperty=nameWithType> 类提供一种机制，用于确定给定的 .NET 实现在编译时或运行时是否支持预定义的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-370">The <xref:System.Runtime.CompilerServices.RuntimeFeature?displayProperty=nameWithType> class provides a mechanism for determine whether a predefined feature is supported on a given .NET implementation at compile time or run time.</span></span> <span data-ttu-id="4d376-371">在编译时，编译器可以检查指定的字段是否存在，以确定是否支持某项功能，如果支持，它会发出利用这一功能的代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-371">At compile time, a compiler can check whether a specified field exists to determine whether the feature is supported; if so, it can emit code that takes advantage of that feature.</span></span> <span data-ttu-id="4d376-372">在运行时，应用程序可以在运行时发出代码之前调用 <xref:System.Runtime.CompilerServices.RuntimeFeature.IsSupported%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-372">At run time, an application can call the <xref:System.Runtime.CompilerServices.RuntimeFeature.IsSupported%2A?displayProperty=nameWithType> method before emitting code at runtime.</span></span> <span data-ttu-id="4d376-373">有关详细信息，请参阅 [Add helper method to describe features supported by the runtime](https://github.com/dotnet/corefx/issues/17116)（添加 helper 方法以描述运行时支持的功能）。</span><span class="sxs-lookup"><span data-stu-id="4d376-373">For more information, see [Add helper method to describe features supported by the runtime](https://github.com/dotnet/corefx/issues/17116).</span></span>

<span data-ttu-id="4d376-374">**值元组类型是可序列化的**</span><span class="sxs-lookup"><span data-stu-id="4d376-374">**Value tuple types are serializable**</span></span>

<span data-ttu-id="4d376-375">从 .NET Framework 4.7.1 起，<xref:System.ValueTuple?displayProperty=nameWithType> 及其相关的泛型类型被标记为[可序列化](xref:System.SerializableAttribute)，允许进行二进制序列化。</span><span class="sxs-lookup"><span data-stu-id="4d376-375">Starting with .NET Framework 4.7.1, <xref:System.ValueTuple?displayProperty=nameWithType> and its associated generic types are marked as [Serializable](xref:System.SerializableAttribute), which allows binary serialization.</span></span> <span data-ttu-id="4d376-376">这样，可以更轻松地将元组类型（如 <xref:System.Tuple%603> 和 <xref:System.Tuple%604>）迁移到值元组类型。</span><span class="sxs-lookup"><span data-stu-id="4d376-376">This should make migrating Tuple types, such as <xref:System.Tuple%603> and <xref:System.Tuple%604>, to value tuple types easier.</span></span> <span data-ttu-id="4d376-377">有关详细信息，请参阅 [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)（.NET Framework 4.7.1 运行时和编译器功能）博客文章中的“Compiler -- ValueTuple is Serializable”（编译器 -- 值元组是可序列化的）。</span><span class="sxs-lookup"><span data-stu-id="4d376-377">For more information, see "Compiler -- ValueTuple is Serializable" in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span>

<span data-ttu-id="4d376-378">**支持只读引用**</span><span class="sxs-lookup"><span data-stu-id="4d376-378">**Support for read-only references**</span></span>

<span data-ttu-id="4d376-379">.NET Framework 4.7.1 增加了 <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="4d376-379">.NET Framework 4.7.1 adds the <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="4d376-380">此特性由语言编译器用于标记具有只读 ref 返回类型或参数的成员。</span><span class="sxs-lookup"><span data-stu-id="4d376-380">This attribute is used by language compilers to mark members that have read-only ref return types or parameters.</span></span> <span data-ttu-id="4d376-381">有关详细信息，请参阅 [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)（.NET Framework 4.7.1 运行时和编译器功能）博客文章中的“Compiler -- Support for ReadOnlyReferences”（编译器 -- 支持只读引用）。</span><span class="sxs-lookup"><span data-stu-id="4d376-381">For more information, see "Compiler -- Support for ReadOnlyReferences" in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span> <span data-ttu-id="4d376-382">有关 ref 返回值的信息，请参阅 [ref 返回值和 ref 局部变量（C# 指南）](../../csharp/programming-guide/classes-and-structs/ref-returns.md)和 [ref 返回值 (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/ref-return-values.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-382">For information on ref return values, see [Ref return values and ref locals (C# Guide)](../../csharp/programming-guide/classes-and-structs/ref-returns.md) and [Ref return values (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/ref-return-values.md).</span></span>

<a name="clr"></a>

#### <a name="common-language-runtime-clr"></a><span data-ttu-id="4d376-383">公共语言运行时 (CLR)</span><span class="sxs-lookup"><span data-stu-id="4d376-383">Common language runtime (CLR)</span></span>

<span data-ttu-id="4d376-384">**垃圾回收性能改进**</span><span class="sxs-lookup"><span data-stu-id="4d376-384">**Garbage collection performance improvements**</span></span>

<span data-ttu-id="4d376-385">.NET Framework 4.7.1 中的垃圾回收 (GC) 的更改提升了整体性能，尤其是大型对象堆 (LOH) 分配的性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-385">Changes to garbage collection (GC) in .NET Framework 4.7.1 improve overall performance, especially for large object heap (LOH) allocations.</span></span> <span data-ttu-id="4d376-386">在 .NET Framework 4.7.1 中，小型对象堆 (SOH) 分配和 LOH 分配使用不同的锁，当后台 GC 整理 SOH 时即发生 LOH 分配。</span><span class="sxs-lookup"><span data-stu-id="4d376-386">In .NET Framework 4.7.1, separate locks are used for small object heap (SOH) and LOH allocations, which allows LOH allocations to occur when background GC is sweeping the SOH.</span></span> <span data-ttu-id="4d376-387">这样，进行大量 LOH 分配的应用程序发生分配锁争用的情况将减少，从而提高性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-387">As a result, applications that make a large number of LOH allocations should see a reduction in allocation lock contention and improved performance.</span></span> <span data-ttu-id="4d376-388">有关详细信息，请参阅 [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/)（.NET Framework 4.7.1 运行时和编译器功能）博客文章中的“Runtime -- GC Performance Improvements”（运行时 -- GC 性能改进）一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-388">For more information, see the "Runtime -- GC Performance Improvements" section in the [.NET Framework 4.7.1 Runtime and Compiler Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-runtime-and-compiler-features/) blog post.</span></span>

<a name="net471"/>

#### <a name="networking"></a><span data-ttu-id="4d376-389">网络</span><span class="sxs-lookup"><span data-stu-id="4d376-389">Networking</span></span>

<span data-ttu-id="4d376-390">**Message.HashAlgorithm 的 SHA-2 支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-390">**SHA-2 support for Message.HashAlgorithm**</span></span>

<span data-ttu-id="4d376-391">在 .NET Framework 4.7 及早期版本中，<xref:System.Messaging.Message.HashAlgorithm%2A?displayProperty=nameWithType> 属性仅支持 <xref:System.Messaging.HashAlgorithm.Md5?displayProperty=nameWithType> 和 <xref:System.Messaging.HashAlgorithm.Sha?displayProperty=nameWithType> 的值。</span><span class="sxs-lookup"><span data-stu-id="4d376-391">In .NET Framework 4.7 and earlier versions, the <xref:System.Messaging.Message.HashAlgorithm%2A?displayProperty=nameWithType> property supported values of <xref:System.Messaging.HashAlgorithm.Md5?displayProperty=nameWithType> and <xref:System.Messaging.HashAlgorithm.Sha?displayProperty=nameWithType> only.</span></span> <span data-ttu-id="4d376-392">从 .NET Framework 4.7.1 开始，还支持 <xref:System.Messaging.HashAlgorithm.Sha256?displayProperty=nameWithType>、<xref:System.Messaging.HashAlgorithm.Sha384?displayProperty=nameWithType> 和 <xref:System.Messaging.HashAlgorithm.Sha512?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="4d376-392">Starting with .NET Framework 4.7.1, <xref:System.Messaging.HashAlgorithm.Sha256?displayProperty=nameWithType>, <xref:System.Messaging.HashAlgorithm.Sha384?displayProperty=nameWithType>, and <xref:System.Messaging.HashAlgorithm.Sha512?displayProperty=nameWithType> are also supported.</span></span> <span data-ttu-id="4d376-393">实际是否使用此值取决于消息队列，因为 <xref:System.Messaging.Message> 实例本身不进行哈希处理，而是简单地将值传递到消息队列。</span><span class="sxs-lookup"><span data-stu-id="4d376-393">Whether this value is actually used depends on MSMQ, since the <xref:System.Messaging.Message> instance itself does no hashing but simply passes on values to MSMQ.</span></span> <span data-ttu-id="4d376-394">有关详细信息，请参阅 [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)（.NET Framework 4.7.1 ASP.NET 和配置功能）博客文章中的“SHA-2 support for Message.HashAlgorithm”（Message.HashAlgorithm 的 SHA-2 支持）一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-394">For more information, see the "SHA-2 support for Message.HashAlgorithm" section in the [.NET Framework 4.7.1 ASP.NET and Configuration features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<a name="asp-net471"></a>

#### <a name="aspnet"></a><span data-ttu-id="4d376-395">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-395">ASP.NET</span></span>

<span data-ttu-id="4d376-396">**ASP.NET 应用程序中的执行步骤**</span><span class="sxs-lookup"><span data-stu-id="4d376-396">**Execution steps in ASP.NET applications**</span></span>

<span data-ttu-id="4d376-397">ASP.NET 处理包括 23 个事件的预定义管道中的请求。</span><span class="sxs-lookup"><span data-stu-id="4d376-397">ASP.NET processes requests in a predefined pipeline that includes 23 events.</span></span> <span data-ttu-id="4d376-398">ASP.NET 执行每个事件处理程序作为一个执行步骤。</span><span class="sxs-lookup"><span data-stu-id="4d376-398">ASP.NET executes each event handler as an execution step.</span></span> <span data-ttu-id="4d376-399">对于 .NET Framework 4.7 之前的 ASP.NET 版本，由于本机和托管线程之间的切换，ASP.NET 无法传送执行上下文。</span><span class="sxs-lookup"><span data-stu-id="4d376-399">In versions of ASP.NET up to .NET Framework 4.7, ASP.NET can't flow the execution context due to switching between native and managed threads.</span></span> <span data-ttu-id="4d376-400">ASP.NET 有选择性地仅传送 <xref:System.Web.HttpContext>。</span><span class="sxs-lookup"><span data-stu-id="4d376-400">Instead, ASP.NET selectively flows only the <xref:System.Web.HttpContext>.</span></span> <span data-ttu-id="4d376-401">从 .NET Framework 4.7.1 开始，<xref:System.Web.HttpApplication.OnExecuteRequestStep(System.Action{System.Web.HttpContextBase,System.Action})?displayProperty=nameWithType> 方法还允许模块还原环境数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-401">Starting with .NET Framework 4.7.1, the <xref:System.Web.HttpApplication.OnExecuteRequestStep(System.Action{System.Web.HttpContextBase,System.Action})?displayProperty=nameWithType> method also allows modules to restore ambient data.</span></span> <span data-ttu-id="4d376-402">此功能针对与跟踪、分析、诊断或事务（例如应用程序的执行流）相关的库。</span><span class="sxs-lookup"><span data-stu-id="4d376-402">This feature is targeted at libraries concerned with tracing, profiling, diagnostics, or transactions, for example, that care about the execution flow of the application.</span></span> <span data-ttu-id="4d376-403">有关详细信息，请参阅 [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)（.NET Framework 4.7.1 ASP.NET 和配置功能）博客文章的“ASP.NET Execution Step Feature”（ASP.NET 执行步骤功能）一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-403">For more information, see the "ASP.NET Execution Step Feature" in the [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<span data-ttu-id="4d376-404">**ASP.NET HttpCookie 分析**</span><span class="sxs-lookup"><span data-stu-id="4d376-404">**ASP.NET HttpCookie parsing**</span></span>

<span data-ttu-id="4d376-405">.NET Framework 4.7.1 包括新的方法 <xref:System.Web.HttpCookie.TryParse%2A?displayProperty=nameWithType>，此方法提供标准化的方式来从字符串创建 <xref:System.Web.HttpCookie> 对象，并精确分配 cookie 值（如过期日期和路径）。</span><span class="sxs-lookup"><span data-stu-id="4d376-405">.NET Framework 4.7.1 includes a new method, <xref:System.Web.HttpCookie.TryParse%2A?displayProperty=nameWithType>, that provides a standardized way to create an <xref:System.Web.HttpCookie> object from a string and accurately assign cookie values such as expiration date and path.</span></span> <span data-ttu-id="4d376-406">有关详细信息，请参阅 [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/)（.NET Framework 4.7.1 ASP.NET 和配置功能）博客文章中的“ASP.NET HttpCookie parsing”（ASP.NET HttpCookie 分析）一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-406">For more information, see "ASP.NET HttpCookie parsing" in the [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://devblogs.microsoft.com/dotnet/net-framework-4-7-1-asp-net-and-configuration-features/) blog post.</span></span>

<span data-ttu-id="4d376-407">**ASP.NET 窗体身份验证凭据的 SHA-2 哈希选项**</span><span class="sxs-lookup"><span data-stu-id="4d376-407">**SHA-2 hash options for ASP.NET forms authentication credentials**</span></span>

<span data-ttu-id="4d376-408">在 .NET Framework 4.7 及其早期版本中，ASP.NET 允许开发者使用 MD5 或 SHA1 在配置文件中存储用户凭据和哈希密码。</span><span class="sxs-lookup"><span data-stu-id="4d376-408">In .NET Framework 4.7 and earlier versions, ASP.NET allowed developers to store user credentials with hashed passwords in configuration files using either MD5 or SHA1.</span></span> <span data-ttu-id="4d376-409">从 .NET Framework 4.7.1 开始，ASP.NET 还支持新的安全 SHA-2 哈希选项（如 SHA256、SHA384 和 SHA512）。</span><span class="sxs-lookup"><span data-stu-id="4d376-409">Starting with .NET Framework 4.7.1, ASP.NET also supports new secure SHA-2 hash options such as SHA256, SHA384, and SHA512.</span></span> <span data-ttu-id="4d376-410">SHA1 保留默认值，非默认哈希算法可以在 Web 配置文件中定义。</span><span class="sxs-lookup"><span data-stu-id="4d376-410">SHA1 remains the default, and a non-default hash algorithm can be defined in the web configuration file.</span></span> <span data-ttu-id="4d376-411">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-411">For example:</span></span>

```xml
<system.web>
    <authentication mode="Forms">
        <forms loginUrl="~/login.aspx">
          <credentials passwordFormat="SHA512">
            <user name="jdoe" password="6D003E98EA1C7F04ABF8FCB375388907B7F3EE06F278DB966BE960E7CBBD103DF30CA6D61F7E7FD981B2E4E3A64D43C836A4BEDCA165C33B163E6BCDC538A664" />
          </credentials>
        </forms>
    </authentication>
</system.web>
```

<a name="v47"></a>

## <a name="whats-new-in-net-framework-47"></a><span data-ttu-id="4d376-412">.NET Framework 4.7 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-412">What's new in .NET Framework 4.7</span></span>

<span data-ttu-id="4d376-413">.NET Framework 4.7 在以下几个领域新增了功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-413">.NET Framework 4.7 includes new features in the following areas:</span></span>

- [<span data-ttu-id="4d376-414">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-414">Base classes</span></span>](#Core47)
- [<span data-ttu-id="4d376-415">网络连接</span><span class="sxs-lookup"><span data-stu-id="4d376-415">Networking</span></span>](#net47)
- [<span data-ttu-id="4d376-416">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-416">ASP.NET</span></span>](#ASP-NET47)
- [<span data-ttu-id="4d376-417">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="4d376-417">Windows Communication Foundation (WCF)</span></span>](#wcf47)
- [<span data-ttu-id="4d376-418">Windows 窗体</span><span class="sxs-lookup"><span data-stu-id="4d376-418">Windows Forms</span></span>](#wf47)
- [<span data-ttu-id="4d376-419">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-419">Windows Presentation Foundation (WPF)</span></span>](#WPF47)

<span data-ttu-id="4d376-420">有关 .NET Framework 4.7 中新增 API 的列表，请参阅 GitHub 上的 [.NET Framework 4.7 API 更改](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-420">For a list of new APIs added to .NET Framework 4.7, see [.NET Framework 4.7 API Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-api-changes.md) on GitHub.</span></span> <span data-ttu-id="4d376-421">有关 .NET Framework 4.7 中功能改进和 bug 修复的列表，请参阅 GitHub 上的 [.NET Framework 4.7 更改列表](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-421">For a list of feature improvements and bug fixes in .NET Framework 4.7, see [.NET Framework 4.7 List of Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-changes.md) on GitHub.</span></span> <span data-ttu-id="4d376-422">有关详细信息，请参阅 .NET 博客中的 [Announcing the .NET Framework 4.7](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-7/)（发布 .NET Framework 4.7）。</span><span class="sxs-lookup"><span data-stu-id="4d376-422">For more information, see [Announcing .NET Framework 4.7](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-7/) in the .NET blog.</span></span>

<a name="Core47"></a>

#### <a name="base-classes"></a><span data-ttu-id="4d376-423">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-423">Base classes</span></span>

<span data-ttu-id="4d376-424">.NET Framework 4.7 通过 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 改进了序列化：</span><span class="sxs-lookup"><span data-stu-id="4d376-424">.NET Framework 4.7 improves serialization by the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>:</span></span>

<span data-ttu-id="4d376-425">**借助椭圆曲线加密 (ECC) 增强了功能** _</span><span class="sxs-lookup"><span data-stu-id="4d376-425">**Enhanced functionality with Elliptic Curve Cryptography (ECC)** _</span></span>

<span data-ttu-id="4d376-426">在 .NET Framework 4.7 中，`ImportParameters(ECParameters)` 方法已添加到 <xref:System.Security.Cryptography.ECDsa> 和 <xref:System.Security.Cryptography.ECDiffieHellman> 类，以允许对象表示已经建立的密钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-426">In .NET Framework 4.7, `ImportParameters(ECParameters)` methods were added to the <xref:System.Security.Cryptography.ECDsa> and <xref:System.Security.Cryptography.ECDiffieHellman> classes to allow for an object to represent an already-established key.</span></span> <span data-ttu-id="4d376-427">此外，还添加了 `ExportParameters(Boolean)` 方法，以便于使用显式曲线参数导出密钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-427">An `ExportParameters(Boolean)` method was also added for exporting the key using explicit curve parameters.</span></span>

<span data-ttu-id="4d376-428">.NET Framework 4.7 现已开始支持其他曲线（其中包括 Brainpool 曲线套件），并添加了预定义的定义，以便于通过新工厂方法 <xref:System.Security.Cryptography.ECDsa.Create%2A> 和 <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A> 简化创建操作。</span><span class="sxs-lookup"><span data-stu-id="4d376-428">.NET Framework 4.7 also adds support for additional curves (including the Brainpool curve suite), and has added predefined definitions for ease-of-creation through the new <xref:System.Security.Cryptography.ECDsa.Create%2A> and <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A> factory methods.</span></span>

<span data-ttu-id="4d376-429">有关 [.NET Framework 4.7 加密改进示例](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e)，请访问 GitHub。</span><span class="sxs-lookup"><span data-stu-id="4d376-429">You can see an [example of .NET Framework 4.7 cryptography improvements](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e) on GitHub.</span></span>

<span data-ttu-id="4d376-430">_ *DataContractJsonSerializer 提供更出色的控制字符支持*\*</span><span class="sxs-lookup"><span data-stu-id="4d376-430">_ *Better support for control characters by the DataContractJsonSerializer*\*</span></span>

<span data-ttu-id="4d376-431">在 .NET Framework 4.7 中，<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 类会将符合 ECMAScript 6 标准的控制字符串行化。</span><span class="sxs-lookup"><span data-stu-id="4d376-431">In .NET Framework 4.7, the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> class serializes control characters in conformity with the ECMAScript 6 standard.</span></span> <span data-ttu-id="4d376-432">面向 .NET Framework 4.7 的应用程序默认启用此行为，而对于在 .NET Framework 4.7 下运行但面向 .NET Framework 先前版本的应用程序来说，可选择启用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-432">This behavior is enabled by default for applications that target .NET Framework 4.7, and is an opt-in feature for applications that are running under .NET Framework 4.7 but target a previous version of .NET Framework.</span></span> <span data-ttu-id="4d376-433">有关详细信息，请参阅[应用程序兼容性](../migration-guide/application-compatibility.md)部分。</span><span class="sxs-lookup"><span data-stu-id="4d376-433">For more information, see the [Application compatibility](../migration-guide/application-compatibility.md) section.</span></span>

<a name="net47"></a>

#### <a name="networking"></a><span data-ttu-id="4d376-434">网络</span><span class="sxs-lookup"><span data-stu-id="4d376-434">Networking</span></span>

<span data-ttu-id="4d376-435">.NET Framework 4.7 新增了以下网络相关功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-435">.NET Framework 4.7 adds the following network-related feature:</span></span>

<span data-ttu-id="4d376-436">**提供对 TLS 协议的默认操作系统支持** _</span><span class="sxs-lookup"><span data-stu-id="4d376-436">**Default operating system support for TLS protocols** _</span></span>

<span data-ttu-id="4d376-437">借助 <xref:System.Net.Security.SslStream?displayProperty=nameWithType> 和上托堆栈组件（如 HTTP、FTP 和 SMTP）使用的 TLS 堆栈，开发者可以使用操作系统支持的默认 TLS 协议。</span><span class="sxs-lookup"><span data-stu-id="4d376-437">The TLS stack, which is used by <xref:System.Net.Security.SslStream?displayProperty=nameWithType> and up-stack components such as HTTP, FTP, and SMTP, allows developers to use the default TLS protocols supported by the operating system.</span></span> <span data-ttu-id="4d376-438">开发者再也不需要对 TLS 版本进行硬编码。</span><span class="sxs-lookup"><span data-stu-id="4d376-438">Developers need no longer hard-code a TLS version.</span></span>

<a name="ASP-NET47"></a>

#### <a name="aspnet"></a><span data-ttu-id="4d376-439">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-439">ASP.NET</span></span>

<span data-ttu-id="4d376-440">在 .NET Framework 4.7 中，ASP.NET 新增了以下功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-440">In .NET Framework 4.7, ASP.NET includes the following new features:</span></span>

<span data-ttu-id="4d376-441">_ *对象缓存扩展性*\*</span><span class="sxs-lookup"><span data-stu-id="4d376-441">_ *Object Cache Extensibility*\*</span></span>

<span data-ttu-id="4d376-442">自 .NET Framework 4.7 起，ASP.NET 新增了一组 API，以便开发者可以替换内存中对象缓存和内存监视的默认 ASP.NET 实现代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-442">Starting with .NET Framework 4.7, ASP.NET adds a new set of APIs that allow developers to replace the default ASP.NET implementations for in-memory object caching and memory monitoring.</span></span> <span data-ttu-id="4d376-443">现在，如果 ASP.NET 实现代码不充分，开发者可以替换以下三个组件中的任意一个：</span><span class="sxs-lookup"><span data-stu-id="4d376-443">Developers can now replace any of the following three components if the ASP.NET implementation is not adequate:</span></span>

- <span data-ttu-id="4d376-444">**对象缓存存储** ：</span><span class="sxs-lookup"><span data-stu-id="4d376-444">**Object Cache Store** .</span></span> <span data-ttu-id="4d376-445">在新的缓存提供程序配置部分中，开发者可以使用新接口 **ICacheStoreProvider** 为 ASP.NET 应用程序插入对象缓存的新实现代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-445">By using the new cache providers configuration section, developers can plug in new implementations of an object cache for an ASP.NET application by using the new **ICacheStoreProvider** interface.</span></span>

- <span data-ttu-id="4d376-446">**内存监视** ：</span><span class="sxs-lookup"><span data-stu-id="4d376-446">**Memory monitoring** .</span></span> <span data-ttu-id="4d376-447">当运行的应用程序接近所配置的专用字节进程限制，或计算机的可用总物理内存不足时，ASP.NET 中的默认内存监视器就会通知应用程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-447">The default memory monitor in ASP.NET notifies applications when they are running close to the configured private bytes limit for the process, or when the machine is low on total available physical RAM.</span></span> <span data-ttu-id="4d376-448">接近这些限制时，就会触发通知。</span><span class="sxs-lookup"><span data-stu-id="4d376-448">When these limits are near, notifications are fired.</span></span> <span data-ttu-id="4d376-449">对于某些应用程序，通知的触发点与限制过近，无法及时响应。</span><span class="sxs-lookup"><span data-stu-id="4d376-449">For some applications, notifications are fired too close to the configured limits to allow for useful reactions.</span></span> <span data-ttu-id="4d376-450">开发人员现在可以编写自己的内存监视器，以通过使用 <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=nameWithType> 属性替换默认的内存监视器。</span><span class="sxs-lookup"><span data-stu-id="4d376-450">Developers can now write their own memory monitors to replace the default by using the <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=nameWithType> property.</span></span>

- <span data-ttu-id="4d376-451">**内存限制响应** ：</span><span class="sxs-lookup"><span data-stu-id="4d376-451">**Memory Limit Reactions** .</span></span> <span data-ttu-id="4d376-452">默认情况下，当接近专用字节进程限制时，ASP.NET 会尝试释放对象缓存，并定期调用 <xref:System.GC.Collect%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="4d376-452">By default, ASP.NET attempts to trim the object cache and periodically call <xref:System.GC.Collect%2A?displayProperty=nameWithType> when the private byte process limit is near.</span></span> <span data-ttu-id="4d376-453">对于某些应用程序，<xref:System.GC.Collect%2A?displayProperty=nameWithType> 调用频率或缓存释放量的效率低下。</span><span class="sxs-lookup"><span data-stu-id="4d376-453">For some applications, the frequency of calls to <xref:System.GC.Collect%2A?displayProperty=nameWithType> or the amount of cache that is trimmed are inefficient.</span></span> <span data-ttu-id="4d376-454">开发者现在可以向应用程序的内存监视器添加 **IObserver** 实现代码，从而替换或补充默认行为。</span><span class="sxs-lookup"><span data-stu-id="4d376-454">Developers can now replace or supplement the default behavior by subscribing **IObserver** implementations to the application's memory monitor.</span></span>

<a name="wcf47"></a>

#### <a name="windows-communication-foundation-wcf"></a><span data-ttu-id="4d376-455">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="4d376-455">Windows Communication Foundation (WCF)</span></span>

<span data-ttu-id="4d376-456">Windows Communication Foundation (WCF) 新增了以下功能和更改：</span><span class="sxs-lookup"><span data-stu-id="4d376-456">Windows Communication Foundation (WCF) adds the following features and changes:</span></span>

<span data-ttu-id="4d376-457">**能够配置 TLS 1.1 或 TLS 1.2 默认消息安全设置**</span><span class="sxs-lookup"><span data-stu-id="4d376-457">**Ability to configure the default message security settings to TLS 1.1 or TLS 1.2**</span></span>

<span data-ttu-id="4d376-458">自 .NET Framework 4.7 起，除了 SSL 3.0 和 TLS 1.0 外，WCF 还允许配置 TLS 1.1 或 TLS 1.2 作为默认消息安全协议。</span><span class="sxs-lookup"><span data-stu-id="4d376-458">Starting with .NET Framework 4.7, WCF allows you to configure TLS 1.1 or TLS 1.2 in addition to SSL 3.0 and TLS 1.0 as the default message security protocol.</span></span> <span data-ttu-id="4d376-459">这是一项选择启用设置；必须向应用程序配置文件添加以下条目，才能启用此设置：</span><span class="sxs-lookup"><span data-stu-id="4d376-459">This is an opt-in setting; to enable it, you must add the following entry to your application configuration file:</span></span>

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
</runtime>
```

<span data-ttu-id="4d376-460">**提升了 WCF 应用程序和 WCF 序列化的可靠性**</span><span class="sxs-lookup"><span data-stu-id="4d376-460">**Improved reliability of WCF applications and WCF serialization**</span></span>

<span data-ttu-id="4d376-461">WCF 包含大量代码更改，消除了争用条件，从而提升了序列化选项的性能和可靠性。</span><span class="sxs-lookup"><span data-stu-id="4d376-461">WCF includes a number of code changes that eliminate race conditions, thereby improving performance and the reliability of serialization options.</span></span> <span data-ttu-id="4d376-462">其中包括:</span><span class="sxs-lookup"><span data-stu-id="4d376-462">These include:</span></span>

- <span data-ttu-id="4d376-463">更好地支持在调用 **SocketConnection.BeginRead** 和 **SocketConnection.Read** 时混合异步和同步代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-463">Better support for mixing asynchronous and synchronous code in calls to **SocketConnection.BeginRead** and **SocketConnection.Read** .</span></span>
- <span data-ttu-id="4d376-464">提升了在中止与 **SharedConnectionListener** 和 **DuplexChannelBinder** 的连接时的可靠性。</span><span class="sxs-lookup"><span data-stu-id="4d376-464">Improved reliability when aborting a connection with **SharedConnectionListener** and **DuplexChannelBinder** .</span></span>
- <span data-ttu-id="4d376-465">提高了调用 <xref:System.Runtime.Serialization.FormatterServices.GetSerializableMembers%28System.Type%29?displayProperty=nameWithType> 方法时序列化操作的可靠性。</span><span class="sxs-lookup"><span data-stu-id="4d376-465">Improved reliability of serialization operations when calling the <xref:System.Runtime.Serialization.FormatterServices.GetSerializableMembers%28System.Type%29?displayProperty=nameWithType> method.</span></span>
- <span data-ttu-id="4d376-466">提升了在调用 **ChannelSynchronizer.RemoveWaiter** 方法以删除等待程序时的可靠性。</span><span class="sxs-lookup"><span data-stu-id="4d376-466">Improved reliability when removing a waiter by calling the **ChannelSynchronizer.RemoveWaiter** method.</span></span>

<a name="wf47"></a>

#### <a name="windows-forms"></a><span data-ttu-id="4d376-467">Windows 窗体</span><span class="sxs-lookup"><span data-stu-id="4d376-467">Windows Forms</span></span>

<span data-ttu-id="4d376-468">在 .NET Framework 4.7 中，Windows 窗体改进了对高 DPI 监视器的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-468">In .NET Framework 4.7, Windows Forms improves support for high DPI monitors.</span></span>

<span data-ttu-id="4d376-469">**高 DPI 支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-469">**High DPI support**</span></span>

<span data-ttu-id="4d376-470">自定位 .NET Framework 4.7 的应用程序起，.NET Framework 为 Windows 窗体应用程序提供高 DPI 和动态 DPI 支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-470">Starting with applications that target .NET Framework 4.7, .NET Framework features high DPI and dynamic DPI support for Windows Forms applications.</span></span> <span data-ttu-id="4d376-471">高 DPI 支持改进了高 DPI 监视器上窗体和控件的布局和外观。</span><span class="sxs-lookup"><span data-stu-id="4d376-471">High DPI support improves the layout and appearance of forms and controls on high DPI monitors.</span></span> <span data-ttu-id="4d376-472">当用户更改正在运行的应用程序的 DPI 或显示比例系数时，动态 DPI 会更改窗体和控件的布局和外观。</span><span class="sxs-lookup"><span data-stu-id="4d376-472">Dynamic DPI changes the layout and appearance of forms and controls when the user changes the DPI or display scale factor of a running application.</span></span>

<span data-ttu-id="4d376-473">高 DPI 支持是一项选择启用功能，可通过在应用程序配置文件中定义 [\<System.Windows.Forms.ConfigurationSection>](../configure-apps/file-schema/winforms/index.md) 部分进行配置。</span><span class="sxs-lookup"><span data-stu-id="4d376-473">High DPI support is an opt-in feature that you configure by defining a [\<System.Windows.Forms.ConfigurationSection>](../configure-apps/file-schema/winforms/index.md) section in your application configuration file.</span></span> <span data-ttu-id="4d376-474">若要详细了解如何向 Windows 窗体应用程序添加高 DPI 支持和动态 DPI 支持，请参阅 [Windows 窗体中的高 DPI 支持](/dotnet/desktop/winforms/high-dpi-support-in-windows-forms)。</span><span class="sxs-lookup"><span data-stu-id="4d376-474">For more information on adding high DPI support and dynamic DPI support to your Windows Forms application, see [High DPI Support in Windows Forms](/dotnet/desktop/winforms/high-dpi-support-in-windows-forms).</span></span>

<a name="WPF47"></a>

#### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="4d376-475">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-475">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="4d376-476">在 .NET Framework 4.7 中，WPF 新增了以下增强功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-476">In .NET Framework 4.7, WPF includes the following enhancements:</span></span>

<span data-ttu-id="4d376-477">**支持基于 Windows WM_POINTER 消息的触控/触笔堆栈**</span><span class="sxs-lookup"><span data-stu-id="4d376-477">**Support for a touch/stylus stack based on Windows WM_POINTER messages**</span></span>

<span data-ttu-id="4d376-478">现在可以视情况使用基于 [WM_POINTER 消息](/previous-versions/windows/desktop/InputMsg/messages)的触控/触笔堆栈，而不使用 Windows Ink 服务平台 (WISP)。</span><span class="sxs-lookup"><span data-stu-id="4d376-478">You now have the option of using a touch/stylus stack based on [WM_POINTER messages](/previous-versions/windows/desktop/InputMsg/messages) instead of the Windows Ink Services Platform (WISP).</span></span> <span data-ttu-id="4d376-479">这是 .NET Framework 中的一项可选择启用的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-479">This is an opt-in feature in .NET Framework.</span></span> <span data-ttu-id="4d376-480">有关详细信息，请参阅[应用程序兼容性](../migration-guide/application-compatibility.md)部分。</span><span class="sxs-lookup"><span data-stu-id="4d376-480">For more information, see the [Application compatibility](../migration-guide/application-compatibility.md) section.</span></span>

<span data-ttu-id="4d376-481">**WPF 打印 API 的新实现代码**</span><span class="sxs-lookup"><span data-stu-id="4d376-481">**New implementation for WPF printing APIs**</span></span>

<span data-ttu-id="4d376-482"><xref:System.Printing.PrintQueue?displayProperty=nameWithType> 类中的 WPF 打印 API 调用 Windows [打印文档包 API](/windows/desktop/printdocs/tailored-app-printing-api)，而不调用弃用的 [XPS 打印 API](/windows/desktop/printdocs/xps-printing)。</span><span class="sxs-lookup"><span data-stu-id="4d376-482">WPF's printing APIs in the <xref:System.Printing.PrintQueue?displayProperty=nameWithType> class call the Windows [Print Document Package API](/windows/desktop/printdocs/tailored-app-printing-api) instead of the deprecated [XPS Print API](/windows/desktop/printdocs/xps-printing).</span></span> <span data-ttu-id="4d376-483">要了解此更改对应用程序兼容性的影响，请参阅[应用程序兼容性](../migration-guide/application-compatibility.md)部分。</span><span class="sxs-lookup"><span data-stu-id="4d376-483">For the impact of this change on application compatibility, see the [Application compatibility](../migration-guide/application-compatibility.md) section.</span></span>

<a name="v462"></a>

## <a name="whats-new-in-net-framework-462"></a><span data-ttu-id="4d376-484">.NET Framework 4.6.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-484">What's new in .NET Framework 4.6.2</span></span>

<span data-ttu-id="4d376-485">.NET Framework 4.6.2 在以下几个领域新增了功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-485">.NET Framework 4.6.2 includes new features in the following areas:</span></span>

- [<span data-ttu-id="4d376-486">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-486">ASP.NET</span></span>](#ASPNET462)

- [<span data-ttu-id="4d376-487">字符类别</span><span class="sxs-lookup"><span data-stu-id="4d376-487">Character categories</span></span>](#Strings)

- [<span data-ttu-id="4d376-488">加密</span><span class="sxs-lookup"><span data-stu-id="4d376-488">Cryptography</span></span>](#Crypto462)

- [<span data-ttu-id="4d376-489">SqlClient</span><span class="sxs-lookup"><span data-stu-id="4d376-489">SqlClient</span></span>](#SQLClient)

- [<span data-ttu-id="4d376-490">Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="4d376-490">Windows Communication Foundation</span></span>](#WCF)

- [<span data-ttu-id="4d376-491">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-491">Windows Presentation Foundation (WPF)</span></span>](#WPF462)

- [<span data-ttu-id="4d376-492">Windows Workflow Foundation (WF)</span><span class="sxs-lookup"><span data-stu-id="4d376-492">Windows Workflow Foundation (WF)</span></span>](#WF462)

- [<span data-ttu-id="4d376-493">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="4d376-493">ClickOnce</span></span>](#clickonce-1)

- [<span data-ttu-id="4d376-494">将 Windows 窗体和 WPF 应用转换为 UWP 应用</span><span class="sxs-lookup"><span data-stu-id="4d376-494">Converting Windows Forms and WPF apps to UWP apps</span></span>](#UWPConvert)

- [<span data-ttu-id="4d376-495">调试改进</span><span class="sxs-lookup"><span data-stu-id="4d376-495">Debugging improvements</span></span>](#Debug462)

<span data-ttu-id="4d376-496">有关 .NET Framework 4.6.2 中新增 API 的列表，请参阅 GitHub 上的 [.NET Framework 4.6.2 API 更改](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-496">For a list of new APIs added to .NET Framework 4.6.2, see [.NET Framework 4.6.2 API Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) on GitHub.</span></span> <span data-ttu-id="4d376-497">有关 .NET Framework 4.6.2 中功能改进和 bug 修复的列表，请参阅 GitHub 上的 [.NET Framework 4.6.2 更改列表](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-497">For a list of feature improvements and bug fixes in .NET Framework 4.6.2, see [.NET Framework 4.6.2 List of Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-changes.md) on GitHub.</span></span> <span data-ttu-id="4d376-498">有关详细信息，请参阅 .NET 博客中的 [Announcing the .NET Framework 4.6.2](https://devblogs.microsoft.com/dotnet/announcing-net-framework-4-6-2/)（发布 .NET Framework 4.6.2）。</span><span class="sxs-lookup"><span data-stu-id="4d376-498">For more information, see [Announcing .NET Framework 4.6.2](https://devblogs.microsoft.com/dotnet/announcing-net-framework-4-6-2/) in the .NET blog.</span></span>

<a name="ASPNET462"></a>

### <a name="aspnet"></a><span data-ttu-id="4d376-499">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-499">ASP.NET</span></span>

<span data-ttu-id="4d376-500">在 .NET Framework 4.6.2 中，ASP.NET 包括以下增强功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-500">In  .NET Framework 4.6.2, ASP.NET includes the following enhancements:</span></span>

<span data-ttu-id="4d376-501">**改进了对数据注释验证程序中本地化错误消息的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-501">**Improved support for localized error messages in data annotation validators**</span></span>

<span data-ttu-id="4d376-502">数据批注验证程序使你能够通过将一个或多个属性添加到类属性来执行验证。</span><span class="sxs-lookup"><span data-stu-id="4d376-502">Data annotation validators enable you to perform validation by adding one or more attributes to a class property.</span></span> <span data-ttu-id="4d376-503">如果验证失败，该属性的 <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> 元素定义错误消息的文本。</span><span class="sxs-lookup"><span data-stu-id="4d376-503">The attribute's <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> element defines the text of the error message if validation fails.</span></span> <span data-ttu-id="4d376-504">自 .NET Framework 4.6.2 起，ASP.NET 简化了错误消息的本地化。</span><span class="sxs-lookup"><span data-stu-id="4d376-504">Starting with .NET Framework 4.6.2, ASP.NET makes it easy to localize error messages.</span></span> <span data-ttu-id="4d376-505">如果有以下情况，将本地化错误消息：</span><span class="sxs-lookup"><span data-stu-id="4d376-505">Error messages will be localized if:</span></span>

1. <span data-ttu-id="4d376-506">验证属性中提供 <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="4d376-506">The <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> is provided in the validation attribute.</span></span>

2. <span data-ttu-id="4d376-507">资源文件存储在 App_LocalResources 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4d376-507">The resource file is stored in the App_LocalResources folder.</span></span>

3. <span data-ttu-id="4d376-508">本地化资源文件名称的格式为 `DataAnnotation.Localization.{`*name*`}.resx`，其中 *name* 是采用 *languageCode*`-`*country/regionCode* 或 *languageCode* 格式的区域性名称。</span><span class="sxs-lookup"><span data-stu-id="4d376-508">The name of the localized resources file has the form `DataAnnotation.Localization.{`*name*`}.resx`, where *name* is a culture name in the format *languageCode*`-`*country/regionCode* or *languageCode* .</span></span>

4. <span data-ttu-id="4d376-509">该资源的项名称是分配给 <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> 属性的字符串，其值是本地化的错误消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-509">The key name of the resource is the string assigned to the <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> attribute,  and its value is the localized error message.</span></span>

<span data-ttu-id="4d376-510">例如，以下数据注释属性定义无效分级的默认区域性错误消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-510">For example, the following data annotation attribute defines the default culture's error message for an invalid rating.</span></span>

```csharp
public class RatingInfo
{
   [Required(ErrorMessage = "The rating must be between 1 and 10.")]
   [Display(Name = "Your Rating")]
   public int Rating { get; set; }
}
```

```vb
Public Class RatingInfo
   <Required(ErrorMessage = "The rating must be between 1 and 10.")>
   <Display(Name = "Your Rating")>
   Public Property Rating As Integer = 1
End Class
```

<span data-ttu-id="4d376-511">然后可以创建一个资源文件 DataAnnotation.Localization.fr.resx，它的键为错误消息字符串，值为本地化的错误消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-511">You can then create a resource file, DataAnnotation.Localization.fr.resx, whose key is the error message string and whose value is the localized error message.</span></span> <span data-ttu-id="4d376-512">该文件必须位于 `App.LocalResources` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4d376-512">The file must be found in the `App.LocalResources` folder.</span></span> <span data-ttu-id="4d376-513">例如，下面列出了键以及它在本地化法语 (fr) 错误消息中的值：</span><span class="sxs-lookup"><span data-stu-id="4d376-513">For example, the following is the key and its value in a localized French (fr) language error message:</span></span>

| <span data-ttu-id="4d376-514">“属性”</span><span class="sxs-lookup"><span data-stu-id="4d376-514">Name</span></span>                                 | <span data-ttu-id="4d376-515">“值”</span><span class="sxs-lookup"><span data-stu-id="4d376-515">Value</span></span>                                     |
| ------------------------------------ | ----------------------------------------- |
| <span data-ttu-id="4d376-516">分级必须介于 1 和 10 之间。</span><span class="sxs-lookup"><span data-stu-id="4d376-516">The rating must be between 1 and 10.</span></span> | <span data-ttu-id="4d376-517">La note doit être comprise entre 1 et 10.</span><span class="sxs-lookup"><span data-stu-id="4d376-517">La note doit être comprise entre 1 et 10.</span></span> |

 <span data-ttu-id="4d376-518">此外，数据批注本地化可扩展。</span><span class="sxs-lookup"><span data-stu-id="4d376-518">In addition, data annotation localization is extensible.</span></span> <span data-ttu-id="4d376-519">开发人员可以通过实现 <xref:System.Web.Globalization.IStringLocalizerProvider> 接口插入自己的字符串本地化工具提供程序，以将本地化字符串存储在资源文件以外的某个位置。</span><span class="sxs-lookup"><span data-stu-id="4d376-519">Developers can plug in their own string localizer provider by implementing the <xref:System.Web.Globalization.IStringLocalizerProvider> interface to store localization string somewhere other than in a resource file.</span></span>

 <span data-ttu-id="4d376-520">**会话状态存储提供程序的异步支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-520">**Async support with session-state store providers**</span></span>

 <span data-ttu-id="4d376-521">ASP.NET 现允许将返回任务的方法与会话状态存储提供程序一起使用，从而允许 ASP.NET 应用获取异步的可伸缩性优势。</span><span class="sxs-lookup"><span data-stu-id="4d376-521">ASP.NET now allows task-returning methods to be used with session-state store providers, thereby allowing ASP.NET apps to get the scalability benefits of async.</span></span> <span data-ttu-id="4d376-522">要使用会话状态存储提供程序支持异步操作，ASP.NET 包括一个新的接口 <xref:System.Web.SessionState.ISessionStateModule?displayProperty=nameWithType>，它继承自 <xref:System.Web.IHttpModule> 并允许开发人员实现其自己的会话状态模块和异步会话存储提供程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-522">To supports asynchronous operations with session state store providers, ASP.NET includes  a new interface, <xref:System.Web.SessionState.ISessionStateModule?displayProperty=nameWithType>, which inherits from <xref:System.Web.IHttpModule> and allows developers to implement their own session-state module and async session store providers.</span></span> <span data-ttu-id="4d376-523">接口定义如下：</span><span class="sxs-lookup"><span data-stu-id="4d376-523">The interface is defined as follows:</span></span>

```csharp
public interface ISessionStateModule : IHttpModule {
    void ReleaseSessionState(HttpContext context);
    Task ReleaseSessionStateAsync(HttpContext context);
}
```

```vb
Public Interface ISessionStateModule : Inherits IHttpModule
   Sub ReleaseSessionState(context As HttpContext)
   Function ReleaseSessionStateAsync(context As HttpContext) As Task
End Interface
```

 <span data-ttu-id="4d376-524">此外，<xref:System.Web.SessionState.SessionStateUtility> 类包括两种新方法：<xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> 和 <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>，可用来支持异步操作。</span><span class="sxs-lookup"><span data-stu-id="4d376-524">In addition, the <xref:System.Web.SessionState.SessionStateUtility> class includes two new methods, <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> and <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>, that can be used to support asynchronous operations.</span></span>

 <span data-ttu-id="4d376-525">**对输出缓存提供程序的异步支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-525">**Async support for output-cache providers**</span></span>

 <span data-ttu-id="4d376-526">自 .NET Framework 4.6.2 起，返回任务的方法可与输出缓存提供程序结合使用，从而实现异步的可伸缩性优势。</span><span class="sxs-lookup"><span data-stu-id="4d376-526">Starting with .NET Framework 4.6.2, task-returning methods can be used with output-cache providers to provide the scalability benefits of async.</span></span>  <span data-ttu-id="4d376-527">实现这些方法的提供程序减少了 Web 服务器上的线程阻止，并提高 ASP.NET 服务的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="4d376-527">Providers that implement these methods reduce thread-blocking on a web server and improve the scalability of an ASP.NET service.</span></span>

 <span data-ttu-id="4d376-528">添加了以下 API 以支持异步输出缓存提供程序：</span><span class="sxs-lookup"><span data-stu-id="4d376-528">The following APIs have been added to support asynchronous output-cache providers:</span></span>

- <span data-ttu-id="4d376-529"><xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=nameWithType> 类，它继承自 <xref:System.Web.Caching.OutputCacheProvider?displayProperty=nameWithType>，并允许开发人员实现异步输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-529">The <xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=nameWithType> class, which inherits from <xref:System.Web.Caching.OutputCacheProvider?displayProperty=nameWithType> and allows developers to implement an asynchronous output-cache provider.</span></span>

- <span data-ttu-id="4d376-530"><xref:System.Web.Caching.OutputCacheUtility> 类，该类提供用于配置输出缓存的 Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-530">The <xref:System.Web.Caching.OutputCacheUtility> class, which provides helper methods for configuring the output cache.</span></span>

- <span data-ttu-id="4d376-531"><xref:System.Web.HttpCachePolicy?displayProperty=nameWithType> 类中的 18 种新方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-531">18 new methods in the <xref:System.Web.HttpCachePolicy?displayProperty=nameWithType> class.</span></span> <span data-ttu-id="4d376-532">它们包括 <xref:System.Web.HttpCachePolicy.GetCacheability%2A>、<xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>、<xref:System.Web.HttpCachePolicy.GetETag%2A>、<xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>、<xref:System.Web.HttpCachePolicy.GetMaxAge%2A>、<xref:System.Web.HttpCachePolicy.GetMaxAge%2A>、<xref:System.Web.HttpCachePolicy.GetNoStore%2A>、<xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>、<xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>、<xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>、<xref:System.Web.HttpCachePolicy.GetRevalidation%2A>、<xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>、<xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>、<xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A> 和 <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>。</span><span class="sxs-lookup"><span data-stu-id="4d376-532">These include <xref:System.Web.HttpCachePolicy.GetCacheability%2A>, <xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>, <xref:System.Web.HttpCachePolicy.GetETag%2A>, <xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetNoStore%2A>, <xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>, <xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>, <xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetRevalidation%2A>, <xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>, <xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>, <xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A>, and <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>.</span></span>

- <span data-ttu-id="4d376-533"><xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=nameWithType> 类中的两种新方法：<xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> 和 <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>。</span><span class="sxs-lookup"><span data-stu-id="4d376-533">2 new methods in the <xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=nameWithType> class:  <xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> and <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>.</span></span>

- <span data-ttu-id="4d376-534"><xref:System.Web.HttpCacheVaryByHeaders?displayProperty=nameWithType> 类中的两种新方法：<xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> 和 <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>。</span><span class="sxs-lookup"><span data-stu-id="4d376-534">2 new methods in the <xref:System.Web.HttpCacheVaryByHeaders?displayProperty=nameWithType> class: <xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> and <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>.</span></span>

- <span data-ttu-id="4d376-535"><xref:System.Web.HttpCacheVaryByParams?displayProperty=nameWithType> 类中的两种新方法：<xref:System.Web.HttpCacheVaryByParams.GetParams%2A> 和 <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>。</span><span class="sxs-lookup"><span data-stu-id="4d376-535">2 new methods in the <xref:System.Web.HttpCacheVaryByParams?displayProperty=nameWithType> class: <xref:System.Web.HttpCacheVaryByParams.GetParams%2A> and <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>.</span></span>

- <span data-ttu-id="4d376-536"><xref:System.Web.Caching.AggregateCacheDependency?displayProperty=nameWithType> 类中的 <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-536">In the <xref:System.Web.Caching.AggregateCacheDependency?displayProperty=nameWithType> class, the <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A> method.</span></span>

- <span data-ttu-id="4d376-537"><xref:System.Web.Caching.CacheDependency> 中的 <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-537">In the <xref:System.Web.Caching.CacheDependency>, the <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A> method.</span></span>

<a name="Strings"></a>

### <a name="character-categories"></a><span data-ttu-id="4d376-538">字符类别</span><span class="sxs-lookup"><span data-stu-id="4d376-538">Character categories</span></span>

<span data-ttu-id="4d376-539">.NET Framework 4.6.2 中的字符是根据 [Unicode 标准 8.0.0 版](https://www.unicode.org/versions/Unicode8.0.0/)进行分类的。</span><span class="sxs-lookup"><span data-stu-id="4d376-539">Characters in .NET Framework 4.6.2 are classified based on the [Unicode Standard, Version 8.0.0](https://www.unicode.org/versions/Unicode8.0.0/).</span></span> <span data-ttu-id="4d376-540">在 .NET Framework 4.6 和 .NET Framework 4.6.1 中，字符是根据 Unicode 6.3 字符类别进行分类。</span><span class="sxs-lookup"><span data-stu-id="4d376-540">In .NET Framework 4.6 and .NET Framework 4.6.1, characters were classified based on Unicode 6.3 character categories.</span></span>

<span data-ttu-id="4d376-541">对 Unicode 8.0 的支持限于 <xref:System.Globalization.CharUnicodeInfo> 类的字符分类以及依赖它的类型和方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-541">Support for Unicode 8.0 is limited to the classification of characters by the <xref:System.Globalization.CharUnicodeInfo> class and to types and methods that rely on it.</span></span> <span data-ttu-id="4d376-542">其中包括 <xref:System.Globalization.StringInfo> 类、重载的 <xref:System.Char.GetUnicodeCategory%2A?displayProperty=nameWithType> 方法和 .NET Framework 正则表达式引擎识别的[字符类](../../standard/base-types/character-classes-in-regular-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-542">These include the <xref:System.Globalization.StringInfo> class, the overloaded <xref:System.Char.GetUnicodeCategory%2A?displayProperty=nameWithType> method, and the [character classes](../../standard/base-types/character-classes-in-regular-expressions.md) recognized by the .NET Framework regular expression engine.</span></span>  <span data-ttu-id="4d376-543">字符及字符串的比较和排序不受此更改影响，仍依赖于基础操作系统，或 Windows 7 系统、.NET Framework 提供的字符数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-543">Character and string comparison and sorting is unaffected by this change and continues to rely on the underlying operating system or, on Windows 7 systems, on character data provided by .NET Framework.</span></span>

<span data-ttu-id="4d376-544">有关从 Unicode 6.0 到 Unicode 7.0 的字符类别的更改，请参阅 Unicode Consortium 网站上的 [Unicode 标准 7.0.0 版](https://www.unicode.org/versions/Unicode7.0.0/)。</span><span class="sxs-lookup"><span data-stu-id="4d376-544">For changes in character categories from Unicode 6.0 to Unicode 7.0, see [The Unicode Standard, Version 7.0.0](https://www.unicode.org/versions/Unicode7.0.0/) at The Unicode Consortium website.</span></span> <span data-ttu-id="4d376-545">有关从 Unicode 7.0 到 Unicode 8.0 的更改，请参阅 Unicode Consortium 网站上的 [Unicode 标准 8.0.0 版](https://www.unicode.org/versions/Unicode8.0.0/)。</span><span class="sxs-lookup"><span data-stu-id="4d376-545">For changes from Unicode 7.0 to Unicode 8.0, see [The Unicode Standard, Version 8.0.0](https://www.unicode.org/versions/Unicode8.0.0/) at The Unicode Consortium website.</span></span>

<a name="Crypto462"></a>

### <a name="cryptography"></a><span data-ttu-id="4d376-546">密码</span><span class="sxs-lookup"><span data-stu-id="4d376-546">Cryptography</span></span>

<span data-ttu-id="4d376-547">**对包含 FIPS 186-3 DSA 的 X509 证书的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-547">**Support for X509 certificates containing FIPS 186-3 DSA**</span></span>

<span data-ttu-id="4d376-548">.NET Framework 4.6.2 现已开始支持密钥超过 FIPS 186-2 1024 位限制的 DSA（数字签名算法）X509 证书。</span><span class="sxs-lookup"><span data-stu-id="4d376-548">.NET Framework 4.6.2 adds support for DSA (Digital Signature Algorithm) X509 certificates whose keys exceed the FIPS 186-2 1024-bit limit.</span></span>

<span data-ttu-id="4d376-549">除了支持更大的 FIPS 186-3 密钥大小之外，.NET Framework 4.6.2 还支持使用 SHA-2 系列的哈希算法（SHA256、SHA384 和 SHA512）计算签名。</span><span class="sxs-lookup"><span data-stu-id="4d376-549">In addition to supporting the larger key sizes of FIPS 186-3, .NET Framework 4.6.2 allows computing signatures with the SHA-2 family of hash algorithms (SHA256, SHA384, and SHA512).</span></span> <span data-ttu-id="4d376-550">FIPS 186-3 支持由新的 <xref:System.Security.Cryptography.DSACng?displayProperty=nameWithType> 类提供。</span><span class="sxs-lookup"><span data-stu-id="4d376-550">FIPS 186-3 support is provided by the new <xref:System.Security.Cryptography.DSACng?displayProperty=nameWithType> class.</span></span>

<span data-ttu-id="4d376-551">为了跟进 .NET Framework 4.6 中的 <xref:System.Security.Cryptography.RSA> 类和 .NET Framework 4.6.1 中的 <xref:System.Security.Cryptography.ECDsa> 类的最新更改，.NET Framework 4.6.2 中的 <xref:System.Security.Cryptography.DSA> 抽象基类有附加方法允许调用方在无需强制转换即可使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-551">In keeping with recent changes to the <xref:System.Security.Cryptography.RSA> class in .NET Framework 4.6 and the <xref:System.Security.Cryptography.ECDsa> class in .NET Framework 4.6.1, the <xref:System.Security.Cryptography.DSA> abstract base class in .NET Framework 4.6.2 has additional methods to allow callers to use this functionality without casting.</span></span> <span data-ttu-id="4d376-552">可以调用 <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=nameWithType> 扩展方法对数据进行签名，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="4d376-552">You can call the <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=nameWithType> extension method to sign data, as the following example shows.</span></span>

```csharp
public static byte[] SignDataDsaSha384(byte[] data, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPrivateKey())
    {
        return dsa.SignData(data, HashAlgorithmName.SHA384);
    }
}
```

```vb
Public Shared Function SignDataDsaSha384(data As Byte(), cert As X509Certificate2) As Byte()
    Using DSA As DSA = cert.GetDSAPrivateKey()
        Return DSA.SignData(data, HashAlgorithmName.SHA384)
    End Using
End Function
```

<span data-ttu-id="4d376-553">并且可以调用 <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=nameWithType> 扩展方法验证已签名的数据，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="4d376-553">And you can call the <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=nameWithType> extension method to verify signed data, as the following example shows.</span></span>

```csharp
public static bool VerifyDataDsaSha384(byte[] data, byte[] signature, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPublicKey())
    {
        return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384);
    }
}
```

```vb
 Public Shared Function VerifyDataDsaSha384(data As Byte(), signature As Byte(), cert As X509Certificate2) As Boolean
    Using dsa As DSA = cert.GetDSAPublicKey()
        Return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384)
    End Using
End Function
```

<span data-ttu-id="4d376-554">**提高了 ECDiffieHellman 密钥派生例程的输入的清晰度**</span><span class="sxs-lookup"><span data-stu-id="4d376-554">**Increased clarity for inputs to ECDiffieHellman key derivation routines**</span></span>

<span data-ttu-id="4d376-555">.NET Framework 3.5 通过三个不同的密钥派生功能 (KDF) 例程增加了对椭圆曲线 Diffie-Hellman 密钥协议的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-555">.NET Framework 3.5 added support for Elliptic Curve Diffie-Hellman Key Agreement with three different Key Derivation Function (KDF) routines.</span></span> <span data-ttu-id="4d376-556">例程的输入以及这些例程本身通过 <xref:System.Security.Cryptography.ECDiffieHellmanCng> 对象上的属性进行配置。</span><span class="sxs-lookup"><span data-stu-id="4d376-556">The inputs to the routines, and the routines themselves, were configured via properties on the <xref:System.Security.Cryptography.ECDiffieHellmanCng> object.</span></span> <span data-ttu-id="4d376-557">但由于不是每个例程都会读取每个输入属性，因此过去很有可能对开发人员造成了困扰。</span><span class="sxs-lookup"><span data-stu-id="4d376-557">But since not every routine read every input property, there was ample room for confusion on the past of the developer.</span></span>

<span data-ttu-id="4d376-558">为了在 .NET Framework 4.6.2 中解决这一问题，已向 <xref:System.Security.Cryptography.ECDiffieHellman> 基类添加以下三种方法，以便更明确地表示这些 KDF 例程及其输入：</span><span class="sxs-lookup"><span data-stu-id="4d376-558">To address this in .NET Framework 4.6.2, the following three methods have been added to the  <xref:System.Security.Cryptography.ECDiffieHellman> base class to more clearly represent these KDF routines and their inputs:</span></span>

|<span data-ttu-id="4d376-559">ECDiffieHellman 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-559">ECDiffieHellman method</span></span>|<span data-ttu-id="4d376-560">描述</span><span class="sxs-lookup"><span data-stu-id="4d376-560">Description</span></span>|
|----------------------------|-----------------|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHash%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|<span data-ttu-id="4d376-561">使用下面的公式派生密钥材料</span><span class="sxs-lookup"><span data-stu-id="4d376-561">Derives key material using the formula</span></span><br /><br /> <span data-ttu-id="4d376-562">HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span><span class="sxs-lookup"><span data-stu-id="4d376-562">HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span></span><br /><br /> <span data-ttu-id="4d376-563">HASH(secretPrepend OrElse *x* OrElse secretAppend)</span><span class="sxs-lookup"><span data-stu-id="4d376-563">HASH(secretPrepend OrElse *x* OrElse secretAppend)</span></span><br /><br /> <span data-ttu-id="4d376-564">其中 *x* 是 EC Diffie-Hellman 算法的计算结果。</span><span class="sxs-lookup"><span data-stu-id="4d376-564">where *x* is the computed result of the EC Diffie-Hellman algorithm.</span></span>|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHmac%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|<span data-ttu-id="4d376-565">使用下面的公式派生密钥材料</span><span class="sxs-lookup"><span data-stu-id="4d376-565">Derives key material using the formula</span></span><br /><br /> <span data-ttu-id="4d376-566">HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span><span class="sxs-lookup"><span data-stu-id="4d376-566">HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)</span></span><br /><br /> <span data-ttu-id="4d376-567">HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)</span><span class="sxs-lookup"><span data-stu-id="4d376-567">HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)</span></span><br /><br /> <span data-ttu-id="4d376-568">其中 *x* 是 EC Diffie-Hellman 算法的计算结果。</span><span class="sxs-lookup"><span data-stu-id="4d376-568">where *x* is the computed result of the EC Diffie-Hellman algorithm.</span></span>|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyTls%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|<span data-ttu-id="4d376-569">使用 TLS 伪随机函数 (PRF) 派生算法派生密钥材料。</span><span class="sxs-lookup"><span data-stu-id="4d376-569">Derives key material using the TLS pseudo-random function (PRF) derivation algorithm.</span></span>|

<span data-ttu-id="4d376-570">**对持久化密钥对称加密的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-570">**Support for persisted-key symmetric encryption**</span></span>

<span data-ttu-id="4d376-571">Windows 加密库 (CNG) 现已开始支持存储持久化对称密钥和使用硬件存储的对称密钥。开发者可通过 .NET Framework 4.6.2 使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-571">The Windows cryptography library (CNG) added support for storing persisted symmetric keys and using hardware-stored symmetric keys, and .NET Framework 4.6.2 made it possible for developers to make use of this feature.</span></span>  <span data-ttu-id="4d376-572">因为密钥名和密钥提供程序的概念是特定于实现的，所以使用此功能要求使用具体实现类型（而不是首选出厂方法）的构造函数（例如，调用 `Aes.Create`）。</span><span class="sxs-lookup"><span data-stu-id="4d376-572">Since the notion of key names and key providers is implementation-specific, using this feature requires utilizing the constructor of the concrete implementation types instead of the preferred factory approach (such as calling `Aes.Create`).</span></span>

<span data-ttu-id="4d376-573">持久化密钥对称加密支持因 AES (<xref:System.Security.Cryptography.AesCng>) 和 3DES (<xref:System.Security.Cryptography.TripleDESCng>) 算法存在。</span><span class="sxs-lookup"><span data-stu-id="4d376-573">Persisted-key symmetric encryption support exists for the AES (<xref:System.Security.Cryptography.AesCng>) and 3DES (<xref:System.Security.Cryptography.TripleDESCng>) algorithms.</span></span> <span data-ttu-id="4d376-574">例如：</span><span class="sxs-lookup"><span data-stu-id="4d376-574">For example:</span></span>

```csharp
public static byte[] EncryptDataWithPersistedKey(byte[] data, byte[] iv)
{
    using (Aes aes = new AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider))
    {
        aes.IV = iv;

        // Using the zero-argument overload is required to make use of the persisted key
        using (ICryptoTransform encryptor = aes.CreateEncryptor())
        {
            if (!encryptor.CanTransformMultipleBlocks)
            {
                throw new InvalidOperationException("This is a sample, this case wasn't handled...");
            }

            return encryptor.TransformFinalBlock(data, 0, data.Length);
        }
    }
}
```

```vb
Public Shared Function EncryptDataWithPersistedKey(data As Byte(), iv As Byte()) As Byte()
    Using Aes As Aes = New AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider)
        Aes.IV = iv

        ' Using the zero-argument overload Is required to make use of the persisted key
        Using encryptor As ICryptoTransform = Aes.CreateEncryptor()
            If Not encryptor.CanTransformMultipleBlocks Then
                Throw New InvalidOperationException("This is a sample, this case wasn't handled...")
            End If
            Return encryptor.TransformFinalBlock(data, 0, data.Length)
        End Using
    End Using
End Function
```

<span data-ttu-id="4d376-575">**对 SHA-2 哈希的 SignedXml 支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-575">**SignedXml support for SHA-2 hashing**</span></span>

<span data-ttu-id="4d376-576">.NET Framework 4.6.2 中的 <xref:System.Security.Cryptography.Xml.SignedXml> 类现已开始支持 RSA-SHA256、RSA-SHA384 和 RSA-SHA512 PKCS#1 签名方法，还支持 SHA256、SHA384 和 SHA512 引用摘要算法。</span><span class="sxs-lookup"><span data-stu-id="4d376-576">.NET Framework 4.6.2 adds support to  the <xref:System.Security.Cryptography.Xml.SignedXml> class for RSA-SHA256, RSA-SHA384, and RSA-SHA512 PKCS#1 signature methods, and SHA256, SHA384, and SHA512 reference digest algorithms.</span></span>

<span data-ttu-id="4d376-577">URI 常量都在 <xref:System.Security.Cryptography.Xml.SignedXml> 上公开：</span><span class="sxs-lookup"><span data-stu-id="4d376-577">The URI constants are all exposed on <xref:System.Security.Cryptography.Xml.SignedXml>:</span></span>

|<span data-ttu-id="4d376-578">SignedXml 字段</span><span class="sxs-lookup"><span data-stu-id="4d376-578">SignedXml field</span></span>|<span data-ttu-id="4d376-579">返回的常量</span><span class="sxs-lookup"><span data-stu-id="4d376-579">Constant</span></span>|
|---------------------|--------------|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA256Url>|<span data-ttu-id="4d376-580">"http://www.w3.org/2001/04/xmlenc#sha256"</span><span class="sxs-lookup"><span data-stu-id="4d376-580">"http://www.w3.org/2001/04/xmlenc#sha256"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA256Url>|<span data-ttu-id="4d376-581">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"</span><span class="sxs-lookup"><span data-stu-id="4d376-581">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA384Url>|<span data-ttu-id="4d376-582">"http://www.w3.org/2001/04/xmldsig-more#sha384"</span><span class="sxs-lookup"><span data-stu-id="4d376-582">"http://www.w3.org/2001/04/xmldsig-more#sha384"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA384Url>|<span data-ttu-id="4d376-583">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"</span><span class="sxs-lookup"><span data-stu-id="4d376-583">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA512Url>|<span data-ttu-id="4d376-584">"http://www.w3.org/2001/04/xmlenc#sha512"</span><span class="sxs-lookup"><span data-stu-id="4d376-584">"http://www.w3.org/2001/04/xmlenc#sha512"</span></span>|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA512Url>|<span data-ttu-id="4d376-585">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"</span><span class="sxs-lookup"><span data-stu-id="4d376-585">"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"</span></span>|

 <span data-ttu-id="4d376-586">已将自定义 <xref:System.Security.Cryptography.SignatureDescription> 处理程序注册到 <xref:System.Security.Cryptography.CryptoConfig> 以添加对这些算法的支持的任何程序将会继续像过去一样工作，但由于现在有平台默认值，所以不再需要 <xref:System.Security.Cryptography.CryptoConfig> 注册。</span><span class="sxs-lookup"><span data-stu-id="4d376-586">Any programs that have registered a custom <xref:System.Security.Cryptography.SignatureDescription> handler into <xref:System.Security.Cryptography.CryptoConfig> to add support for these algorithms will continue to function as they did in the past, but since there are now platform defaults, the <xref:System.Security.Cryptography.CryptoConfig> registration is no longer necessary.</span></span>

<a name="SQLClient"></a>

### <a name="sqlclient"></a><span data-ttu-id="4d376-587">SqlClient</span><span class="sxs-lookup"><span data-stu-id="4d376-587">SqlClient</span></span>

<span data-ttu-id="4d376-588">SQL Server 的 .NET framework 数据提供程序 (<xref:System.Data.SqlClient?displayProperty=nameWithType>) 包括 .NET Framework 4.6.2 中的以下新功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-588">.NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient?displayProperty=nameWithType>) includes the following new features in .NET Framework 4.6.2:</span></span>

<span data-ttu-id="4d376-589">**Azure SQL 数据库的连接池和超时**</span><span class="sxs-lookup"><span data-stu-id="4d376-589">**Connection pooling and timeouts with Azure SQL databases**</span></span>

<span data-ttu-id="4d376-590">启用连接池并出现超时或其他登录错误后，会缓存一个异常，并会在接下来的 5 秒到 1 分钟内尝试任何后续连接时引发缓存的异常。</span><span class="sxs-lookup"><span data-stu-id="4d376-590">When connection pooling is enabled and a timeout or other login error occurs, an exception is cached, and the cached exception is thrown on any subsequent connection attempt for the next 5 seconds to 1 minute.</span></span> <span data-ttu-id="4d376-591">有关详细信息，请参阅 [SQL Server 连接池 (ADO.NET)](../data/adonet/sql-server-connection-pooling.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-591">For more information, see [SQL Server Connection Pooling (ADO.NET)](../data/adonet/sql-server-connection-pooling.md).</span></span>

<span data-ttu-id="4d376-592">连接到 Azure SQL 数据库时此行为是不可取的，因为连接尝试可能会失败，出现通常会快速恢复的暂时性错误。</span><span class="sxs-lookup"><span data-stu-id="4d376-592">This behavior is not desirable when connecting to Azure SQL Databases, since connection attempts can fail with transient errors that are typically recovered quickly.</span></span> <span data-ttu-id="4d376-593">为更好地优化连接重试体验，会在与 Azure SQL 数据库连接失败时删除连接池阻塞期行为。</span><span class="sxs-lookup"><span data-stu-id="4d376-593">To better optimize the connection retry experience, the connection pool blocking period behavior is removed when connections to Azure SQL Databases fail.</span></span>

<span data-ttu-id="4d376-594">新 `PoolBlockingPeriod` 关键字的添加使你能够选择最适合你的应用的阻塞期。</span><span class="sxs-lookup"><span data-stu-id="4d376-594">The addition of the new `PoolBlockingPeriod` keyword lets you select the blocking period best suited for your app.</span></span> <span data-ttu-id="4d376-595">值包括：</span><span class="sxs-lookup"><span data-stu-id="4d376-595">Values include:</span></span>

<xref:System.Data.SqlClient.PoolBlockingPeriod.Auto>

<span data-ttu-id="4d376-596">已禁用连接到 Azure SQL 数据库的应用程序的连接池阻塞期，已启用连接到任何其他 SQL Server 实例的应用程序的连接池阻塞期。</span><span class="sxs-lookup"><span data-stu-id="4d376-596">The connection pool blocking period for an application that connects to an Azure SQL Database is disabled, and the connection pool blocking period for an application that connects to any other SQL Server instance is enabled.</span></span> <span data-ttu-id="4d376-597">这是默认值。</span><span class="sxs-lookup"><span data-stu-id="4d376-597">This is the default value.</span></span> <span data-ttu-id="4d376-598">如果 Server 终结点名称采用以下任一结尾，则将它们视为 Azure SQL 数据库：</span><span class="sxs-lookup"><span data-stu-id="4d376-598">If the Server endpoint name ends with any of the following, they are considered Azure SQL Databases:</span></span>

- <span data-ttu-id="4d376-599">.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="4d376-599">.database.windows.net</span></span>

- <span data-ttu-id="4d376-600">.database.chinacloudapi.cn</span><span class="sxs-lookup"><span data-stu-id="4d376-600">.database.chinacloudapi.cn</span></span>

- <span data-ttu-id="4d376-601">.database.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="4d376-601">.database.usgovcloudapi.net</span></span>

- <span data-ttu-id="4d376-602">.database.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="4d376-602">.database.cloudapi.de</span></span>

<xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock>

<span data-ttu-id="4d376-603">连接池阻塞期始终处于启用状态。</span><span class="sxs-lookup"><span data-stu-id="4d376-603">The connection pool blocking period is always enabled.</span></span>

<xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock>

<span data-ttu-id="4d376-604">连接池阻塞期始终处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="4d376-604">The connection pool blocking period is always disabled.</span></span>

<span data-ttu-id="4d376-605">**Always Encrypted 的增强功能**</span><span class="sxs-lookup"><span data-stu-id="4d376-605">**Enhancements for Always Encrypted**</span></span>

<span data-ttu-id="4d376-606">SQLClient 引入了针对 Always Encrypted 的两个增强功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-606">SQLClient introduces two enhancements for Always Encrypted:</span></span>

- <span data-ttu-id="4d376-607">为改善针对加密数据库列的参数化查询的性能，现会缓存查询参数的加密元数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-607">To improve performance of parameterized queries against encrypted database columns, encryption metadata for query parameters is now cached.</span></span> <span data-ttu-id="4d376-608">将 <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=nameWithType> 属性设置为 `true`（这是默认值）时，如果多次调用相同的查询，则客户端只从服务器检索一次参数元数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-608">With the <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=nameWithType> property set to `true` (which is the default value), if the same query is called multiple times, the client retrieves parameter metadata from the server only once.</span></span>

- <span data-ttu-id="4d376-609">密钥缓存中的列加密密钥条目现会在可配置时间间隔后被逐出，使用 <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=nameWithType> 属性设置。</span><span class="sxs-lookup"><span data-stu-id="4d376-609">Column encryption key entries in the key cache are now evicted after a configurable time interval, set using the <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=nameWithType> property.</span></span>

<a name="WCF"></a>

### <a name="windows-communication-foundation"></a><span data-ttu-id="4d376-610">Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="4d376-610">Windows Communication Foundation</span></span>

<span data-ttu-id="4d376-611">在 .NET Framework 4.6.2 中，Windows Communication Foundation 在以下几个方面进行了增强：</span><span class="sxs-lookup"><span data-stu-id="4d376-611">In .NET Framework 4.6.2, Windows Communication Foundation has been enhanced in the following areas:</span></span>

<span data-ttu-id="4d376-612">**使用 CNG 对存储的证书的 WCF 传输安全支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-612">**WCF transport security support for certificates stored using CNG**</span></span>

<span data-ttu-id="4d376-613">WCF 传输安全使用 Windows 加密库 (CNG) 支持存储的证书。</span><span class="sxs-lookup"><span data-stu-id="4d376-613">WCF transport security supports certificates stored using the Windows cryptography library (CNG).</span></span> <span data-ttu-id="4d376-614">在 .NET Framework 4.6.2 中，此支持仅限于将证书与指数长度不超过 32 位的公钥结合使用。</span><span class="sxs-lookup"><span data-stu-id="4d376-614">In .NET Framework 4.6.2, this support is limited to using certificates with a public key that has an exponent no more than 32 bits in length.</span></span> <span data-ttu-id="4d376-615">对于定位 .NET Framework 4.6.2 的应用程序，此功能默认启用。</span><span class="sxs-lookup"><span data-stu-id="4d376-615">When an application targets .NET Framework 4.6.2, this feature is on by default.</span></span>

<span data-ttu-id="4d376-616">对面向 .NET Framework 4.6.1 及更低版本，但在 .NET Framework 4.6.2 上运行的应用程序，可在 app.config 或 web.config 文件的 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 部分中添加以下代码行来启用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-616">For applications that target .NET Framework 4.6.1 and earlier but are running on .NET Framework 4.6.2, this feature can be enabled by adding the following line to the [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) section of the app.config or web.config file.</span></span>

```xml
<AppContextSwitchOverrides
    value="Switch.System.ServiceModel.DisableCngCertificates=false"
/>
```

<span data-ttu-id="4d376-617">这还可以使用代码以编程方式完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-617">This can also be done programmatically with code like the following:</span></span>

```csharp
private const string DisableCngCertificates = @"Switch.System.ServiceModel.DisableCngCertificates";
AppContext.SetSwitch(disableCngCertificates, false);
```

```vb
Const DisableCngCertificates As String = "Switch.System.ServiceModel.DisableCngCertificates"
AppContext.SetSwitch(disableCngCertificates, False)
```

<span data-ttu-id="4d376-618">**通过 DataContractJsonSerializer 类更好地支持多个夏令时调整规则**</span><span class="sxs-lookup"><span data-stu-id="4d376-618">**Better support for multiple daylight saving time adjustment rules by the DataContractJsonSerializer class**</span></span>

<span data-ttu-id="4d376-619">客户可以使用应用程序配置设置来确定 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 类是否支持一个时区的多个调整规则。</span><span class="sxs-lookup"><span data-stu-id="4d376-619">Customers can use an application configuration setting to determine whether the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> class supports multiple adjustment rules for a single time zone.</span></span> <span data-ttu-id="4d376-620">这是一项可以选择使用的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-620">This is an opt-in feature.</span></span> <span data-ttu-id="4d376-621">若要启用它，将以下设置添加到 app.config 文件中：</span><span class="sxs-lookup"><span data-stu-id="4d376-621">To enable it, add the following setting to your app.config file:</span></span>

```xml
<runtime>
     <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseTimeZoneInfo=false" />
</runtime>
```

<span data-ttu-id="4d376-622">启用此功能后，<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 对象使用 <xref:System.TimeZoneInfo> 类型（而不是 <xref:System.TimeZone> 类型）来反序列化日期和时间数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-622">When this feature is enabled, a <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> object uses the <xref:System.TimeZoneInfo> type instead of the <xref:System.TimeZone> type to deserialize date and time data.</span></span> <span data-ttu-id="4d376-623"><xref:System.TimeZoneInfo> 支持多个调整规则，这样就可以使用历史时区数据；<xref:System.TimeZone> 却不支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-623"><xref:System.TimeZoneInfo> supports multiple adjustment rules, which makes it possible to work with historic time zone data;   <xref:System.TimeZone> does not.</span></span>

<span data-ttu-id="4d376-624">若要详细了解 <xref:System.TimeZoneInfo> 结构和时区调整，请参阅[时区概述](../../standard/datetime/time-zone-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-624">For more information on the <xref:System.TimeZoneInfo> structure and time zone adjustments, see [Time Zone Overview](../../standard/datetime/time-zone-overview.md).</span></span>

<span data-ttu-id="4d376-625">**NetNamedPipeBinding 最佳匹配**</span><span class="sxs-lookup"><span data-stu-id="4d376-625">**NetNamedPipeBinding best match**</span></span>

<span data-ttu-id="4d376-626">WCF 包含可以在客户端应用程序上设置以确保它们始终连接到服务的新应用设置，该服务在与它们请求的最匹配的 URI 上进行侦听。</span><span class="sxs-lookup"><span data-stu-id="4d376-626">WCF has a new app setting that can be set on client applications to ensure they always connect to the service listening on the URI that best matches the one that they request.</span></span> <span data-ttu-id="4d376-627">将此应用设置设置为 `false`（默认值）时，客户端可以使用 <xref:System.ServiceModel.NetNamedPipeBinding> 尝试连接到服务，该服务在是所请求 URI 的子字符串的 URI 上进行侦听。</span><span class="sxs-lookup"><span data-stu-id="4d376-627">With this app setting set to `false` (the default), it is possible for clients using <xref:System.ServiceModel.NetNamedPipeBinding> to attempt to connect to a service listening on a URI that is a substring of the requested URI.</span></span>

<span data-ttu-id="4d376-628">例如，一个客户端尝试连接到在 `net.pipe://localhost/Service1` 处进行侦听的服务，但该计算机上使用管理员特权运行的另一个服务在 `net.pipe://localhost` 处进行侦听。</span><span class="sxs-lookup"><span data-stu-id="4d376-628">For example, a client tries to connect to a service listening at `net.pipe://localhost/Service1`, but a different service on that machine running with administrator privilege is listening at `net.pipe://localhost`.</span></span> <span data-ttu-id="4d376-629">将此应用设置设置为 `false` 时，客户端将尝试连接到错误的服务。</span><span class="sxs-lookup"><span data-stu-id="4d376-629">With this app setting set to `false`, the client would attempt to connect to the wrong service.</span></span> <span data-ttu-id="4d376-630">将应用设置设置为 `true` 后，客户端将始终连接到最匹配的服务。</span><span class="sxs-lookup"><span data-stu-id="4d376-630">After setting the app setting to `true`, the client will always connect to the best matching service.</span></span>

> [!NOTE]
> <span data-ttu-id="4d376-631">使用 <xref:System.ServiceModel.NetNamedPipeBinding> 的客户端基于服务的基址（如果存在）而不是完整终结点地址查找服务。</span><span class="sxs-lookup"><span data-stu-id="4d376-631">Clients using <xref:System.ServiceModel.NetNamedPipeBinding> find services based on the service's base address (if it exists) rather than the full endpoint address.</span></span> <span data-ttu-id="4d376-632">若要确保此设置始终有效，则服务应使用唯一基址。</span><span class="sxs-lookup"><span data-stu-id="4d376-632">To ensure this setting always works the service should use a unique base address.</span></span>

<span data-ttu-id="4d376-633">若要启用此更改，将以下应用设置添加到客户端应用程序的 App.config 或 Web.config 文件中：</span><span class="sxs-lookup"><span data-stu-id="4d376-633">To enable this change, add the following app setting to your client application's App.config or Web.config file:</span></span>

```xml
<configuration>
    <appSettings>
        <add key="wcf:useBestMatchNamedPipeUri" value="true" />
    </appSettings>
</configuration>
```

<span data-ttu-id="4d376-634">**SSL 3.0 不是默认协议**</span><span class="sxs-lookup"><span data-stu-id="4d376-634">**SSL 3.0 is not a default protocol**</span></span>

<span data-ttu-id="4d376-635">结合使用 NetTcp 与传输安全和证书的凭据类型时，SSL 3.0 不再是用于协商安全连接的默认协议。</span><span class="sxs-lookup"><span data-stu-id="4d376-635">When using NetTcp with transport security and a credential type of certificate, SSL 3.0 is no longer a default protocol used for negotiating a secure connection.</span></span> <span data-ttu-id="4d376-636">在大多数情况下，应该不会影响现有应用，因为 TLS 1.0 包含在 NetTcp 的协议列表中。</span><span class="sxs-lookup"><span data-stu-id="4d376-636">In most cases, there should be no impact to existing apps, because TLS 1.0 is included in the protocol list for NetTcp.</span></span> <span data-ttu-id="4d376-637">所有现有客户端应该能够至少使用 TLS 1.0 协商连接。</span><span class="sxs-lookup"><span data-stu-id="4d376-637">All existing clients should be able to negotiate a connection using at least TLS 1.0.</span></span> <span data-ttu-id="4d376-638">如果 Ssl3 必需，则使用以下配置机制之一将其添加到协商协议的列表。</span><span class="sxs-lookup"><span data-stu-id="4d376-638">If Ssl3 is required, use one of the following configuration mechanisms to add it to the list of negotiated protocols.</span></span>

- <span data-ttu-id="4d376-639"><xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=nameWithType> 属性</span><span class="sxs-lookup"><span data-stu-id="4d376-639">The <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=nameWithType> property</span></span>

- <span data-ttu-id="4d376-640"><xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> 属性</span><span class="sxs-lookup"><span data-stu-id="4d376-640">The <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> property</span></span>

- <span data-ttu-id="4d376-641">[\<netTcpBinding>](../configure-apps/file-schema/wcf/nettcpbinding.md) 部分的 [\<transport>](../configure-apps/file-schema/wcf/transport-of-nettcpbinding.md) 部分</span><span class="sxs-lookup"><span data-stu-id="4d376-641">The [\<transport>](../configure-apps/file-schema/wcf/transport-of-nettcpbinding.md) section of the [\<netTcpBinding>](../configure-apps/file-schema/wcf/nettcpbinding.md) section</span></span>

- <span data-ttu-id="4d376-642">[\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) 部分的 [\<sslStreamSecurity>](../configure-apps/file-schema/wcf/sslstreamsecurity.md) 部分</span><span class="sxs-lookup"><span data-stu-id="4d376-642">The [\<sslStreamSecurity>](../configure-apps/file-schema/wcf/sslstreamsecurity.md) section of the [\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md) section</span></span>

<a name="WPF462"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="4d376-643">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-643">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="4d376-644">在 .NET Framework 4.6.2 中，Windows Presentation Foundation 在以下几个方面进行了增强：</span><span class="sxs-lookup"><span data-stu-id="4d376-644">In .NET Framework 4.6.2, Windows Presentation Foundation has been enhanced in the following areas:</span></span>

<span data-ttu-id="4d376-645">**组排序**</span><span class="sxs-lookup"><span data-stu-id="4d376-645">**Group sorting**</span></span>

<span data-ttu-id="4d376-646">使用 <xref:System.Windows.Data.CollectionView> 对象对数据进行分组的应用程序现在可以显式声明如何对组进行排序。</span><span class="sxs-lookup"><span data-stu-id="4d376-646">An application that uses a <xref:System.Windows.Data.CollectionView> object to group data can now explicitly declare how to  sort the groups.</span></span> <span data-ttu-id="4d376-647">显式排序可解决在应用动态添加或删除组，或在它更改分组中包含的项属性的值时出现的非直观排序问题。</span><span class="sxs-lookup"><span data-stu-id="4d376-647">Explicit sorting addresses the problem of non-intuitive ordering that occurs when an app dynamically adds or removes groups, or when it changes the value of item properties involved in grouping.</span></span> <span data-ttu-id="4d376-648">它还可通过将分组属性比较从完整集合排序移动到组排序来改善组创建过程的性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-648">It can also improve the performance of the group creation process by moving comparisons of the grouping properties from the sort of the full collection to the sort of the groups.</span></span>

<span data-ttu-id="4d376-649">为支持组排序，新的 <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=nameWithType> 和 <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=nameWithType> 属性描述如何对 <xref:System.ComponentModel.GroupDescription> 对象生成的组的集合进行排序。</span><span class="sxs-lookup"><span data-stu-id="4d376-649">To support group sorting, the new <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=nameWithType> and <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=nameWithType> properties describe how to sort the collection of groups produced by the <xref:System.ComponentModel.GroupDescription> object.</span></span> <span data-ttu-id="4d376-650">这类似于同名 <xref:System.Windows.Data.ListCollectionView> 属性描述如何对数据项进行排序的方式。</span><span class="sxs-lookup"><span data-stu-id="4d376-650">This is analogous to the way the identically named <xref:System.Windows.Data.ListCollectionView> properties describe how to sort the data items.</span></span>

<span data-ttu-id="4d376-651"><xref:System.Windows.Data.PropertyGroupDescription> 类的两个新静态属性：<xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> 和 <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>，可用于最常见的情况。</span><span class="sxs-lookup"><span data-stu-id="4d376-651">Two new static properties of the <xref:System.Windows.Data.PropertyGroupDescription> class,  <xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> and <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>, can be used for the most common cases.</span></span>

<span data-ttu-id="4d376-652">例如，下面的 XAML 按年龄分组数据，按升序对年龄组排序，并按姓氏分组每个年龄组内的项。</span><span class="sxs-lookup"><span data-stu-id="4d376-652">For example, the following XAML groups data by age, sort the age groups in ascending order, and group the items within each age group by last name.</span></span>

```xaml
<GroupDescriptions>
     <PropertyGroupDescription
         PropertyName="Age"
         CustomSort=
              "{x:Static PropertyGroupDescription.CompareNamesAscending}"/>
     </PropertyGroupDescription>
</GroupDescriptions>

<SortDescriptions>
     <SortDescription PropertyName="LastName"/>
</SortDescriptions>
```

<span data-ttu-id="4d376-653">**触控键盘支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-653">**Touch keyboard support**</span></span>

<span data-ttu-id="4d376-654">在可采用文本输入的控件接收触摸输入时，通过自动调用和解除 Windows 10 中的触控键盘，可在 WPF 应用程序中启用焦点跟踪。</span><span class="sxs-lookup"><span data-stu-id="4d376-654">Touch keyboard support enables focus tracking in WPF applications by automatically invoking and dismissing the touch Keyboard in Windows 10 when the touch input is received by a control that can take textual input.</span></span>

<span data-ttu-id="4d376-655">在 .NET framework 的早期版本中，WPF 应用程序不能在不禁用 WPF 笔/触摸手势支持的情况下选择加入焦点跟踪。</span><span class="sxs-lookup"><span data-stu-id="4d376-655">In previous versions of .NET Framework, WPF applications can't opt into the focus tracking without disabling WPF pen/touch gesture support.</span></span> <span data-ttu-id="4d376-656">因此，WPF 应用程序必须选择完整的 WPF 触摸支持或依赖于 Windows 鼠标提升。</span><span class="sxs-lookup"><span data-stu-id="4d376-656">As a result, WPF applications must choose between full WPF touch support or rely on Windows mouse promotion.</span></span>

<span data-ttu-id="4d376-657">**按监视器 DPI**</span><span class="sxs-lookup"><span data-stu-id="4d376-657">**Per-monitor DPI**</span></span>

<span data-ttu-id="4d376-658">为了支持最近激增的 WPF 应用程序高 DPI 和混合 DPI 环境，.NET Framework 4.6.2 中的 WPF 启用了按监视器 DPI 感知。</span><span class="sxs-lookup"><span data-stu-id="4d376-658">To support the recent proliferation of high-DPI and hybrid-DPI environments for WPF apps, WPF in .NET Framework 4.6.2 enables per-monitor awareness.</span></span> <span data-ttu-id="4d376-659">有关如何使 WPF 应用成为按监视器 DPI 感知的详细信息，请参阅 GitHub 上的[示例和开发人员指南](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI)。</span><span class="sxs-lookup"><span data-stu-id="4d376-659">See the [samples and developer guide](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI) on GitHub for more information about how to enable your WPF app to become per-monitor DPI aware.</span></span>

<span data-ttu-id="4d376-660">在 .NET framework 的早期版本中，WPF 应用为系统 DPI 感知。</span><span class="sxs-lookup"><span data-stu-id="4d376-660">In previous versions of .NET Framework, WPF apps are system-DPI aware.</span></span> <span data-ttu-id="4d376-661">换而言之，应用程序的 UI 由操作系统相应地进行缩放，具体取决于在其上呈现应用的监视器的 DPI。</span><span class="sxs-lookup"><span data-stu-id="4d376-661">In other words, the application's UI is scaled by the OS as appropriate, depending on the DPI of the monitor on which the app is rendered.</span></span>

<span data-ttu-id="4d376-662">对于在 .NET Framework 4.6.2 下运行的应用程序，可在应用程序配置文件的 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 部分中添加配置语句，在 WPF 应用程序中禁用按监视器 DPI 更改，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-662">For apps running under .NET Framework 4.6.2, you can disable per-monitor DPI changes in WPF apps by adding a configuration statement to the [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) section of your application configuration file, as follows:</span></span>

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.Windows.DoNotScaleForDpiChanges=false"/>
</runtime>
```

<a name="WF462"></a>

### <a name="windows-workflow-foundation-wf"></a><span data-ttu-id="4d376-663">Windows Workflow Foundation (WF)</span><span class="sxs-lookup"><span data-stu-id="4d376-663">Windows Workflow Foundation (WF)</span></span>

<span data-ttu-id="4d376-664">在 .NET Framework 4.6.2 中，Windows Workflow Foundation 在以下几个方面进行了增强：</span><span class="sxs-lookup"><span data-stu-id="4d376-664">In .NET Framework 4.6.2, Windows Workflow Foundation has been enhanced in the following area:</span></span>

<span data-ttu-id="4d376-665">**在重新托管的 WF 设计器中支持 C# 表达式和 IntelliSense**</span><span class="sxs-lookup"><span data-stu-id="4d376-665">**Support for C# expressions and IntelliSense in the Rehosted WF Designer**</span></span>

<span data-ttu-id="4d376-666">自 .NET Framework 4.5 起，WF 支持在 Visual Studio 设计器和代码工作流中使用 C# 表达式。</span><span class="sxs-lookup"><span data-stu-id="4d376-666">Starting with .NET Framework 4.5, WF supports C# expressions in both the Visual Studio Designer and in code workflows.</span></span> <span data-ttu-id="4d376-667">重新托管的工作流设计器是 WF 的一项重要功能，允许工作流设计器位于 Visual Studio 外部的应用程序中（如 WPF 中）。</span><span class="sxs-lookup"><span data-stu-id="4d376-667">The Rehosted Workflow Designer is a key feature of WF that allows for the Workflow Designer to be in an application outside Visual Studio (for example, in WPF).</span></span>  <span data-ttu-id="4d376-668">Windows Workflow Foundation 提供在重新托管的工作流设计器中支持 C# 表达式和 IntelliSense 的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-668">Windows Workflow Foundation provides the ability to support C# expressions and IntelliSense in the Rehosted Workflow Designer.</span></span> <span data-ttu-id="4d376-669">有关详细信息，请参阅 [Windows Workflow Foundation 博客](/archive/blogs/workflowteam/building-c-expressions-support-and-intellisense-in-the-rehosted-workflow-designer)。</span><span class="sxs-lookup"><span data-stu-id="4d376-669">For more information, see the [Windows Workflow Foundation blog](/archive/blogs/workflowteam/building-c-expressions-support-and-intellisense-in-the-rehosted-workflow-designer).</span></span>

<span data-ttu-id="4d376-670">`Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio` 在低于 4.6.2 的 .NET Framework 版本中，客户从 Visual Studio 重新生成工作流项目时，WF 设计器 IntelliSense 会中断。</span><span class="sxs-lookup"><span data-stu-id="4d376-670">`Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio` In versions of the .NET Framework prior to 4.6.2, WF Designer IntelliSense is broken when a customer rebuilds a workflow project from Visual Studio.</span></span> <span data-ttu-id="4d376-671">虽然项目生成成功，但在设计器中找不到该工作流类型，并且来自 IntelliSense 的缺少工作流类型的警告会出现在 **错误列表** 窗口中。</span><span class="sxs-lookup"><span data-stu-id="4d376-671">While the project build is successful, the workflow types are not found on the designer, and warnings from IntelliSense for the missing workflow types appear in the **Error List** window.</span></span> <span data-ttu-id="4d376-672">.NET Framework 4.6.2 解决了这个问题，并让 IntelliSense 可供使用。</span><span class="sxs-lookup"><span data-stu-id="4d376-672">.NET Framework 4.6.2 addresses this issue and makes IntelliSense available.</span></span>

<span data-ttu-id="4d376-673">**启用了工作流跟踪的工作流 V1 应用程序现以 FIPS 模式运行**</span><span class="sxs-lookup"><span data-stu-id="4d376-673">**Workflow V1 applications with Workflow Tracking on now run under FIPS-mode**</span></span>

<span data-ttu-id="4d376-674">已启用 FIPS 兼容模式的计算机现在可以成功运行启用了工作流跟踪的工作流版本 1 样式的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-674">Machines with FIPS Compliance Mode enabled can now successfully run a workflow Version 1-style application with Workflow tracking on.</span></span> <span data-ttu-id="4d376-675">若要启用此方案，必须对 app.config 文件进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="4d376-675">To enable this scenario, you must make the following change to your app.config file:</span></span>

```xml
<add key="microsoft:WorkflowRuntime:FIPSRequired" value="true" />
```

<span data-ttu-id="4d376-676">如果未启用此方案，运行应用程序将继续生成异常，并显示消息“此实现不是 Windows 平台 FIPS 验证的加密算法的一部分”。</span><span class="sxs-lookup"><span data-stu-id="4d376-676">If this scenario is not enabled, running the application continues to generate an exception with the message, "This implementation is not part of the Windows Platform FIPS validated cryptographic algorithms."</span></span>

<span data-ttu-id="4d376-677">**结合使用动态更新和 Visual Studio 工作流设计器时的工作流改进**</span><span class="sxs-lookup"><span data-stu-id="4d376-677">**Workflow Improvements when using Dynamic Update with Visual Studio Workflow Designer**</span></span>

<span data-ttu-id="4d376-678">工作流设计器、流程图活动设计器和其他工作流活动设计器现在已成功加载并显示调用 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> 方法后已保存的工作流。</span><span class="sxs-lookup"><span data-stu-id="4d376-678">The Workflow Designer, FlowChart Activity Designer, and other Workflow Activity Designers now successfully load and display workflows that have been saved after calling  the <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d376-679">在 .NET Framework 4.6.2 之前的 .NET Framework 版本中，在 Visual Studio 中为调用 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> 后保存的工作流加载 XAML 文件可能会导致以下问题：</span><span class="sxs-lookup"><span data-stu-id="4d376-679">In versions of the .NET Framework before .NET Framework 4.6.2, loading a XAML file in Visual Studio for a workflow that has been saved after calling <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> can result in the following issues:</span></span>

- <span data-ttu-id="4d376-680">工作流设计器无法正确加载 XAML 文件（当 <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=nameWithType> 位于行末尾处时）。</span><span class="sxs-lookup"><span data-stu-id="4d376-680">The Workflow Designer can't load the XAML file correctly (when the <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=nameWithType> is at the end of the line).</span></span>

- <span data-ttu-id="4d376-681">流程图活动设计器或其他工作流活动设计器可能在其默认位置显示所有对象，与附加的属性值相反。</span><span class="sxs-lookup"><span data-stu-id="4d376-681">Flowchart Activity Designer or other Workflow Activity Designers may display all objects in their default locations as opposed to attached property values.</span></span>

<a name="clickonce-1"></a>

### <a name="clickonce"></a><span data-ttu-id="4d376-682">ClickOnce</span><span class="sxs-lookup"><span data-stu-id="4d376-682">ClickOnce</span></span>

<span data-ttu-id="4d376-683">除现已支持的 1.0 协议以外，ClickOnce 已更新为还支持 TLS 1.1 和 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="4d376-683">ClickOnce has been updated to support TLS 1.1 and TLS 1.2 in addition to the 1.0 protocol, which it already supports.</span></span> <span data-ttu-id="4d376-684">ClickOnce 会自动检测哪种协议必需；启用 TLS 1.1 和 1.2 支持无需 ClickOnce 应用程序中的任何额外步骤。</span><span class="sxs-lookup"><span data-stu-id="4d376-684">ClickOnce automatically detects which protocol is required; no extra steps within the ClickOnce application are required to enable TLS 1.1 and 1.2 support.</span></span>

<a name="UWPConvert"></a>

### <a name="converting-windows-forms-and-wpf-apps-to--uwp-apps"></a><span data-ttu-id="4d376-685">将 Windows 窗体和 WPF 应用转换为 UWP 应用</span><span class="sxs-lookup"><span data-stu-id="4d376-685">Converting Windows Forms and WPF apps to  UWP apps</span></span>

<span data-ttu-id="4d376-686">Windows 现在提供将现有 Windows 桌面应用（包括 WPF 和 Windows 窗体应用）引入通用 Windows 平台 (UWP) 的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-686">Windows now offers capabilities to bring existing Windows desktop apps, including WPF and Windows Forms apps, to the Universal Windows Platform (UWP).</span></span> <span data-ttu-id="4d376-687">这项技术充当的是一座桥梁，使你能够逐渐将现有代码库迁移到 UWP，从而将你的应用引入所有 Windows 10 设备。</span><span class="sxs-lookup"><span data-stu-id="4d376-687">This technology acts as a bridge by enabling you to gradually migrate your existing code base to UWP, thereby bringing your app to all Windows 10 devices.</span></span>

<span data-ttu-id="4d376-688">转换后的桌面应用会获得应用标识，类似于 UWP 应用的应用标识，该标识使 UWP API 可访问以启用如动态磁贴和通知等功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-688">Converted desktop apps gain an app identity similar to the app identity of UWP apps, which makes UWP APIs accessible to enable features such as Live Tiles and notifications.</span></span> <span data-ttu-id="4d376-689">应用的行为将继续像以前一样，并作为完全信任应用运行。</span><span class="sxs-lookup"><span data-stu-id="4d376-689">The app continues to behave as before and runs as a full trust app.</span></span> <span data-ttu-id="4d376-690">应用转换之后，可将应用容器进程添加到现有的完全信任进程，以添加自适应用户界面。</span><span class="sxs-lookup"><span data-stu-id="4d376-690">Once the app is converted, an app container process can be added to the existing full trust process to add an adaptive user interface.</span></span> <span data-ttu-id="4d376-691">将所有功能移动到应用容器进程后，可以删除完全信任进程，并且可对所有 Windows 10 设备提供新的 UWP 应用。</span><span class="sxs-lookup"><span data-stu-id="4d376-691">When all functionality is moved to the app container process, the full trust process can be removed and the new UWP app can be made available to all Windows 10 devices.</span></span>

<a name="Debug462"></a>

### <a name="debugging-improvements"></a><span data-ttu-id="4d376-692">调试改进</span><span class="sxs-lookup"><span data-stu-id="4d376-692">Debugging improvements</span></span>

<span data-ttu-id="4d376-693">非托管调试 API 在 .NET Framework 4.6.2 中得到了增强，可在引发 <xref:System.NullReferenceException> 时执行附加分析，让你能够确定单行源代码中哪个变量是 `null`。</span><span class="sxs-lookup"><span data-stu-id="4d376-693">The *unmanaged debugging API* has been enhanced in .NET Framework 4.6.2 to perform additional analysis when a <xref:System.NullReferenceException> is thrown so that it is possible to determine which variable in a single line of source code is `null`.</span></span>   <span data-ttu-id="4d376-694">为支持此方案，已将以下 API 添加到非托管调试 API。</span><span class="sxs-lookup"><span data-stu-id="4d376-694">To support this scenario, the following APIs have been added to the unmanaged debugging API.</span></span>

- <span data-ttu-id="4d376-695">[ICorDebugCode4](../unmanaged-api/debugging/icordebugcode4-interface.md)、[ICorDebugVariableHome](../unmanaged-api/debugging/icordebugvariablehome-interface.md) 和 [ICorDebugVariableHomeEnum](../unmanaged-api/debugging/icordebugvariablehomeenum-interface.md) 接口，它们公开托管变量的本机位置。</span><span class="sxs-lookup"><span data-stu-id="4d376-695">The [ICorDebugCode4](../unmanaged-api/debugging/icordebugcode4-interface.md), [ICorDebugVariableHome](../unmanaged-api/debugging/icordebugvariablehome-interface.md), and [ICorDebugVariableHomeEnum](../unmanaged-api/debugging/icordebugvariablehomeenum-interface.md) interfaces, which expose the native homes of managed variables.</span></span> <span data-ttu-id="4d376-696">这使调试器能够在 <xref:System.NullReferenceException> 发生时执行某些代码流分析并逆向工作，以确定对应于为 `null` 的本机位置的托管变量。</span><span class="sxs-lookup"><span data-stu-id="4d376-696">This enables debuggers to do some code flow analysis when a  <xref:System.NullReferenceException> occurs and to work backwards to determine the managed variable that corresponds to the native location that was `null`.</span></span>

- <span data-ttu-id="4d376-697">[ICorDebugType2::GetTypeID](../unmanaged-api/debugging/icordebugtype2-gettypeid-method.md) 方法提供 ICorDebugType 到 [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) 的映射，这使调试器能够获取 [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md)，而无需 ICorDebugType 的实例。</span><span class="sxs-lookup"><span data-stu-id="4d376-697">The [ICorDebugType2::GetTypeID](../unmanaged-api/debugging/icordebugtype2-gettypeid-method.md) method provides a mapping for ICorDebugType to [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md), which allows the debugger to obtain a [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) without an instance of the ICorDebugType.</span></span> <span data-ttu-id="4d376-698">然后，[COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) 上现有的 API 可用于确定该类型的类布局。</span><span class="sxs-lookup"><span data-stu-id="4d376-698">Existing APIs on [COR_TYPEID](../unmanaged-api/debugging/cor-typeid-structure.md) can then be used to determine the class layout of the type.</span></span>

<a name="v461"></a>

## <a name="whats-new-in-net-framework-461"></a><span data-ttu-id="4d376-699">.NET Framework 4.6.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-699">What's new in .NET Framework 4.6.1</span></span>

<span data-ttu-id="4d376-700">.NET Framework 4.6.1 在以下几个领域新增了功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-700">.NET Framework 4.6.1 includes new features in the following areas:</span></span>

- [<span data-ttu-id="4d376-701">加密</span><span class="sxs-lookup"><span data-stu-id="4d376-701">Cryptography</span></span>](#Crypto)

- [<span data-ttu-id="4d376-702">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-702">ADO.NET</span></span>](#ADO.NET461)

- [<span data-ttu-id="4d376-703">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-703">Windows Presentation Foundation (WPF)</span></span>](#WPF461)

- [<span data-ttu-id="4d376-704">Windows Workflow Foundation</span><span class="sxs-lookup"><span data-stu-id="4d376-704">Windows Workflow Foundation</span></span>](#WWF461)

- [<span data-ttu-id="4d376-705">分析</span><span class="sxs-lookup"><span data-stu-id="4d376-705">Profiling</span></span>](#Profile461)

- [<span data-ttu-id="4d376-706">NGen</span><span class="sxs-lookup"><span data-stu-id="4d376-706">NGen</span></span>](#NGEN461)

<span data-ttu-id="4d376-707">若要详细了解 .NET Framework 4.6.1，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="4d376-707">For more information on .NET Framework 4.6.1, see the following topics:</span></span>

- [<span data-ttu-id="4d376-708">.NET Framework 4.6.1 更改列表</span><span class="sxs-lookup"><span data-stu-id="4d376-708">.NET Framework 4.6.1 list of changes</span></span>](https://github.com/Microsoft/dotnet/blob/master/releases/net461/dotnet461-changes.md)

- [<span data-ttu-id="4d376-709">4.6.1 中的应用程序兼容性</span><span class="sxs-lookup"><span data-stu-id="4d376-709">Application Compatibility in 4.6.1</span></span>](../migration-guide/application-compatibility.md)

- <span data-ttu-id="4d376-710">[.NET Framework API 差异](https://github.com/Microsoft/dotnet/blob/master/releases/net461/dotnet461-api-changes.md)（在 GitHub 上）</span><span class="sxs-lookup"><span data-stu-id="4d376-710">[.NET Framework API diff](https://github.com/Microsoft/dotnet/blob/master/releases/net461/dotnet461-api-changes.md) (on GitHub)</span></span>

<a name="Crypto"></a>

### <a name="cryptography-support-for-x509-certificates-containing-ecdsa"></a><span data-ttu-id="4d376-711">加密：支持包含 ECDSA 在内的 X509 证书</span><span class="sxs-lookup"><span data-stu-id="4d376-711">Cryptography: Support for X509 certificates containing ECDSA</span></span>

<span data-ttu-id="4d376-712">.NET Framework 4.6 添加了针对 X509 证书的 RSACng 支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-712">.NET Framework 4.6 added RSACng support for X509 certificates.</span></span> <span data-ttu-id="4d376-713">.NET Framework 4.6.1 现已开始支持 ECDSA（椭圆曲线数字签名算法）X509 证书。</span><span class="sxs-lookup"><span data-stu-id="4d376-713">.NET Framework 4.6.1 adds support for ECDSA (Elliptic Curve Digital Signature Algorithm) X509 certificates.</span></span>

<span data-ttu-id="4d376-714">ECDSA 可提供更好的性能，是一种比 RSA 更安全的加密算法，从而可在传输层安全性 (TLS) 性能和可伸缩性十分重要的情况下提供极佳选择。</span><span class="sxs-lookup"><span data-stu-id="4d376-714">ECDSA offers better performance and is a more secure cryptography algorithm than RSA, providing an excellent choice where Transport Layer Security (TLS) performance and scalability is a concern.</span></span> <span data-ttu-id="4d376-715">.NET Framework 实现可将调用包装到现有 Windows 功能中。</span><span class="sxs-lookup"><span data-stu-id="4d376-715">The .NET Framework implementation wraps calls into existing Windows functionality.</span></span>

<span data-ttu-id="4d376-716">下面的示例代码展示了如何利用 .NET Framework 4.6.1 中新增的 ECDSA X509 证书支持，轻松生成字节流的签名。</span><span class="sxs-lookup"><span data-stu-id="4d376-716">The following example code shows how easy it is to generate a signature for a byte stream by using the new  support for ECDSA  X509 certificates included in .NET Framework 4.6.1.</span></span>

[!code-csharp[whatsnew.461.crypto#1](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#1)]
[!code-vb[whatsnew.461.crypto#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code461.vb#1)]

<span data-ttu-id="4d376-717">这与在 .NET Framework 4.6 中生成签名所需的代码形成了鲜明对比。</span><span class="sxs-lookup"><span data-stu-id="4d376-717">This offers a marked contrast to the code needed to generate a signature in .NET Framework 4.6.</span></span>

[!code-csharp[whatsnew.461.crypto#2](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#2)]
[!code-vb[whatsnew.461.crypto#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code46.vb#2)]

<a name="ADO.NET461"></a>

### <a name="adonet"></a><span data-ttu-id="4d376-718">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-718">ADO.NET</span></span>

<span data-ttu-id="4d376-719">以下内容已添加到 ADO.NET 中：</span><span class="sxs-lookup"><span data-stu-id="4d376-719">The following have been added to ADO.NET:</span></span>

<span data-ttu-id="4d376-720">**针对硬件保护密钥的 Always Encrypted 支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-720">**Always Encrypted support for hardware protected keys**</span></span>

<span data-ttu-id="4d376-721">ADO.NET 现在支持以本机方式在硬件安全模块 (HSM) 中存储始终加密列主密钥。</span><span class="sxs-lookup"><span data-stu-id="4d376-721">ADO.NET now supports storing Always Encrypted column master keys natively in Hardware Security Modules (HSMs).</span></span> <span data-ttu-id="4d376-722">借助此支持，客户可以利用存储在 HSM 中的非对称密钥，而不必编写自定义列主密钥存储提供程序并在应用程序中注册它们。</span><span class="sxs-lookup"><span data-stu-id="4d376-722">With this support, customers can leverage asymmetric keys stored in HSMs without having to write custom column master key store providers and registering them in applications.</span></span>

<span data-ttu-id="4d376-723">客户需要在应用服务器或客户端计算机上安装 HSM 供应商提供的 CSP 提供程序或 CNG 密钥存储提供程序，才能访问使用存储在 HSM 中的列主密钥保护的始终加密数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-723">Customers need to install the HSM vendor-provided CSP provider or CNG key store providers on the app servers or client computers in order to access Always Encrypted data protected with column master keys stored in a HSM.</span></span>

<span data-ttu-id="4d376-724">**改进了 AlwaysOn 的 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> 连接行为**</span><span class="sxs-lookup"><span data-stu-id="4d376-724">**Improved <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> connection behavior for AlwaysOn**</span></span>

<span data-ttu-id="4d376-725">SqlClient 现在可自动提供与 AlwaysOn 可用性组 (AG) 之间的更快连接。</span><span class="sxs-lookup"><span data-stu-id="4d376-725">SqlClient now automatically provides faster connections to an AlwaysOn Availability Group (AG).</span></span> <span data-ttu-id="4d376-726">它以透明方式检测应用程序是否连接到不同子网上的 AlwaysOn 可用性组 (AG)，快速发现当前的活动服务器并提供与服务器之间的连接。</span><span class="sxs-lookup"><span data-stu-id="4d376-726">It transparently detects whether your application is connecting to an AlwaysOn availability group (AG) on a different subnet and quickly discovers the current active server and provides a connection to the server.</span></span> <span data-ttu-id="4d376-727">在此版本之前，应用程序必须将连接字符串设置为包括 `"MultisubnetFailover=true"`，以指示它已连接到 AlwaysOn 可用性组。</span><span class="sxs-lookup"><span data-stu-id="4d376-727">Prior to this release, an application had to set the connection string to include `"MultisubnetFailover=true"` to indicate that it was connecting to an AlwaysOn Availability Group.</span></span> <span data-ttu-id="4d376-728">如果未将连接关键字设置为 `true`，则应用程序可能会在连接到 AlwaysOn 可用性组时遇到超时。</span><span class="sxs-lookup"><span data-stu-id="4d376-728">Without setting the connection keyword to `true`, an application might experience a timeout while connecting to an AlwaysOn Availability Group.</span></span> <span data-ttu-id="4d376-729">使用此版本时，应用程序 *无需* 再将 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="4d376-729">With this release, an application does *not* need to set <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> to `true` anymore.</span></span> <span data-ttu-id="4d376-730">有关对 Always On 可用性组的 SqlClient 支持的详细信息，请参阅[对高可用性、灾难恢复的 SqlClient 支持](../data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-730">For more information about SqlClient support for Always On Availability Groups, see [SqlClient Support for High Availability, Disaster Recovery](../data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).</span></span>

<a name="WPF461"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="4d376-731">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-731">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="4d376-732">Windows Presentation Foundation 包括一些改进和更改。</span><span class="sxs-lookup"><span data-stu-id="4d376-732">Windows Presentation Foundation includes a number of improvements and changes.</span></span>

<span data-ttu-id="4d376-733">**提升了性能**</span><span class="sxs-lookup"><span data-stu-id="4d376-733">**Improved performance**</span></span>

<span data-ttu-id="4d376-734">在 .NET Framework 4.6.1 中，触控事件的触发延迟问题得到了解决。</span><span class="sxs-lookup"><span data-stu-id="4d376-734">The delay in firing touch events has been fixed in .NET Framework 4.6.1.</span></span> <span data-ttu-id="4d376-735">此外在快速输入过程中，在 <xref:System.Windows.Controls.RichTextBox> 控件中输入不再占用呈现线程。</span><span class="sxs-lookup"><span data-stu-id="4d376-735">In addition, typing in a <xref:System.Windows.Controls.RichTextBox> control no longer ties up the render thread during fast input.</span></span>

<span data-ttu-id="4d376-736">**拼写检查改进**</span><span class="sxs-lookup"><span data-stu-id="4d376-736">**Spell checking improvements**</span></span>

<span data-ttu-id="4d376-737">WPF 中的拼写检查器在 Windows 8.1 和更高版本上进行了更新，可利用操作系统支持对其他语言进行拼写检查。</span><span class="sxs-lookup"><span data-stu-id="4d376-737">The spell checker in WPF has been updated on Windows 8.1 and later versions to leverage operating system support for spell-checking additional languages.</span></span>  <span data-ttu-id="4d376-738">在 Windows 8.1 之前的 Windows 版本上，功能方面没有更改。</span><span class="sxs-lookup"><span data-stu-id="4d376-738">There is no change in functionality on Windows versions prior to Windows 8.1.</span></span>

<span data-ttu-id="4d376-739">与以前版本的 .NET Framework 一样，可通过按以下顺序查找信息来检测 <xref:System.Windows.Controls.TextBox> 控件或 <xref:System.Windows.Controls.RichTextBox> 块的语言：</span><span class="sxs-lookup"><span data-stu-id="4d376-739">As in previous versions of .NET Framework, the language for a <xref:System.Windows.Controls.TextBox> control ora <xref:System.Windows.Controls.RichTextBox> block is detected by looking for information in the following order:</span></span>

- <span data-ttu-id="4d376-740">`xml:lang`（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="4d376-740">`xml:lang`, if it is present.</span></span>

- <span data-ttu-id="4d376-741">当前输入语言。</span><span class="sxs-lookup"><span data-stu-id="4d376-741">Current input language.</span></span>

- <span data-ttu-id="4d376-742">当前线程区域性。</span><span class="sxs-lookup"><span data-stu-id="4d376-742">Current thread culture.</span></span>

<span data-ttu-id="4d376-743">有关 WPF 中语言支持的详细信息，请参阅[有关 .NET Framework 4.6.1 功能的 WPF 博客文章](https://devblogs.microsoft.com/wpf/wpf-in-net-4-6-1/)。</span><span class="sxs-lookup"><span data-stu-id="4d376-743">For more information on language support in WPF, see the [WPF blog post on .NET Framework 4.6.1 features](https://devblogs.microsoft.com/wpf/wpf-in-net-4-6-1/).</span></span>

<span data-ttu-id="4d376-744">**针对每用户自定义词典的附加支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-744">**Additional support for per-user custom dictionaries**</span></span>

<span data-ttu-id="4d376-745">在 .NET Framework 4.6.1 中，WPF 可识别全局注册的自定义字典。</span><span class="sxs-lookup"><span data-stu-id="4d376-745">In .NET Framework 4.6.1, WPF recognizes custom dictionaries that are registered globally.</span></span> <span data-ttu-id="4d376-746">除了能够针对每个控件注册它们，还提供了此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-746">This capability is available in addition to the ability to register them per-control.</span></span>

<span data-ttu-id="4d376-747">在以前版本的 WPF 中，自定义词典无法识别已排除的单词和自动更正列表。</span><span class="sxs-lookup"><span data-stu-id="4d376-747">In previous versions of WPF, custom dictionaries did not recognize Excluded Words and AutoCorrect lists.</span></span> <span data-ttu-id="4d376-748">在 Windows 8.1 和 Windows 10 上，通过使用可以置于 `%AppData%\Microsoft\Spelling\<language tag>` 目录下的文件来支持它们。</span><span class="sxs-lookup"><span data-stu-id="4d376-748">They are supported on Windows 8.1 and Windows 10 through the use of files that can be placed under the `%AppData%\Microsoft\Spelling\<language tag>` directory.</span></span>  <span data-ttu-id="4d376-749">以下规则适用于这些文件：</span><span class="sxs-lookup"><span data-stu-id="4d376-749">The following rules apply to these files:</span></span>

- <span data-ttu-id="4d376-750">这些文件应具有扩展名 .dic（用于已添加的单词）、.exc（用于已排除的单词）或 .acl（用于自动更正）。</span><span class="sxs-lookup"><span data-stu-id="4d376-750">The files should have extensions of .dic (for added words), .exc (for excluded words), or .acl (for AutoCorrect).</span></span>

- <span data-ttu-id="4d376-751">这些文件应是以字节顺序标记 (BOM) 开头的 UTF-16 LE 纯文本。</span><span class="sxs-lookup"><span data-stu-id="4d376-751">The files should be UTF-16 LE plaintext that starts with the Byte Order Mark (BOM).</span></span>

- <span data-ttu-id="4d376-752">每行应包含一个单词（位于已添加和已排除的单词列表中），或是其中用竖线 ("&#124;") 分隔单词的自动更正对（位于自动更正单词列表中）。</span><span class="sxs-lookup"><span data-stu-id="4d376-752">Each line should consist of a word (in the added and excluded word lists), or an autocorrect pair with the words separated by a vertical bar ("&#124;") (in the AutoCorrect word list).</span></span>

- <span data-ttu-id="4d376-753">这些文件被视为只读，不会由系统进行修改。</span><span class="sxs-lookup"><span data-stu-id="4d376-753">These files are considered read-only and are not modified by the system.</span></span>

> [!NOTE]
> <span data-ttu-id="4d376-754">WPF 拼写检查 API 不直接支持这些新文件格式，在应用程序中向 WPF 提供自定义词典应继续使用 .lex 文件。</span><span class="sxs-lookup"><span data-stu-id="4d376-754">These new file-formats are not directly supported by the WPF spell checking APIs, and the custom dictionaries supplied to WPF in applications should continue to use .lex files.</span></span>

<span data-ttu-id="4d376-755">**示例**</span><span class="sxs-lookup"><span data-stu-id="4d376-755">**Samples**</span></span>

<span data-ttu-id="4d376-756">[Microsoft/WPF 示例](https://github.com/Microsoft/WPF-Samples) GitHub 存储库中具有大量的 WPF 示例。</span><span class="sxs-lookup"><span data-stu-id="4d376-756">There are a number of WPF samples on the [Microsoft/WPF-Samples](https://github.com/Microsoft/WPF-Samples) GitHub repository.</span></span> <span data-ttu-id="4d376-757">可通过向我们发送拉取请求或建立 [GitHub 问题](https://github.com/Microsoft/WPF-Samples/issues)来帮助我们改进示例。</span><span class="sxs-lookup"><span data-stu-id="4d376-757">Help us improve our samples by sending us a pull-request or opening a [GitHub issue](https://github.com/Microsoft/WPF-Samples/issues).</span></span>

<span data-ttu-id="4d376-758">**DirectX 扩展**</span><span class="sxs-lookup"><span data-stu-id="4d376-758">**DirectX extensions**</span></span>

<span data-ttu-id="4d376-759">WPF 包括一个 [NuGet 包](https://www.nuget.org/packages/Microsoft.Wpf.Interop.DirectX-x86/)，它提供 <xref:System.Windows.Interop.D3DImage> 的新实现，从而使你可以轻松地与 DX10 和 Dx11 内容进行互操作。</span><span class="sxs-lookup"><span data-stu-id="4d376-759">WPF includes a [NuGet package](https://www.nuget.org/packages/Microsoft.Wpf.Interop.DirectX-x86/) that provides new implementations of <xref:System.Windows.Interop.D3DImage> that make it easy for you to interoperate with DX10 and Dx11 content.</span></span> <span data-ttu-id="4d376-760">此包的代码已开放源代码，在 [GitHub 上](https://github.com/Microsoft/WPFDXInterop)提供。</span><span class="sxs-lookup"><span data-stu-id="4d376-760">The code for this package has been open sourced and is available [on GitHub](https://github.com/Microsoft/WPFDXInterop).</span></span>

<a name="WWF461"></a>

### <a name="windows-workflow-foundation-transactions"></a><span data-ttu-id="4d376-761">Windows Workflow Foundation：事务</span><span class="sxs-lookup"><span data-stu-id="4d376-761">Windows Workflow Foundation: Transactions</span></span>

<span data-ttu-id="4d376-762"><xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> 方法现在可以使用 MSDTC 以外的分布式事务管理器来提升事务。</span><span class="sxs-lookup"><span data-stu-id="4d376-762">The <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> method can now use a distributed transaction manager other than MSDTC to promote the transaction.</span></span> <span data-ttu-id="4d376-763">可通过将 GUID 事务提升程序标识符指定为新的 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> 重载来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="4d376-763">You do this by specifying a GUID transaction promoter identifier to the  new <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> overload .</span></span> <span data-ttu-id="4d376-764">如果此操作成功，则会对事务的功能施加一些限制。</span><span class="sxs-lookup"><span data-stu-id="4d376-764">If this operation is successful, there are limitations placed on the capabilities of the transaction.</span></span> <span data-ttu-id="4d376-765">非 MSDTC 事务提升程序登记之后，以下方法会引发 <xref:System.Transactions.TransactionPromotionException>，因为这些方法需要提升到 MSDTC：</span><span class="sxs-lookup"><span data-stu-id="4d376-765">Once a non-MSDTC transaction promoter is enlisted, the following methods throw a <xref:System.Transactions.TransactionPromotionException> because these methods require promotion to MSDTC:</span></span>

- <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetDtcTransaction%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetExportCookie%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetTransmitterPropagationToken%2A?displayProperty=nameWithType>

<span data-ttu-id="4d376-766">非 MSDTC 事务提升程序登记之后，它必须使用它定义的协议来用于将来的持久登记。</span><span class="sxs-lookup"><span data-stu-id="4d376-766">Once a non-MSDTC transaction promoter is enlisted, it must be used for future durable enlistments by using protocols that it defines.</span></span> <span data-ttu-id="4d376-767">事务提升程序的 <xref:System.Guid> 可以使用 <xref:System.Transactions.Transaction.PromoterType%2A> 属性来获取。</span><span class="sxs-lookup"><span data-stu-id="4d376-767">The <xref:System.Guid> of the transaction promoter can be obtained by using the <xref:System.Transactions.Transaction.PromoterType%2A> property.</span></span> <span data-ttu-id="4d376-768">当事务提升时，事务提升程序会提供表示提升令牌的 <xref:System.Byte> 数组。</span><span class="sxs-lookup"><span data-stu-id="4d376-768">When the transaction promotes, the transaction promoter provides a <xref:System.Byte> array that represents the promoted token.</span></span> <span data-ttu-id="4d376-769">应用程序可以使用 <xref:System.Transactions.Transaction.GetPromotedToken%2A> 方法获取非 MSDTC 提升事务的提升令牌。</span><span class="sxs-lookup"><span data-stu-id="4d376-769">An application can obtain the promoted token for a non-MSDTC promoted transaction with the <xref:System.Transactions.Transaction.GetPromotedToken%2A> method.</span></span>

<span data-ttu-id="4d376-770">新 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> 重载的用户必须遵循特定调用序列，才能使提升操作成功完成。</span><span class="sxs-lookup"><span data-stu-id="4d376-770">Users of the new <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> overload must follow a specific call sequence in order for the promotion operation to complete successfully.</span></span> <span data-ttu-id="4d376-771">这些规则记录在该方法的文档中。</span><span class="sxs-lookup"><span data-stu-id="4d376-771">These rules are documented in the method's documentation.</span></span>

<a name="Profile461"></a>

### <a name="profiling"></a><span data-ttu-id="4d376-772">分析</span><span class="sxs-lookup"><span data-stu-id="4d376-772">Profiling</span></span>

<span data-ttu-id="4d376-773">非托管分析 API 在以下方面得到了增强：</span><span class="sxs-lookup"><span data-stu-id="4d376-773">The unmanaged profiling API has been enhanced as follows:</span></span>

- <span data-ttu-id="4d376-774">更好地支持在 [ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) 接口中访问 PDB。</span><span class="sxs-lookup"><span data-stu-id="4d376-774">Better support for accessing PDBs in the [ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) interface.</span></span>

  <span data-ttu-id="4d376-775">在 ASP.NET Core 中，由 Roslyn 在内存中编译程序集正变得更加常见。</span><span class="sxs-lookup"><span data-stu-id="4d376-775">In ASP.NET Core, it is becoming much more common for assemblies to be compiled in-memory by Roslyn.</span></span> <span data-ttu-id="4d376-776">对于创建分析工具的开发人员而言，这意味着过去在磁盘上进行序列化的 PDB 可能会不再存在。</span><span class="sxs-lookup"><span data-stu-id="4d376-776">For developers making profiling tools, this means that PDBs that historically were serialized on disk may no longer be present.</span></span> <span data-ttu-id="4d376-777">对于代码覆盖率或逐行性能分析这类任务，分析器工具通常使用 PDB 将代码映射回源行。</span><span class="sxs-lookup"><span data-stu-id="4d376-777">Profiler tools often use PDBs to map code back to source lines for tasks such as code coverage or line-by-line performance analysis.</span></span> <span data-ttu-id="4d376-778">[ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) 接口现在包含两种新方法（[ICorProfilerInfo7::GetInMemorySymbolsLength](../unmanaged-api/profiling/icorprofilerinfo7-getinmemorysymbolslength-method.md) 和 [ICorProfilerInfo7::ReadInMemorySymbols](../unmanaged-api/profiling/icorprofilerinfo7-readinmemorysymbols.md)），可为这些探查器工具提供对内存中 PDB 数据的访问。通过使用新 API，探查器可以采用字节数组形式获取内存中 PDB 的内容，然后对它进行处理或将它序列化到磁盘。</span><span class="sxs-lookup"><span data-stu-id="4d376-778">The [ICorProfilerInfo7](../unmanaged-api/profiling/icorprofilerinfo7-interface.md) interface now includes two new methods, [ICorProfilerInfo7::GetInMemorySymbolsLength](../unmanaged-api/profiling/icorprofilerinfo7-getinmemorysymbolslength-method.md) and [ICorProfilerInfo7::ReadInMemorySymbols](../unmanaged-api/profiling/icorprofilerinfo7-readinmemorysymbols.md), to provide these profiler tools with access to the in-memory PDB data, By using the new APIs, a profiler can obtain the contents of an in-memory PDB as a byte array and then process it or serialize it to disk.</span></span>

- <span data-ttu-id="4d376-779">使用 ICorProfiler 接口可更好地检测。</span><span class="sxs-lookup"><span data-stu-id="4d376-779">Better instrumentation with the ICorProfiler interface.</span></span>

  <span data-ttu-id="4d376-780">使用 `ICorProfiler` API 的 ReJit 功能进行动态检测的分析器现在可以修改某些元数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-780">Profilers that are using the `ICorProfiler` APIs ReJit functionality for dynamic instrumentation can now modify some metadata.</span></span> <span data-ttu-id="4d376-781">以前这类工具可以随时检测 IL，但只能在模块加载时修改元数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-781">Previously such tools could instrument IL at any time, but metadata could only be modified at module load time.</span></span> <span data-ttu-id="4d376-782">因为 IL 引用元数据，所以这会限制可以进行的检测的种类。</span><span class="sxs-lookup"><span data-stu-id="4d376-782">Because IL refers to metadata, this limited the kinds of instrumentation that could be done.</span></span> <span data-ttu-id="4d376-783">我们通过添加 [ICorProfilerInfo7::ApplyMetaData](../unmanaged-api/profiling/icorprofilerinfo7-applymetadata-method.md) 方法来支持在模块加载之后编辑元数据的子集（特别是通过添加新的 `AssemblyRef`、`TypeRef`、`TypeSpec`、`MemberRef`、`MemberSpec` 和 `UserString` 记录），解除了其中一些限制。</span><span class="sxs-lookup"><span data-stu-id="4d376-783">We have lifted some of those limits by adding the [ICorProfilerInfo7::ApplyMetaData](../unmanaged-api/profiling/icorprofilerinfo7-applymetadata-method.md) method to support a subset of metadata edits after the module loads, in particular by adding new `AssemblyRef`, `TypeRef`, `TypeSpec`, `MemberRef`, `MemberSpec`, and `UserString` records.</span></span> <span data-ttu-id="4d376-784">通过此更改可以进行范围广得多的动态检测。</span><span class="sxs-lookup"><span data-stu-id="4d376-784">This change makes a much broader range of on-the-fly instrumentation possible.</span></span>

<a name="NGEN461"></a>

### <a name="native-image-generator-ngen-pdbs"></a><span data-ttu-id="4d376-785">本机映像生成器 (NGEN) PDB</span><span class="sxs-lookup"><span data-stu-id="4d376-785">Native Image Generator (NGEN) PDBs</span></span>

<span data-ttu-id="4d376-786">跨计算机事件跟踪允许客户在计算机 A 上分析一个程序，并在计算机 B 上查看具有源行映射的分析数据。通过使用以前版本的 .NET Framework，用户会将所有模块和本机映像从分析计算机复制到包含 IL PDB 的分析计算机来创建源到本机映射。</span><span class="sxs-lookup"><span data-stu-id="4d376-786">Cross-machine event tracing allows customers to profile a program on Machine A and look at the profiling data with source line mapping on Machine B. Using previous versions of .NET Framework, the user would copy all the modules and native images from the profiled machine to the analysis machine that contains the IL PDB to create the source-to-native mapping.</span></span> <span data-ttu-id="4d376-787">虽然此过程在文件相对较小（如用于手机应用程序）时可能工作良好，但是文件在桌面系统上可能非常大，需要很长时间来进行复制。</span><span class="sxs-lookup"><span data-stu-id="4d376-787">While this process may work well when the files are relatively small, such as for phone applications, the files can be very large on desktop systems and require significant time to copy.</span></span>

<span data-ttu-id="4d376-788">借助 Ngen PDB，NGen 可以创建包含 IL 到本机映射的 PDB，而无需依赖于 IL PDB。</span><span class="sxs-lookup"><span data-stu-id="4d376-788">With Ngen PDBs, NGen can create a PDB that contains the IL-to-native mapping without a dependency on the IL PDB.</span></span> <span data-ttu-id="4d376-789">在我们的跨计算机事件跟踪方案中，只需将计算机 A 生成的本机映像 PDB 复制到计算机 B，并使用[调试接口访问 API](/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk-reference) 读取 IL PDB 的源到 IL 映射和本机映像 PDB 的 IL 到本机映射。</span><span class="sxs-lookup"><span data-stu-id="4d376-789">In our cross-machine event tracing scenario, all that is needed is to copy the native image PDB that is generated by Machine A to Machine B and to use [Debug Interface Access APIs](/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk-reference) to read the IL PDB's source-to-IL mapping and the native image PDB's IL-to-native mapping.</span></span> <span data-ttu-id="4d376-790">组合这两个映射可提供源到本机映射。</span><span class="sxs-lookup"><span data-stu-id="4d376-790">Combining both mappings provides a source-to-native mapping.</span></span> <span data-ttu-id="4d376-791">由于本机映像 PDB 远小于所有模块和本机映像，因此从计算机 A 复制到计算机 B 的过程要快得多。</span><span class="sxs-lookup"><span data-stu-id="4d376-791">Since the native image PDB is much smaller than all the modules and native images, the process of copying from Machine A to Machine B is much faster.</span></span>

<a name="v46"></a>

## <a name="whats-new-in-net-2015"></a><span data-ttu-id="4d376-792">.NET 2015 的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-792">What's new in .NET 2015</span></span>

<span data-ttu-id="4d376-793">.NET 2015 引入了 .NET Framework 4.6 和 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="4d376-793">.NET 2015 introduces .NET Framework 4.6 and .NET Core.</span></span> <span data-ttu-id="4d376-794">一些新功能两者都适用，而另一些功能则是 .NET Framework 4.6 或 .NET Core 的专属功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-794">Some new features apply to both, and other features are specific to .NET Framework 4.6 or .NET Core.</span></span>

- <span data-ttu-id="4d376-795">**ASP.NET Core**</span><span class="sxs-lookup"><span data-stu-id="4d376-795">**ASP.NET Core**</span></span>

  <span data-ttu-id="4d376-796">.NET 2015 包括 ASP.NET Core，是一个用于生成基于云的新式应用的精益 .NET 实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-796">.NET 2015 includes ASP.NET Core, which is a lean .NET implementation for building modern cloud-based apps.</span></span> <span data-ttu-id="4d376-797">ASP.NET Core 是模块化的，因此你可以仅包括应用程序所需的那些功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-797">ASP.NET Core is modular so you can include only those features that are needed in your application.</span></span> <span data-ttu-id="4d376-798">其可承载于 IIS 上或自承载于自定义过程中，并且你可以在同一服务器上运行具有不同版本 .NET Framework 的应用。</span><span class="sxs-lookup"><span data-stu-id="4d376-798">It can be hosted on IIS or self-hosted in a custom process, and you can run apps with different versions of the .NET Framework on the same server.</span></span> <span data-ttu-id="4d376-799">它包括为云部署而设计的新环境配置系统。</span><span class="sxs-lookup"><span data-stu-id="4d376-799">It includes a new environment configuration system that is designed for cloud deployment.</span></span>

  <span data-ttu-id="4d376-800">MVC、Web API 和 Web Pages 统一至称为 MVC 6 的单个 Framework。</span><span class="sxs-lookup"><span data-stu-id="4d376-800">MVC, Web API, and Web Pages are unified into a single framework called MVC 6.</span></span> <span data-ttu-id="4d376-801">通过 Visual Studio 2015 或更高版本中的新工具生成 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="4d376-801">You build ASP.NET Core apps through tools in Visual Studio 2015 or later.</span></span> <span data-ttu-id="4d376-802">现有应用程序将在新 .NET Framework 上工作；但是，若要生成使用 MVC 6 或 SignalR 3 的应用，则必须使用 Visual Studio 2015 或更高版本中的项目系统。</span><span class="sxs-lookup"><span data-stu-id="4d376-802">Your existing applications will work on the new .NET Framework; however to build an app that uses MVC 6 or SignalR 3, you must use the project system in Visual Studio 2015 or later.</span></span>

  <span data-ttu-id="4d376-803">有关信息，请参阅 [ASP.NET Core](/aspnet/core/)。</span><span class="sxs-lookup"><span data-stu-id="4d376-803">For information, see [ASP.NET Core](/aspnet/core/).</span></span>

- <span data-ttu-id="4d376-804">**ASP.NET 更新**</span><span class="sxs-lookup"><span data-stu-id="4d376-804">**ASP.NET Updates**</span></span>

  - <span data-ttu-id="4d376-805">**基于任务的 API，用于异步响应刷新**</span><span class="sxs-lookup"><span data-stu-id="4d376-805">**Task-based API for Asynchronous Response Flushing**</span></span>

    <span data-ttu-id="4d376-806">ASP.NET 现在提供一个基于任务的简单 API <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=nameWithType> 用于异步响应刷新，它允许通过使用你的语言的 `async/await` 支持来异步刷新响应。</span><span class="sxs-lookup"><span data-stu-id="4d376-806">ASP.NET now provides a simple task-based API for asynchronous response flushing, <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=nameWithType>, that allows responses to be flushed asynchronously by using your language's `async/await` support.</span></span>

  - <span data-ttu-id="4d376-807">**模型绑定支持 Task 返回方法**</span><span class="sxs-lookup"><span data-stu-id="4d376-807">**Model binding supports task-returning methods**</span></span>

    <span data-ttu-id="4d376-808">在 .NET Framework 4.5 中，ASP.NET 增加了模型绑定功能，启用了一种以代码为中心的可扩展方法，用于在 Web 窗体页面和用户控件中执行基于 CRUD 的数据操作。</span><span class="sxs-lookup"><span data-stu-id="4d376-808">In .NET Framework 4.5, ASP.NET added the Model Binding feature that enabled an extensible, code-focused approach to CRUD-based data operations in Web Forms pages and user controls.</span></span> <span data-ttu-id="4d376-809">模型绑定系统现在支持 <xref:System.Threading.Tasks.Task>-returning 模型绑定方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-809">The Model Binding system now supports <xref:System.Threading.Tasks.Task>-returning model binding methods.</span></span> <span data-ttu-id="4d376-810">此功能使得 Web 窗体开发人员在使用较新版本的 ORM（包括实体框架）时，能获得异步的可伸缩性优点以及数据绑定系统的易用性。</span><span class="sxs-lookup"><span data-stu-id="4d376-810">This feature allows Web Forms developers to get the scalability benefits of async with the ease of the data-binding system when using newer versions of ORMs, including the Entity Framework.</span></span>

    <span data-ttu-id="4d376-811">异步模型绑定由 `aspnet:EnableAsyncModelBinding` 配置设置控制。</span><span class="sxs-lookup"><span data-stu-id="4d376-811">Async model binding is controlled by the `aspnet:EnableAsyncModelBinding` configuration setting.</span></span>

    ```xml
    <appSettings>
        <add key=" aspnet:EnableAsyncModelBinding" value="true|false" />
    </appSettings>
    ```

    <span data-ttu-id="4d376-812">在定位 .NET Framework 4.6 的应用程序中，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="4d376-812">On apps the target .NET Framework 4.6, it defaults to `true`.</span></span> <span data-ttu-id="4d376-813">在定位旧版 .NET Framework 但在 .NET Framework 4.6 上运行的应用程序中，默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="4d376-813">On apps running on .NET Framework 4.6 that target an earlier version of .NET Framework, it is `false` by default.</span></span> <span data-ttu-id="4d376-814">可以通过将配置设置设置为 `true` 来启用它。</span><span class="sxs-lookup"><span data-stu-id="4d376-814">It can be enabled by setting the configuration setting to `true`.</span></span>

  - <span data-ttu-id="4d376-815">**HTTP/2 支持 (Windows 10)**</span><span class="sxs-lookup"><span data-stu-id="4d376-815">**HTTP/2 Support (Windows 10)**</span></span>

    <span data-ttu-id="4d376-816">[HTTP/2](https://www.wikipedia.org/wiki/HTTP/2) 是新版的 HTTP 协议，提供更好的连接利用率（客户端和服务器之间的往返更少），从而减少为用户加载网页的延迟。</span><span class="sxs-lookup"><span data-stu-id="4d376-816">[HTTP/2](https://www.wikipedia.org/wiki/HTTP/2) is a new version of the HTTP protocol that provides much better connection utilization (fewer round-trips between client and server), resulting in lower latency web page loading for users.</span></span>  <span data-ttu-id="4d376-817">网页（而不是服务）从 HTTP/2 中获益最多，因为该协议优化多个作为单个体验的一部分进行请求的项目。</span><span class="sxs-lookup"><span data-stu-id="4d376-817">Web pages (as opposed to services) benefit the most from HTTP/2, since the protocol optimizes for multiple artifacts being requested as part of a single experience.</span></span> <span data-ttu-id="4d376-818">已向 .NET Framework 4.6 中的 ASP.NET 添加了 HTTP/2 支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-818">HTTP/2 support has been added to ASP.NET in .NET Framework 4.6.</span></span> <span data-ttu-id="4d376-819">因为网络功能存在于多个层，所以 Windows、IIS 和 ASP.NET 中均需要新功能以启用 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="4d376-819">Because networking functionality exists at multiple layers, new features were required in Windows, in IIS, and in ASP.NET to enable HTTP/2.</span></span> <span data-ttu-id="4d376-820">必须在 Windows 10 上运行，以便将 HTTP/2 与 ASP.NET 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="4d376-820">You must be running on Windows 10 to use HTTP/2 with ASP.NET.</span></span>

    <span data-ttu-id="4d376-821">HTTP/2 也受到支持，默认情况下在使用 <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> API 的 Windows 10 通用 Windows 平台 (UWP) 上使用。</span><span class="sxs-lookup"><span data-stu-id="4d376-821">HTTP/2 is also supported and on by default for Windows 10 Universal Windows Platform (UWP) apps that use the <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> API.</span></span>

    <span data-ttu-id="4d376-822">为了提供一种方法来使用 ASP.NET 应用程序中的 [PUSH_PROMISE](https://httpwg.github.io/http2-spec/#PUSH_PROMISE) 功能，已向 <xref:System.Web.HttpResponse> 类添加了一种具有两个重载（<xref:System.Web.HttpResponse.PushPromise%28System.String%29> 和 <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29>）的新方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-822">In order to provide a way to use the [PUSH_PROMISE](https://httpwg.github.io/http2-spec/#PUSH_PROMISE) feature in ASP.NET applications, a new method with two overloads, <xref:System.Web.HttpResponse.PushPromise%28System.String%29> and <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29>, has been added to the <xref:System.Web.HttpResponse> class.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d376-823">尽管 ASP.NET Core 支持 HTTP/2，不过尚未添加针对 PUSH PROMISE 功能的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-823">While ASP.NET Core supports HTTP/2, support for the PUSH PROMISE feature has not yet been added.</span></span>

    <span data-ttu-id="4d376-824">浏览器和 Web 服务器（Windows 上的 IIS）执行所有工作。</span><span class="sxs-lookup"><span data-stu-id="4d376-824">The browser and the web server (IIS on Windows) do all the work.</span></span> <span data-ttu-id="4d376-825">无需为用户执行任何繁重任务。</span><span class="sxs-lookup"><span data-stu-id="4d376-825">You don't have to do any heavy-lifting for your users.</span></span>

    <span data-ttu-id="4d376-826">大多数[主要浏览器都支持 HTTP/2](https://www.wikipedia.org/wiki/HTTP/2)，因此很可能你的用户将从 HTTP/2 支持中受益（如果你的服务器支持它）。</span><span class="sxs-lookup"><span data-stu-id="4d376-826">Most of the [major browsers support HTTP/2](https://www.wikipedia.org/wiki/HTTP/2), so it's likely that your users will benefit from HTTP/2 support if your server supports it.</span></span>

  - <span data-ttu-id="4d376-827">**对令牌绑定协议的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-827">**Support for the Token Binding Protocol**</span></span>

    <span data-ttu-id="4d376-828">Microsoft 和 Google 一直在针对身份验证的新方法进行合作，这种方法称为[令牌绑定协议](https://github.com/TokenBinding/Internet-Drafts)。</span><span class="sxs-lookup"><span data-stu-id="4d376-828">Microsoft and Google have been collaborating on a new approach to authentication, called the [Token Binding Protocol](https://github.com/TokenBinding/Internet-Drafts).</span></span> <span data-ttu-id="4d376-829">前提是罪犯可以盗取并使用身份验证令牌（在你的浏览器缓存中）以访问本应安全的资源（例如你的银行帐户），而无需知道密码或任何其他特权。</span><span class="sxs-lookup"><span data-stu-id="4d376-829">The premise is that authentication tokens (in your browser cache) can be stolen and used by criminals to access otherwise secure resources (for example, your bank account) without requiring your password or any other privileged knowledge.</span></span> <span data-ttu-id="4d376-830">新协议旨在缓解此问题。</span><span class="sxs-lookup"><span data-stu-id="4d376-830">The new protocol aims to mitigate this problem.</span></span>

    <span data-ttu-id="4d376-831">令牌绑定协议将在 Windows 10 中作为浏览器功能实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-831">The Token Binding Protocol will be implemented in Windows 10 as a browser feature.</span></span> <span data-ttu-id="4d376-832">ASP.NET 应用将参与该协议，以使身份验证令牌验证为合法。</span><span class="sxs-lookup"><span data-stu-id="4d376-832">ASP.NET apps will participate in the protocol, so that authentication tokens are validated to be legitimate.</span></span> <span data-ttu-id="4d376-833">客户端和服务器实现建立由协议指定的端到端的保护。</span><span class="sxs-lookup"><span data-stu-id="4d376-833">The client and the server implementations establish the end-to-end protection specified by the protocol.</span></span>

  - <span data-ttu-id="4d376-834">**随机字符串哈希算法**</span><span class="sxs-lookup"><span data-stu-id="4d376-834">**Randomized string hash algorithms**</span></span>

    <span data-ttu-id="4d376-835">.NET Framework 4.5 引入了[随机字符串哈希算法](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-835">.NET Framework 4.5 introduced a [randomized string hash algorithm](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).</span></span> <span data-ttu-id="4d376-836">但是，由于某些 ASP.NET 功能依赖于稳定的哈希代码，因此 ASP.NET 不支持该算法。</span><span class="sxs-lookup"><span data-stu-id="4d376-836">However, it was not supported by ASP.NET because of some ASP.NET features depended on a stable hash code.</span></span> <span data-ttu-id="4d376-837">在 .NET Framework 4.6 中，现在支持随机字符串哈希算法。</span><span class="sxs-lookup"><span data-stu-id="4d376-837">In .NET Framework 4.6, randomized string hash algorithms are now supported.</span></span> <span data-ttu-id="4d376-838">若要启用此功能，请使用 `aspnet:UseRandomizedStringHashAlgorithm` 配置设置。</span><span class="sxs-lookup"><span data-stu-id="4d376-838">To enable this feature, use the `aspnet:UseRandomizedStringHashAlgorithm` config setting.</span></span>

    ```xml
    <appSettings>
        <add key="aspnet:UseRandomizedStringHashAlgorithm" value="true|false" />
    </appSettings>
    ```

- <span data-ttu-id="4d376-839">**ADO.NET**</span><span class="sxs-lookup"><span data-stu-id="4d376-839">**ADO.NET**</span></span>

  <span data-ttu-id="4d376-840">ADO.NET 现在支持 SQL Server 2016 社区技术预览版 2 (CTP2) 中提供的 Always Encrypted 功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-840">ADO .NET now supports the Always Encrypted feature available in SQL Server 2016 Community Technology Preview 2 (CTP2).</span></span> <span data-ttu-id="4d376-841">借助 Always Encrypted，SQL Server 可对加密数据执行操作，并且最重要的是，加密密钥与应用程序一起驻留在客户的受信任环境内，而不是驻留在服务器上。</span><span class="sxs-lookup"><span data-stu-id="4d376-841">With Always Encrypted, SQL Server can perform operations on encrypted data, and best of all the encryption key resides with the application inside the customer's trusted environment and not on the server.</span></span> <span data-ttu-id="4d376-842">Always Encrypted 可确保客户数据的安全，因此 DBA 没有纯文本数据的访问权限。</span><span class="sxs-lookup"><span data-stu-id="4d376-842">Always Encrypted secures customer data so DBAs do not have access to plain text data.</span></span> <span data-ttu-id="4d376-843">数据的加密和解密都在驱动程序级别以透明方式执行，从而将现有应用程序必须做出的更改减至最少。</span><span class="sxs-lookup"><span data-stu-id="4d376-843">Encryption and decryption of data happens transparently at the driver level, minimizing changes that have to be made to existing applications.</span></span> <span data-ttu-id="4d376-844">有关详细信息，请参阅 [Always Encrypted（数据库引擎）](/sql/relational-databases/security/encryption/always-encrypted-database-engine)和 [Always Encrypted（客户端开发）](/sql/relational-databases/security/encryption/always-encrypted-client-development)。</span><span class="sxs-lookup"><span data-stu-id="4d376-844">For details, see [Always Encrypted (Database Engine)](/sql/relational-databases/security/encryption/always-encrypted-database-engine) and [Always Encrypted (client development)](/sql/relational-databases/security/encryption/always-encrypted-client-development).</span></span>

- <span data-ttu-id="4d376-845">**托管代码的 64 位 JIT 编译器**</span><span class="sxs-lookup"><span data-stu-id="4d376-845">**64-bit JIT Compiler for managed code**</span></span>

  <span data-ttu-id="4d376-846">.NET Framework 4.6 采用新版 64 位 JIT 编译器（最初代码名为 RyuJIT）。</span><span class="sxs-lookup"><span data-stu-id="4d376-846">.NET Framework 4.6 features a new version of the 64-bit JIT compiler (originally code-named RyuJIT).</span></span> <span data-ttu-id="4d376-847">新的 64 位编译器相较旧的 64 位 JIT 编译器具有显著的性能提升。</span><span class="sxs-lookup"><span data-stu-id="4d376-847">The new 64-bit compiler provides significant performance improvements over the older 64-bit JIT compiler.</span></span> <span data-ttu-id="4d376-848">新的 64 位编译器针对 .NET Framework 4.6 上运行的 64 位进程而启用。</span><span class="sxs-lookup"><span data-stu-id="4d376-848">The new 64-bit compiler is enabled for 64-bit processes running on top of .NET Framework 4.6.</span></span> <span data-ttu-id="4d376-849">如果你的应用被编译为 64 位或 AnyCPU 并在 64 位操作系统上运行，则它将在 64 位进程中运行。</span><span class="sxs-lookup"><span data-stu-id="4d376-849">Your app will run in a 64-bit process if it is compiled as 64-bit or AnyCPU and is running on a 64-bit operating system.</span></span> <span data-ttu-id="4d376-850">虽然已采取谨慎的措施来使到新编译器的转换尽可能透明，但行为也可能发生变化。</span><span class="sxs-lookup"><span data-stu-id="4d376-850">While care has been taken to make the transition to the new compiler as transparent as possible, changes in behavior are possible.</span></span>

  <span data-ttu-id="4d376-851">新的 64 位 JIT 编译器还包括硬件 SIMD 加速功能，结合 <xref:System.Numerics> 命名空间中支持 SIMD 的类型使用时，可以获得良好的性能提升。</span><span class="sxs-lookup"><span data-stu-id="4d376-851">The new 64-bit JIT compiler also includes hardware SIMD acceleration features when coupled with SIMD-enabled types in the <xref:System.Numerics> namespace, which can yield good performance improvements.</span></span>

- <span data-ttu-id="4d376-852">**程序集加载程序改进**</span><span class="sxs-lookup"><span data-stu-id="4d376-852">**Assembly loader improvements**</span></span>

  <span data-ttu-id="4d376-853">通过在加载相应的 NGEN 映像后卸载 IL 程序集，程序集加载程序现在能更有效地利用内存。</span><span class="sxs-lookup"><span data-stu-id="4d376-853">The assembly loader now uses memory more efficiently by unloading IL assemblies after a corresponding NGEN image is loaded.</span></span> <span data-ttu-id="4d376-854">此更改会降低虚拟内存（这对诸如 Visual Studio 等的大型 32 位应用特别有益），还会节省物理内存。</span><span class="sxs-lookup"><span data-stu-id="4d376-854">This change decreases virtual memory, which is particularly beneficial for large 32-bit apps (such as Visual Studio), and also saves physical memory.</span></span>

- <span data-ttu-id="4d376-855">**基类库更改**</span><span class="sxs-lookup"><span data-stu-id="4d376-855">**Base class library changes**</span></span>

  <span data-ttu-id="4d376-856">为了启用关键方案，已向 .NET Framework 4.6 添加了许多新 API。</span><span class="sxs-lookup"><span data-stu-id="4d376-856">Many new APIs have been added around to .NET Framework 4.6 to enable key scenarios.</span></span> <span data-ttu-id="4d376-857">这些包括以下更改和添加：</span><span class="sxs-lookup"><span data-stu-id="4d376-857">These include the following changes and additions:</span></span>

  - <span data-ttu-id="4d376-858">**IReadOnlyCollection\<T> 实现**</span><span class="sxs-lookup"><span data-stu-id="4d376-858">**IReadOnlyCollection\<T> implementations**</span></span>

    <span data-ttu-id="4d376-859">其他集合实现 <xref:System.Collections.Generic.IReadOnlyCollection%601>，例如 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601>。</span><span class="sxs-lookup"><span data-stu-id="4d376-859">Additional collections implement <xref:System.Collections.Generic.IReadOnlyCollection%601> such as <xref:System.Collections.Generic.Queue%601> and <xref:System.Collections.Generic.Stack%601>.</span></span>

  - <span data-ttu-id="4d376-860">**CultureInfo.CurrentCulture 和 CultureInfo.CurrentUICulture**</span><span class="sxs-lookup"><span data-stu-id="4d376-860">**CultureInfo.CurrentCulture and CultureInfo.CurrentUICulture**</span></span>

    <span data-ttu-id="4d376-861"><xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 属性现在是读写而不是只读。</span><span class="sxs-lookup"><span data-stu-id="4d376-861">The <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> and <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> properties are now read-write rather than read-only.</span></span> <span data-ttu-id="4d376-862">如果你向这些属性分配一个新 <xref:System.Globalization.CultureInfo> 对象，则由 `Thread.CurrentThread.CurrentCulture` 属性定义的当前线程区域性和由 `Thread.CurrentThread.CurrentUICulture` 属性定义在当前 UI 线程区域性也会更改。</span><span class="sxs-lookup"><span data-stu-id="4d376-862">If you assign a new <xref:System.Globalization.CultureInfo> object to these properties, the current thread culture defined by the `Thread.CurrentThread.CurrentCulture` property and the current UI thread culture defined by the `Thread.CurrentThread.CurrentUICulture` properties also change.</span></span>

  - <span data-ttu-id="4d376-863">**垃圾回收 (GC) 增强功能**</span><span class="sxs-lookup"><span data-stu-id="4d376-863">**Enhancements to garbage collection (GC)**</span></span>

    <span data-ttu-id="4d376-864"><xref:System.GC> 类现在包括允许你在执行关键路径期间禁止垃圾回收的 <xref:System.GC.TryStartNoGCRegion%2A> 和 <xref:System.GC.EndNoGCRegion%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-864">The <xref:System.GC> class now includes <xref:System.GC.TryStartNoGCRegion%2A> and <xref:System.GC.EndNoGCRegion%2A> methods that allow you to disallow garbage collection during the execution of a critical path.</span></span>

    <span data-ttu-id="4d376-865"><xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=nameWithType> 方法的新重载允许你控制小型对象堆和大型对象堆是否均扫频和压缩或仅扫频。</span><span class="sxs-lookup"><span data-stu-id="4d376-865">A new overload of the <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=nameWithType> method allows you to control whether both the small object heap and the large object heap are swept and compacted or swept only.</span></span>

  - <span data-ttu-id="4d376-866">**启用了 SIMD 的类型**</span><span class="sxs-lookup"><span data-stu-id="4d376-866">**SIMD-enabled types**</span></span>

    <span data-ttu-id="4d376-867"><xref:System.Numerics> 命名空间现在包括许多支持 SIMD 的类型，如 <xref:System.Numerics.Matrix3x2>、<xref:System.Numerics.Matrix4x4>、<xref:System.Numerics.Plane>、<xref:System.Numerics.Quaternion>、<xref:System.Numerics.Vector2>、<xref:System.Numerics.Vector3> 和 <xref:System.Numerics.Vector4>。</span><span class="sxs-lookup"><span data-stu-id="4d376-867">The <xref:System.Numerics> namespace now includes a number of SIMD-enabled types, such as <xref:System.Numerics.Matrix3x2>, <xref:System.Numerics.Matrix4x4>, <xref:System.Numerics.Plane>, <xref:System.Numerics.Quaternion>, <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3>, and <xref:System.Numerics.Vector4>.</span></span>

    <span data-ttu-id="4d376-868">由于新的 64 位 JIT 编译器还包括硬件 SIMD 加速功能，将支持 SIMD 的类型与新的 64 位 JIT 编译器一起使用时，会带来特别显著的性能提升。</span><span class="sxs-lookup"><span data-stu-id="4d376-868">Because the new 64-bit JIT compiler also includes hardware SIMD acceleration features, there are especially significant performance improvements when using the SIMD-enabled types with the new 64-bit JIT compiler.</span></span>

  - <span data-ttu-id="4d376-869">**加密更新**</span><span class="sxs-lookup"><span data-stu-id="4d376-869">**Cryptography updates**</span></span>

    <span data-ttu-id="4d376-870"><xref:System.Security.Cryptography?displayProperty=nameWithType> API 更新为支持 [Windows CNG 加密 API](/windows/desktop/SecCNG/cng-reference)。</span><span class="sxs-lookup"><span data-stu-id="4d376-870">The <xref:System.Security.Cryptography?displayProperty=nameWithType> API is being updated to support the [Windows CNG cryptography APIs](/windows/desktop/SecCNG/cng-reference).</span></span> <span data-ttu-id="4d376-871">以前版本的 .NET Framework 完全依赖于[早期版本的 Windows 加密 API](/windows/desktop/SecCrypto/cryptography-portal)，以用作 <xref:System.Security.Cryptography?displayProperty=nameWithType> 实现的基础。</span><span class="sxs-lookup"><span data-stu-id="4d376-871">Previous versions of the .NET Framework have relied entirely on an [earlier version of the Windows Cryptography APIs](/windows/desktop/SecCrypto/cryptography-portal) as the basis for the <xref:System.Security.Cryptography?displayProperty=nameWithType> implementation.</span></span> <span data-ttu-id="4d376-872">我们已经请求支持 CNG API，因为它支持[现代加密算法](/windows/desktop/SecCNG/cng-features#suite-b-support)，这对某些类别的应用十分重要。</span><span class="sxs-lookup"><span data-stu-id="4d376-872">We have had requests to support the CNG API, since it supports [modern cryptography algorithms](/windows/desktop/SecCNG/cng-features#suite-b-support), which are important for certain categories of apps.</span></span>

    <span data-ttu-id="4d376-873">.NET Framework 4.6 包括以下新的增强功能以支持 Windows CNG 加密 API：</span><span class="sxs-lookup"><span data-stu-id="4d376-873">.NET Framework 4.6 includes the following new enhancements to support the Windows CNG cryptography APIs:</span></span>

    - <span data-ttu-id="4d376-874">X509 证书（`System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` 和 `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`）的一组扩展方法，如果可能，它们将返回基于 CNG 的实现，而不返回基于 CAPI 的实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-874">A set of extension methods for X509 Certificates, `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` and `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`, that return a CNG-based implementation rather than a CAPI-based implementation when possible.</span></span> <span data-ttu-id="4d376-875">（一些智能卡等仍需要 CAPI，并由 API 处理回退）。</span><span class="sxs-lookup"><span data-stu-id="4d376-875">(Some smartcards, etc., still require CAPI, and the APIs handle the fallback).</span></span>

    - <span data-ttu-id="4d376-876"><xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> 类，该类提供 RSA 算法的 CNG 实现。</span><span class="sxs-lookup"><span data-stu-id="4d376-876">The <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType> class, which provides a CNG implementation of the RSA algorithm.</span></span>

    - <span data-ttu-id="4d376-877">RSA API 的增强功能，常见操作不再需要转换。</span><span class="sxs-lookup"><span data-stu-id="4d376-877">Enhancements to the RSA API so that common actions no longer require casting.</span></span> <span data-ttu-id="4d376-878">例如，使用 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 对象加密数据需要类似以前版本的 .NET Framework 中的以下代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-878">For example, encrypting data using an <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> object requires code like the following in previous versions of .NET Framework.</span></span>

      [!code-csharp[WhatsNew.Casting#1](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#1)]
      [!code-vb[WhatsNew.Casting#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#1)]

      <span data-ttu-id="4d376-879">可采用如下方式重写在 .NET Framework 4.6 中使用新加密 API 的代码以避免转换。</span><span class="sxs-lookup"><span data-stu-id="4d376-879">Code that uses the new cryptography APIs in .NET Framework 4.6 can be rewritten as follows to avoid the cast.</span></span>

      [!code-csharp[WhatsNew.Casting#2](~/samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#2)]
      [!code-vb[WhatsNew.Casting#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#2)]

  - <span data-ttu-id="4d376-880">**支持将日期和时间与 UNIX 时间相互转换**</span><span class="sxs-lookup"><span data-stu-id="4d376-880">**Support for converting dates and times to or from Unix time**</span></span>

    <span data-ttu-id="4d376-881">以下新方法已添加到 <xref:System.DateTimeOffset> 结构，以支持将日期和时间转换为 UNIX 时间或将 UNIX 时间转换为日期和时间：</span><span class="sxs-lookup"><span data-stu-id="4d376-881">The following new methods have been added to the <xref:System.DateTimeOffset> structure to support converting date and time values to or from Unix time:</span></span>

    - <xref:System.DateTimeOffset.FromUnixTimeSeconds%2A?displayProperty=nameWithType>

    - <xref:System.DateTimeOffset.FromUnixTimeMilliseconds%2A?displayProperty=nameWithType>

    - <xref:System.DateTimeOffset.ToUnixTimeSeconds%2A?displayProperty=nameWithType>

    - <xref:System.DateTimeOffset.ToUnixTimeMilliseconds%2A?displayProperty=nameWithType>

  - <span data-ttu-id="4d376-882">**兼容性开关**</span><span class="sxs-lookup"><span data-stu-id="4d376-882">**Compatibility switches**</span></span>

    <span data-ttu-id="4d376-883"><xref:System.AppContext> 类添加一个新的兼容性功能，使库编写器可为其用户提供统一的新功能选择退出机制。</span><span class="sxs-lookup"><span data-stu-id="4d376-883">The <xref:System.AppContext> class adds a new compatibility feature that enables library writers to provide a uniform opt-out mechanism for new functionality for their users.</span></span> <span data-ttu-id="4d376-884">它在组件之间建立松耦合的协定，以便与选择退出请求进行通信。</span><span class="sxs-lookup"><span data-stu-id="4d376-884">It establishes a loosely coupled contract between components in order to communicate an opt-out request.</span></span> <span data-ttu-id="4d376-885">对现有功能进行更改时，此功能通常很重要。</span><span class="sxs-lookup"><span data-stu-id="4d376-885">This capability is typically important when a change is made to existing functionality.</span></span> <span data-ttu-id="4d376-886">相反，已有新功能隐式选择加入。</span><span class="sxs-lookup"><span data-stu-id="4d376-886">Conversely, there is already an implicit opt-in for new functionality.</span></span>

    <span data-ttu-id="4d376-887">使用 <xref:System.AppContext>，库定义并公开兼容性开关，而依赖于这些开关的代码可以设置这些开关以影响库行为。</span><span class="sxs-lookup"><span data-stu-id="4d376-887">With <xref:System.AppContext>, libraries define and expose compatibility switches, while code that depends on them can set those switches to affect the library behavior.</span></span> <span data-ttu-id="4d376-888">默认情况下，库提供新功能；如果设置了开关，则只更改新功能（即，它们提供以前的功能）。</span><span class="sxs-lookup"><span data-stu-id="4d376-888">By default, libraries provide the new functionality, and they only alter it (that is, they provide the previous functionality) if the switch is set.</span></span>

    <span data-ttu-id="4d376-889">应用程序（或库）可以声明相关库定义的开关的值（始终是 <xref:System.Boolean> 值）。</span><span class="sxs-lookup"><span data-stu-id="4d376-889">An application (or a library) can declare the value of a switch (which is always a <xref:System.Boolean> value) that a dependent library defines.</span></span> <span data-ttu-id="4d376-890">该开关始终隐式 `false`。</span><span class="sxs-lookup"><span data-stu-id="4d376-890">The switch is always implicitly `false`.</span></span> <span data-ttu-id="4d376-891">将此开关设置为 `true` 将启用它。</span><span class="sxs-lookup"><span data-stu-id="4d376-891">Setting the switch to `true` enables it.</span></span> <span data-ttu-id="4d376-892">将此开关显式设置为 `false` 将提供新行为。</span><span class="sxs-lookup"><span data-stu-id="4d376-892">Explicitly setting the switch to `false` provides the new behavior.</span></span>

    ```csharp
    AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", true);
    ```

    ```vb
    AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", True)
    ```

    <span data-ttu-id="4d376-893">库必须检查使用者是否已声明该开关的值，并且相应地作用于它。</span><span class="sxs-lookup"><span data-stu-id="4d376-893">The library must check if a consumer has declared the value of the switch and then appropriately act on it.</span></span>

    ```csharp
    if (!AppContext.TryGetSwitch("Switch.AmazingLib.ThrowOnException", out shouldThrow))
    {
        // This is the case where the switch value was not set by the application.
        // The library can choose to get the value of shouldThrow by other means.
        // If no overrides nor default values are specified, the value should be 'false'.
        // A false value implies the latest behavior.
    }

    // The library can use the value of shouldThrow to throw exceptions or not.
    if (shouldThrow)
    {
        // old code
    }
    else
    {
        // new code
    }
    ```

    ```vb
    If Not AppContext.TryGetSwitch("Switch.AmazingLib.ThrowOnException", shouldThrow) Then
        ' This is the case where the switch value was not set by the application.
        ' The library can choose to get the value of shouldThrow by other means.
        ' If no overrides nor default values are specified, the value should be 'false'.
        ' A false value implies the latest behavior.
    End If

    ' The library can use the value of shouldThrow to throw exceptions or not.
    If shouldThrow Then
        ' old code
    Else
        ' new code
    End If
    ```

    <span data-ttu-id="4d376-894">使用一致的开关格式是有益的，因为它们是由库公开的正式协定。</span><span class="sxs-lookup"><span data-stu-id="4d376-894">It's beneficial to use a consistent format for switches, since they are a formal contract exposed by a library.</span></span> <span data-ttu-id="4d376-895">以下是两种明显的格式。</span><span class="sxs-lookup"><span data-stu-id="4d376-895">The following are two obvious formats.</span></span>

    - <span data-ttu-id="4d376-896">*Switch* . *namespace* . *switchname*</span><span class="sxs-lookup"><span data-stu-id="4d376-896">*Switch* . *namespace* . *switchname*</span></span>

    - <span data-ttu-id="4d376-897">*Switch* . *library* . *switchname*</span><span class="sxs-lookup"><span data-stu-id="4d376-897">*Switch* . *library* . *switchname*</span></span>

  - <span data-ttu-id="4d376-898">**更改为基于任务的异步模式 (TAP)**</span><span class="sxs-lookup"><span data-stu-id="4d376-898">**Changes to the task-based asynchronous pattern (TAP)**</span></span>

    <span data-ttu-id="4d376-899">对于面向 .NET Framework 4.6、<xref:System.Threading.Tasks.Task> 和 <xref:System.Threading.Tasks.Task%601> 对象的应用，请继承调用线程的区域性和 UI 区域性。</span><span class="sxs-lookup"><span data-stu-id="4d376-899">For apps that target .NET Framework 4.6, <xref:System.Threading.Tasks.Task> and <xref:System.Threading.Tasks.Task%601> objects inherit the culture and UI culture of the calling thread.</span></span> <span data-ttu-id="4d376-900">面向早期 .NET Framework 版本或不面向特定版本的 .NET Framework 的应用的行为不受影响。</span><span class="sxs-lookup"><span data-stu-id="4d376-900">The behavior of apps that target previous versions of .NET Framework, or that do not target a specific version of .NET Framework, is unaffected.</span></span> <span data-ttu-id="4d376-901">有关详细信息，请参阅 <xref:System.Globalization.CultureInfo> 类主题中的“区域性和基于任务的异步操作”一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-901">For more information, see the "Culture and task-based asynchronous operations" section of the <xref:System.Globalization.CultureInfo> class topic.</span></span>

    <span data-ttu-id="4d376-902"><xref:System.Threading.AsyncLocal%601?displayProperty=nameWithType> 类允许你表示对于给定异步控制流（如 `async` 方法）来说是本地数据的环境数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-902">The <xref:System.Threading.AsyncLocal%601?displayProperty=nameWithType> class allows you to represent ambient data that is local to a given asynchronous control flow, such as an `async` method.</span></span> <span data-ttu-id="4d376-903">它可用于跨线程保存数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-903">It can be used to persist data across threads.</span></span> <span data-ttu-id="4d376-904">你还可以定义一个回调方法，该回调方法在环境数据发生变化时就会发出通知，而不论环境数据发生变化的原因是 <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=nameWithType> 属性显式更改还是线程遇到上下文转换。</span><span class="sxs-lookup"><span data-stu-id="4d376-904">You can also define a callback method that is notified whenever the ambient data changes either because the <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=nameWithType> property was explicitly changed, or because the thread encountered a context transition.</span></span>

    <span data-ttu-id="4d376-905">三种便利方法（<xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=nameWithType>、<xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=nameWithType>）已添加到基于任务的异步模式 (TAP)，以返回处于特定状态的已完成任务。</span><span class="sxs-lookup"><span data-stu-id="4d376-905">Three convenience methods, <xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=nameWithType>, and <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=nameWithType>, have been added to the task-based asynchronous pattern (TAP) to return completed tasks in a particular state.</span></span>

    <span data-ttu-id="4d376-906"><xref:System.IO.Pipes.NamedPipeClientStream> 类现在支持与其新的 <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A> 进行异步通信。</span><span class="sxs-lookup"><span data-stu-id="4d376-906">The <xref:System.IO.Pipes.NamedPipeClientStream> class now supports asynchronous communication with its new <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A>.</span></span> <span data-ttu-id="4d376-907">方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-907">method.</span></span>

  - <span data-ttu-id="4d376-908">**EventSource 现在支持写入事件日志**</span><span class="sxs-lookup"><span data-stu-id="4d376-908">**EventSource now supports writing to the Event log**</span></span>

    <span data-ttu-id="4d376-909">除了在计算机上创建的任何现有 ETW 会话外，现在你还可以使用 <xref:System.Diagnostics.Tracing.EventSource> 类将管理或操作消息记录到事件日志中。</span><span class="sxs-lookup"><span data-stu-id="4d376-909">You now can use the <xref:System.Diagnostics.Tracing.EventSource> class to log administrative or operational messages to the event log, in addition to any existing ETW sessions created on the machine.</span></span> <span data-ttu-id="4d376-910">在过去，你必须使用 Microsoft.Diagnostics.Tracing.EventSource NuGet 包才能实现此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-910">In the past, you had to use the Microsoft.Diagnostics.Tracing.EventSource NuGet package for this functionality.</span></span> <span data-ttu-id="4d376-911">此功能现在内置于 .NET Framework 4.6 中。</span><span class="sxs-lookup"><span data-stu-id="4d376-911">This functionality is now built-into .NET Framework 4.6.</span></span>

    <span data-ttu-id="4d376-912">NuGet 包和 .NET Framework 4.6 都更新了以下功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-912">Both the NuGet package and .NET Framework 4.6 have been updated with the following features:</span></span>

    - <span data-ttu-id="4d376-913">**动态事件**</span><span class="sxs-lookup"><span data-stu-id="4d376-913">**Dynamic events**</span></span>

      <span data-ttu-id="4d376-914">允许在不创建事件方法的情况下“在运行过程中”定义事件。</span><span class="sxs-lookup"><span data-stu-id="4d376-914">Allows events defined "on the fly" without creating event methods.</span></span>

    - <span data-ttu-id="4d376-915">**丰富的负载**</span><span class="sxs-lookup"><span data-stu-id="4d376-915">**Rich payloads**</span></span>

      <span data-ttu-id="4d376-916">允许将专门特性化的类和数组以及基元类型作为负载传递</span><span class="sxs-lookup"><span data-stu-id="4d376-916">Allows specially attributed classes and arrays as well as primitive types to be passed as a payload</span></span>

    - <span data-ttu-id="4d376-917">**活动跟踪**</span><span class="sxs-lookup"><span data-stu-id="4d376-917">**Activity tracking**</span></span>

      <span data-ttu-id="4d376-918">使“开始”和“停止”事件用 ID 标记在它们之间发生的事件，以表示当前处于活动状态的所有活动。</span><span class="sxs-lookup"><span data-stu-id="4d376-918">Causes Start and Stop events to tag events between them with an ID that represents all currently active activities.</span></span>

    <span data-ttu-id="4d376-919">为了支持这些功能，已将重载的 <xref:System.Diagnostics.Tracing.EventSource.Write%2A> 方法添加到了 <xref:System.Diagnostics.Tracing.EventSource> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-919">To support these features, the overloaded <xref:System.Diagnostics.Tracing.EventSource.Write%2A> method has been added to the <xref:System.Diagnostics.Tracing.EventSource> class.</span></span>

- <span data-ttu-id="4d376-920">**Windows Presentation Foundation (WPF)**</span><span class="sxs-lookup"><span data-stu-id="4d376-920">**Windows Presentation Foundation (WPF)**</span></span>

  - <span data-ttu-id="4d376-921">**HDPI 改进**</span><span class="sxs-lookup"><span data-stu-id="4d376-921">**HDPI improvements**</span></span>

    <span data-ttu-id="4d376-922">在 .NET Framework 4.6 中，WPF 现提供更出色的 HDPI 支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-922">HDPI support in WPF is now better in .NET Framework 4.6.</span></span> <span data-ttu-id="4d376-923">已对布局舍入进行了更改，以减少带边框的控件中的剪切实例。</span><span class="sxs-lookup"><span data-stu-id="4d376-923">Changes have been made to layout rounding to reduce instances of clipping in controls with borders.</span></span> <span data-ttu-id="4d376-924">默认情况下，仅当你的 <xref:System.Runtime.Versioning.TargetFrameworkAttribute> 设置为 .NET 4.6 时才启用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-924">By default, this feature is enabled only if your <xref:System.Runtime.Versioning.TargetFrameworkAttribute> is set to .NET 4.6.</span></span>  <span data-ttu-id="4d376-925">对于面向旧版 Framework，但在 .NET Framework 4.6 上运行的应用程序，可通过在 app.config 文件的 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 部分中添加下面的代码行，选择启用新行为：</span><span class="sxs-lookup"><span data-stu-id="4d376-925">Applications that target earlier versions of the framework but are running on .NET Framework 4.6 can opt in to the new behavior by adding the following line to the [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) section of the app.config file:</span></span>

    ```xml
    <AppContextSwitchOverrides
    value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false"
    />
    ```

    <span data-ttu-id="4d376-926">跨越具有不同 DPI 设置（多 DPI 设置）的多个监视器的 WPF 窗口现在完全呈现，且没有涂黑区域。</span><span class="sxs-lookup"><span data-stu-id="4d376-926">WPF windows straddling multiple monitors with different DPI settings (Multi-DPI setup) are now completely rendered without blacked-out regions.</span></span> <span data-ttu-id="4d376-927">可以通过将下面的行添加到 app.config 文件的 `<appSettings>` 部分来选择退出此行为，以禁用此新行为：</span><span class="sxs-lookup"><span data-stu-id="4d376-927">You can opt out of this behavior by adding the following line to the `<appSettings>` section of the app.config file to disable this new behavior:</span></span>

    ```xml
    <add key="EnableMultiMonitorDisplayClipping" value="true"/>
    ```

    <span data-ttu-id="4d376-928">已向 <xref:System.Windows.Input.Cursor?displayProperty=nameWithType> 添加了对基于 DPI 设置自动加载右侧光标的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-928">Support for automatically loading the right cursor based on DPI setting has been added to  <xref:System.Windows.Input.Cursor?displayProperty=nameWithType>.</span></span>

  - <span data-ttu-id="4d376-929">**触摸更好**</span><span class="sxs-lookup"><span data-stu-id="4d376-929">**Touch is better**</span></span>

    <span data-ttu-id="4d376-930">在 .NET Framework 4.6 中，客户在 [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) 中报告的触控服务导致不可预测行为发生的问题得到了解决。</span><span class="sxs-lookup"><span data-stu-id="4d376-930">Customer reports on [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) that touch produces unpredictable behavior have been addressed in .NET Framework 4.6.</span></span> <span data-ttu-id="4d376-931">Windows 应用商店应用程序和 WPF 应用程序的双击阈值现在与 Windows 8.1 及更高版本中的相同。</span><span class="sxs-lookup"><span data-stu-id="4d376-931">The double tap threshold for Windows Store applications and WPF applications is now the same in Windows 8.1 and above.</span></span>

  - <span data-ttu-id="4d376-932">**透明子窗口支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-932">**Transparent child window support**</span></span>

    <span data-ttu-id="4d376-933">.NET Framework 4.6 中的 WPF 支持在 Windows 8.1 及更高版本中使用透明子窗口。</span><span class="sxs-lookup"><span data-stu-id="4d376-933">WPF in .NET Framework 4.6 supports transparent child windows in Windows 8.1 and above.</span></span> <span data-ttu-id="4d376-934">这使得你可以在顶层窗口中创建非矩形的透明子窗口。</span><span class="sxs-lookup"><span data-stu-id="4d376-934">This allows you to create non-rectangular and transparent child windows in your top-level windows.</span></span> <span data-ttu-id="4d376-935">你可以通过将 <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=nameWithType> 属性设置为 `true` 启用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-935">You can enable this feature by setting the <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=nameWithType> property to `true`.</span></span>

- <span data-ttu-id="4d376-936">**Windows Communication Foundation (WCF)**</span><span class="sxs-lookup"><span data-stu-id="4d376-936">**Windows Communication Foundation (WCF)**</span></span>

  - <span data-ttu-id="4d376-937">**SSL 支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-937">**SSL support**</span></span>

    <span data-ttu-id="4d376-938">将 NetTcp 用于传输安全和客户端身份验证时，除了 SSL 3.0 和 TLS 1.0，WCF 现在还支持 SSL 版本 TLS 1.1 和 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="4d376-938">WCF now supports SSL version TLS 1.1 and TLS 1.2, in addition to SSL 3.0 and TLS 1.0, when using NetTcp with transport security and client authentication.</span></span> <span data-ttu-id="4d376-939">现在可选择要使用的协议，或禁用旧的次要安全协议。</span><span class="sxs-lookup"><span data-stu-id="4d376-939">It is now possible to select which protocol to use, or to disable old lesser secure protocols.</span></span> <span data-ttu-id="4d376-940">可以通过设置 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> 属性或通过将以下内容添加到配置文件来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="4d376-940">This can be done either by setting the <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> property or by adding the following to a configuration file.</span></span>

    ```xml
    <netTcpBinding>
        <binding>
          <security mode= "None|Transport|Message|TransportWithMessageCredential" >
              <transport clientCredentialType="None|Windows|Certificate"
                        protectionLevel="None|Sign|EncryptAndSign"
                        sslProtocols="Ssl3|Tls1|Tls11|Tls12">
                </transport>
          </security>
        </binding>
    </netTcpBinding>
    ```

  - <span data-ttu-id="4d376-941">**使用不同的 HTTP 连接发送消息**</span><span class="sxs-lookup"><span data-stu-id="4d376-941">**Sending messages using different HTTP connections**</span></span>

    <span data-ttu-id="4d376-942">WCF 现在允许用户确保使用不同的基础 HTTP 连接发送特定消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-942">WCF now allows users to ensure certain messages are sent using different underlying HTTP connections.</span></span> <span data-ttu-id="4d376-943">有两种方法可以实现此目的：</span><span class="sxs-lookup"><span data-stu-id="4d376-943">There are two ways to do this:</span></span>

    - <span data-ttu-id="4d376-944">**使用连接组名称前缀**</span><span class="sxs-lookup"><span data-stu-id="4d376-944">**Using a connection group name prefix**</span></span>

      <span data-ttu-id="4d376-945">用户可以指定 WCF 将用作连接组名称前缀的字符串。</span><span class="sxs-lookup"><span data-stu-id="4d376-945">Users can specify a string that WCF will use as a prefix for the connection group name.</span></span> <span data-ttu-id="4d376-946">使用不同的基础 HTTP 连接发送具有不同前缀的两个消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-946">Two messages with different prefixes are sent using different underlying HTTP connections.</span></span> <span data-ttu-id="4d376-947">通过将键/值对添加到消息的 <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=nameWithType> 属性来设置前缀。</span><span class="sxs-lookup"><span data-stu-id="4d376-947">You set the prefix by adding a key/value pair to the message's <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="4d376-948">键是“HttpTransportConnectionGroupNamePrefix”，值是所需的前缀。</span><span class="sxs-lookup"><span data-stu-id="4d376-948">The key is "HttpTransportConnectionGroupNamePrefix"; the value is the desired prefix.</span></span>

    - <span data-ttu-id="4d376-949">**使用不同的通道工厂**</span><span class="sxs-lookup"><span data-stu-id="4d376-949">**Using different channel factories**</span></span>

      <span data-ttu-id="4d376-950">用户还可以启用一种功能，以确保使用由不同通道工厂所创建通道发送的消息将使用不同的基础 HTTP 连接。</span><span class="sxs-lookup"><span data-stu-id="4d376-950">Users can also enable a feature that ensures that messages sent using channels created by different channel factories will use different underlying HTTP connections.</span></span> <span data-ttu-id="4d376-951">若要启用此功能，用户必须将以下 `appSetting` 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="4d376-951">To enable this feature, users must set the following `appSetting` to `true`:</span></span>

      ```xml
      <appSettings>
          <add key="wcf:httpTransportBinding:useUniqueConnectionPoolPerFactory" value="true" />
      </appSettings>
      ```

- <span data-ttu-id="4d376-952">**Windows Workflow Foundation (WWF)**</span><span class="sxs-lookup"><span data-stu-id="4d376-952">**Windows Workflow Foundation (WWF)**</span></span>

  <span data-ttu-id="4d376-953">现在可以指定当请求超时之前存在某个未完成的“非协议”书签时，工作流服务针对无序操作请求将保持的秒数。</span><span class="sxs-lookup"><span data-stu-id="4d376-953">You can now specify the number of seconds a workflow service will hold on to an out-of-order operation request when there is an outstanding "non-protocol" bookmark before timing out the request.</span></span> <span data-ttu-id="4d376-954">“非协议”书签是不与未完成的“接收”活动相关的书签。</span><span class="sxs-lookup"><span data-stu-id="4d376-954">A "non-protocol" bookmark is a bookmark that is not related to outstanding Receive activities.</span></span> <span data-ttu-id="4d376-955">某些活动会在其实现内创建非协议书签，因此非协议书签的存在可能不太明显。</span><span class="sxs-lookup"><span data-stu-id="4d376-955">Some activities create non-protocol bookmarks within their implementation, so it may not be obvious that a non-protocol bookmark exists.</span></span> <span data-ttu-id="4d376-956">此类书签包括“状态”和“选取”。</span><span class="sxs-lookup"><span data-stu-id="4d376-956">These include State and Pick.</span></span> <span data-ttu-id="4d376-957">因此，如果你拥有使用状态机实现的工作流服务，或包含“选取”活动的工作流服务，你将很可能具有非协议书签。</span><span class="sxs-lookup"><span data-stu-id="4d376-957">So if you have a workflow service implemented with a state machine or containing a Pick activity, you will most likely have non-protocol bookmarks.</span></span> <span data-ttu-id="4d376-958">通过将如下所示的行添加到 app.config 文件的 `appSettings` 部分来指定时间间隔：</span><span class="sxs-lookup"><span data-stu-id="4d376-958">You specify the interval by adding a line like the following to the `appSettings` section of your app.config file:</span></span>

  ```xml
  <add key="microsoft:WorkflowServices:FilterResumeTimeoutInSeconds" value="60"/>
  ```

  <span data-ttu-id="4d376-959">默认值为 60 秒。</span><span class="sxs-lookup"><span data-stu-id="4d376-959">The default value is 60 seconds.</span></span> <span data-ttu-id="4d376-960">如果 `value` 设置为 0，则会立即拒绝无序请求并出现错误，错误文本如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d376-960">If `value` is set to 0, out-of-order requests are immediately rejected with a fault with text that looks like this:</span></span>

  ```console
  Operation 'Request3|{http://tempuri.org/}IService' on service instance with identifier '2b0667b6-09c8-4093-9d02-f6c67d534292' cannot be performed at this time. Please ensure that the operations are performed in the correct order and that the binding in use provides ordered delivery guarantees.
  ```

  <span data-ttu-id="4d376-961">当收到无序操作消息且没有非协议书签时，你将收到同一条消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-961">This is the same message that you receive if an out-of-order operation message is received and there are no non-protocol bookmarks.</span></span>

  <span data-ttu-id="4d376-962">如果 `FilterResumeTimeoutInSeconds` 元素的值为非零，且没有非协议书签并且超时间隔过期，则操作失败并出现超时消息。</span><span class="sxs-lookup"><span data-stu-id="4d376-962">If the value of the `FilterResumeTimeoutInSeconds` element is non-zero, there are non-protocol bookmarks, and the timeout interval expires, the operation fails with a timeout message.</span></span>

- <span data-ttu-id="4d376-963">**事务**</span><span class="sxs-lookup"><span data-stu-id="4d376-963">**Transactions**</span></span>

  <span data-ttu-id="4d376-964">你现在可以包含事务的分布式事务标识符，该事务导致了引发派生自 <xref:System.Transactions.TransactionException> 的异常。</span><span class="sxs-lookup"><span data-stu-id="4d376-964">You can now include the distributed transaction identifier for the transaction that has caused an exception derived from <xref:System.Transactions.TransactionException> to be thrown.</span></span> <span data-ttu-id="4d376-965">通过将以下键添加到 app.config 文件的 `appSettings` 部分来完成此操作：</span><span class="sxs-lookup"><span data-stu-id="4d376-965">You do this by adding the following key to the `appSettings` section of your app.config file:</span></span>

  ```xml
  <add key="Transactions:IncludeDistributedTransactionIdInExceptionMessage" value="true"/>
  ```

  <span data-ttu-id="4d376-966">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="4d376-966">The default value is `false`.</span></span>

- <span data-ttu-id="4d376-967">**网络连接**</span><span class="sxs-lookup"><span data-stu-id="4d376-967">**Networking**</span></span>

  - <span data-ttu-id="4d376-968">**套接字重用**</span><span class="sxs-lookup"><span data-stu-id="4d376-968">**Socket reuse**</span></span>

    <span data-ttu-id="4d376-969">Windows 10 包括一个新的高可伸缩性网络算法，它能通过重用出站 TCP 连接的本地端口来更好地利用计算机资源。</span><span class="sxs-lookup"><span data-stu-id="4d376-969">Windows 10 includes a new high-scalability networking algorithm that makes better use of machine resources by reusing local ports for outbound TCP connections.</span></span> <span data-ttu-id="4d376-970">.NET Framework 4.6 支持新算法，这使得 .NET 应用可以充分利用新的行为。</span><span class="sxs-lookup"><span data-stu-id="4d376-970">.NET Framework 4.6 supports the new algorithm, enabling .NET apps to take advantage of the new behavior.</span></span> <span data-ttu-id="4d376-971">在以前版本的 Windows 中，有人工并发连接限制（通常为 16,384，即动态端口范围的默认大小），这可能导致负载下的端口耗尽，从而限制了服务的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="4d376-971">In previous versions of Windows, there was an artificial concurrent connection limit (typically 16,384, the default size of the dynamic port range), which could limit the scalability of a service by causing port exhaustion when under load.</span></span>

    <span data-ttu-id="4d376-972">在 .NET Framework 4.6 中，添加了两个 API，用于启用端口重用，有效撤消了并发连接方面的 64 KB 限制：</span><span class="sxs-lookup"><span data-stu-id="4d376-972">In .NET Framework 4.6, two APIs have been added to enable port reuse, which effectively removes the 64 KB limit on concurrent connections:</span></span>

    - <span data-ttu-id="4d376-973"><xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> 枚举值。</span><span class="sxs-lookup"><span data-stu-id="4d376-973">The <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> enumeration value.</span></span>

    - <span data-ttu-id="4d376-974"><xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="4d376-974">The <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> property.</span></span>

    <span data-ttu-id="4d376-975">默认情况下，<xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> 属性为 `false`，除非 `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` 注册表项的 `HWRPortReuseOnSocketBind` 值设置为 0x1。</span><span class="sxs-lookup"><span data-stu-id="4d376-975">By default, the <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> property is `false` unless the `HWRPortReuseOnSocketBind` value of the `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` registry key is set to 0x1.</span></span> <span data-ttu-id="4d376-976">若要对 HTTP 连接启用本地端口重用，请将 <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> 属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="4d376-976">To enable local port reuse on HTTP connections, set the <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> property to `true`.</span></span> <span data-ttu-id="4d376-977">这将导致来自 <xref:System.Net.Http.HttpClient> 和 <xref:System.Net.HttpWebRequest> 的所有传出 TCP 套接字连接使用新的 Windows 10 套接字选项 [SO_REUSE_UNICASTPORT](/windows/desktop/WinSock/sol-socket-socket-options)，该选项将启用本地端口重用。</span><span class="sxs-lookup"><span data-stu-id="4d376-977">This causes all outgoing TCP socket connections from <xref:System.Net.Http.HttpClient> and <xref:System.Net.HttpWebRequest> to use a new Windows 10 socket option, [SO_REUSE_UNICASTPORT](/windows/desktop/WinSock/sol-socket-socket-options), that enables local port reuse.</span></span>

    <span data-ttu-id="4d376-978">调用 <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=nameWithType> 等方法时，编写仅限套接字的应用程序的开发人员可以指定 <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> 选项，以便出站套接字在绑定期间重用本地端口。</span><span class="sxs-lookup"><span data-stu-id="4d376-978">Developers writing a sockets-only application can specify the <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> option when calling a method such as <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=nameWithType> so that outbound sockets reuse local ports during binding.</span></span>

  - <span data-ttu-id="4d376-979">**对国际域名和 PunyCode 的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-979">**Support for international domain names and PunyCode**</span></span>

    <span data-ttu-id="4d376-980">一个新属性 <xref:System.Uri.IdnHost%2A> 已添加到了 <xref:System.Uri> 类，以更好地支持国际域名和 PunyCode。</span><span class="sxs-lookup"><span data-stu-id="4d376-980">A new property, <xref:System.Uri.IdnHost%2A>, has been added to the <xref:System.Uri> class to better support international domain names and PunyCode.</span></span>

- <span data-ttu-id="4d376-981">**在 Windows 窗体控件中调整大小。**</span><span class="sxs-lookup"><span data-stu-id="4d376-981">**Resizing in Windows Forms controls.**</span></span>

  <span data-ttu-id="4d376-982">此功能已在 .NET Framework 4.6 中展开，以包括绘制 <xref:System.Drawing.Design.UITypeEditor> 时所使用的 <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> 属性所指定的 <xref:System.Windows.Forms.DomainUpDown><xref:System.Windows.Forms.NumericUpDown><xref:System.Windows.Forms.DataGridViewComboBoxColumn><xref:System.Windows.Forms.DataGridViewColumn> 和 <xref:System.Windows.Forms.ToolStripSplitButton> 类型和矩形。</span><span class="sxs-lookup"><span data-stu-id="4d376-982">This feature has been expanded in .NET Framework 4.6 to include the <xref:System.Windows.Forms.DomainUpDown>, <xref:System.Windows.Forms.NumericUpDown>, <xref:System.Windows.Forms.DataGridViewComboBoxColumn>, <xref:System.Windows.Forms.DataGridViewColumn> and <xref:System.Windows.Forms.ToolStripSplitButton> types and the rectangle specified by the <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> property used when drawing a <xref:System.Drawing.Design.UITypeEditor>.</span></span>

  <span data-ttu-id="4d376-983">这是一项可以选择使用的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-983">This is an opt-in feature.</span></span> <span data-ttu-id="4d376-984">若要启用它，在应用程序配置 (app.config) 文件中将 `EnableWindowsFormsHighDpiAutoResizing` 元素设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="4d376-984">To enable it, set the `EnableWindowsFormsHighDpiAutoResizing` element to `true` in the application configuration (app.config) file:</span></span>

  ```xml
  <appSettings>
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
  </appSettings>
  ```

- <span data-ttu-id="4d376-985">**对代码页编码的支持**</span><span class="sxs-lookup"><span data-stu-id="4d376-985">**Support for code page encodings**</span></span>

  <span data-ttu-id="4d376-986">.NET Core 主要支持 Unicode 编码，在代码页编码方面默认提供一定程度的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-986">.NET Core primarily supports the Unicode encodings and by default provides limited support for code page encodings.</span></span> <span data-ttu-id="4d376-987">可以使用 <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=nameWithType> 方法注册代码页编码，从而支持 .NET Framework 可用但 .NET Core 不支持的代码页编码。</span><span class="sxs-lookup"><span data-stu-id="4d376-987">You can add support for code page encodings available in .NET Framework but unsupported in .NET Core by registering code page encodings with the <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d376-988">有关详细信息，请参阅 <xref:System.Text.CodePagesEncodingProvider?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="4d376-988">For more information, see <xref:System.Text.CodePagesEncodingProvider?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="4d376-989">**.NET Native**</span><span class="sxs-lookup"><span data-stu-id="4d376-989">**.NET Native**</span></span>

  <span data-ttu-id="4d376-990">定位 .NET Core 且用 C# 或 Visual Basic 编写的 Windows 10 相关 Windows 应用程序可以利用将应用程序编译为本机代码（而非 IL）的新技术。</span><span class="sxs-lookup"><span data-stu-id="4d376-990">Windows apps for Windows 10 that target .NET Core and are written in C# or Visual Basic can take advantage of a new technology that compiles apps to native code rather than IL.</span></span> <span data-ttu-id="4d376-991">它们所生成的应用程序具有启动和执行时间更快速的特点。</span><span class="sxs-lookup"><span data-stu-id="4d376-991">They produce apps characterized by faster startup and execution times.</span></span> <span data-ttu-id="4d376-992">有关详细信息，请参阅[使用 .NET Native 编译应用](../net-native/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-992">For more information, see [Compiling Apps with .NET Native](../net-native/index.md).</span></span> <span data-ttu-id="4d376-993">有关探讨与 JIT 编译和 NGEN 的差别以及对你的代码的意义的 .NET Native 概述，请参阅 [.NET Native 和编译](../net-native/net-native-and-compilation.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-993">For an overview of .NET Native that examines how it differs from both JIT compilation and NGEN and what that means for your code, see [.NET Native and Compilation](../net-native/net-native-and-compilation.md).</span></span>

  <span data-ttu-id="4d376-994">使用 Visual Studio 2015 或更高版本进行编译时，默认将应用程序编译为本机代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-994">Your apps are compiled to native code by default when you compile them with Visual Studio 2015 or later.</span></span> <span data-ttu-id="4d376-995">有关详细信息，请参阅 [.NET Native 入门](../net-native/getting-started-with-net-native.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-995">For more information, see [Getting Started with .NET Native](../net-native/getting-started-with-net-native.md).</span></span>

  <span data-ttu-id="4d376-996">为了支持调试 .NET Native 应用，已向非托管调试 API 添加大量新的接口和枚举。</span><span class="sxs-lookup"><span data-stu-id="4d376-996">To support debugging .NET Native apps, a number of new interfaces and enumerations have been added to the unmanaged debugging API.</span></span> <span data-ttu-id="4d376-997">有关详细信息，请参阅[调试（非托管 API 参考）](../unmanaged-api/debugging/index.md)主题。</span><span class="sxs-lookup"><span data-stu-id="4d376-997">For more information, see the [Debugging (Unmanaged API Reference)](../unmanaged-api/debugging/index.md) topic.</span></span>

- <span data-ttu-id="4d376-998">**开放源代码 .NET Framework 包**</span><span class="sxs-lookup"><span data-stu-id="4d376-998">**Open-source .NET Framework packages**</span></span>

  <span data-ttu-id="4d376-999">.NET Core 包（如不可变集合）、[SIMD API](https://www.nuget.org/packages/Microsoft.Bcl.Simd) 以及网络 API（如在 <xref:System.Net.Http> 命名空间中找到的网络 API）现在都可在 [GitHub](https://github.com/) 上用作开放源代码程序包。</span><span class="sxs-lookup"><span data-stu-id="4d376-999">.NET Core packages such as the immutable collections, [SIMD APIs](https://www.nuget.org/packages/Microsoft.Bcl.Simd), and networking APIs such as those found in the <xref:System.Net.Http> namespace are now available as open-source packages on [GitHub](https://github.com/).</span></span> <span data-ttu-id="4d376-1000">要访问代码，请参阅 [GitHub 上的 .NET](https://github.com/dotnet/runtime)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1000">To access the code, see [.NET on GitHub](https://github.com/dotnet/runtime).</span></span> <span data-ttu-id="4d376-1001">有关详细信息以及如何参与这些包，请参阅 [.NET Core 和开放源代码](../get-started/net-core-and-open-source.md)、[GitHub 上的 .NET 主页](https://github.com/dotnet/home)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1001">For more information and how to contribute to these packages, see [.NET Core and Open-Source](../get-started/net-core-and-open-source.md), [.NET Home Page on GitHub](https://github.com/dotnet/home).</span></span>

<a name="v452"></a>

## <a name="whats-new-in-net-framework-452"></a><span data-ttu-id="4d376-1002">.NET Framework 4.5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-1002">What's new in .NET Framework 4.5.2</span></span>

- <span data-ttu-id="4d376-1003">**ASP.NET 应用的新 API。**</span><span class="sxs-lookup"><span data-stu-id="4d376-1003">**New APIs for ASP.NET apps.**</span></span> <span data-ttu-id="4d376-1004">新的 <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=nameWithType> 和 <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=nameWithType> 方法使你可以在响应刷新到客户端应用时检查并修改响应标头和状态代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-1004">The new <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=nameWithType> and <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=nameWithType> methods let you inspect and modify response headers and status code as the response is being flushed to the client app.</span></span> <span data-ttu-id="4d376-1005">考虑使用这些方法，而不是 <xref:System.Web.HttpApplication.PreSendRequestHeaders> 和 <xref:System.Web.HttpApplication.PreSendRequestContent> 事件；它们更为高效可靠。</span><span class="sxs-lookup"><span data-stu-id="4d376-1005">Consider using these methods instead of the <xref:System.Web.HttpApplication.PreSendRequestHeaders> and <xref:System.Web.HttpApplication.PreSendRequestContent> events; they are more efficient and reliable.</span></span>

  <span data-ttu-id="4d376-1006"><xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=nameWithType> 方法使你可以规划小型后台工作项目。</span><span class="sxs-lookup"><span data-stu-id="4d376-1006">The <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=nameWithType> method lets you schedule small background work items.</span></span> <span data-ttu-id="4d376-1007">ASP.NET 跟踪这些项目，并防止 IIS 在所有后台工作项目完成之前突然中止辅助进程。</span><span class="sxs-lookup"><span data-stu-id="4d376-1007">ASP.NET tracks these items and prevents IIS from abruptly terminating the worker process until all background work items have completed.</span></span> <span data-ttu-id="4d376-1008">无法在 ASP.NET 托管的应用域之外调用此方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-1008">This method can't be called outside an ASP.NET managed app domain.</span></span>

  <span data-ttu-id="4d376-1009">新的 <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=nameWithType> 和 <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=nameWithType> 属性返回用于指示是否已编写响应标头的布尔值。</span><span class="sxs-lookup"><span data-stu-id="4d376-1009">The new <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=nameWithType> and <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=nameWithType> properties return Boolean values that indicate whether the response headers have been written.</span></span> <span data-ttu-id="4d376-1010">你可以使用这些属性确保对诸如 <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=nameWithType>（如果已编写标头，它将引发异常）等 API 的调用将成功。</span><span class="sxs-lookup"><span data-stu-id="4d376-1010">You can use these properties to make sure that calls to APIs such as <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=nameWithType> (which throw exceptions if the headers have been written) will succeed.</span></span>

- <span data-ttu-id="4d376-1011">**在 Windows 窗体控件中调整大小。**</span><span class="sxs-lookup"><span data-stu-id="4d376-1011">**Resizing in Windows Forms controls.**</span></span> <span data-ttu-id="4d376-1012">此功能已扩展。</span><span class="sxs-lookup"><span data-stu-id="4d376-1012">This feature has been expanded.</span></span> <span data-ttu-id="4d376-1013">你现在可以使用系统 DPI 设置调整下面其他控件的组件大小（例如，组合框中的下拉箭头）：</span><span class="sxs-lookup"><span data-stu-id="4d376-1013">You can now use the system DPI setting to resize components of the following additional controls (for example, the drop-down arrow in combo boxes):</span></span>

  - <xref:System.Windows.Forms.ComboBox>
  - <xref:System.Windows.Forms.ToolStripComboBox>
  - <xref:System.Windows.Forms.ToolStripMenuItem>
  - <xref:System.Windows.Forms.Cursor>
  - <xref:System.Windows.Forms.DataGridView>
  - <xref:System.Windows.Forms.DataGridViewComboBoxColumn>

  <span data-ttu-id="4d376-1014">这是一项可以选择使用的功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1014">This is an opt-in feature.</span></span> <span data-ttu-id="4d376-1015">若要启用它，在应用程序配置 (app.config) 文件中将 `EnableWindowsFormsHighDpiAutoResizing` 元素设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="4d376-1015">To enable it, set the `EnableWindowsFormsHighDpiAutoResizing` element to `true` in the application configuration (app.config) file:</span></span>

  ```xml
  <appSettings>
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
  </appSettings>
  ```

- <span data-ttu-id="4d376-1016">**新工作流功能。**</span><span class="sxs-lookup"><span data-stu-id="4d376-1016">**New workflow feature.**</span></span> <span data-ttu-id="4d376-1017">使用 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> 方法（并且因此实现 <xref:System.Transactions.IPromotableSinglePhaseNotification> 接口）的资源管理器可以使用新的 <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> 方法来请求以下内容：</span><span class="sxs-lookup"><span data-stu-id="4d376-1017">A resource manager that's using the <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> method (and therefore implementing the <xref:System.Transactions.IPromotableSinglePhaseNotification> interface) can use the new <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> method to request the following:</span></span>

  - <span data-ttu-id="4d376-1018">将该事物提升为 Microsoft 分布式事务处理协调器 (MSDTC) 事物。</span><span class="sxs-lookup"><span data-stu-id="4d376-1018">Promote the transaction to a Microsoft Distributed Transaction Coordinator (MSDTC) transaction.</span></span>

  - <span data-ttu-id="4d376-1019">使用 <xref:System.Transactions.IPromotableSinglePhaseNotification> 替换 <xref:System.Transactions.ISinglePhaseNotification>，它是支持单阶段提交的持久性登记。</span><span class="sxs-lookup"><span data-stu-id="4d376-1019">Replace <xref:System.Transactions.IPromotableSinglePhaseNotification> with an <xref:System.Transactions.ISinglePhaseNotification>, which is a durable enlistment that supports single phase commits.</span></span>

  <span data-ttu-id="4d376-1020">此操作可以在相同的应用域内执行，而且不需要任何用于与 MSDTC 交互的额外非托管代码即可执行提升。</span><span class="sxs-lookup"><span data-stu-id="4d376-1020">This can be done within the same app domain, and doesn't require any extra unmanaged code to interact with MSDTC to perform the promotion.</span></span> <span data-ttu-id="4d376-1021">仅当存在从 <xref:System.Transactions?displayProperty=nameWithType> 对由可提升登记实现的 <xref:System.Transactions.IPromotableSinglePhaseNotification>`Promote` 方法进行的未处理调用时，才可调用新方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-1021">The new method can be called only when there's an outstanding call from <xref:System.Transactions?displayProperty=nameWithType> to the <xref:System.Transactions.IPromotableSinglePhaseNotification>`Promote` method that's implemented by the promotable enlistment.</span></span>

- <span data-ttu-id="4d376-1022">**分析改进。**</span><span class="sxs-lookup"><span data-stu-id="4d376-1022">**Profiling improvements.**</span></span> <span data-ttu-id="4d376-1023">以下新的非托管分析 API 提供更强大的分析功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-1023">The following new unmanaged profiling APIs provide more robust profiling:</span></span>

  - [<span data-ttu-id="4d376-1024">COR_PRF_ASSEMBLY_REFERENCE_INFO 结构</span><span class="sxs-lookup"><span data-stu-id="4d376-1024">COR_PRF_ASSEMBLY_REFERENCE_INFO Structure</span></span>](../unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md)
  - [<span data-ttu-id="4d376-1025">COR_PRF_HIGH_MONITOR 枚举</span><span class="sxs-lookup"><span data-stu-id="4d376-1025">COR_PRF_HIGH_MONITOR Enumeration</span></span>](../unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md)
  - [<span data-ttu-id="4d376-1026">GetAssemblyReferences 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1026">GetAssemblyReferences Method</span></span>](../unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md)
  - [<span data-ttu-id="4d376-1027">GetEventMask2 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1027">GetEventMask2 Method</span></span>](../unmanaged-api/profiling/icorprofilerinfo5-geteventmask2-method.md)
  - [<span data-ttu-id="4d376-1028">SetEventMask2 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1028">SetEventMask2 Method</span></span>](../unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md)
  - [<span data-ttu-id="4d376-1029">AddAssemblyReference 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1029">AddAssemblyReference Method</span></span>](../unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)

  <span data-ttu-id="4d376-1030">之前的 `ICorProfiler` 实现支持依赖程序集的延迟加载。</span><span class="sxs-lookup"><span data-stu-id="4d376-1030">Previous `ICorProfiler` implementations supported lazy loading of dependent assemblies.</span></span> <span data-ttu-id="4d376-1031">新的分析 API 需要立即加载由探查器注入的依赖程序集，而不是在应用完全初始化后加载。</span><span class="sxs-lookup"><span data-stu-id="4d376-1031">The new profiling APIs require dependent assemblies that are injected by the profiler to be loadable immediately, instead of being loaded after the app is fully initialized.</span></span> <span data-ttu-id="4d376-1032">此更改不会影响现有 `ICorProfiler` API 的用户。</span><span class="sxs-lookup"><span data-stu-id="4d376-1032">This change doesn't affect users of the existing `ICorProfiler` APIs.</span></span>

- <span data-ttu-id="4d376-1033">**调试改进。**</span><span class="sxs-lookup"><span data-stu-id="4d376-1033">**Debugging improvements.**</span></span> <span data-ttu-id="4d376-1034">以下新的未托管调试 API 提供与探查器更好的集成。</span><span class="sxs-lookup"><span data-stu-id="4d376-1034">The following new unmanaged debugging APIs provide better integration with a profiler.</span></span> <span data-ttu-id="4d376-1035">你现在可以访问由探查器插入的元数据，以及转储调试时编译器 ReJIT 请求所生成的本地变量和代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-1035">You can now access metadata inserted by the profiler as well as local variables and code produced by compiler ReJIT requests when dump debugging.</span></span>

  - [<span data-ttu-id="4d376-1036">SetWriteableMetadataUpdateMode 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1036">SetWriteableMetadataUpdateMode Method</span></span>](../unmanaged-api/debugging/icordebugprocess7-setwriteablemetadataupdatemode-method.md)
  - [<span data-ttu-id="4d376-1037">EnumerateLocalVariablesEx 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1037">EnumerateLocalVariablesEx Method</span></span>](../unmanaged-api/debugging/icordebugilframe4-enumeratelocalvariablesex-method.md)
  - [<span data-ttu-id="4d376-1038">GetLocalVariableEx 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1038">GetLocalVariableEx Method</span></span>](../unmanaged-api/debugging/icordebugilframe4-getlocalvariableex-method.md)
  - [<span data-ttu-id="4d376-1039">GetCodeEx 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1039">GetCodeEx Method</span></span>](../unmanaged-api/debugging/icordebugilframe4-getcodeex-method.md)
  - [<span data-ttu-id="4d376-1040">GetActiveReJitRequestILCode 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1040">GetActiveReJitRequestILCode Method</span></span>](../unmanaged-api/debugging/icordebugfunction3-getactiverejitrequestilcode-method.md)
  - [<span data-ttu-id="4d376-1041">GetInstrumentedILMap 方法</span><span class="sxs-lookup"><span data-stu-id="4d376-1041">GetInstrumentedILMap Method</span></span>](../unmanaged-api/debugging/icordebugilcode2-getinstrumentedilmap-method.md)

- <span data-ttu-id="4d376-1042">**事件跟踪更改。**</span><span class="sxs-lookup"><span data-stu-id="4d376-1042">**Event tracing changes.**</span></span> <span data-ttu-id="4d376-1043">.NET Framework 4.5.2 为较大的表面区域启用进程外的基于 Windows 事件跟踪 (ETW) 的活动跟踪。</span><span class="sxs-lookup"><span data-stu-id="4d376-1043">.NET Framework 4.5.2 enables out-of-process, Event Tracing for Windows (ETW)-based activity tracing for a larger surface area.</span></span> <span data-ttu-id="4d376-1044">这将使高级电源管理 (APM) 供应商提供轻型工具，这些工具可精确跟踪跨线程单个请求和活动的成本。</span><span class="sxs-lookup"><span data-stu-id="4d376-1044">This enables Advanced Power Management (APM) vendors to provide lightweight tools that accurately track the costs of individual requests and activities that cross threads.</span></span>  <span data-ttu-id="4d376-1045">仅当 ETW 控制器启用它们时，才会引发这些事件；因此，这些更改不会影响之前编写的 ETW 代码或在禁用 ETW 的情况下运行的代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-1045">These events are raised only when ETW controllers enable them; therefore, the changes don't affect previously written ETW code or code that runs with ETW disabled.</span></span>

- <span data-ttu-id="4d376-1046">**提升事务并将其转换为持久登记**</span><span class="sxs-lookup"><span data-stu-id="4d376-1046">**Promoting a transaction and converting it to a durable enlistment**</span></span>

  <span data-ttu-id="4d376-1047"><xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> 是 .NET Framework 4.5.2 和 4.6 中新增的 API：</span><span class="sxs-lookup"><span data-stu-id="4d376-1047"><xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> is a new API added to .NET Framework 4.5.2 and 4.6:</span></span>

  ```csharp
  [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]
  public Enlistment PromoteAndEnlistDurable(Guid resourceManagerIdentifier,
                                            IPromotableSinglePhaseNotification promotableNotification,
                                            ISinglePhaseNotification enlistmentNotification,
                                            EnlistmentOptions enlistmentOptions)
  ```

  ```vb
  <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")>
  public Function PromoteAndEnlistDurable(resourceManagerIdentifier As Guid,
                                          promotableNotification As IPromotableSinglePhaseNotification,
                                          enlistmentNotification As ISinglePhaseNotification,
                                          enlistmentOptions As EnlistmentOptions) As Enlistment
  ```

  <span data-ttu-id="4d376-1048">该方法可能会由登记使用，该登记先前通过 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> 创建以响应 <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-1048">The method may be used by an enlistment that was previously created by <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> in response to the <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d376-1049">它要求 `System.Transactions` 将事务提升为 MSDTC 事务，并将可提升的登记“转换”为持久登记。</span><span class="sxs-lookup"><span data-stu-id="4d376-1049">It asks `System.Transactions` to promote the transaction to an MSDTC transaction and to "convert" the promotable enlistment to a durable enlistment.</span></span> <span data-ttu-id="4d376-1050">此方法成功完成后，`System.Transactions` 将不再引用 <xref:System.Transactions.IPromotableSinglePhaseNotification> 接口，将来的所有通知都将到达所提供的 <xref:System.Transactions.ISinglePhaseNotification> 接口。</span><span class="sxs-lookup"><span data-stu-id="4d376-1050">After this method completes successfully, the <xref:System.Transactions.IPromotableSinglePhaseNotification> interface will no longer be referenced by `System.Transactions`, and any future notifications will arrive on the provided <xref:System.Transactions.ISinglePhaseNotification> interface.</span></span> <span data-ttu-id="4d376-1051">相关登记必须作为持久登记，以支持事务日志记录和恢复。</span><span class="sxs-lookup"><span data-stu-id="4d376-1051">The enlistment in question must act as a durable enlistment, supporting transaction logging and recovery.</span></span> <span data-ttu-id="4d376-1052">请参阅 <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType> 了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="4d376-1052">Refer to <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType> for details.</span></span> <span data-ttu-id="4d376-1053">此外，登记必须支持 <xref:System.Transactions.ISinglePhaseNotification>。</span><span class="sxs-lookup"><span data-stu-id="4d376-1053">In addition, the enlistment must support <xref:System.Transactions.ISinglePhaseNotification>.</span></span>  <span data-ttu-id="4d376-1054">此方法 *只能* 在处理 <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> 调用时调用。</span><span class="sxs-lookup"><span data-stu-id="4d376-1054">This method can *only* be called while processing an <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType> call.</span></span> <span data-ttu-id="4d376-1055">如果不是这种情况，则会引发 <xref:System.Transactions.TransactionException> 异常。</span><span class="sxs-lookup"><span data-stu-id="4d376-1055">If that is not the case, a <xref:System.Transactions.TransactionException> exception is thrown.</span></span>

<a name="v451"></a>

## <a name="whats-new-in-net-framework-451"></a><span data-ttu-id="4d376-1056">.NET Framework 4.5.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-1056">What's new in .NET Framework 4.5.1</span></span>

<span data-ttu-id="4d376-1057">**2014 年 4 月版更新** ：</span><span class="sxs-lookup"><span data-stu-id="4d376-1057">**April 2014 updates** :</span></span>

- <span data-ttu-id="4d376-1058">[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/p/?LinkId=393658) 包括对可移植类库模板的更新，以支持以下方案：</span><span class="sxs-lookup"><span data-stu-id="4d376-1058">[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/p/?LinkId=393658) includes updates to the Portable Class Library templates to support these scenarios:</span></span>

  - <span data-ttu-id="4d376-1059">你可以使用面向 Windows 8.1、Windows Phone 8.1 和 Windows Phone Silverlight 8.1 的可移植库中的 Windows 运行时 API。</span><span class="sxs-lookup"><span data-stu-id="4d376-1059">You can use Windows Runtime APIs in portable libraries that target Windows 8.1, Windows Phone 8.1, and Windows Phone Silverlight 8.1.</span></span>

  - <span data-ttu-id="4d376-1060">在面向 Windows 8.1 或 Windows Phone 8.1 时，你可以在可移植库中包含 XAML（Windows.UI.XAML 类型）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1060">You can include XAML (Windows.UI.XAML types) in portable libraries when you target Windows 8.1 or Windows Phone 8.1.</span></span> <span data-ttu-id="4d376-1061">支持以下 XAML 模板：空白页、资源字典、模板控件和用户控件。</span><span class="sxs-lookup"><span data-stu-id="4d376-1061">The following XAML templates are supported:  Blank Page, Resource Dictionary, Templated Control, and User Control.</span></span>

  - <span data-ttu-id="4d376-1062">你可以创建可移植 Windows 运行时组件（.winmd 文件）以用于面向 Windows 8.1 和 Windows Phone 8.1 的应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="4d376-1062">You can create a portable Windows Runtime component (.winmd file) for use in Store apps that target Windows 8.1 and Windows Phone 8.1.</span></span>

  - <span data-ttu-id="4d376-1063">你可以重定 Windows 应用商店或 Windows Phone 应用商店类库（例如可移植类库）的目标。</span><span class="sxs-lookup"><span data-stu-id="4d376-1063">You can retarget a Windows Store or Windows Phone Store class library like a Portable Class Library.</span></span>

  <span data-ttu-id="4d376-1064">有关这些更改的详细信息，请参阅[可移植类库](../cross-platform/portable-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1064">For more information about these changes, see [Portable Class Library](../cross-platform/portable-class-library.md).</span></span>

- <span data-ttu-id="4d376-1065">.NET Framework 内容集现在包括 .NET Native 相关文档，这是一种用于生成和部署 Windows 应用程序的预编译技术。</span><span class="sxs-lookup"><span data-stu-id="4d376-1065">The .NET Framework content set now includes documentation for .NET Native, which is a precompilation technology for building and deploying Windows apps.</span></span> <span data-ttu-id="4d376-1066">为了提升性能，.NET Native 将应用程序直接编译为本机代码，而不是中间语言 (IL)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1066">.NET Native compiles your apps directly to native code, rather than to intermediate language (IL), for better performance.</span></span> <span data-ttu-id="4d376-1067">有关详细信息，请参阅[使用 .NET Native 编译应用](../net-native/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1067">For details, see [Compiling Apps with .NET Native](../net-native/index.md).</span></span>

- <span data-ttu-id="4d376-1068">[.NET Framework 引用源](https://referencesource.microsoft.com/)提供新的浏览体验和增强功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1068">The [.NET Framework Reference Source](https://referencesource.microsoft.com/) provides a new browsing experience and enhanced functionality.</span></span> <span data-ttu-id="4d376-1069">现在可以联机浏览 .NET Framework 源代码，[下载引用](https://referencesource.microsoft.com/download.html)以供脱机查看，并在调试时逐步执行源（包括修补程序和更新）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1069">You can now browse through the .NET Framework source code online, [download the reference](https://referencesource.microsoft.com/download.html) for offline viewing, and step through the sources (including patches and updates) during debugging.</span></span> <span data-ttu-id="4d376-1070">有关详细信息，请参阅日志 [.NET 引用源的全新外观](https://devblogs.microsoft.com/dotnet/a-new-look-for-net-reference-source/)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1070">For more information, see the blog entry [A new look for .NET Reference Source](https://devblogs.microsoft.com/dotnet/a-new-look-for-net-reference-source/).</span></span>

<span data-ttu-id="4d376-1071">.NET Framework 4.5.1 基类中的新增功能和增强包括：</span><span class="sxs-lookup"><span data-stu-id="4d376-1071">New features and enhancements in the base classes in .NET Framework 4.5.1 include:</span></span>

- <span data-ttu-id="4d376-1072">程序集的自动绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="4d376-1072">Automatic binding redirection for assemblies.</span></span> <span data-ttu-id="4d376-1073">自 Visual Studio 2013 起，编译定位 .NET Framework 4.5.1 的应用程序时，如果应用程序或其组件引用同一程序集的多个版本，那么绑定重定向可能会被添加到应用程序配置文件中。</span><span class="sxs-lookup"><span data-stu-id="4d376-1073">Starting with Visual Studio 2013, when you compile an app that targets .NET Framework 4.5.1, binding redirects may be added to the app configuration file if your app or its components reference multiple versions of the same assembly.</span></span> <span data-ttu-id="4d376-1074">你也可以对面向 .NET framework 的早期版本的项目启用此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1074">You can also enable this feature for projects that target older versions of .NET Framework.</span></span> <span data-ttu-id="4d376-1075">有关详细信息，请参阅[如何：启用和禁用自动绑定重定向](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1075">For more information, see [How to: Enable and Disable Automatic Binding Redirection](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).</span></span>

- <span data-ttu-id="4d376-1076">可以收集诊断信息，以帮助开发人员提高服务器和云应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1076">Ability to collect diagnostics information to help developers improve the performance of server and cloud applications.</span></span> <span data-ttu-id="4d376-1077">有关详细信息，请参阅 <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> 类中的 <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> 和 <xref:System.Diagnostics.Tracing.EventSource> 方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-1077">For more information, see the <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> and <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> methods in the <xref:System.Diagnostics.Tracing.EventSource> class.</span></span>

- <span data-ttu-id="4d376-1078">可以在垃圾回收过程中显式压缩大对象堆 (LOH)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1078">Ability to explicitly compact the large object heap (LOH) during garbage collection.</span></span> <span data-ttu-id="4d376-1079">有关更多信息，请参见 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="4d376-1079">For more information, see the <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType> property.</span></span>

- <span data-ttu-id="4d376-1080">其他性能改进，例如 ASP.NET 应用挂起、多核 JIT 改进，以及更新 .NET Framework 后更快的应用启动。</span><span class="sxs-lookup"><span data-stu-id="4d376-1080">Additional performance improvements such as ASP.NET app suspension, multi-core JIT improvements, and faster app startup after a .NET Framework update.</span></span> <span data-ttu-id="4d376-1081">有关详细信息，请参阅 [.NET Framework 4.5.1 公告](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/)和 [ASP.NET 应用挂起](https://devblogs.microsoft.com/dotnet/asp-net-app-suspend-responsive-shared-net-web-hosting/)博客文章。</span><span class="sxs-lookup"><span data-stu-id="4d376-1081">For details, see the [.NET Framework 4.5.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/) and the [ASP.NET app suspend](https://devblogs.microsoft.com/dotnet/asp-net-app-suspend-responsive-shared-net-web-hosting/) blog post.</span></span>

<span data-ttu-id="4d376-1082">Windows 窗体的改进包括：</span><span class="sxs-lookup"><span data-stu-id="4d376-1082">Improvements to Windows Forms include:</span></span>

- <span data-ttu-id="4d376-1083">在 Windows 窗体控件中调整大小。</span><span class="sxs-lookup"><span data-stu-id="4d376-1083">Resizing in Windows Forms controls.</span></span> <span data-ttu-id="4d376-1084">你可以使用系统 DPI 设置调整控件（例如，显示在属性网格中的图标）组件的大小，方法是使用应用的应用程序配置文件 (app.config) 中的条目选择使用该功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1084">You can use the system DPI setting to resize components of controls (for example, the icons that appear in a property grid) by opting in with an entry in the application configuration file (app.config) for your app.</span></span> <span data-ttu-id="4d376-1085">此功能当前在以下 Windows 窗体控件中受支持：</span><span class="sxs-lookup"><span data-stu-id="4d376-1085">This feature is currently supported in the following Windows Forms controls:</span></span>

  - <xref:System.Windows.Forms.PropertyGrid>
  - <xref:System.Windows.Forms.TreeView>
  - <span data-ttu-id="4d376-1086"><xref:System.Windows.Forms.DataGridView> 的某些方面（有关支持的其他控件，请参阅 [4.5.2 中的新功能](#v452)）</span><span class="sxs-lookup"><span data-stu-id="4d376-1086">Some aspects of the <xref:System.Windows.Forms.DataGridView> (see [new features in 4.5.2](#v452) for additional controls supported)</span></span>

  <span data-ttu-id="4d376-1087">若要启用此功能，请将新的 \<appSettings> 元素添加到配置文件 (app.config) 并将 `EnableWindowsFormsHighDpiAutoResizing` 元素设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="4d376-1087">To enable this feature, add a new \<appSettings> element to the configuration file (app.config) and set the `EnableWindowsFormsHighDpiAutoResizing` element to `true`:</span></span>

  ```xml
  <appSettings>
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
  </appSettings>
  ```

<span data-ttu-id="4d376-1088">有关在 Visual Studio 2013 中调试 .NET Framework 应用程序的改进包括：</span><span class="sxs-lookup"><span data-stu-id="4d376-1088">Improvements when debugging your .NET Framework apps in Visual Studio 2013 include:</span></span>

- <span data-ttu-id="4d376-1089">返回 Visual Studio 调试器中的值。</span><span class="sxs-lookup"><span data-stu-id="4d376-1089">Return values in the Visual Studio debugger.</span></span> <span data-ttu-id="4d376-1090">在 Visual Studio 2013 中调试托管应用程序时，“自动”窗口会显示方法的返回类型和值。</span><span class="sxs-lookup"><span data-stu-id="4d376-1090">When you debug a managed app in Visual Studio 2013, the Autos window displays return types and values for methods.</span></span> <span data-ttu-id="4d376-1091">此信息可用于桌面、Windows 应用商店和 Windows Phone 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-1091">This information is available for desktop, Windows Store, and Windows Phone apps.</span></span> <span data-ttu-id="4d376-1092">有关详细信息，请参阅[检查方法调用的返回值](/previous-versions/visualstudio/visual-studio-2013/dn323257(v=vs.120))。</span><span class="sxs-lookup"><span data-stu-id="4d376-1092">For more information, see [Examine return values of method calls](/previous-versions/visualstudio/visual-studio-2013/dn323257(v=vs.120)).</span></span>

- <span data-ttu-id="4d376-1093">针对 64 位应用程序的“编辑并继续”。</span><span class="sxs-lookup"><span data-stu-id="4d376-1093">Edit and Continue for 64-bit apps.</span></span> <span data-ttu-id="4d376-1094">Visual Studio 2013 支持对桌面、Windows 应用商店和 Windows Phone 相关 64 位托管应用程序使用“编辑并继续”功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1094">Visual Studio 2013 supports the Edit and Continue feature for 64-bit managed apps for desktop, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="4d376-1095">现有的限制对 32 位和 64 位应用仍然有效（请参阅[支持的代码更改 (C#)](/visualstudio/debugger/supported-code-changes-csharp) 文章的最后一节）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1095">The existing limitations remain in effect for both 32-bit and 64-bit apps (see the last section of the [Supported Code Changes (C#)](/visualstudio/debugger/supported-code-changes-csharp) article).</span></span>

- <span data-ttu-id="4d376-1096">异步识别调试。</span><span class="sxs-lookup"><span data-stu-id="4d376-1096">Async-aware debugging.</span></span> <span data-ttu-id="4d376-1097">为了简化在 Visual Studio 2013 中调试异步应用程序，调用堆栈隐藏了编译器提供的基础结构代码以支持异步编程，并链入了逻辑父框架，以便你可以更加明确逻辑程序的执行情况。</span><span class="sxs-lookup"><span data-stu-id="4d376-1097">To make it easier to debug asynchronous apps in Visual Studio 2013, the call stack hides the infrastructure code provided by compilers to support asynchronous programming, and also chains in logical parent frames so you can follow logical program execution more clearly.</span></span> <span data-ttu-id="4d376-1098">“任务”窗口将替换“并行任务”窗口，并显示与特定断点相关的任务，还会显示应用程序中当前处于活动状态或计划状态的任何其他任务。</span><span class="sxs-lookup"><span data-stu-id="4d376-1098">A Tasks window replaces the Parallel Tasks window and displays tasks that relate to a particular breakpoint, and also displays any other tasks that are currently active or scheduled in the app.</span></span> <span data-ttu-id="4d376-1099">可以在 [.NET Framework 4.5.1 公告](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/)的“异步识别调试”一节中了解此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1099">You can read about this feature in the "Async-aware debugging" section of the [.NET Framework 4.5.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/).</span></span>

- <span data-ttu-id="4d376-1100">改进对 Windows 运行时组件的异常支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1100">Better exception support for Windows Runtime components.</span></span> <span data-ttu-id="4d376-1101">在 Windows 8.1 中，Windows 应用商店应用抛出的异常保留了导致异常抛出的错误的相关信息（甚至可跨语言）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1101">In Windows 8.1, exceptions that arise from Windows Store apps preserve information about the error that caused the exception, even across language boundaries.</span></span> <span data-ttu-id="4d376-1102">可以在 [.NET Framework 4.5.1 公告](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/)的“Windows 应用商店应用开发”一节中了解此功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1102">You can read about this feature in the "Windows Store app development" section of the [.NET Framework 4.5.1 announcement](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-5-1-preview/).</span></span>

<span data-ttu-id="4d376-1103">自 Visual Studio 2013 起，可以使用[托管配置文件引导式优化工具 (Mpgo.exe)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md) 来优化 Windows 8.x 应用商店应用和桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-1103">Starting with Visual Studio 2013, you can use the [Managed Profile Guided Optimization Tool (Mpgo.exe)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md) to optimize Windows 8.x Store apps as well as desktop apps.</span></span>

<span data-ttu-id="4d376-1104">有关 ASP.NET 4.5.1 中的新功能，请参阅[适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具发行说明](/aspnet/visual-studio/overview/2013/release-notes).</span><span class="sxs-lookup"><span data-stu-id="4d376-1104">For new features in ASP.NET 4.5.1, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](/aspnet/visual-studio/overview/2013/release-notes).</span></span>

<a name="v45"></a>

## <a name="whats-new-in-net-framework-45"></a><span data-ttu-id="4d376-1105">.NET Framework 4.5 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-1105">What's new in .NET Framework 4.5</span></span>

### <a name="base-classes"></a><span data-ttu-id="4d376-1106">基类</span><span class="sxs-lookup"><span data-stu-id="4d376-1106">Base classes</span></span>

- <span data-ttu-id="4d376-1107">能够在部署期间通过检测并关闭 .NET Framework 4 应用程序来减少系统重启。</span><span class="sxs-lookup"><span data-stu-id="4d376-1107">Ability to reduce system restarts by detecting and closing .NET Framework 4 applications during deployment.</span></span> <span data-ttu-id="4d376-1108">请参阅[在 .NET Framework 4.5 安装期间减少系统重新启动](../deployment/reducing-system-restarts.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1108">See [Reducing System Restarts During .NET Framework 4.5 Installations](../deployment/reducing-system-restarts.md).</span></span>

- <span data-ttu-id="4d376-1109">支持 64 位平台上大于 2 GB 的数组。</span><span class="sxs-lookup"><span data-stu-id="4d376-1109">Support for arrays that are larger than 2 gigabytes (GB) on 64-bit platforms.</span></span> <span data-ttu-id="4d376-1110">此功能可在应用程序配置文件中启用。</span><span class="sxs-lookup"><span data-stu-id="4d376-1110">This feature can be enabled in the application configuration file.</span></span> <span data-ttu-id="4d376-1111">请查看 [\<gcAllowVeryLargeObjects> 元素](../configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md)，其中还列出了有关对象大小和数组大小的其他限制。</span><span class="sxs-lookup"><span data-stu-id="4d376-1111">See the [\<gcAllowVeryLargeObjects> element](../configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md), which also lists other restrictions on object size and array size.</span></span>

- <span data-ttu-id="4d376-1112">通过服务器的后台垃圾回收来改进性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1112">Better performance through background garbage collection for servers.</span></span> <span data-ttu-id="4d376-1113">在 .NET Framework 4.5 中使用服务器垃圾回收功能时，后台垃圾回收功能会自动启用。</span><span class="sxs-lookup"><span data-stu-id="4d376-1113">When you use server garbage collection in .NET Framework 4.5, background garbage collection is automatically enabled.</span></span> <span data-ttu-id="4d376-1114">请参阅[垃圾回收的基础](../../standard/garbage-collection/fundamentals.md)主题的“后台服务器垃圾回收”一节。</span><span class="sxs-lookup"><span data-stu-id="4d376-1114">See the Background Server Garbage Collection section of the [Fundamentals of Garbage Collection](../../standard/garbage-collection/fundamentals.md) topic.</span></span>

- <span data-ttu-id="4d376-1115">后台实时 (JIT) 编译，可在多核处理器上使用此功能改进应用程序性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1115">Background just-in-time (JIT) compilation, which is optionally available on multi-core processors to improve application performance.</span></span> <span data-ttu-id="4d376-1116">请参阅 <xref:System.Runtime.ProfileOptimization>。</span><span class="sxs-lookup"><span data-stu-id="4d376-1116">See <xref:System.Runtime.ProfileOptimization>.</span></span>

- <span data-ttu-id="4d376-1117">可以限制正则表达式引擎在超时之前持续尝试解析正则表达式的时间。请参阅 <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="4d376-1117">Ability to limit how long the regular expression engine will attempt to resolve a regular expression before it times out. See the <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=nameWithType> property.</span></span>

- <span data-ttu-id="4d376-1118">定义应用程序域的默认区域性的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1118">Ability to define the default culture for an application domain.</span></span> <span data-ttu-id="4d376-1119">请参阅 <xref:System.Globalization.CultureInfo> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1119">See the <xref:System.Globalization.CultureInfo> class.</span></span>

- <span data-ttu-id="4d376-1120">Unicode (UTF-16) 编码的控制台支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1120">Console support for Unicode (UTF-16) encoding.</span></span> <span data-ttu-id="4d376-1121">请参阅 <xref:System.Console> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1121">See the <xref:System.Console> class.</span></span>

- <span data-ttu-id="4d376-1122">支持对区域性字符串排序和比较数据进行版本控制。</span><span class="sxs-lookup"><span data-stu-id="4d376-1122">Support for versioning of cultural string ordering and comparison data.</span></span> <span data-ttu-id="4d376-1123">请参阅 <xref:System.Globalization.SortVersion> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1123">See the <xref:System.Globalization.SortVersion> class.</span></span>

- <span data-ttu-id="4d376-1124">改进检索资源时的性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1124">Better performance when retrieving resources.</span></span> <span data-ttu-id="4d376-1125">请参阅[打包和部署资源](../resources/packaging-and-deploying-resources-in-desktop-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1125">See [Packaging and Deploying Resources](../resources/packaging-and-deploying-resources-in-desktop-apps.md).</span></span>

- <span data-ttu-id="4d376-1126">Zip 压缩改进，可减少压缩文件的大小。</span><span class="sxs-lookup"><span data-stu-id="4d376-1126">Zip compression improvements to reduce the size of a compressed file.</span></span> <span data-ttu-id="4d376-1127">请参阅 <xref:System.IO.Compression?displayProperty=nameWithType> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="4d376-1127">See the <xref:System.IO.Compression?displayProperty=nameWithType> namespace.</span></span>

- <span data-ttu-id="4d376-1128">可以通过 <xref:System.Reflection.Context.CustomReflectionContext> 类自定义用于重写默认反射行为的反射上下文。</span><span class="sxs-lookup"><span data-stu-id="4d376-1128">Ability to customize a reflection context to override default reflection behavior through the <xref:System.Reflection.Context.CustomReflectionContext> class.</span></span>

- <span data-ttu-id="4d376-1129">在 Windows 8 上使用 <xref:System.Globalization.IdnMapping?displayProperty=nameWithType> 类时支持应用程序国际化域名 (IDNA) 标准的 2008 版。</span><span class="sxs-lookup"><span data-stu-id="4d376-1129">Support for the 2008 version of the Internationalized Domain Names in Applications (IDNA) standard when the <xref:System.Globalization.IdnMapping?displayProperty=nameWithType> class is used  on Windows 8.</span></span>

- <span data-ttu-id="4d376-1130">在 Windows 8 上使用 .NET Framework 时，可以将字符串比较委托给操作系统（这将实现 Unicode 6.0）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1130">Delegation of string comparison to the operating system, which implements Unicode 6.0, when the .NET Framework is used on Windows 8.</span></span> <span data-ttu-id="4d376-1131">在其他平台上运行时，.NET Framework 包括其自己的字符串比较数据，这将实现 Unicode 5.x。</span><span class="sxs-lookup"><span data-stu-id="4d376-1131">When running on other platforms, the .NET Framework includes its own string comparison data, which implements Unicode 5.x.</span></span> <span data-ttu-id="4d376-1132">请参阅 <xref:System.String> 类和 <xref:System.Globalization.SortVersion> 类的“备注”部分。</span><span class="sxs-lookup"><span data-stu-id="4d376-1132">See the <xref:System.String> class and the Remarks section of the <xref:System.Globalization.SortVersion> class.</span></span>

- <span data-ttu-id="4d376-1133">能够为每个应用程序域计算字符串的哈希代码。</span><span class="sxs-lookup"><span data-stu-id="4d376-1133">Ability to compute the hash codes for strings on a per application domain basis.</span></span> <span data-ttu-id="4d376-1134">请查看 [\<UseRandomizedStringHashAlgorithm> 元素](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1134">See [\<UseRandomizedStringHashAlgorithm> Element](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).</span></span>

- <span data-ttu-id="4d376-1135">类型反射支持 <xref:System.Type> 和 <xref:System.Reflection.TypeInfo> 类之间的拆分。</span><span class="sxs-lookup"><span data-stu-id="4d376-1135">Type reflection support split between <xref:System.Type> and <xref:System.Reflection.TypeInfo> classes.</span></span> <span data-ttu-id="4d376-1136">请参阅 [.NET Framework 中用于 Windows 应用商店应用的反射](../reflection-and-codedom/reflection-for-windows-store-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1136">See [Reflection in the .NET Framework for Windows Store Apps](../reflection-and-codedom/reflection-for-windows-store-apps.md).</span></span>

### <a name="managed-extensibility-framework-mef"></a><span data-ttu-id="4d376-1137">Managed Extensibility Framework (MEF)</span><span class="sxs-lookup"><span data-stu-id="4d376-1137">Managed Extensibility Framework (MEF)</span></span>

<span data-ttu-id="4d376-1138">在 .NET Framework 4.5 中，Managed Extensibility Framework (MEF) 新增了以下功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-1138">In .NET Framework 4.5, the Managed Extensibility Framework (MEF) provides the following new features:</span></span>

- <span data-ttu-id="4d376-1139">对泛型类型的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1139">Support for generic types.</span></span>

- <span data-ttu-id="4d376-1140">利用基于约定的编程模型，你可以基于命名约定而非特性创建各个部分。</span><span class="sxs-lookup"><span data-stu-id="4d376-1140">Convention-based programming model that enables you to create parts based on naming conventions rather than attributes.</span></span>

- <span data-ttu-id="4d376-1141">多个范围。</span><span class="sxs-lookup"><span data-stu-id="4d376-1141">Multiple scopes.</span></span>

- <span data-ttu-id="4d376-1142">创建 Windows 8.x 应用商店应用时可以使用一部分 MEF。</span><span class="sxs-lookup"><span data-stu-id="4d376-1142">A subset of MEF that you can use when you create Windows 8.x Store apps.</span></span> <span data-ttu-id="4d376-1143">此子集可作为 NuGet 库中的[可下载程序包](https://www.nuget.org/packages/Microsoft.Composition)提供。</span><span class="sxs-lookup"><span data-stu-id="4d376-1143">This subset is available as a [downloadable package](https://www.nuget.org/packages/Microsoft.Composition) from the NuGet Gallery.</span></span> <span data-ttu-id="4d376-1144">若要安装此程序包，请在 Visual Studio 中打开项目，从“项目”菜单中选择“管理 NuGet 包”，然后联机搜索 `Microsoft.Composition` 程序包。</span><span class="sxs-lookup"><span data-stu-id="4d376-1144">To install the package, open your project in Visual Studio, choose **Manage NuGet Packages** from the **Project** menu, and search online for the `Microsoft.Composition` package.</span></span>

<span data-ttu-id="4d376-1145">有关详细信息，请参阅 [Managed Extensibility Framework (MEF)](../mef/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1145">For more information, see [Managed Extensibility Framework (MEF)](../mef/index.md).</span></span>

### <a name="asynchronous-file-operations"></a><span data-ttu-id="4d376-1146">异步文件操作</span><span class="sxs-lookup"><span data-stu-id="4d376-1146">Asynchronous file operations</span></span>

<span data-ttu-id="4d376-1147">在 .NET Framework 4.5 中，已向 C# 和 Visual Basic 语言添加新的异步功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1147">In .NET Framework 4.5, new asynchronous features were added to the C# and Visual Basic languages.</span></span> <span data-ttu-id="4d376-1148">这些功能将添加用于执行异步操作的基于任务的模型。</span><span class="sxs-lookup"><span data-stu-id="4d376-1148">These features add a task-based model for performing asynchronous operations.</span></span> <span data-ttu-id="4d376-1149">若要使用此新模型，请使用 I/O 类中的异步方法。</span><span class="sxs-lookup"><span data-stu-id="4d376-1149">To use this new model, use the asynchronous methods in the I/O classes.</span></span> <span data-ttu-id="4d376-1150">请参阅[异步文件 I/O](../../standard/io/asynchronous-file-i-o.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1150">See [Asynchronous File I/O](../../standard/io/asynchronous-file-i-o.md).</span></span>

<a name="tools"></a>

### <a name="tools"></a><span data-ttu-id="4d376-1151">工具</span><span class="sxs-lookup"><span data-stu-id="4d376-1151">Tools</span></span>

<span data-ttu-id="4d376-1152">在 .NET Framework 4.5 中，使用资源文件生成器 (Resgen.exe)，可以通过 .NET Framework 程序集中嵌入的 .resources 文件创建用于 Windows 8.x 应用商店应用的 .resw 文件。</span><span class="sxs-lookup"><span data-stu-id="4d376-1152">In .NET Framework 4.5, Resource File Generator (Resgen.exe) enables you to create a .resw file for use in Windows 8.x Store apps from a .resources file embedded in a .NET Framework assembly.</span></span> <span data-ttu-id="4d376-1153">有关详细信息，请参阅 [Resgen.exe（资源文件生成器）](../tools/resgen-exe-resource-file-generator.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1153">For more information, see [Resgen.exe (Resource File Generator)](../tools/resgen-exe-resource-file-generator.md).</span></span>

<span data-ttu-id="4d376-1154">利用按托管配置优化 (Mpgo.exe) 工具，你可以通过优化本机映像程序集来改进应用程序的启动时间、内存使用率（工作集大小）和吞吐量。</span><span class="sxs-lookup"><span data-stu-id="4d376-1154">Managed Profile Guided Optimization (Mpgo.exe) enables you to improve application startup time, memory utilization (working set size), and throughput by optimizing native image assemblies.</span></span> <span data-ttu-id="4d376-1155">该命令行工具会针对本机映像应用程序程序集生成配置文件数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-1155">The command-line tool generates profile data for native image application assemblies.</span></span> <span data-ttu-id="4d376-1156">请参阅 [Mpgo.exe（按托管配置文件优化工具）](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1156">See [Mpgo.exe (Managed Profile Guided Optimization Tool)](../tools/mpgo-exe-managed-profile-guided-optimization-tool.md).</span></span> <span data-ttu-id="4d376-1157">自 Visual Studio 2013 起，可以使用 Mpgo.exe 优化 Windows 8.x 应用商店应用和桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="4d376-1157">Starting with Visual Studio 2013, you can use Mpgo.exe to optimize Windows 8.x Store apps as well as desktop apps.</span></span>

<a name="parallel"></a>

### <a name="parallel-computing"></a><span data-ttu-id="4d376-1158">并行计算</span><span class="sxs-lookup"><span data-stu-id="4d376-1158">Parallel computing</span></span>

<span data-ttu-id="4d376-1159">.NET Framework 4.5 新增了多项有关并行计算的功能和改进。</span><span class="sxs-lookup"><span data-stu-id="4d376-1159">.NET Framework 4.5 provides several new features and improvements for parallel computing.</span></span> <span data-ttu-id="4d376-1160">其中包括改进的性能、增强的控件、对异步编程的增强支持、新的数据流库以及对并行调试和性能分析的增强支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1160">These include improved performance, increased control, improved support for asynchronous programming, a new dataflow library, and improved support for parallel debugging and performance analysis.</span></span> <span data-ttu-id="4d376-1161">请参阅“使用 .NET 进行并行编程”博客中的 [.NET 4.5 中有关并行的新增功能](https://devblogs.microsoft.com/pfxteam/whats-new-for-parallelism-in-net-4-5/)条目。</span><span class="sxs-lookup"><span data-stu-id="4d376-1161">See the entry [What's New for Parallelism in .NET 4.5](https://devblogs.microsoft.com/pfxteam/whats-new-for-parallelism-in-net-4-5/) in the Parallel Programming with .NET blog.</span></span>

<a name="web"></a>

### <a name="web"></a><span data-ttu-id="4d376-1162">Web</span><span class="sxs-lookup"><span data-stu-id="4d376-1162">Web</span></span>

<span data-ttu-id="4d376-1163">ASP.NET 4.5 和 4.5.1 为 Web 窗体、WebSocket 支持、异步处理程序、性能增强和许多其他功能添加了模型绑定。</span><span class="sxs-lookup"><span data-stu-id="4d376-1163">ASP.NET 4.5 and 4.5.1 add model binding for Web Forms, WebSocket support, asynchronous handlers, performance enhancements, and many other features.</span></span> <span data-ttu-id="4d376-1164">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="4d376-1164">For more information, see the following resources:</span></span>

- <span data-ttu-id="4d376-1165">[ASP.NET 4.5 和 Visual Studio 2012](/previous-versions/aspnet/hh420390(v=vs.110))</span><span class="sxs-lookup"><span data-stu-id="4d376-1165">[ASP.NET 4.5 and Visual Studio 2012](/previous-versions/aspnet/hh420390(v=vs.110))</span></span>

- [<span data-ttu-id="4d376-1166">适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具发行说明</span><span class="sxs-lookup"><span data-stu-id="4d376-1166">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>](/aspnet/visual-studio/overview/2013/release-notes)

### <a name="networking"></a><span data-ttu-id="4d376-1167">网络连接<a name="networking"></a></span><span class="sxs-lookup"><span data-stu-id="4d376-1167">Networking <a name="networking"></a></span></span>

<span data-ttu-id="4d376-1168">.NET Framework 4.5 新增了 HTTP 应用程序的编程接口。</span><span class="sxs-lookup"><span data-stu-id="4d376-1168">.NET Framework 4.5 provides a new programming interface for HTTP applications.</span></span> <span data-ttu-id="4d376-1169">有关详细信息，请参阅新的 <xref:System.Net.Http?displayProperty=nameWithType> 和 <xref:System.Net.Http.Headers?displayProperty=nameWithType> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="4d376-1169">For more information, see the new <xref:System.Net.Http?displayProperty=nameWithType> and <xref:System.Net.Http.Headers?displayProperty=nameWithType> namespaces.</span></span>

<span data-ttu-id="4d376-1170">还包含针对用于接受 WebSocket 连接并与之交互（通过使用现有 <xref:System.Net.HttpListener> 和相关类）的新编程接口的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1170">Support is also included for a new programming interface for accepting and interacting with a WebSocket connection by using the existing <xref:System.Net.HttpListener> and related classes.</span></span> <span data-ttu-id="4d376-1171">有关详细信息，请参阅新的 <xref:System.Net.WebSockets> 命名空间和 <xref:System.Net.HttpListener> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1171">For more information, see the new <xref:System.Net.WebSockets> namespace and the <xref:System.Net.HttpListener> class.</span></span>

<span data-ttu-id="4d376-1172">此外，.NET Framework 4.5 新增了以下网络改进：</span><span class="sxs-lookup"><span data-stu-id="4d376-1172">In addition, .NET Framework 4.5 includes the following networking improvements:</span></span>

- <span data-ttu-id="4d376-1173">与 RFC 兼容的 URI 支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1173">RFC-compliant URI support.</span></span> <span data-ttu-id="4d376-1174">有关详细信息，请参阅 <xref:System.Uri> 和相关类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1174">For more information, see <xref:System.Uri> and related classes.</span></span>

- <span data-ttu-id="4d376-1175">对国际域名 (IDN) 分析的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1175">Support for Internationalized Domain Name (IDN) parsing.</span></span> <span data-ttu-id="4d376-1176">有关详细信息，请参阅 <xref:System.Uri> 和相关类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1176">For more information, see <xref:System.Uri> and related classes.</span></span>

- <span data-ttu-id="4d376-1177">对电子邮件地址国际化 (EAI) 的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1177">Support for Email Address Internationalization (EAI).</span></span> <span data-ttu-id="4d376-1178">有关更多信息，请参见 <xref:System.Net.Mail> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="4d376-1178">For more information, see the <xref:System.Net.Mail> namespace.</span></span>

- <span data-ttu-id="4d376-1179">改进的 IPv6 支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1179">Improved IPv6 support.</span></span> <span data-ttu-id="4d376-1180">有关更多信息，请参见 <xref:System.Net.NetworkInformation> 命名空间。</span><span class="sxs-lookup"><span data-stu-id="4d376-1180">For more information, see the <xref:System.Net.NetworkInformation> namespace.</span></span>

- <span data-ttu-id="4d376-1181">双重模式套接字支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1181">Dual-mode socket support.</span></span> <span data-ttu-id="4d376-1182">有关更多信息，请参见 <xref:System.Net.Sockets.Socket> 和 <xref:System.Net.Sockets.TcpListener> 类。</span><span class="sxs-lookup"><span data-stu-id="4d376-1182">For more information, see the <xref:System.Net.Sockets.Socket> and <xref:System.Net.Sockets.TcpListener> classes.</span></span>

<a name="client"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="4d376-1183">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="4d376-1183">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="4d376-1184">在 .NET Framework 4.5 中，Windows Presentation Foundation (WPF) 在以下几个领域进行了更改和改进：</span><span class="sxs-lookup"><span data-stu-id="4d376-1184">In .NET Framework 4.5, Windows Presentation Foundation (WPF) contains changes and improvements in the following areas:</span></span>

- <span data-ttu-id="4d376-1185">利用新的 <xref:System.Windows.Controls.Ribbon.Ribbon> 控件，你可以实现承载快速访问工具栏、应用程序菜单和选项卡的功能区用户界面。</span><span class="sxs-lookup"><span data-stu-id="4d376-1185">The new <xref:System.Windows.Controls.Ribbon.Ribbon> control, which enables you to implement a ribbon user interface that hosts a Quick Access Toolbar, Application Menu, and tabs.</span></span>

- <span data-ttu-id="4d376-1186">支持同步和异步数据验证的新 <xref:System.ComponentModel.INotifyDataErrorInfo> 接口。</span><span class="sxs-lookup"><span data-stu-id="4d376-1186">The new <xref:System.ComponentModel.INotifyDataErrorInfo> interface, which supports synchronous and asynchronous data validation.</span></span>

- <span data-ttu-id="4d376-1187"><xref:System.Windows.Controls.VirtualizingPanel> 和 <xref:System.Windows.Threading.Dispatcher> 类的新功能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1187">New features for the <xref:System.Windows.Controls.VirtualizingPanel> and <xref:System.Windows.Threading.Dispatcher> classes.</span></span>

- <span data-ttu-id="4d376-1188">通过在非 UI 线程上访问集合，改进了在显示大型分组数据集时的性能。</span><span class="sxs-lookup"><span data-stu-id="4d376-1188">Improved performance when displaying large sets of grouped data, and by accessing collections on non-UI threads.</span></span>

- <span data-ttu-id="4d376-1189">针对静态属性的数据绑定、针对实现 <xref:System.Reflection.ICustomTypeProvider> 接口的自定义类型的数据绑定，以及从绑定表达式中检索数据绑定信息。</span><span class="sxs-lookup"><span data-stu-id="4d376-1189">Data binding to static properties, data binding to custom types that implement the <xref:System.Reflection.ICustomTypeProvider> interface, and retrieval of data binding information from a binding expression.</span></span>

- <span data-ttu-id="4d376-1190">在值发生更改时重新定位数据（实时数据整理）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1190">Repositioning of data as the values change (live shaping).</span></span>

- <span data-ttu-id="4d376-1191">能够检查项目容器的数据上下文是否已断开连接。</span><span class="sxs-lookup"><span data-stu-id="4d376-1191">Ability to check whether the data context for an item container is disconnected.</span></span>

- <span data-ttu-id="4d376-1192">能够设置属性更改和数据源更新之间的时间间隔。</span><span class="sxs-lookup"><span data-stu-id="4d376-1192">Ability to set the amount of time that should elapse between property changes and data source updates.</span></span>

- <span data-ttu-id="4d376-1193">改进了对实现弱事件模式的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1193">Improved support for implementing weak event patterns.</span></span> <span data-ttu-id="4d376-1194">此外，事件现在可以接受标记扩展。</span><span class="sxs-lookup"><span data-stu-id="4d376-1194">Also, events can now accept markup extensions.</span></span>

<a name="windows_communication_foundation"></a>

### <a name="windows-communication-foundation-wcf"></a><span data-ttu-id="4d376-1195">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="4d376-1195">Windows Communication Foundation (WCF)</span></span>

<span data-ttu-id="4d376-1196">为了更轻松地编写和维护 Windows Communication Foundation (WCF) 应用程序，.NET Framework 4.5 中新增了以下功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-1196">In .NET Framework 4.5, the following features have been added to make it simpler to write and maintain Windows Communication Foundation (WCF) applications:</span></span>

- <span data-ttu-id="4d376-1197">简化生成的配置文件。</span><span class="sxs-lookup"><span data-stu-id="4d376-1197">Simplification of generated configuration files.</span></span>

- <span data-ttu-id="4d376-1198">对协定优先开发的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1198">Support for contract-first development.</span></span>

- <span data-ttu-id="4d376-1199">能够更轻松地配置 ASP.NET 兼容模式。</span><span class="sxs-lookup"><span data-stu-id="4d376-1199">Ability to configure ASP.NET compatibility mode more easily.</span></span>

- <span data-ttu-id="4d376-1200">对默认传输属性值的更改，可减小你必须设置这些值的可能性。</span><span class="sxs-lookup"><span data-stu-id="4d376-1200">Changes in default transport property values to reduce the likelihood that you will have to set them.</span></span>

- <span data-ttu-id="4d376-1201">对 <xref:System.Xml.XmlDictionaryReaderQuotas> 类进行更新，可减小你必须手动为 XML 字典读取器配置配额的可能性。</span><span class="sxs-lookup"><span data-stu-id="4d376-1201">Updates to the <xref:System.Xml.XmlDictionaryReaderQuotas> class to reduce the likelihood that you will have to manually configure quotas for XML dictionary readers.</span></span>

- <span data-ttu-id="4d376-1202">作为生成过程的一部分，由 Visual Studio 验证 WCF 配置文件，以便你可以在运行应用程序之前检测配置错误。</span><span class="sxs-lookup"><span data-stu-id="4d376-1202">Validation of WCF configuration files by Visual Studio as part of the build process, so you can detect configuration errors before you run your application.</span></span>

- <span data-ttu-id="4d376-1203">新的异步流支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1203">New asynchronous streaming support.</span></span>

- <span data-ttu-id="4d376-1204">新的 HTTPS 协议映射，使你能够更轻松地通过 Internet Information Services (IIS) 在 HTTPS 上公开终结点。</span><span class="sxs-lookup"><span data-stu-id="4d376-1204">New HTTPS protocol mapping to make it easier to expose an endpoint over HTTPS with Internet Information Services (IIS).</span></span>

- <span data-ttu-id="4d376-1205">能够通过将 `?singleWSDL` 追加到服务 URL，来在单个 WSDL 文档中生成元数据。</span><span class="sxs-lookup"><span data-stu-id="4d376-1205">Ability to generate metadata in a single WSDL document by appending `?singleWSDL` to the service URL.</span></span>

- <span data-ttu-id="4d376-1206">WebSockets 支持，通过端口 80 和 443 启用真正的双向通信，其性能特性与 TCP 传输类似。</span><span class="sxs-lookup"><span data-stu-id="4d376-1206">Websockets support to enable true bidirectional communication over ports 80 and 443 with performance characteristics similar to the TCP transport.</span></span>

- <span data-ttu-id="4d376-1207">对在代码中配置服务的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1207">Support for configuring services in code.</span></span>

- <span data-ttu-id="4d376-1208">XML 编辑器工具提示。</span><span class="sxs-lookup"><span data-stu-id="4d376-1208">XML Editor tooltips.</span></span>

- <span data-ttu-id="4d376-1209"><xref:System.ServiceModel.ChannelFactory> 缓存支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1209"><xref:System.ServiceModel.ChannelFactory> caching support.</span></span>

- <span data-ttu-id="4d376-1210">二进制文件编码器压缩支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1210">Binary encoder compression support.</span></span>

- <span data-ttu-id="4d376-1211">对 UDP 传输的支持，这可使开发人员编写使用“发后不理”消息的服务。</span><span class="sxs-lookup"><span data-stu-id="4d376-1211">Support for a UDP transport that enables developers to write services that use "fire and forget" messaging.</span></span> <span data-ttu-id="4d376-1212">客户端向服务发送消息，且不希望从该服务获得响应。</span><span class="sxs-lookup"><span data-stu-id="4d376-1212">A client sends a message to a service and expects no response from the service.</span></span>

- <span data-ttu-id="4d376-1213">能够在使用 HTTP 传输和传输安全性时，支持单个 WCF 终结点上的多个身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="4d376-1213">Ability to support multiple authentication modes on a single WCF endpoint when using the HTTP transport and transport security.</span></span>

- <span data-ttu-id="4d376-1214">对使用国际域名 (IDN) 的 WCF 服务的支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1214">Support for WCF services that use internationalized domain names (IDNs).</span></span>

<span data-ttu-id="4d376-1215">有关详细信息，请参阅 [Windows Communication Foundation 中的新增功能](../wcf/whats-new.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1215">For more information, see [What's New in Windows Communication Foundation](../wcf/whats-new.md).</span></span>

<a name="windows_workflow_foundation"></a>

### <a name="windows-workflow-foundation-wf"></a><span data-ttu-id="4d376-1216">Windows Workflow Foundation (WF)</span><span class="sxs-lookup"><span data-stu-id="4d376-1216">Windows Workflow Foundation (WF)</span></span>

<span data-ttu-id="4d376-1217">在 .NET Framework 4.5 中，已向 Windows Workflow Foundation (WF) 添加多项新功能，包括：</span><span class="sxs-lookup"><span data-stu-id="4d376-1217">In .NET Framework 4.5, several new features were added to Windows Workflow Foundation (WF), including:</span></span>

- <span data-ttu-id="4d376-1218">首次作为 .NET Framework 4.0.1（[.NET Framework 4 平台更新 1](/archive/blogs/endpoint/microsoft-net-framework-4-platform-update-1)）的一部分引入的状态机工作流。</span><span class="sxs-lookup"><span data-stu-id="4d376-1218">State machine workflows, which were first introduced as part of .NET Framework 4.0.1 ([.NET Framework 4 Platform Update 1](/archive/blogs/endpoint/microsoft-net-framework-4-platform-update-1)).</span></span> <span data-ttu-id="4d376-1219">此更新包括可使开发人员创建状态机工作流的多个新类和活动。</span><span class="sxs-lookup"><span data-stu-id="4d376-1219">This update included several new classes and activities that enabled developers to create state machine workflows.</span></span> <span data-ttu-id="4d376-1220">这些类和活动已针对 .NET Framework 4.5 更新为包含：</span><span class="sxs-lookup"><span data-stu-id="4d376-1220">These classes and activities were updated for .NET Framework 4.5 to include:</span></span>

  - <span data-ttu-id="4d376-1221">对状态设置断点的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1221">The ability to set breakpoints on states.</span></span>

  - <span data-ttu-id="4d376-1222">在工作流设计器中复制和粘贴转换的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1222">The ability to copy and paste transitions in the workflow designer.</span></span>

  - <span data-ttu-id="4d376-1223">对共享的触发器转换创建的设计器支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1223">Designer support for shared trigger transition creation.</span></span>

  - <span data-ttu-id="4d376-1224">创建状态机工作流的活动，包括：<xref:System.Activities.Statements.StateMachine>、<xref:System.Activities.Statements.State> 和 <xref:System.Activities.Statements.Transition>。</span><span class="sxs-lookup"><span data-stu-id="4d376-1224">Activities for creating state machine workflows, including: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State>, and <xref:System.Activities.Statements.Transition>.</span></span>

- <span data-ttu-id="4d376-1225">增强的工作流设计器功能如下:</span><span class="sxs-lookup"><span data-stu-id="4d376-1225">Enhanced Workflow Designer features such as the following:</span></span>

  - <span data-ttu-id="4d376-1226">Visual Studio 中增强的工作流搜索功能，包括“快速查找”和“在文件中查找”。</span><span class="sxs-lookup"><span data-stu-id="4d376-1226">Enhanced workflow search capabilities in Visual Studio, including **Quick Find** and **Find in Files** .</span></span>

  - <span data-ttu-id="4d376-1227">将第二个子活动添加到容器活动中时自动创建“序列”活动以及在“序列”活动中包括这两个活动的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1227">Ability to automatically create a Sequence activity when a second child activity is added to a container activity, and to include both activities in the Sequence activity.</span></span>

  - <span data-ttu-id="4d376-1228">平移支持，可让工作流的可见部分发生更改，而无需使用滚动条。</span><span class="sxs-lookup"><span data-stu-id="4d376-1228">Panning support, which enables the visible portion of a workflow to be changed without using the scroll bars.</span></span>

  - <span data-ttu-id="4d376-1229">新“文档大纲”视图，它在树样式的大纲视图中显示工作流组件并允许在“文档大纲”视图中选择组件。</span><span class="sxs-lookup"><span data-stu-id="4d376-1229">A new **Document Outline** view that shows the components of a workflow in a tree-style outline view and lets you select a component in the **Document Outline** view.</span></span>

  - <span data-ttu-id="4d376-1230">向活动中添加批注的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1230">Ability to add annotations to activities.</span></span>

  - <span data-ttu-id="4d376-1231">通过使用工作流设计器定义和使用活动委托的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1231">Ability to define and consume activity delegates by using the workflow designer.</span></span>

  - <span data-ttu-id="4d376-1232">状态机和流程图工作流中活动和转换的自动连接和自动插入。</span><span class="sxs-lookup"><span data-stu-id="4d376-1232">Auto-connect and auto-insert for activities and transitions in state machine and flowchart workflows.</span></span>

- <span data-ttu-id="4d376-1233">XAML 文件的单个元素中工作流的视图状态信息存储，以便你可以轻松定位和编辑视图状态信息。</span><span class="sxs-lookup"><span data-stu-id="4d376-1233">Storage of the view state information for a workflow in a single element in the XAML file, so you can easily locate and edit the view state information.</span></span>

- <span data-ttu-id="4d376-1234">可防止子活动持久化的 NoPersistScope 容器活动。</span><span class="sxs-lookup"><span data-stu-id="4d376-1234">A NoPersistScope container activity to prevent child activities from persisting.</span></span>

- <span data-ttu-id="4d376-1235">对 C# 表达式的支持：</span><span class="sxs-lookup"><span data-stu-id="4d376-1235">Support for C# expressions:</span></span>

  - <span data-ttu-id="4d376-1236">使用 Visual Basic 的工作流项目将使用 Visual Basic 表达式，C# 工作流项目将使用 C# 表达式。</span><span class="sxs-lookup"><span data-stu-id="4d376-1236">Workflow projects that use Visual Basic will use Visual Basic expressions, and C# workflow projects will use C# expressions.</span></span>

  - <span data-ttu-id="4d376-1237">在 Visual Studio 2010 中创建并具有 Visual Basic 表达式的 C# 工作流项目与使用 C# 表达式的 C# 工作流项目兼容。</span><span class="sxs-lookup"><span data-stu-id="4d376-1237">C# workflow projects that were created in Visual Studio 2010 and that have Visual Basic expressions are compatible with C# workflow projects that use C# expressions.</span></span>

- <span data-ttu-id="4d376-1238">版本控制增强功能：</span><span class="sxs-lookup"><span data-stu-id="4d376-1238">Versioning enhancements:</span></span>

  - <span data-ttu-id="4d376-1239">新 <xref:System.Activities.WorkflowIdentity> 类，它提供了保留的工作流实例与其工作流定义之间的映射。</span><span class="sxs-lookup"><span data-stu-id="4d376-1239">The new  <xref:System.Activities.WorkflowIdentity> class, which provides a mapping between a persisted workflow instance and its workflow definition.</span></span>

  - <span data-ttu-id="4d376-1240">同一主机中多个工作流版本的并行执行，包括 <xref:System.ServiceModel.Activities.WorkflowServiceHost>。</span><span class="sxs-lookup"><span data-stu-id="4d376-1240">Side-by-side execution of multiple workflow versions in the same host, including <xref:System.ServiceModel.Activities.WorkflowServiceHost>.</span></span>

  - <span data-ttu-id="4d376-1241">在动态更新中，修改保留的工作流实例的定义的能力。</span><span class="sxs-lookup"><span data-stu-id="4d376-1241">In Dynamic Update, the ability to modify the definition of a persisted workflow instance.</span></span>

- <span data-ttu-id="4d376-1242">协定优先工作流服务开发，它为自动生成活动以匹配现有服务协定提供支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1242">Contract-first workflow service development, which provides support for automatically generating activities to match an existing service contract.</span></span>

<span data-ttu-id="4d376-1243">有关详细信息，请参阅 [Windows Workflow Foundation 中的新增功能](../windows-workflow-foundation/whats-new-in-wf-in-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1243">For more information, see [What's New in Windows Workflow Foundation](../windows-workflow-foundation/whats-new-in-wf-in-dotnet.md).</span></span>

<a name="tailored"></a>

### <a name="net-for-windows-8x-store-apps"></a><span data-ttu-id="4d376-1244">适用于 Windows 8.x 应用商店应用的 .NET</span><span class="sxs-lookup"><span data-stu-id="4d376-1244">.NET for Windows 8.x Store apps</span></span>

<span data-ttu-id="4d376-1245">Windows 8.x 应用商店应用专为特定外形规格而设计，并利用 Windows 操作系统的强大技术支持。</span><span class="sxs-lookup"><span data-stu-id="4d376-1245">Windows 8.x Store apps are designed for specific form factors and leverage the power of the Windows operating system.</span></span> <span data-ttu-id="4d376-1246">可以使用一部分 .NET Framework 4.5 或 4.5.1 生成用 C# 或 Visual Basic 编写的 Windows 相关 Windows 8.x 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="4d376-1246">A subset of .NET Framework 4.5 or 4.5.1 is available for building Windows 8.x Store apps for Windows by using C# or Visual Basic.</span></span> <span data-ttu-id="4d376-1247">该部分被称作适用于 Windows 8.x 应用商店应用的 .NET，详见[概述](/previous-versions/windows/apps/br230302(v=vs.140))</span><span class="sxs-lookup"><span data-stu-id="4d376-1247">This subset is called .NET for Windows 8.x Store apps and is discussed in an [overview](/previous-versions/windows/apps/br230302(v=vs.140)).</span></span>

### <a name="portable-class-libraries"></a><span data-ttu-id="4d376-1248">可移植类库<a name="portable"></a></span><span class="sxs-lookup"><span data-stu-id="4d376-1248">Portable Class Libraries <a name="portable"></a></span></span>

<span data-ttu-id="4d376-1249">利用 Visual Studio 2012（及更高版本）中的可移植类库项目，可以编写和生成在多个 .NET Framework 平台上运行的托管程序集。</span><span class="sxs-lookup"><span data-stu-id="4d376-1249">The Portable Class Library project in Visual Studio 2012 (and later versions) enables you to write and build managed assemblies that work on multiple .NET Framework platforms.</span></span> <span data-ttu-id="4d376-1250">使用可移植类库项目，可以选择目标平台（如 Windows Phone 和适用于 Windows 8.x 应用商店应用的 .NET）。</span><span class="sxs-lookup"><span data-stu-id="4d376-1250">Using a Portable Class Library project, you choose the platforms (such as Windows Phone and .NET for Windows 8.x Store apps) to target.</span></span> <span data-ttu-id="4d376-1251">项目中的可用类型和成员自动限制为这些平台中的公共类型和成员。</span><span class="sxs-lookup"><span data-stu-id="4d376-1251">The available types and members in your project are automatically restricted to the common types and members across these platforms.</span></span> <span data-ttu-id="4d376-1252">有关详细信息，请参阅[可移植类库](../cross-platform/portable-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="4d376-1252">For more information, see [Portable Class Library](../cross-platform/portable-class-library.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d376-1253">请参阅</span><span class="sxs-lookup"><span data-stu-id="4d376-1253">See also</span></span>

- [<span data-ttu-id="4d376-1254">.NET Framework 和带外版本</span><span class="sxs-lookup"><span data-stu-id="4d376-1254">The .NET Framework and Out-of-Band Releases</span></span>](../get-started/the-net-framework-and-out-of-band-releases.md)
- [<span data-ttu-id="4d376-1255">.NET Framework 中辅助功能的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-1255">What's new in accessibility in .NET Framework</span></span>](whats-new-in-accessibility.md)
- [<span data-ttu-id="4d376-1256">Visual Studio 2019 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4d376-1256">What's New in Visual Studio 2019</span></span>](/visualstudio/ide/whats-new-visual-studio-2019)
- [<span data-ttu-id="4d376-1257">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4d376-1257">ASP.NET</span></span>](/aspnet)
- [<span data-ttu-id="4d376-1258">Visual Studio 中的 C++ 新变化</span><span class="sxs-lookup"><span data-stu-id="4d376-1258">What's New for C++ in Visual Studio</span></span>](/cpp/what-s-new-for-visual-cpp-in-visual-studio)
