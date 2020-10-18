---
title: 结构“<structurename>”至少必须包含一个实例成员变量或至少必须包含一个未标记为“Custom”的实例事件声明
ms.date: 07/20/2015
f1_keywords:
- bc30941
- vbc30941
helpviewer_keywords:
- BC30941
ms.assetid: 7054cc1e-bac3-4c3d-82f3-35772bd8dd3b
ms.openlocfilehash: 4e7ef82659c43be08ee444eaf3f4df663f7aaa53
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159646"
---
# <a name="bc30941-structure-structurename-must-contain-at-least-one-instance-member-variable-or-at-least-one-instance-event-declaration-not-marked-custom"></a><span data-ttu-id="3c76e-102">BC30941：结构 " \<structurename> " 必须包含至少一个实例成员变量或至少包含一个未标记为 "Custom" 的实例事件声明</span><span class="sxs-lookup"><span data-stu-id="3c76e-102">BC30941: Structure '\<structurename>' must contain at least one instance member variable or at least one instance event declaration not marked 'Custom'</span></span>

<span data-ttu-id="3c76e-103">结构定义不包括任何非共享变量或非共享的非自定义事件。</span><span class="sxs-lookup"><span data-stu-id="3c76e-103">A structure definition does not include any nonshared variables or nonshared noncustom events.</span></span>

 <span data-ttu-id="3c76e-104">每个结构都必须有一个适用于每个特定实例的变量或事件， (非共享的) ，而不是共同 ([共享](../modifiers/shared.md)) 中的所有实例。</span><span class="sxs-lookup"><span data-stu-id="3c76e-104">Every structure must have either a variable or an event that applies to each specific instance (nonshared) instead of to all instances collectively ([Shared](../modifiers/shared.md)).</span></span> <span data-ttu-id="3c76e-105">非共享常量、属性和过程不满足此要求。</span><span class="sxs-lookup"><span data-stu-id="3c76e-105">Nonshared constants, properties, and procedures do not satisfy this requirement.</span></span> <span data-ttu-id="3c76e-106">此外，如果没有非共享变量并且只有一个非共享事件，则该事件不能是 `Custom` 事件。</span><span class="sxs-lookup"><span data-stu-id="3c76e-106">In addition, if there are no nonshared variables and only one nonshared event, that event cannot be a `Custom` event.</span></span>

 <span data-ttu-id="3c76e-107">**错误 ID：** BC30941</span><span class="sxs-lookup"><span data-stu-id="3c76e-107">**Error ID:** BC30941</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="3c76e-108">更正此错误</span><span class="sxs-lookup"><span data-stu-id="3c76e-108">To correct this error</span></span>

- <span data-ttu-id="3c76e-109">定义至少一个不是的变量或事件 `Shared` 。</span><span class="sxs-lookup"><span data-stu-id="3c76e-109">Define at least one variable or event that is not `Shared`.</span></span> <span data-ttu-id="3c76e-110">如果只定义了一个事件，则它必须是非自定义以及非共享的。</span><span class="sxs-lookup"><span data-stu-id="3c76e-110">If you define only one event, it must be noncustom as well as nonshared.</span></span>

## <a name="see-also"></a><span data-ttu-id="3c76e-111">另请参阅</span><span class="sxs-lookup"><span data-stu-id="3c76e-111">See also</span></span>

- [<span data-ttu-id="3c76e-112">结构</span><span class="sxs-lookup"><span data-stu-id="3c76e-112">Structures</span></span>](../../programming-guide/language-features/data-types/structures.md)
- [<span data-ttu-id="3c76e-113">如何：声明结构</span><span class="sxs-lookup"><span data-stu-id="3c76e-113">How to: Declare a Structure</span></span>](../../programming-guide/language-features/data-types/how-to-declare-a-structure.md)
- [<span data-ttu-id="3c76e-114">Structure 语句</span><span class="sxs-lookup"><span data-stu-id="3c76e-114">Structure Statement</span></span>](../statements/structure-statement.md)
