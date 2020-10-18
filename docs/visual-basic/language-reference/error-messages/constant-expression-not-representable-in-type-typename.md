---
title: 常量表达式无法在类型“<typename>”中表示
ms.date: 07/20/2015
f1_keywords:
- bc30439
- vbc30439
helpviewer_keywords:
- BC30439
ms.assetid: 0a842906-3bc5-4946-8a37-3e3da883ef63
ms.openlocfilehash: e18f05c0d6a37ac4563b554d7ba943ba21131f85
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163163"
---
# <a name="bc30439-constant-expression-not-representable-in-type-typename"></a><span data-ttu-id="e5442-102">BC30439：常量表达式无法在类型 "" 中表示 \<typename></span><span class="sxs-lookup"><span data-stu-id="e5442-102">BC30439: Constant expression not representable in type '\<typename>'</span></span>

<span data-ttu-id="e5442-103">你正在尝试评估将无法适应目标类型的常量，这通常是因为它溢出范围。</span><span class="sxs-lookup"><span data-stu-id="e5442-103">You are trying to evaluate a constant that will not fit into the target type, usually because it is overflowing the range.</span></span>

 <span data-ttu-id="e5442-104">**错误 ID：** BC30439</span><span class="sxs-lookup"><span data-stu-id="e5442-104">**Error ID:** BC30439</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="e5442-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="e5442-105">To correct this error</span></span>

1. <span data-ttu-id="e5442-106">将目标类型更改为可处理该常量的目标类型。</span><span class="sxs-lookup"><span data-stu-id="e5442-106">Change the target type to one that can handle the constant.</span></span>

## <a name="see-also"></a><span data-ttu-id="e5442-107">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e5442-107">See also</span></span>

- [<span data-ttu-id="e5442-108">常量概述</span><span class="sxs-lookup"><span data-stu-id="e5442-108">Constants Overview</span></span>](../../programming-guide/language-features/constants-enums/constants-overview.md)
- [<span data-ttu-id="e5442-109">常量和枚举</span><span class="sxs-lookup"><span data-stu-id="e5442-109">Constants and Enumerations</span></span>](../constants-and-enumerations.md)
