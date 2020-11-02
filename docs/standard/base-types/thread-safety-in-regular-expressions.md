---
title: 正则表达式中的线程安全
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET regular expressions, threads
- regular expressions, threads
- searching with regular expressions, threads
- parsing text with regular expressions, threads
- pattern-matching with regular expressions, threads
ms.assetid: 7c4a167b-5236-4cde-a2ca-58646230730f
ms.openlocfilehash: 29ff647d623c047c63c52732a3e8bce5f0e95d6c
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889278"
---
# <a name="thread-safety-in-regular-expressions"></a><span data-ttu-id="95f10-102">正则表达式中的线程安全</span><span class="sxs-lookup"><span data-stu-id="95f10-102">Thread Safety in Regular Expressions</span></span>
<span data-ttu-id="95f10-103"><xref:System.Text.RegularExpressions.Regex> 类本身是线程安全且不可变的（只读）。</span><span class="sxs-lookup"><span data-stu-id="95f10-103">The <xref:System.Text.RegularExpressions.Regex> class itself is thread safe and immutable (read-only).</span></span> <span data-ttu-id="95f10-104">也就是说，可以在任何线程上创建 **Regex** 对象并在线程间共享；可以从任何线程调用匹配方法并且始终不会更改全局状态。</span><span class="sxs-lookup"><span data-stu-id="95f10-104">That is, **Regex** objects can be created on any thread and shared between threads; matching methods can be called from any thread and never alter any global state.</span></span>  
  
 <span data-ttu-id="95f10-105">不过，应对一个线程使用 Regex 返回的结果对象（Match 和 MatchCollection）。</span><span class="sxs-lookup"><span data-stu-id="95f10-105">However, result objects ( **Match** and **MatchCollection** ) returned by **Regex** should be used on a single thread.</span></span> <span data-ttu-id="95f10-106">尽管其中许多对象在逻辑上是不可变的，但其实现可以延迟某些结果的计算以提高性能，因此，调用方必须序列化对这些对象的访问。</span><span class="sxs-lookup"><span data-stu-id="95f10-106">Although many of these objects are logically immutable, their implementations could delay computation of some results to improve performance, and as a result, callers must serialize access to them.</span></span>  
  
 <span data-ttu-id="95f10-107">如果需要在多个线程上共享 **Regex** 结果对象，则通过调用对象的同步方法，可以将这些对象转换成线程安全的实例。</span><span class="sxs-lookup"><span data-stu-id="95f10-107">If there is a need to share **Regex** result objects on multiple threads, these objects can be converted to thread-safe instances by calling their synchronized methods.</span></span> <span data-ttu-id="95f10-108">除枚举器外，所有正则表达式类都是线程安全的或者可以通过同步方法转换成线程安全对象。</span><span class="sxs-lookup"><span data-stu-id="95f10-108">With the exception of enumerators, all regular expression classes are thread safe or can be converted into thread-safe objects by a synchronized method.</span></span>  
  
 <span data-ttu-id="95f10-109">枚举器是唯一例外。</span><span class="sxs-lookup"><span data-stu-id="95f10-109">Enumerators are the only exception.</span></span> <span data-ttu-id="95f10-110">应用程序必须序列化对集合枚举器的调用。</span><span class="sxs-lookup"><span data-stu-id="95f10-110">An application must serialize calls to collection enumerators.</span></span> <span data-ttu-id="95f10-111">规则为，如果可以在多个线程上同时枚举一个集合，则应该同步枚举器所遍历集合的根对象上的枚举器方法。</span><span class="sxs-lookup"><span data-stu-id="95f10-111">The rule is that if a collection can be enumerated on more than one thread simultaneously, you should synchronize enumerator methods on the root object of the collection traversed by the enumerator.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="95f10-112">另请参阅</span><span class="sxs-lookup"><span data-stu-id="95f10-112">See also</span></span>

- [<span data-ttu-id="95f10-113">.NET 正则表达式</span><span class="sxs-lookup"><span data-stu-id="95f10-113">.NET Regular Expressions</span></span>](regular-expressions.md)
