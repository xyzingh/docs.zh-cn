---
description: override 修饰符 - C# 参考
title: override 修饰符 - C# 参考
ms.date: 10/22/2020
f1_keywords:
- override
- override_CSharpKeyword
helpviewer_keywords:
- override keyword [C#]
ms.assetid: dd1907a8-acf8-46d3-80b9-c2ca4febada8
ms.openlocfilehash: 618200183348e68a4600adb9592a635f61f6a875
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434873"
---
# <a name="override-c-reference"></a><span data-ttu-id="bd640-103">override（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="bd640-103">override (C# reference)</span></span>

<span data-ttu-id="bd640-104">扩展或修改继承的方法、属性、索引器或事件的抽象或虚拟实现需要 `override` 修饰符。</span><span class="sxs-lookup"><span data-stu-id="bd640-104">The `override` modifier is required to extend or modify the abstract or virtual implementation of an inherited method, property, indexer, or event.</span></span>

<span data-ttu-id="bd640-105">在以下示例中，`Square` 类必须提供 `GetArea` 的重写实现，因为 `GetArea` 继承自抽象 `Shape` 类：</span><span class="sxs-lookup"><span data-stu-id="bd640-105">In the following example, the `Square` class must provide an overridden implementation of `GetArea` because `GetArea` is inherited from the abstract `Shape` class:</span></span>

[!code-csharp[csrefKeywordsModifiers#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#1)]

<span data-ttu-id="bd640-106">`override` 方法提供从基类继承的方法的新实现。</span><span class="sxs-lookup"><span data-stu-id="bd640-106">An `override` method provides a new implementation of the method inherited from a base class.</span></span> <span data-ttu-id="bd640-107">通过 `override` 声明重写的方法称为重写基方法。</span><span class="sxs-lookup"><span data-stu-id="bd640-107">The method that is overridden by an `override` declaration is known as the overridden base method.</span></span> <span data-ttu-id="bd640-108">`override` 方法必须具有与重写基方法相同的签名。</span><span class="sxs-lookup"><span data-stu-id="bd640-108">An `override` method must have the same signature as the overridden base method.</span></span> <span data-ttu-id="bd640-109">从 C# 9.0 开始，`override` 方法支持协变返回类型。</span><span class="sxs-lookup"><span data-stu-id="bd640-109">Beginning with C# 9.0, `override` methods support covariant return types.</span></span> <span data-ttu-id="bd640-110">具体而言，`override` 方法的返回类型可从相应基方法的返回类型派生。</span><span class="sxs-lookup"><span data-stu-id="bd640-110">In particular, the return type of an `override` method can derive from the return type of the corresponding base method.</span></span> <span data-ttu-id="bd640-111">在 C# 8.0 和更早版本中，`override` 方法和重写基方法的返回类型必须相同。</span><span class="sxs-lookup"><span data-stu-id="bd640-111">In C# 8.0 and earlier, the return types of an `override` method and the overridden base method must be the same.</span></span>

<span data-ttu-id="bd640-112">不能重写非虚方法或静态方法。</span><span class="sxs-lookup"><span data-stu-id="bd640-112">You cannot override a non-virtual or static method.</span></span> <span data-ttu-id="bd640-113">重写基方法必须是 `virtual`、`abstract` 或 `override`。</span><span class="sxs-lookup"><span data-stu-id="bd640-113">The overridden base method must be `virtual`, `abstract`, or `override`.</span></span>

<span data-ttu-id="bd640-114">`override` 声明不能更改 `virtual` 方法的可访问性。</span><span class="sxs-lookup"><span data-stu-id="bd640-114">An `override` declaration cannot change the accessibility of the `virtual` method.</span></span> <span data-ttu-id="bd640-115">`override` 方法和 `virtual` 方法必须具有相同[级别访问修饰符](access-modifiers.md)。</span><span class="sxs-lookup"><span data-stu-id="bd640-115">Both the `override` method and the `virtual` method must have the same [access level modifier](access-modifiers.md).</span></span>

<span data-ttu-id="bd640-116">不能使用 `new`、`static` 或 `virtual` 修饰符修改 `override` 方法。</span><span class="sxs-lookup"><span data-stu-id="bd640-116">You cannot use the `new`, `static`, or `virtual` modifiers to modify an `override` method.</span></span>

<span data-ttu-id="bd640-117">重写属性声明必须指定与继承的属性完全相同的访问修饰符、类型和名称。</span><span class="sxs-lookup"><span data-stu-id="bd640-117">An overriding property declaration must specify exactly the same access modifier, type, and name as the inherited property.</span></span> <span data-ttu-id="bd640-118">从 C# 9.0 开始，只读重写属性支持协变返回类型。</span><span class="sxs-lookup"><span data-stu-id="bd640-118">Beginning with C# 9.0, read-only overriding properties support covariant return types.</span></span> <span data-ttu-id="bd640-119">重写属性必须为 `virtual`、`abstract` 或 `override`。</span><span class="sxs-lookup"><span data-stu-id="bd640-119">The overridden property must be `virtual`, `abstract`, or `override`.</span></span>

<span data-ttu-id="bd640-120">有关如何使用 `override` 关键字的详细信息，请参阅[使用 Override 和 New 关键字进行版本控制](../../programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)和[了解何时使用 Override 和 New 关键字](../../programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)。</span><span class="sxs-lookup"><span data-stu-id="bd640-120">For more information about how to use the `override` keyword, see [Versioning with the Override and New Keywords](../../programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) and [Knowing when to use Override and New Keywords](../../programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).</span></span> <span data-ttu-id="bd640-121">有关继承的信息，请参阅[继承](../../programming-guide/classes-and-structs/inheritance.md)。</span><span class="sxs-lookup"><span data-stu-id="bd640-121">For information about inheritance, see [Inheritance](../../programming-guide/classes-and-structs/inheritance.md).</span></span>

## <a name="example"></a><span data-ttu-id="bd640-122">示例</span><span class="sxs-lookup"><span data-stu-id="bd640-122">Example</span></span>

<span data-ttu-id="bd640-123">此示例定义一个名为 `Employee` 的基类和一个名为 `SalesEmployee` 的派生类。</span><span class="sxs-lookup"><span data-stu-id="bd640-123">This example defines a base class named `Employee`, and a derived class named `SalesEmployee`.</span></span> <span data-ttu-id="bd640-124">`SalesEmployee` 类包含一个额外字段 `salesbonus`，并且重写方法 `CalculatePay` 以将它考虑在内。</span><span class="sxs-lookup"><span data-stu-id="bd640-124">The `SalesEmployee` class includes an extra field, `salesbonus`, and overrides the method `CalculatePay` in order to take it into account.</span></span>

[!code-csharp[csrefKeywordsModifiers#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#9)]

## <a name="c-language-specification"></a><span data-ttu-id="bd640-125">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="bd640-125">C# language specification</span></span>

<span data-ttu-id="bd640-126">有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)中的[重写方法](~/_csharplang/spec/classes.md#override-methods)部分。</span><span class="sxs-lookup"><span data-stu-id="bd640-126">For more information, see the [Override methods](~/_csharplang/spec/classes.md#override-methods) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="bd640-127">有关协变返回类型的详细信息，请参阅[功能建议说明](~/_csharplang/proposals/csharp-9.0/covariant-returns.md)。</span><span class="sxs-lookup"><span data-stu-id="bd640-127">For more information about covariant return types, see the [feature proposal note](~/_csharplang/proposals/csharp-9.0/covariant-returns.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="bd640-128">另请参阅</span><span class="sxs-lookup"><span data-stu-id="bd640-128">See also</span></span>

- [<span data-ttu-id="bd640-129">C# 参考</span><span class="sxs-lookup"><span data-stu-id="bd640-129">C# reference</span></span>](../index.md)
- [<span data-ttu-id="bd640-130">继承</span><span class="sxs-lookup"><span data-stu-id="bd640-130">Inheritance</span></span>](../../programming-guide/classes-and-structs/inheritance.md)
- [<span data-ttu-id="bd640-131">C# 关键字</span><span class="sxs-lookup"><span data-stu-id="bd640-131">C# keywords</span></span>](index.md)
- [<span data-ttu-id="bd640-132">修饰符</span><span class="sxs-lookup"><span data-stu-id="bd640-132">Modifiers</span></span>](index.md)
- [<span data-ttu-id="bd640-133">abstract</span><span class="sxs-lookup"><span data-stu-id="bd640-133">abstract</span></span>](abstract.md)
- [<span data-ttu-id="bd640-134">virtual</span><span class="sxs-lookup"><span data-stu-id="bd640-134">virtual</span></span>](virtual.md)
- [<span data-ttu-id="bd640-135">new（修饰符）</span><span class="sxs-lookup"><span data-stu-id="bd640-135">new (modifier)</span></span>](new-modifier.md)
- [<span data-ttu-id="bd640-136">多态性</span><span class="sxs-lookup"><span data-stu-id="bd640-136">Polymorphism</span></span>](../../programming-guide/classes-and-structs/polymorphism.md)
