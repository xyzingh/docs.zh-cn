---
title: 根命名空间 <namespacename> 中的名称 <fullnamespacename> 不符合 CLS
ms.date: 07/20/2015
f1_keywords:
- vbc40039
- bc40039
helpviewer_keywords:
- BC40039
ms.assetid: c5bd5914-ae71-416a-8bed-f76f644f78be
ms.openlocfilehash: 48e020cb74641279a4f402e47034514d78dfc4fc
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160205"
---
# <a name="bc40039-name-namespacename-in-the-root-namespace-fullnamespacename-is-not-cls-compliant"></a><span data-ttu-id="572df-102">BC40039： \<namespacename> 根命名空间中的名称 \<fullnamespacename> 不符合 CLS</span><span class="sxs-lookup"><span data-stu-id="572df-102">BC40039: Name \<namespacename> in the root namespace \<fullnamespacename> is not CLS-compliant</span></span>

<span data-ttu-id="572df-103">程序集标记为 `<CLSCompliant(True)>` ，但根命名空间名称的元素以下划线 (`_`) 开头。</span><span class="sxs-lookup"><span data-stu-id="572df-103">An assembly is marked as `<CLSCompliant(True)>`, but an element of the root namespace name begins with an underscore (`_`).</span></span>

 <span data-ttu-id="572df-104">编程元素可以包含一个或多个下划线，但要符合 [语言独立性和 Language-Independent 组件](../../../standard/language-independence-and-language-independent-components.md) (CLS) ，它不能以下划线开头。</span><span class="sxs-lookup"><span data-stu-id="572df-104">A programming element can contain one or more underscores, but to be compliant with the [Language Independence and Language-Independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS), it must not begin with an underscore.</span></span> <span data-ttu-id="572df-105">请参阅 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)。</span><span class="sxs-lookup"><span data-stu-id="572df-105">See [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md).</span></span>

 <span data-ttu-id="572df-106">当将 <xref:System.CLSCompliantAttribute> 应用到编程元素中时，需要将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合性。</span><span class="sxs-lookup"><span data-stu-id="572df-106">When you apply the <xref:System.CLSCompliantAttribute> to a programming element, you set the attribute's `isCompliant` parameter to either `True` or `False` to indicate compliance or noncompliance.</span></span> <span data-ttu-id="572df-107">此参数没有默认值，必须为其提供一个值。</span><span class="sxs-lookup"><span data-stu-id="572df-107">There is no default for this parameter, and you must supply a value.</span></span>

 <span data-ttu-id="572df-108">如果不将 <xref:System.CLSCompliantAttribute> 应用到元素，则它将被视为不符合规范。</span><span class="sxs-lookup"><span data-stu-id="572df-108">If you do not apply the <xref:System.CLSCompliantAttribute> to an element, it is considered to be noncompliant.</span></span>

 <span data-ttu-id="572df-109">默认情况下，此消息是一个警告。</span><span class="sxs-lookup"><span data-stu-id="572df-109">By default, this message is a warning.</span></span> <span data-ttu-id="572df-110">有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="572df-110">For information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="572df-111">**错误 ID：** BC40039</span><span class="sxs-lookup"><span data-stu-id="572df-111">**Error ID:** BC40039</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="572df-112">更正此错误</span><span class="sxs-lookup"><span data-stu-id="572df-112">To correct this error</span></span>

- <span data-ttu-id="572df-113">如果需要符合 CLS，请更改根命名空间名称，使其所有元素都不以下划线开头。</span><span class="sxs-lookup"><span data-stu-id="572df-113">If you require CLS compliance, change the root namespace name so that none of its elements begins with an underscore.</span></span>

- <span data-ttu-id="572df-114">如果要求命名空间名称保持不变，则 <xref:System.CLSCompliantAttribute> 从程序集删除或将其标记为 `<CLSCompliant(False)>` 。</span><span class="sxs-lookup"><span data-stu-id="572df-114">If you require that the namespace name remain unchanged, then remove the <xref:System.CLSCompliantAttribute> from the assembly or mark it as `<CLSCompliant(False)>`.</span></span>

## <a name="see-also"></a><span data-ttu-id="572df-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="572df-115">See also</span></span>

- [<span data-ttu-id="572df-116">Namespace 语句</span><span class="sxs-lookup"><span data-stu-id="572df-116">Namespace Statement</span></span>](../statements/namespace-statement.md)
- [<span data-ttu-id="572df-117">Visual Basic 中的命名空间</span><span class="sxs-lookup"><span data-stu-id="572df-117">Namespaces in Visual Basic</span></span>](../../programming-guide/program-structure/namespaces.md)
- [<span data-ttu-id="572df-118">-rootnamespace</span><span class="sxs-lookup"><span data-stu-id="572df-118">-rootnamespace</span></span>](../../reference/command-line-compiler/rootnamespace.md)
- [<span data-ttu-id="572df-119">“项目设计器”->“应用程序”页 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="572df-119">Application Page, Project Designer (Visual Basic)</span></span>](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [<span data-ttu-id="572df-120">Declared Element Names</span><span class="sxs-lookup"><span data-stu-id="572df-120">Declared Element Names</span></span>](../../programming-guide/language-features/declared-elements/declared-element-names.md)
- [<span data-ttu-id="572df-121">Visual Basic 命名约定</span><span class="sxs-lookup"><span data-stu-id="572df-121">Visual Basic Naming Conventions</span></span>](../../programming-guide/program-structure/naming-conventions.md)
