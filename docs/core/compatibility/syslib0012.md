---
title: SYSLIB0012 警告
description: 了解有关生成编译时警告 SYSLIB0012 的过时信息。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 2ed93b6eefbaa861faca319f0cc9bf19ac741f3b
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333043"
---
# <a name="syslib0012-assemblycodebase-and-assemblyescapedcodebase-are-obsolete"></a><span data-ttu-id="31f0a-103">SYSLIB0012：Assembly.CodeBase 和 Assembly.EscapedCodeBase 已过时</span><span class="sxs-lookup"><span data-stu-id="31f0a-103">SYSLIB0012: Assembly.CodeBase and Assembly.EscapedCodeBase are obsolete</span></span>

<span data-ttu-id="31f0a-104">从 .NET 5.0 开始，以下 API 标记为已过时。</span><span class="sxs-lookup"><span data-stu-id="31f0a-104">The following APIs are marked as obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="31f0a-105">在代码中使用这些 API 会在编译时生成警告 `SYSLIB0012`。</span><span class="sxs-lookup"><span data-stu-id="31f0a-105">Using them in code generates warning `SYSLIB0012` at compile time.</span></span>

- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType>

<span data-ttu-id="31f0a-106">解决方法</span><span class="sxs-lookup"><span data-stu-id="31f0a-106">Workaround</span></span>

<span data-ttu-id="31f0a-107">请改用 <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="31f0a-107">Use <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> instead.</span></span>
