---
title: “<expression>”不能用作类型约束
ms.date: 07/20/2015
f1_keywords:
- bc32061
- vbc32061
helpviewer_keywords:
- BC32061
ms.assetid: b17821b7-fa14-4397-a211-6e2a14079f09
ms.openlocfilehash: 6e55bfdc175f285b335512e64f4c2407bdb0e8c7
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163085"
---
# <a name="bc32061-expression-cannot-be-used-as-a-type-constraint"></a><span data-ttu-id="8d8a1-102">BC32061： " \<expression> " 不能用作类型约束</span><span class="sxs-lookup"><span data-stu-id="8d8a1-102">BC32061: '\<expression>' cannot be used as a type constraint</span></span>

<span data-ttu-id="8d8a1-103">约束列表包含的表达式不表示对类型形参的有效约束。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-103">A constraint list includes an expression that does not represent a valid constraint on a type parameter.</span></span>

 <span data-ttu-id="8d8a1-104">约束列表对传递给类型形参的类型实参有一定要求。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-104">A constraint list imposes requirements on the type argument passed to the type parameter.</span></span> <span data-ttu-id="8d8a1-105">你可以采用任意组合指定以下要求：</span><span class="sxs-lookup"><span data-stu-id="8d8a1-105">You can specify the following requirements in any combination:</span></span>

- <span data-ttu-id="8d8a1-106">该类型实参必须实现一个或多个接口</span><span class="sxs-lookup"><span data-stu-id="8d8a1-106">The type argument must implement one or more interfaces</span></span>

- <span data-ttu-id="8d8a1-107">该类型实参最多从一个类继承</span><span class="sxs-lookup"><span data-stu-id="8d8a1-107">The type argument must inherit from at most one class</span></span>

- <span data-ttu-id="8d8a1-108">类型实参必须公开一个创建代码可以访问的无形参构造函数（包括 `New` 约束）</span><span class="sxs-lookup"><span data-stu-id="8d8a1-108">The type argument must expose a parameterless constructor that the creating code can access (include the `New` constraint)</span></span>

 <span data-ttu-id="8d8a1-109">如果不在约束列表中包括任何特定类或接口，则可以通过指定以下内容之一来施加更常规的要求：</span><span class="sxs-lookup"><span data-stu-id="8d8a1-109">If you do not include any specific class or interface in the constraint list, you can impose a more general requirement by specifying one of the following:</span></span>

- <span data-ttu-id="8d8a1-110">类型参数必须是值类型（包括 `Structure` 约束）</span><span class="sxs-lookup"><span data-stu-id="8d8a1-110">The type argument must be a value type (include the `Structure` constraint)</span></span>

- <span data-ttu-id="8d8a1-111">类型参数必须是引用类型（包括 `Class` 约束）</span><span class="sxs-lookup"><span data-stu-id="8d8a1-111">The type argument must be a reference type (include the `Class` constraint)</span></span>

 <span data-ttu-id="8d8a1-112">不能为同一类型参数同时指定 `Structure` 和 `Class` ，并且它们两个都只能指定一次。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-112">You cannot specify both `Structure` and `Class` for the same type parameter, and you cannot specify either one more than once.</span></span>

 <span data-ttu-id="8d8a1-113">**错误 ID：** BC32061</span><span class="sxs-lookup"><span data-stu-id="8d8a1-113">**Error ID:** BC32061</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="8d8a1-114">更正此错误</span><span class="sxs-lookup"><span data-stu-id="8d8a1-114">To correct this error</span></span>

- <span data-ttu-id="8d8a1-115">验证表达式及其元素是否拼写正确。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-115">Verify that the expression and its elements are spelled correctly.</span></span>

- <span data-ttu-id="8d8a1-116">如果表达式不符合前面列出的要求，请从约束列表中将其删除。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-116">If the expression does not qualify for the preceding list of requirements, remove it from the constraint list.</span></span>

- <span data-ttu-id="8d8a1-117">如果表达式引用接口或类，请验证编译器是否有权访问该接口或类。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-117">If the expression refers to an interface or class, verify that the compiler has access to that interface or class.</span></span> <span data-ttu-id="8d8a1-118">可能需要限定其名称，并可能需要添加一个项目引用。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-118">You might need to qualify its name, and you might need to add a reference to your project.</span></span> <span data-ttu-id="8d8a1-119">有关详细信息，请参阅对已 [声明元素的引用](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)中的 "项目引用"。</span><span class="sxs-lookup"><span data-stu-id="8d8a1-119">For more information, see "References to Projects" in [References to Declared Elements](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8d8a1-120">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8d8a1-120">See also</span></span>

- [<span data-ttu-id="8d8a1-121">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8d8a1-121">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
- [<span data-ttu-id="8d8a1-122">Value Types and Reference Types</span><span class="sxs-lookup"><span data-stu-id="8d8a1-122">Value Types and Reference Types</span></span>](../../programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [<span data-ttu-id="8d8a1-123">References to Declared Elements</span><span class="sxs-lookup"><span data-stu-id="8d8a1-123">References to Declared Elements</span></span>](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
