---
title: SYSLIB0004 警告
description: 了解有关生成编译时警告 SYSLIB0004 的过时信息。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: ba7cd8a890a89000b241d286c9d8069ba1398849
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333054"
---
# <a name="syslib0004-the-constrained-execution-region-cer-feature-is-not-supported"></a><span data-ttu-id="d9ffe-103">SYSLIB0004：不支持受约束的执行区域 (CER) 功能</span><span class="sxs-lookup"><span data-stu-id="d9ffe-103">SYSLIB0004: The constrained execution region (CER) feature is not supported</span></span>

<span data-ttu-id="d9ffe-104">[受约束的执行区域 (CER)](../../framework/performance/constrained-execution-regions.md) 功能仅在 .NET Framework 中受支持。</span><span class="sxs-lookup"><span data-stu-id="d9ffe-104">The [Constrained execution regions (CER)](../../framework/performance/constrained-execution-regions.md) feature is supported only in .NET Framework.</span></span> <span data-ttu-id="d9ffe-105">因此从 .NET 5.0 开始，与 CER 相关的各种 API 标记为已过时。</span><span class="sxs-lookup"><span data-stu-id="d9ffe-105">As such, various CER-related APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="d9ffe-106">使用这些 API 会在编译时生成警告 `SYSLIB0004`。</span><span class="sxs-lookup"><span data-stu-id="d9ffe-106">Using these APIs generates warning `SYSLIB0004` at compile time.</span></span>

<span data-ttu-id="d9ffe-107">以下与 CER 相关的 API 已过时：</span><span class="sxs-lookup"><span data-stu-id="d9ffe-107">The following CER-related APIs are obsolete:</span></span>

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(System.Runtime.CompilerServices.RuntimeHelpers.TryCode,System.Runtime.CompilerServices.RuntimeHelpers.CleanupCode,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegionsNoOP?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareContractedDelegate(System.Delegate)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ProbeForSufficientStack?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Cer?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Consistency?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute?displayProperty=nameWithType>

## <a name="see-also"></a><span data-ttu-id="d9ffe-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d9ffe-108">See also</span></span>

- [<span data-ttu-id="d9ffe-109">受约束的执行区域</span><span class="sxs-lookup"><span data-stu-id="d9ffe-109">Constrained execution regions</span></span>](../../framework/performance/constrained-execution-regions.md)
