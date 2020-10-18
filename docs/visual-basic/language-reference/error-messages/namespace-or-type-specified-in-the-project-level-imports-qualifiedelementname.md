---
title: 在项目级 Imports“<qualifiedelementname>”中指定的命名空间或类型不包含任何公共成员，或者找不到该命名空间或类型
ms.date: 07/20/2015
f1_keywords:
- vbc40057
- bc40057
helpviewer_keywords:
- BC40057
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
ms.openlocfilehash: 54ee046cda998be8bd70e531918d6ab2a67d0494
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160114"
---
# <a name="bc40057-namespace-or-type-specified-in-the-project-level-imports-qualifiedelementname-doesnt-contain-any-public-member-or-cannot-be-found"></a><span data-ttu-id="b30f5-102">BC40057：在项目级 Imports "" 中指定的命名空间或类型 \<qualifiedelementname> 不包含任何公共成员，或者找不到该命名空间或类型</span><span class="sxs-lookup"><span data-stu-id="b30f5-102">BC40057: Namespace or type specified in the project-level Imports '\<qualifiedelementname>' doesn't contain any public member or cannot be found</span></span>

<span data-ttu-id="b30f5-103">项目级 Imports "" 中指定的命名空间或类型 \<qualifiedelementname> 不包含任何公共成员，或者找不到该命名空间或类型。</span><span class="sxs-lookup"><span data-stu-id="b30f5-103">Namespace or type specified in the project-level Imports '\<qualifiedelementname>' doesn't contain any public member or cannot be found.</span></span> <span data-ttu-id="b30f5-104">请确保定义命名空间或类型，并且至少包含一个公共成员。</span><span class="sxs-lookup"><span data-stu-id="b30f5-104">Make sure the namespace or the type is defined and contains at least one public member.</span></span> <span data-ttu-id="b30f5-105">请确保别名不包含其他别名。</span><span class="sxs-lookup"><span data-stu-id="b30f5-105">Make sure the alias name doesn't contain other aliases.</span></span>

 <span data-ttu-id="b30f5-106">项目的导入属性指定的包含元素无法找到或未定义任何 `Public` 成员。</span><span class="sxs-lookup"><span data-stu-id="b30f5-106">An import property of a project specifies a containing element that either cannot be found or does not define any `Public` members.</span></span>

 <span data-ttu-id="b30f5-107">*包含元素*可以是命名空间、类、结构、模块、接口或枚举。</span><span class="sxs-lookup"><span data-stu-id="b30f5-107">A *containing element* can be a namespace, class, structure, module, interface, or enumeration.</span></span> <span data-ttu-id="b30f5-108">包含元素包含变量、过程或其他包含元素等成员。</span><span class="sxs-lookup"><span data-stu-id="b30f5-108">The containing element contains members, such as variables, procedures, or other containing elements.</span></span>

 <span data-ttu-id="b30f5-109">导入的目的是允许你的代码访问命名空间或类型成员，而无需对其进行限定。</span><span class="sxs-lookup"><span data-stu-id="b30f5-109">The purpose of importing is to allow your code to access namespace or type members without having to qualify them.</span></span> <span data-ttu-id="b30f5-110">你的项目可能还需要添加对命名空间或类型的引用。</span><span class="sxs-lookup"><span data-stu-id="b30f5-110">Your project might also need to add a reference to the namespace or type.</span></span> <span data-ttu-id="b30f5-111">有关详细信息，请参阅对已 [声明元素的引用](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)中的 "导入包含元素"。</span><span class="sxs-lookup"><span data-stu-id="b30f5-111">For more information, see "Importing Containing Elements" in [References to Declared Elements](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md).</span></span>

 <span data-ttu-id="b30f5-112">如果编译器找不到指定的包含元素，则它无法解析使用它的引用。</span><span class="sxs-lookup"><span data-stu-id="b30f5-112">If the compiler cannot find the specified containing element, then it cannot resolve references that use it.</span></span> <span data-ttu-id="b30f5-113">如果找到元素但元素未公开任何 `Public` 成员，则不会成功进行引用。</span><span class="sxs-lookup"><span data-stu-id="b30f5-113">If it finds the element but the element does not expose any `Public` members, then no reference can be successful.</span></span> <span data-ttu-id="b30f5-114">在这两种情况下，导入元素是毫无意义的。</span><span class="sxs-lookup"><span data-stu-id="b30f5-114">In either case it is meaningless to import the element.</span></span>

 <span data-ttu-id="b30f5-115">使用 " **项目设计器** " 可以指定要导入的元素。</span><span class="sxs-lookup"><span data-stu-id="b30f5-115">You use the **Project Designer** to specify elements to import.</span></span> <span data-ttu-id="b30f5-116">使用 "**引用**" 页的 "**导入的命名空间**" 部分。</span><span class="sxs-lookup"><span data-stu-id="b30f5-116">Use the **Imported namespaces** section of the **References** page.</span></span> <span data-ttu-id="b30f5-117">可以通过双击 "**解决方案资源管理器**中的 **" 我的项目**"图标来转到"**项目设计器**"。</span><span class="sxs-lookup"><span data-stu-id="b30f5-117">You can get to the **Project Designer** by double-clicking the **My Project** icon in **Solution Explorer**.</span></span>

 <span data-ttu-id="b30f5-118">**错误 ID：** BC40057</span><span class="sxs-lookup"><span data-stu-id="b30f5-118">**Error ID:** BC40057</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="b30f5-119">更正此错误</span><span class="sxs-lookup"><span data-stu-id="b30f5-119">To correct this error</span></span>

1. <span data-ttu-id="b30f5-120">打开 " **项目设计器** "，并切换到 " **引用** " 页。</span><span class="sxs-lookup"><span data-stu-id="b30f5-120">Open the **Project Designer** and switch to the **Reference** page.</span></span>

2. <span data-ttu-id="b30f5-121">在 " **导入的命名空间** " 部分中，验证是否可以从项目访问包含元素。</span><span class="sxs-lookup"><span data-stu-id="b30f5-121">In the **Imported namespaces** section, verify that the containing element is accessible from your project.</span></span>

3. <span data-ttu-id="b30f5-122">验证包含元素是否至少公开一个 `Public` 成员。</span><span class="sxs-lookup"><span data-stu-id="b30f5-122">Verify that the containing element exposes at least one `Public` member.</span></span>

## <a name="see-also"></a><span data-ttu-id="b30f5-123">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b30f5-123">See also</span></span>

- [<span data-ttu-id="b30f5-124">项目设计器 -&gt;“引用”页 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b30f5-124">References Page, Project Designer (Visual Basic)</span></span>](/visualstudio/ide/reference/references-page-project-designer-visual-basic)
- [<span data-ttu-id="b30f5-125">管理项目和解决方案属性</span><span class="sxs-lookup"><span data-stu-id="b30f5-125">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)
- [<span data-ttu-id="b30f5-126">公共</span><span class="sxs-lookup"><span data-stu-id="b30f5-126">Public</span></span>](../modifiers/public.md)
- [<span data-ttu-id="b30f5-127">Visual Basic 中的命名空间</span><span class="sxs-lookup"><span data-stu-id="b30f5-127">Namespaces in Visual Basic</span></span>](../../programming-guide/program-structure/namespaces.md)
- [<span data-ttu-id="b30f5-128">References to Declared Elements</span><span class="sxs-lookup"><span data-stu-id="b30f5-128">References to Declared Elements</span></span>](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
