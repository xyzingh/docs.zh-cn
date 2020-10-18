---
title: 对象或类不支持事件集
ms.date: 07/20/2015
f1_keywords:
- vbrID459
ms.assetid: 785df3f3-2aae-4a25-af36-1f9879d4e5fd
ms.openlocfilehash: c5e8b8de3477147fc3174cdbee401c89753004ad
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159945"
---
# <a name="object-or-class-does-not-support-the-set-of-events"></a><span data-ttu-id="a5a8a-102">对象或类不支持事件集</span><span class="sxs-lookup"><span data-stu-id="a5a8a-102">Object or class does not support the set of events</span></span>

<span data-ttu-id="a5a8a-103">您尝试使用的 `WithEvents` 变量的组件无法作为指定事件集的事件源。</span><span class="sxs-lookup"><span data-stu-id="a5a8a-103">You tried to use a `WithEvents` variable with a component that cannot work as an event source for the specified set of events.</span></span> <span data-ttu-id="a5a8a-104">例如，你想要接收对象的事件，然后创建第一个对象的另一个对象 `Implements` 。</span><span class="sxs-lookup"><span data-stu-id="a5a8a-104">For example, you wanted to sink the events of an object, then create another object that `Implements` the first object.</span></span> <span data-ttu-id="a5a8a-105">尽管你可能会认为可以从实现的对象接收事件，但并不总是这样。</span><span class="sxs-lookup"><span data-stu-id="a5a8a-105">Although you might think you could sink the events from the implemented object, this is not always the case.</span></span> <span data-ttu-id="a5a8a-106">`Implements` 仅实现方法和属性的接口。</span><span class="sxs-lookup"><span data-stu-id="a5a8a-106">`Implements` only implements an interface for methods and properties.</span></span> <span data-ttu-id="a5a8a-107">`WithEvents` 不支持私有 `UserControls` ，因为引发的类型信息 `ObjectEvent` 在运行时不可用。</span><span class="sxs-lookup"><span data-stu-id="a5a8a-107">`WithEvents` is not supported for private `UserControls`, because the type info needed to raise the `ObjectEvent` is not available at run time.</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="a5a8a-108">更正此错误</span><span class="sxs-lookup"><span data-stu-id="a5a8a-108">To correct this error</span></span>

- <span data-ttu-id="a5a8a-109">不能接收不是源事件的组件的事件。</span><span class="sxs-lookup"><span data-stu-id="a5a8a-109">You cannot sink events for a component that does not source events.</span></span>

## <a name="see-also"></a><span data-ttu-id="a5a8a-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a5a8a-110">See also</span></span>

- [<span data-ttu-id="a5a8a-111">WithEvents</span><span class="sxs-lookup"><span data-stu-id="a5a8a-111">WithEvents</span></span>](../modifiers/withevents.md)
- [<span data-ttu-id="a5a8a-112">Implements 语句</span><span class="sxs-lookup"><span data-stu-id="a5a8a-112">Implements Statement</span></span>](../statements/implements-statement.md)
