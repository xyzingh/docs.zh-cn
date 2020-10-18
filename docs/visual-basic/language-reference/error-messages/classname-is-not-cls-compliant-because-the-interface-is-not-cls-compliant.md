---
title: “<classname>”不符合 CLS，因为它所实现的接口“<interfacename>”不符合 CLS
ms.date: 07/20/2015
f1_keywords:
- bc40029
- vbc40029
helpviewer_keywords:
- BC40029
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
ms.openlocfilehash: 936bc78d87613a8492347df0f65688bbef6e2ca4
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163176"
---
# <a name="bc40029-classname-is-not-cls-compliant-because-the-interface-interfacename-it-implements-is-not-cls-compliant"></a><span data-ttu-id="b7c89-102">BC40029： " \<classname> " 不符合 cls，因为它所实现的接口 " \<interfacename> " 不符合 cls</span><span class="sxs-lookup"><span data-stu-id="b7c89-102">BC40029: '\<classname>' is not CLS-compliant because the interface '\<interfacename>' it implements is not CLS-compliant</span></span>

<span data-ttu-id="b7c89-103">当某一类或接口派生自或实现标记为 `<CLSCompliant(True)>` 的类型时，该类或接口将被标记为 `<CLSCompliant(False)>` 。</span><span class="sxs-lookup"><span data-stu-id="b7c89-103">A class or interface is marked as `<CLSCompliant(True)>` when it derives from or implements a type that is marked as `<CLSCompliant(False)>` or is not marked.</span></span>

 <span data-ttu-id="b7c89-104">为了使某个类或接口符合 [语言独立性并 Language-Independent 组件](../../../standard/language-independence-and-language-independent-components.md) (CLS) ，其整个继承层次结构必须是兼容的。</span><span class="sxs-lookup"><span data-stu-id="b7c89-104">For a class or interface to be compliant with the [Language Independence and Language-Independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS), its entire inheritance hierarchy must be compliant.</span></span> <span data-ttu-id="b7c89-105">这意味着从它继承的每一个类型，不管是直接还是间接继承，都必须符合。</span><span class="sxs-lookup"><span data-stu-id="b7c89-105">That means every type from which it inherits, directly or indirectly, must be compliant.</span></span> <span data-ttu-id="b7c89-106">同样，如果一个类实现一个或多个接口，则其整个继承层次结构都必须符合。</span><span class="sxs-lookup"><span data-stu-id="b7c89-106">Similarly, if a class implements one or more interfaces, they must all be compliant throughout their inheritance hierarchies.</span></span>

 <span data-ttu-id="b7c89-107">当将 <xref:System.CLSCompliantAttribute> 应用到编程元素中时，需要将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合性。</span><span class="sxs-lookup"><span data-stu-id="b7c89-107">When you apply the <xref:System.CLSCompliantAttribute> to a programming element, you set the attribute's `isCompliant` parameter to either `True` or `False` to indicate compliance or noncompliance.</span></span> <span data-ttu-id="b7c89-108">此参数没有默认值，必须为其提供一个值。</span><span class="sxs-lookup"><span data-stu-id="b7c89-108">There is no default for this parameter, and you must supply a value.</span></span>

 <span data-ttu-id="b7c89-109">如果不将 <xref:System.CLSCompliantAttribute> 应用到元素，则它将被视为不符合规范。</span><span class="sxs-lookup"><span data-stu-id="b7c89-109">If you do not apply the <xref:System.CLSCompliantAttribute> to an element, it is considered to be noncompliant.</span></span>

 <span data-ttu-id="b7c89-110">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="b7c89-110">By default, this message is a warning.</span></span> <span data-ttu-id="b7c89-111">有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="b7c89-111">For information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="b7c89-112">**错误 ID：** BC40029</span><span class="sxs-lookup"><span data-stu-id="b7c89-112">**Error ID:** BC40029</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="b7c89-113">更正此错误</span><span class="sxs-lookup"><span data-stu-id="b7c89-113">To correct this error</span></span>

- <span data-ttu-id="b7c89-114">如果你需要 CLS 符合性，请在不同的继承层次结构或实现方案中定义此类型。</span><span class="sxs-lookup"><span data-stu-id="b7c89-114">If you require CLS compliance, define this type within a different inheritance hierarchy or implementation scheme.</span></span>

- <span data-ttu-id="b7c89-115">如果你要求此类型保留在其当前的继承层次结构或实现方案中，请从其定义中删除 <xref:System.CLSCompliantAttribute> ，或将其标记为 `<CLSCompliant(False)>`。</span><span class="sxs-lookup"><span data-stu-id="b7c89-115">If you require that this type remain within its current inheritance hierarchy or implementation scheme, remove the <xref:System.CLSCompliantAttribute> from its definition or mark it as `<CLSCompliant(False)>`.</span></span>
