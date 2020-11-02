---
title: 如何：在任务中包装 EAP 模式
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to wrap EAP patterns
ms.assetid: f11ed467-af2f-4504-8a2e-299a6c36d44e
ms.openlocfilehash: 339544ce9f0ee44097d1a60e0d2c2035d81f674d
ms.sourcegitcommit: 6d09ae36acba0b0e2ba47999f8f1a725795462a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "92925358"
---
# <a name="how-to-wrap-eap-patterns-in-a-task"></a>如何：在任务中包装 EAP 模式
下面的示例演示如何通过使用 <xref:System.Threading.Tasks.TaskCompletionSource%601> 将任意基于事件的异步模式 (EAP) 操作序列公开为一个任务。 此示例还展示了如何使用 <xref:System.Threading.CancellationToken> 对 <xref:System.Net.WebClient> 对象调用内置的取消方法。  
  
## <a name="example"></a>示例  
 [!code-csharp[FromAsync#08](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#08)]
 [!code-vb[FromAsync#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#08)]  
  
## <a name="see-also"></a>另请参阅

- [TPL 和传统 .NET 异步编程](tpl-and-traditional-async-programming.md)
