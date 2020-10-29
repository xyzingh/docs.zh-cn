---
title: SYSLIB0006 警告
description: 了解有关生成编译时警告 SYSLIB0006 的过时信息。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 45d2d8ec6ad99996f8b8f46d0c2e0ac2e02cf450
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333063"
---
# <a name="syslib0006-threadabort-is-not-supported"></a><span data-ttu-id="afd6d-103">SYSLIB0006：不支持 Thread.Abort</span><span class="sxs-lookup"><span data-stu-id="afd6d-103">SYSLIB0006: Thread.Abort is not supported</span></span>

<span data-ttu-id="afd6d-104">从 .NET 5.0 开始，以下 API 标记为已过时。</span><span class="sxs-lookup"><span data-stu-id="afd6d-104">The following APIs are marked obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="afd6d-105">使用这些 API 会在编译时生成警告 `SYSLIB0006`。</span><span class="sxs-lookup"><span data-stu-id="afd6d-105">Use of these APIs generates warning `SYSLIB0006` at compile time.</span></span>

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

## <a name="workaround"></a><span data-ttu-id="afd6d-106">解决方法</span><span class="sxs-lookup"><span data-stu-id="afd6d-106">Workaround</span></span>

<span data-ttu-id="afd6d-107">使用 <xref:System.Threading.CancellationToken> 中止对工作单元的处理，而不是调用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="afd6d-107">Use a <xref:System.Threading.CancellationToken> to abort processing of a unit of work instead of calling <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="afd6d-108">以下示例说明了 <xref:System.Threading.CancellationToken> 的用法。</span><span class="sxs-lookup"><span data-stu-id="afd6d-108">The following example illustrates the use of <xref:System.Threading.CancellationToken>.</span></span>

```csharp
void ProcessPendingWorkItemsNew(CancellationToken cancellationToken)
{
    if (QueryIsMoreWorkPending())
    {
        // If the CancellationToken is marked as "needs to cancel",
        // this will throw the appropriate exception.
        cancellationToken.ThrowIfCancellationRequested();

        WorkItem work = DequeueWorkItem();
        ProcessWorkItem(work);
    }
}
```

## <a name="see-also"></a><span data-ttu-id="afd6d-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="afd6d-109">See also</span></span>

- [<span data-ttu-id="afd6d-110">Thread.Abort 已过时 - 中断性变更</span><span class="sxs-lookup"><span data-stu-id="afd6d-110">Thread.Abort is obsolete - breaking change</span></span>](3.1-5.0.md#threadabort-is-obsolete)
- [<span data-ttu-id="afd6d-111">托管线程中的取消</span><span class="sxs-lookup"><span data-stu-id="afd6d-111">Cancellation in managed threads</span></span>](../../standard/threading/cancellation-in-managed-threads.md)
