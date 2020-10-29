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
# <a name="syslib0006-threadabort-is-not-supported"></a>SYSLIB0006：不支持 Thread.Abort

从 .NET 5.0 开始，以下 API 标记为已过时。 使用这些 API 会在编译时生成警告 `SYSLIB0006`。

- <xref:System.Threading.Thread.Abort?displayProperty=nameWithType>
- <xref:System.Threading.Thread.Abort(System.Object)?displayProperty=nameWithType>

## <a name="workaround"></a>解决方法

使用 <xref:System.Threading.CancellationToken> 中止对工作单元的处理，而不是调用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>。 以下示例说明了 <xref:System.Threading.CancellationToken> 的用法。

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

## <a name="see-also"></a>另请参阅

- [Thread.Abort 已过时 - 中断性变更](3.1-5.0.md#threadabort-is-obsolete)
- [托管线程中的取消](../../standard/threading/cancellation-in-managed-threads.md)
