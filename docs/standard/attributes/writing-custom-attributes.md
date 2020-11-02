---
title: 编写自定义特性
description: 在 .NET 中设计你自己的自定义属性。 自定义属性本质上是直接或间接派生自 System.Attribute 的类。
ms.date: 07/17/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- multiple attribute instances
- AttributeTargets enumeration
- attributes [.NET], custom
- AllowMultiple property
- custom attributes
- AttributeUsageAttribute class, custom attributes
- Inherited property
- attribute classes, declaring
ms.assetid: 97216f69-bde8-49fd-ac40-f18c500ef5dc
ms.openlocfilehash: 670f34083834b35d26e6018372948022eec17d47
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889187"
---
# <a name="writing-custom-attributes"></a><span data-ttu-id="3b9ab-104">编写自定义特性</span><span class="sxs-lookup"><span data-stu-id="3b9ab-104">Writing Custom Attributes</span></span>
<span data-ttu-id="3b9ab-105">要设计你自己的自定义特性，无需掌握许多新的概念。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-105">To design your own custom attributes, you do not need to master many new concepts.</span></span> <span data-ttu-id="3b9ab-106">如果你熟悉面向对象的编程，并且知道如何设计类，那么你已经具备大部分所需知识。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-106">If you are familiar with object-oriented programming and know how to design classes, you already have most of the knowledge needed.</span></span> <span data-ttu-id="3b9ab-107">自定义特性本质上是直接或间接派生自 <xref:System.Attribute?displayProperty=nameWithType>的传统类。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-107">Custom attributes are essentially traditional classes that derive directly or indirectly from <xref:System.Attribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="3b9ab-108">与传统类一样，自定义特性包含用于存储和检索数据的方法。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-108">Just like traditional classes, custom attributes contain methods that store and retrieve data.</span></span>  
  
 <span data-ttu-id="3b9ab-109">正确设计自定义特性的主要步骤如下：</span><span class="sxs-lookup"><span data-stu-id="3b9ab-109">The primary steps to properly design custom attribute classes are as follows:</span></span>  
  
- [<span data-ttu-id="3b9ab-110">应用 AttributeUsageAttribute</span><span class="sxs-lookup"><span data-stu-id="3b9ab-110">Applying the AttributeUsageAttribute</span></span>](#applying-the-attributeusageattribute)  
  
- [<span data-ttu-id="3b9ab-111">声明特性类</span><span class="sxs-lookup"><span data-stu-id="3b9ab-111">Declaring the attribute class</span></span>](#declaring-the-attribute-class)  
  
- [<span data-ttu-id="3b9ab-112">声明构造函数</span><span class="sxs-lookup"><span data-stu-id="3b9ab-112">Declaring constructors</span></span>](#declaring-constructors)  
  
- [<span data-ttu-id="3b9ab-113">声明属性</span><span class="sxs-lookup"><span data-stu-id="3b9ab-113">Declaring properties</span></span>](#declaring-properties)  
  
 <span data-ttu-id="3b9ab-114">本节描述上述各个步骤，并以 [自定义特性的示例](#custom-attribute-example)结束本节的描述。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-114">This section describes each of these steps and concludes with a [custom attribute example](#custom-attribute-example).</span></span>  
  
## <a name="applying-the-attributeusageattribute"></a><span data-ttu-id="3b9ab-115">应用 AttributeUsageAttribute</span><span class="sxs-lookup"><span data-stu-id="3b9ab-115">Applying the AttributeUsageAttribute</span></span>  
 <span data-ttu-id="3b9ab-116">自定义特性声明以 <xref:System.AttributeUsageAttribute?displayProperty=nameWithType> 开头，定义了特性类的一些主要特征。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-116">A custom attribute declaration begins with the <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>, which defines some of the key characteristics of your attribute class.</span></span> <span data-ttu-id="3b9ab-117">例如，你可以指定其他类是否可以继承你的特性，或者指定此特性可以应用到哪些元素。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-117">For example, you can specify whether your attribute can be inherited by other classes or specify which elements the attribute can be applied to.</span></span> <span data-ttu-id="3b9ab-118">下面的代码片段演示了 <xref:System.AttributeUsageAttribute> 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-118">The following code fragment demonstrates how to use the <xref:System.AttributeUsageAttribute>.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#5)]
 [!code-csharp[Conceptual.Attributes.Usage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#5)]
 [!code-vb[Conceptual.Attributes.Usage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#5)]  
  
 <span data-ttu-id="3b9ab-119"><xref:System.AttributeUsageAttribute> 包含下列三个成员，它们对创建自定义属性非常重要：[AttributeTargets](#attributetargets-member)、[Inherited](#inherited-property) 和 [AllowMultiple](#allowmultiple-property)。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-119">The <xref:System.AttributeUsageAttribute> has three members that are important for the creation of custom attributes: [AttributeTargets](#attributetargets-member), [Inherited](#inherited-property), and [AllowMultiple](#allowmultiple-property).</span></span>  
  
### <a name="attributetargets-member"></a><span data-ttu-id="3b9ab-120">AttributeTargets 成员</span><span class="sxs-lookup"><span data-stu-id="3b9ab-120">AttributeTargets Member</span></span>  
 <span data-ttu-id="3b9ab-121">上述示例中指定了 <xref:System.AttributeTargets.All?displayProperty=nameWithType>，它表示此特性可应用于所有程序元素。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-121">In the previous example, <xref:System.AttributeTargets.All?displayProperty=nameWithType> is specified, indicating that this attribute can be applied to all program elements.</span></span> <span data-ttu-id="3b9ab-122">或者，你可指定 <xref:System.AttributeTargets.Class?displayProperty=nameWithType> 和 <xref:System.AttributeTargets.Method?displayProperty=nameWithType>，前者表示你的特性仅可适用于一个类，后者表示你的特性仅可应用于一种方法。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-122">Alternatively, you can specify <xref:System.AttributeTargets.Class?displayProperty=nameWithType>, indicating that your attribute can be applied only to a class, or <xref:System.AttributeTargets.Method?displayProperty=nameWithType>, indicating that your attribute can be applied only to a method.</span></span> <span data-ttu-id="3b9ab-123">所有程序元素都可以通过这种方式使用自定义特性来标记，以对其进行描述。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-123">All program elements can be marked for description by a custom attribute in this manner.</span></span>  
  
 <span data-ttu-id="3b9ab-124">你还可传递多个 <xref:System.AttributeTargets> 值。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-124">You can also pass multiple <xref:System.AttributeTargets> values.</span></span> <span data-ttu-id="3b9ab-125">下面的代码段指定了自定义特性可应用于任何类或方法。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-125">The following code fragment specifies that a custom attribute can be applied to any class or method.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#6)]
 [!code-csharp[Conceptual.Attributes.Usage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#6)]
 [!code-vb[Conceptual.Attributes.Usage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#6)]  
  
### <a name="inherited-property"></a><span data-ttu-id="3b9ab-126">Inherited 属性</span><span class="sxs-lookup"><span data-stu-id="3b9ab-126">Inherited Property</span></span>  
 <span data-ttu-id="3b9ab-127"><xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> 属性指明要对其应用属性的类的派生类能否继承此属性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-127">The <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> property indicates whether your attribute can be inherited by classes that are derived from the classes to which your attribute is applied.</span></span> <span data-ttu-id="3b9ab-128">此属性使用 `true`（默认值）或 `false` 标志。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-128">This property takes either a `true` (the default) or `false` flag.</span></span> <span data-ttu-id="3b9ab-129">在下例中，`MyAttribute` 的 <xref:System.AttributeUsageAttribute.Inherited%2A> 值为默认值 `true`，而 `YourAttribute` 的 <xref:System.AttributeUsageAttribute.Inherited%2A> 值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-129">In the following example, `MyAttribute` has a default <xref:System.AttributeUsageAttribute.Inherited%2A> value of `true`, while `YourAttribute` has an <xref:System.AttributeUsageAttribute.Inherited%2A> value of `false`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Attributes.Usage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#7)]
 [!code-vb[Conceptual.Attributes.Usage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#7)]  
  
 <span data-ttu-id="3b9ab-130">然后，这两个特性应用于基类 `MyClass`中的方法。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-130">The two attributes are then applied to a method in the base class `MyClass`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#9)]
 [!code-csharp[Conceptual.Attributes.Usage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#9)]
 [!code-vb[Conceptual.Attributes.Usage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#9)]  
  
 <span data-ttu-id="3b9ab-131">最后，从基类 `YourClass` 中继承类 `MyClass`。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-131">Finally, the class `YourClass` is inherited from the base class `MyClass`.</span></span> <span data-ttu-id="3b9ab-132">方法 `MyMethod` 显示 `MyAttribute`，但不显示 `YourAttribute`。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-132">The method `MyMethod` shows `MyAttribute`, but not `YourAttribute`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#10)]
 [!code-csharp[Conceptual.Attributes.Usage#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#10)]
 [!code-vb[Conceptual.Attributes.Usage#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#10)]  
  
### <a name="allowmultiple-property"></a><span data-ttu-id="3b9ab-133">AllowMultiple 属性</span><span class="sxs-lookup"><span data-stu-id="3b9ab-133">AllowMultiple Property</span></span>  
 <span data-ttu-id="3b9ab-134"><xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=nameWithType> 属性指明元素能否包含属性的多个实例。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-134">The <xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=nameWithType> property indicates whether multiple instances of your attribute can exist on an element.</span></span> <span data-ttu-id="3b9ab-135">如果设置为 `true`，则允许多个实例；如果设置为 `false`（默认值），则只允许一个实例。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-135">If set to `true`, multiple instances are allowed; if set to `false` (the default), only one instance is allowed.</span></span>  
  
 <span data-ttu-id="3b9ab-136">在下例中，`MyAttribute` 的 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 值为默认值 `false`，而 `YourAttribute` 的值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-136">In the following example, `MyAttribute` has a default <xref:System.AttributeUsageAttribute.AllowMultiple%2A> value of `false`, while `YourAttribute` has a value of `true`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#11)]
 [!code-csharp[Conceptual.Attributes.Usage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#11)]
 [!code-vb[Conceptual.Attributes.Usage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#11)]  
  
 <span data-ttu-id="3b9ab-137">当应用这些特性的多个实例时， `MyAttribute` 会生成编译器错误。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-137">When multiple instances of these attributes are applied, `MyAttribute` produces a compiler error.</span></span> <span data-ttu-id="3b9ab-138">下面的代码示例显示 `YourAttribute` 的有效用法和 `MyAttribute`的无效用法。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-138">The following code example shows the valid use of `YourAttribute` and the invalid use of `MyAttribute`.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#13)]
 [!code-csharp[Conceptual.Attributes.Usage#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#13)]
 [!code-vb[Conceptual.Attributes.Usage#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#13)]  
  
 <span data-ttu-id="3b9ab-139">如果 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 属性和 <xref:System.AttributeUsageAttribute.Inherited%2A> 属性都设置为 `true`，则从另一个类继承的类可继承一个特性，并且具有同一子类中应用的同一特性的另一个实例。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-139">If both the <xref:System.AttributeUsageAttribute.AllowMultiple%2A> property and the <xref:System.AttributeUsageAttribute.Inherited%2A> property are set to `true`, a class that is inherited from another class can inherit an attribute and have another instance of the same attribute applied in the same child class.</span></span> <span data-ttu-id="3b9ab-140">如果 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 设置为 `false`，则父类中的所有特性的值将被子类中同一特性的新实例覆盖。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-140">If <xref:System.AttributeUsageAttribute.AllowMultiple%2A> is set to `false`, the values of any attributes in the parent class will be overwritten by new instances of the same attribute in the child class.</span></span>  
  
## <a name="declaring-the-attribute-class"></a><span data-ttu-id="3b9ab-141">声明特性类</span><span class="sxs-lookup"><span data-stu-id="3b9ab-141">Declaring the Attribute Class</span></span>  
 <span data-ttu-id="3b9ab-142">应用 <xref:System.AttributeUsageAttribute>以后，可以开始定义特性的细节。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-142">After you apply the <xref:System.AttributeUsageAttribute>, you can begin to define the specifics of your attribute.</span></span> <span data-ttu-id="3b9ab-143">特性类的声明类似于传统类的声明，如以下代码所示。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-143">The declaration of an attribute class looks similar to the declaration of a traditional class, as demonstrated by the following code.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#14)]
 [!code-csharp[Conceptual.Attributes.Usage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#14)]
 [!code-vb[Conceptual.Attributes.Usage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#14)]  
  
 <span data-ttu-id="3b9ab-144">此特性定义说明了以下几点：</span><span class="sxs-lookup"><span data-stu-id="3b9ab-144">This attribute definition demonstrates the following points:</span></span>  
  
- <span data-ttu-id="3b9ab-145">特性类必须声明为公共类。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-145">Attribute classes must be declared as public classes.</span></span>  
  
- <span data-ttu-id="3b9ab-146">按照约定，特性类的名称以单词 **Attribute** 结束。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-146">By convention, the name of the attribute class ends with the word **Attribute** .</span></span> <span data-ttu-id="3b9ab-147">尽管没有要求，但仍建议执行此约定以保证可读性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-147">While not required, this convention is recommended for readability.</span></span> <span data-ttu-id="3b9ab-148">应用特性时，可以选择是否包含单词 Attribute。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-148">When the attribute is applied, the inclusion of the word Attribute is optional.</span></span>  
  
- <span data-ttu-id="3b9ab-149">所有特性类必须直接或间接从 <xref:System.Attribute?displayProperty=nameWithType> 继承。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-149">All attribute classes must inherit directly or indirectly from <xref:System.Attribute?displayProperty=nameWithType>.</span></span>  
  
- <span data-ttu-id="3b9ab-150">在 Microsoft Visual Basic 中，所有自定义特性类必须具有 <xref:System.AttributeUsageAttribute?displayProperty=nameWithType> 特性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-150">In Microsoft Visual Basic, all custom attribute classes must have the <xref:System.AttributeUsageAttribute?displayProperty=nameWithType> attribute.</span></span>  
  
## <a name="declaring-constructors"></a><span data-ttu-id="3b9ab-151">声明构造函数</span><span class="sxs-lookup"><span data-stu-id="3b9ab-151">Declaring Constructors</span></span>  
 <span data-ttu-id="3b9ab-152">与传统类的初始化方式相同，使用构造函数初始化特性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-152">Attributes are initialized with constructors in the same way as traditional classes.</span></span> <span data-ttu-id="3b9ab-153">下面的代码段阐明了典型的特性构造函数。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-153">The following code fragment illustrates a typical attribute constructor.</span></span> <span data-ttu-id="3b9ab-154">此公共构造函数采用一个参数，并设置一个等于其值的成员变量。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-154">This public constructor takes a parameter and sets a member variable equal to its value.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#15)]
 [!code-csharp[Conceptual.Attributes.Usage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#15)]
 [!code-vb[Conceptual.Attributes.Usage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#15)]  
  
 <span data-ttu-id="3b9ab-155">可以重载此构造函数以适应值的各种组合。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-155">You can overload the constructor to accommodate different combinations of values.</span></span> <span data-ttu-id="3b9ab-156">如果你还为自定义特性类定义了 [属性](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)) ，则在初始化该特性时可以使用命名参数和定位参数的组合。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-156">If you also define a [property](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)) for your custom attribute class, you can use a combination of named and positional parameters when initializing the attribute.</span></span> <span data-ttu-id="3b9ab-157">通常情况下，将所有必选的参数定义为定位参数，将所有可选的参数定义为命名参数。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-157">Typically, you define all required parameters as positional and all optional parameters as named.</span></span> <span data-ttu-id="3b9ab-158">在这种情况下，没有必选参数则无法初始化特性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-158">In this case, the attribute cannot be initialized without the required parameter.</span></span> <span data-ttu-id="3b9ab-159">其他所有参数都是可选参数。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-159">All other parameters are optional.</span></span> <span data-ttu-id="3b9ab-160">请注意，在 Visual Basic 中，特性类的构造函数不应使用 ParamArray 参数。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-160">Note that in Visual Basic, constructors for an attribute class should not use a ParamArray argument.</span></span>  
  
 <span data-ttu-id="3b9ab-161">下面的代码示例显示如何使用可选和必选参数应用使用上例中的构造函数的特性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-161">The following code example shows how an attribute that uses the previous constructor can be applied using optional and required parameters.</span></span> <span data-ttu-id="3b9ab-162">该示例假定特性有一个必选的布尔值和一个可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-162">It assumes that the attribute has one required Boolean value and one optional string property.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#17)]
 [!code-csharp[Conceptual.Attributes.Usage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#17)]
 [!code-vb[Conceptual.Attributes.Usage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#17)]  
  
## <a name="declaring-properties"></a><span data-ttu-id="3b9ab-163">声明属性</span><span class="sxs-lookup"><span data-stu-id="3b9ab-163">Declaring Properties</span></span>  
 <span data-ttu-id="3b9ab-164">如果你想要定义一个命名参数，或者提供一种简单的方法来返回由特性存储的值，请声明 [属性](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120))。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-164">If you want to define a named parameter or provide an easy way to return the values stored by your attribute, declare a [property](/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)).</span></span> <span data-ttu-id="3b9ab-165">应将特性的属性声明为公共实体，此公告实体包含将返回的数据类型的描述。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-165">Attribute properties should be declared as public entities with a description of the data type that will be returned.</span></span> <span data-ttu-id="3b9ab-166">定义将保存属性值的变量，并将此变量与 **get** 和 **set** 方法相关联。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-166">Define the variable that will hold the value of your property and associate it with the **get** and **set** methods.</span></span> <span data-ttu-id="3b9ab-167">下面的代码示例说明如何在特性中实现一个简单属性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-167">The following code example demonstrates how to implement a simple property in your attribute.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#16](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#16)]
 [!code-csharp[Conceptual.Attributes.Usage#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#16)]
 [!code-vb[Conceptual.Attributes.Usage#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#16)]  
  
## <a name="custom-attribute-example"></a><span data-ttu-id="3b9ab-168">自定义特性的示例</span><span class="sxs-lookup"><span data-stu-id="3b9ab-168">Custom Attribute Example</span></span>  
 <span data-ttu-id="3b9ab-169">本节内容结合了前面的信息，显示如何设计一个简单特性来记录有关代码段的作者的信息。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-169">This section incorporates the previous information and shows how to design a simple attribute that documents information about the author of a section of code.</span></span> <span data-ttu-id="3b9ab-170">本示例中的特性存储了编程人员的姓名和级别，以及是否已检查此代码的信息。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-170">The attribute in this example stores the name and level of the programmer, and whether the code has been reviewed.</span></span> <span data-ttu-id="3b9ab-171">它使用三个私有变量来存储要保存的实际值。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-171">It uses three private variables to store the actual values to save.</span></span> <span data-ttu-id="3b9ab-172">每个变量用获取和设置这些值的公共属性表示。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-172">Each variable is represented by a public property that gets and sets the values.</span></span> <span data-ttu-id="3b9ab-173">最后，使用两个必选参数定义构造函数。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-173">Finally, the constructor is defined with two required parameters.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#4)]
 [!code-csharp[Conceptual.Attributes.Usage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#4)]
 [!code-vb[Conceptual.Attributes.Usage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#4)]  
  
 <span data-ttu-id="3b9ab-174">可以采用以下任一种方法，使用全称 `DeveloperAttribute`或缩写名称 `Developer`应用此特性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-174">You can apply this attribute using the full name, `DeveloperAttribute`, or using the abbreviated name, `Developer`, in one of the following ways.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#12)]
 [!code-csharp[Conceptual.Attributes.Usage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#12)]
 [!code-vb[Conceptual.Attributes.Usage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#12)]  
  
 <span data-ttu-id="3b9ab-175">第一个示例显示只应用了必选命名参数的特性，第二个示例显示同时应用了必选参数和可选参数的特性。</span><span class="sxs-lookup"><span data-stu-id="3b9ab-175">The first example shows the attribute applied with only the required named parameters, while the second example shows the attribute applied with both the required and optional parameters.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3b9ab-176">请参阅</span><span class="sxs-lookup"><span data-stu-id="3b9ab-176">See also</span></span>

- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>
- [<span data-ttu-id="3b9ab-177">特性</span><span class="sxs-lookup"><span data-stu-id="3b9ab-177">Attributes</span></span>](index.md)
