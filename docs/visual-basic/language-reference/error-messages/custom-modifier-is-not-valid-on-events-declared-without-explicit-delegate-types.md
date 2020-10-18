---
title: “Custom”修饰符在未用显式委托类型声明的事件上无效
ms.date: 07/20/2015
f1_keywords:
- vbc31122
- bc31122
helpviewer_keywords:
- BC31122
ms.assetid: 6911f0d1-641a-473b-906d-8ee5681194be
ms.openlocfilehash: a2277e3778c2c252fd4b1eaeb033d549f041c15c
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160628"
---
# <a name="bc31122-custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types"></a><span data-ttu-id="1509a-102">BC31122： "Custom" 修饰符在没有显式委托类型的声明事件上无效</span><span class="sxs-lookup"><span data-stu-id="1509a-102">BC31122: 'Custom' modifier is not valid on events declared without explicit delegate types</span></span>

<span data-ttu-id="1509a-103">与非自定义事件不同， `Custom Event` 声明在 `As` 事件名称后需要一个子句，该事件名称显式指定事件的委托类型。</span><span class="sxs-lookup"><span data-stu-id="1509a-103">Unlike a non-custom event, a `Custom Event` declaration requires an `As` clause following the event name that explicitly specifies the delegate type for the event.</span></span>

 <span data-ttu-id="1509a-104">可使用 `As` 子句和显式委托类型定义非自定义事件，或使用紧跟在事件名称后面的参数列表定义。</span><span class="sxs-lookup"><span data-stu-id="1509a-104">Non-custom events can be defined either with an `As` clause and an explicit delegate type, or with a parameter list immediately following the event name.</span></span>

 <span data-ttu-id="1509a-105">**错误 ID：** BC31122</span><span class="sxs-lookup"><span data-stu-id="1509a-105">**Error ID:** BC31122</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="1509a-106">更正此错误</span><span class="sxs-lookup"><span data-stu-id="1509a-106">To correct this error</span></span>

1. <span data-ttu-id="1509a-107">定义与自定义事件具有相同参数列表的委托。</span><span class="sxs-lookup"><span data-stu-id="1509a-107">Define a delegate with the same parameter list as the custom event.</span></span>

     <span data-ttu-id="1509a-108">例如，如果定义了 `Custom Event` `Custom Event Test(ByVal sender As Object, ByVal i As Integer)` ，则相应的委托将如下所示。</span><span class="sxs-lookup"><span data-stu-id="1509a-108">For example, if the `Custom Event` was defined by `Custom Event Test(ByVal sender As Object, ByVal i As Integer)`, then the corresponding delegate would be the following.</span></span>

     [!code-vb[VbVbalrEventError#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#18)]

2. <span data-ttu-id="1509a-109">将自定义事件的参数列表替换为 `As` 指定委托类型的子句。</span><span class="sxs-lookup"><span data-stu-id="1509a-109">Replace the parameter list of the custom event with an `As` clause specifying the delegate type.</span></span>

     <span data-ttu-id="1509a-110">继续此示例，将 `Custom Event` 按如下所示重写声明。</span><span class="sxs-lookup"><span data-stu-id="1509a-110">Continuing with the example, `Custom Event` declaration would be rewritten as follows.</span></span>

     [!code-vb[VbVbalrEventError#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#19)]

## <a name="example"></a><span data-ttu-id="1509a-111">示例</span><span class="sxs-lookup"><span data-stu-id="1509a-111">Example</span></span>

 <span data-ttu-id="1509a-112">此示例声明一个 `Custom Event` ，并指定 `As` 具有委托类型的必需子句。</span><span class="sxs-lookup"><span data-stu-id="1509a-112">This example declares a `Custom Event` and specifies the required `As` clause with a delegate type.</span></span>

 [!code-vb[VbVbalrEventError#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#2)]

## <a name="see-also"></a><span data-ttu-id="1509a-113">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1509a-113">See also</span></span>

- [<span data-ttu-id="1509a-114">Event 语句</span><span class="sxs-lookup"><span data-stu-id="1509a-114">Event Statement</span></span>](../statements/event-statement.md)
- [<span data-ttu-id="1509a-115">Delegate 语句</span><span class="sxs-lookup"><span data-stu-id="1509a-115">Delegate Statement</span></span>](../statements/delegate-statement.md)
- [<span data-ttu-id="1509a-116">事件</span><span class="sxs-lookup"><span data-stu-id="1509a-116">Events</span></span>](../../programming-guide/language-features/events/index.md)
