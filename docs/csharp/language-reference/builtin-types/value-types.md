---
description: 了解 C# 中的值类型、种类以及内置值类型
title: 值类型 - C# 参考
ms.date: 01/22/2020
f1_keywords:
- cs.valuetypes
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
ms.openlocfilehash: 6fb33ad2eb3f6a5e8f6506527f3807f31bf33fdc
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471646"
---
# <a name="value-types-c-reference"></a><span data-ttu-id="6fcc6-103">值类型（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="6fcc6-103">Value types (C# reference)</span></span>

<span data-ttu-id="6fcc6-104">值类型和[引用类型](../keywords/reference-types.md)是 C# 类型的两个主要类别。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-104">*Value types* and [reference types](../keywords/reference-types.md) are the two main categories of C# types.</span></span> <span data-ttu-id="6fcc6-105">值类型的变量包含类型的实例。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-105">A variable of a value type contains an instance of the type.</span></span> <span data-ttu-id="6fcc6-106">它不同于引用类型的变量，后者包含对类型实例的引用。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-106">This differs from a variable of a reference type, which contains a reference to an instance of the type.</span></span> <span data-ttu-id="6fcc6-107">默认情况下，在[分配](../operators/assignment-operator.md)中，通过将实参传递给方法并返回方法结果来复制变量值。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-107">By default, on [assignment](../operators/assignment-operator.md), passing an argument to a method, and returning a method result, variable values are copied.</span></span> <span data-ttu-id="6fcc6-108">对于值类型变量，会复制相应的类型实例。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-108">In the case of value-type variables, the corresponding type instances are copied.</span></span> <span data-ttu-id="6fcc6-109">以下示例演示了该行为：</span><span class="sxs-lookup"><span data-stu-id="6fcc6-109">The following example demonstrates that behavior:</span></span>

[!code-csharp[copy of values](snippets/shared/ValueTypes.cs#ValueTypeCopied)]

<span data-ttu-id="6fcc6-110">如前面的示例所示，对值类型变量的操作只影响存储在变量中的值类型实例。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-110">As the preceding example shows, operations on a value-type variable affect only that instance of the value type, stored in the variable.</span></span>

<span data-ttu-id="6fcc6-111">如果值类型包含引用类型的数据成员，则在复制值类型实例时，只会复制对引用类型实例的引用。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-111">If a value type contains a data member of a reference type, only the reference to the instance of the reference type is copied when a value-type instance is copied.</span></span> <span data-ttu-id="6fcc6-112">副本和原始值类型实例都具有对同一引用类型实例的访问权限。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-112">Both the copy and original value-type instance have access to the same reference-type instance.</span></span> <span data-ttu-id="6fcc6-113">以下示例演示了该行为：</span><span class="sxs-lookup"><span data-stu-id="6fcc6-113">The following example demonstrates that behavior:</span></span>

[!code-csharp[shallow copy](snippets/shared/ValueTypes.cs#ShallowCopy)]

> [!NOTE]
> <span data-ttu-id="6fcc6-114">若要使代码更不易出错、更可靠，请定义并使用不可变的值类型。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-114">To make your code less error-prone and more robust, define and use immutable value types.</span></span> <span data-ttu-id="6fcc6-115">本文仅为演示目的使用可变值类型。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-115">This article uses mutable value types only for demonstration purposes.</span></span>

## <a name="kinds-of-value-types"></a><span data-ttu-id="6fcc6-116">值类型的种类</span><span class="sxs-lookup"><span data-stu-id="6fcc6-116">Kinds of value types</span></span>

<span data-ttu-id="6fcc6-117">值类型可以是以下种类之一：</span><span class="sxs-lookup"><span data-stu-id="6fcc6-117">A value type can be one of the two following kinds:</span></span>

- <span data-ttu-id="6fcc6-118">[结构类型](struct.md)，用于封装数据和相关功能</span><span class="sxs-lookup"><span data-stu-id="6fcc6-118">a [structure type](struct.md), which encapsulates data and related functionality</span></span>
- <span data-ttu-id="6fcc6-119">[枚举类型](enum.md)，由一组命名常数定义，表示一个选择或选择组合</span><span class="sxs-lookup"><span data-stu-id="6fcc6-119">an [enumeration type](enum.md), which is defined by a set of named constants and represents a choice or a combination of choices</span></span>

<span data-ttu-id="6fcc6-120">[可为 null 值类型](nullable-value-types.md) `T?` 表示其基础值类型 `T` 的所有值及额外的 [null](../keywords/null.md) 值。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-120">A [nullable value type](nullable-value-types.md) `T?` represents all values of its underlying value type `T` and an additional [null](../keywords/null.md) value.</span></span> <span data-ttu-id="6fcc6-121">不能将 `null` 分配给值类型的变量，除非它是可为 null 的值类型。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-121">You cannot assign `null` to a variable of a value type, unless it's a nullable value type.</span></span>

## <a name="built-in-value-types"></a><span data-ttu-id="6fcc6-122">内置值类型</span><span class="sxs-lookup"><span data-stu-id="6fcc6-122">Built-in value types</span></span>

<span data-ttu-id="6fcc6-123">C# 提供以下内置值类型，也称为“简单类型”：</span><span class="sxs-lookup"><span data-stu-id="6fcc6-123">C# provides the following built-in value types, also known as *simple types* :</span></span>

- [<span data-ttu-id="6fcc6-124">整型数值类型</span><span class="sxs-lookup"><span data-stu-id="6fcc6-124">Integral numeric types</span></span>](integral-numeric-types.md)
- [<span data-ttu-id="6fcc6-125">浮点型数值类型</span><span class="sxs-lookup"><span data-stu-id="6fcc6-125">Floating-point numeric types</span></span>](floating-point-numeric-types.md)
- <span data-ttu-id="6fcc6-126">[bool](bool.md)，表示布尔值</span><span class="sxs-lookup"><span data-stu-id="6fcc6-126">[bool](bool.md) that represents a Boolean value</span></span>
- <span data-ttu-id="6fcc6-127">[char](char.md)，表示 Unicode UTF-16 字符</span><span class="sxs-lookup"><span data-stu-id="6fcc6-127">[char](char.md) that represents a Unicode UTF-16 character</span></span>

<span data-ttu-id="6fcc6-128">所有简单值都是结构类型，它们与其他结构类型的不同之处在于，它们允许特定的额外操作：</span><span class="sxs-lookup"><span data-stu-id="6fcc6-128">All simple types are structure types and differ from other structure types in that they permit certain additional operations:</span></span>

- <span data-ttu-id="6fcc6-129">可以使用文字为简单类型提供值。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-129">You can use literals to provide a value of a simple type.</span></span> <span data-ttu-id="6fcc6-130">例如，`'A'` 是类型 `char` 的文本，`2001` 是类型 `int` 的文本。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-130">For example, `'A'` is a literal of the type `char` and `2001` is a literal of the type `int`.</span></span>

- <span data-ttu-id="6fcc6-131">可以使用 [const](../keywords/const.md) 关键字声明简单类型的常数。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-131">You can declare constants of the simple types with the [const](../keywords/const.md) keyword.</span></span> <span data-ttu-id="6fcc6-132">不能具有其他结构类型的常数。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-132">It's not possible to have constants of other structure types.</span></span>

- <span data-ttu-id="6fcc6-133">常数表达式的操作数都是简单类型的常数，在编译时进行评估。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-133">Constant expressions, whose operands are all constants of the simple types, are evaluated at compile time.</span></span>

<span data-ttu-id="6fcc6-134">从 C# 7.0 开始，C# 支持[值元组](value-tuples.md)。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-134">Beginning with C# 7.0, C# supports [value tuples](value-tuples.md).</span></span> <span data-ttu-id="6fcc6-135">值元组是值类型，而不是简单类型。</span><span class="sxs-lookup"><span data-stu-id="6fcc6-135">A value tuple is a value type, but not a simple type.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="6fcc6-136">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="6fcc6-136">C# language specification</span></span>

<span data-ttu-id="6fcc6-137">有关更多信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的以下部分：</span><span class="sxs-lookup"><span data-stu-id="6fcc6-137">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="6fcc6-138">值类型</span><span class="sxs-lookup"><span data-stu-id="6fcc6-138">Value types</span></span>](~/_csharplang/spec/types.md#value-types)
- [<span data-ttu-id="6fcc6-139">简单类型</span><span class="sxs-lookup"><span data-stu-id="6fcc6-139">Simple types</span></span>](~/_csharplang/spec/types.md#simple-types)
- [<span data-ttu-id="6fcc6-140">变量</span><span class="sxs-lookup"><span data-stu-id="6fcc6-140">Variables</span></span>](~/_csharplang/spec/variables.md)

## <a name="see-also"></a><span data-ttu-id="6fcc6-141">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6fcc6-141">See also</span></span>

- [<span data-ttu-id="6fcc6-142">C# 参考</span><span class="sxs-lookup"><span data-stu-id="6fcc6-142">C# reference</span></span>](../index.md)
- <xref:System.ValueType?displayProperty=nameWithType>
- [<span data-ttu-id="6fcc6-143">引用类型</span><span class="sxs-lookup"><span data-stu-id="6fcc6-143">Reference types</span></span>](../keywords/reference-types.md)
