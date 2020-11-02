---
title: 检索存储在特性中的信息
description: 了解如何检索存储在特性中的信息，例如，对于同一范围内的特性实例、多个实例，以及不同范围内的多个实例。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- retrieving attributes
- multiple attribute instances
- attributes [.NET], retrieving
ms.assetid: 37dfe4e3-7da0-48b6-a3d9-398981524e1c
ms.openlocfilehash: 710f3e3d1051bad4a61e59e330204d622b9fd683
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889200"
---
# <a name="retrieving-information-stored-in-attributes"></a><span data-ttu-id="cffbb-103">检索存储在特性中的信息</span><span class="sxs-lookup"><span data-stu-id="cffbb-103">Retrieving Information Stored in Attributes</span></span>
<span data-ttu-id="cffbb-104">检索自定义属性的过程非常简单。</span><span class="sxs-lookup"><span data-stu-id="cffbb-104">Retrieving a custom attribute is a simple process.</span></span> <span data-ttu-id="cffbb-105">首先，声明要检索的属性实例。</span><span class="sxs-lookup"><span data-stu-id="cffbb-105">First, declare an instance of the attribute you want to retrieve.</span></span> <span data-ttu-id="cffbb-106">然后，使用 <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=nameWithType> 方法，用要检索的属性的值初始化新属性。</span><span class="sxs-lookup"><span data-stu-id="cffbb-106">Then, use the <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=nameWithType> method to initialize the new attribute to the value of the attribute you want to retrieve.</span></span> <span data-ttu-id="cffbb-107">在初始化新属性后，只需使用它的属性即可获取值。</span><span class="sxs-lookup"><span data-stu-id="cffbb-107">Once the new attribute is initialized, you simply use its properties to get the values.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="cffbb-108">本主题介绍了如何为执行上下文中加载的代码检索属性。</span><span class="sxs-lookup"><span data-stu-id="cffbb-108">This topic describes how to retrieve attributes for code loaded into the execution context.</span></span> <span data-ttu-id="cffbb-109">若要为仅反射上下文中加载的代码检索属性，必须使用 <xref:System.Reflection.CustomAttributeData> 类，如以下所述：[如何：将程序集加载到仅反射上下文中](../../framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)。</span><span class="sxs-lookup"><span data-stu-id="cffbb-109">To retrieve attributes for code loaded into the reflection-only context, you must use the <xref:System.Reflection.CustomAttributeData> class, as shown in [How to: Load Assemblies into the Reflection-Only Context](../../framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).</span></span>  
  
 <span data-ttu-id="cffbb-110">此部分介绍了如何通过以下方式检索属性：</span><span class="sxs-lookup"><span data-stu-id="cffbb-110">This section describes the following ways to retrieve attributes:</span></span>  
  
- [<span data-ttu-id="cffbb-111">检索一个属性实例</span><span class="sxs-lookup"><span data-stu-id="cffbb-111">Retrieving a single instance of an attribute</span></span>](#cpconretrievingsingleinstanceofattribute)  
  
- [<span data-ttu-id="cffbb-112">检索应用于同一范围的多个属性实例</span><span class="sxs-lookup"><span data-stu-id="cffbb-112">Retrieving multiple instances of an attribute applied to the same scope</span></span>](#cpconretrievingmultipleinstancesofattributeappliedtosamescope)  
  
- [<span data-ttu-id="cffbb-113">检索应用于不同范围的多个属性实例</span><span class="sxs-lookup"><span data-stu-id="cffbb-113">Retrieving multiple instances of an attribute applied to different scopes</span></span>](#cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes)  
  
<a name="cpconretrievingsingleinstanceofattribute"></a>
## <a name="retrieving-a-single-instance-of-an-attribute"></a><span data-ttu-id="cffbb-114">检索一个属性实例</span><span class="sxs-lookup"><span data-stu-id="cffbb-114">Retrieving a Single Instance of an Attribute</span></span>  
 <span data-ttu-id="cffbb-115">在下面的示例中，`DeveloperAttribute`（如上一部分所述）在类一级适用于 `MainApp` 类。</span><span class="sxs-lookup"><span data-stu-id="cffbb-115">In the following example, the `DeveloperAttribute` (described in the previous section) is applied to the `MainApp` class on the class level.</span></span> <span data-ttu-id="cffbb-116">`GetAttribute` 方法使用 GetCustomAttribute 在类一级检索 `DeveloperAttribute` 中存储的值，再在控制台中显示它们。</span><span class="sxs-lookup"><span data-stu-id="cffbb-116">The `GetAttribute` method uses **GetCustomAttribute** to retrieve the values stored in `DeveloperAttribute` on the class level before displaying them to the console.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#18)]
 [!code-csharp[Conceptual.Attributes.Usage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#18)]
 [!code-vb[Conceptual.Attributes.Usage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#18)]  
  
 <span data-ttu-id="cffbb-117">此程序在执行时显示以下文本。</span><span class="sxs-lookup"><span data-stu-id="cffbb-117">This program displays the following text when executed.</span></span>  
  
```console  
The Name Attribute is: Joan Smith.  
The Level Attribute is: 42.  
The Reviewed Attribute is: True.  
```  
  
 <span data-ttu-id="cffbb-118">如果找不到属性，GetCustomAttribute 方法会将 `MyAttribute` 初始化为 NULL 值。</span><span class="sxs-lookup"><span data-stu-id="cffbb-118">If the attribute is not found, the **GetCustomAttribute** method initializes `MyAttribute` to a null value.</span></span> <span data-ttu-id="cffbb-119">此示例在 `MyAttribute` 中查找此类实例，并在找不到属性时通知用户。</span><span class="sxs-lookup"><span data-stu-id="cffbb-119">This example checks `MyAttribute` for such an instance and notifies the user if no attribute is found.</span></span> <span data-ttu-id="cffbb-120">如果在类范围中找不到 `DeveloperAttribute`，控制台中显示以下消息。</span><span class="sxs-lookup"><span data-stu-id="cffbb-120">If the `DeveloperAttribute` is not found in the class scope, the following message displays to the console.</span></span>  
  
```console  
The attribute was not found.
```  
  
 <span data-ttu-id="cffbb-121">此示例假定属性定义位于当前的命名空间中。</span><span class="sxs-lookup"><span data-stu-id="cffbb-121">This example assumes that the attribute definition is in the current namespace.</span></span> <span data-ttu-id="cffbb-122">请注意，如果属性定义不在当前的命名空间中，请导入属性定义所在的命名空间。</span><span class="sxs-lookup"><span data-stu-id="cffbb-122">Remember to import the namespace in which the attribute definition resides if it is not in the current namespace.</span></span>  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtosamescope"></a>
## <a name="retrieving-multiple-instances-of-an-attribute-applied-to-the-same-scope"></a><span data-ttu-id="cffbb-123">检索应用于同一范围的多个属性实例</span><span class="sxs-lookup"><span data-stu-id="cffbb-123">Retrieving Multiple Instances of an Attribute Applied to the Same Scope</span></span>  
 <span data-ttu-id="cffbb-124">在上一示例中，要检查的类和要查找的特定属性都传递给 <xref:System.Attribute.GetCustomAttribute%2A>。</span><span class="sxs-lookup"><span data-stu-id="cffbb-124">In the previous example, the class to inspect and the specific attribute to find are passed to <xref:System.Attribute.GetCustomAttribute%2A>.</span></span> <span data-ttu-id="cffbb-125">此代码非常适用于只有一个属性实例在类一级应用的情况。</span><span class="sxs-lookup"><span data-stu-id="cffbb-125">That code works well if only one instance of an attribute is applied on the class level.</span></span> <span data-ttu-id="cffbb-126">不过，如果在相同的类一级应用多个属性实例，GetCustomAttribute 方法不会检索所有信息。</span><span class="sxs-lookup"><span data-stu-id="cffbb-126">However, if multiple instances of an attribute are applied on the same class level, the **GetCustomAttribute** method does not retrieve all the information.</span></span> <span data-ttu-id="cffbb-127">如果同一属性的多个实例应用于相同范围，可以使用 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType> 将所有属性实例添加到数组中。</span><span class="sxs-lookup"><span data-stu-id="cffbb-127">In cases where multiple instances of the same attribute are applied to the same scope, you can use <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType> to place all instances of an attribute into an array.</span></span> <span data-ttu-id="cffbb-128">例如，如果在相同的类一级应用两个 `DeveloperAttribute` 实例，可以将 `GetAttribute` 方法修改为显示在这两个属性中找到的信息。</span><span class="sxs-lookup"><span data-stu-id="cffbb-128">For example, if two instances of `DeveloperAttribute` are applied on the class level of the same class, the `GetAttribute` method can be modified to display the information found in both attributes.</span></span> <span data-ttu-id="cffbb-129">请注意，若要在同一级别应用多个属性，必须在 <xref:System.AttributeUsageAttribute> 中定义属性，并将 AllowMultiple 属性设为 true。</span><span class="sxs-lookup"><span data-stu-id="cffbb-129">Remember, to apply multiple attributes on the same level, the attribute must be defined with the **AllowMultiple** property set to **true** in the <xref:System.AttributeUsageAttribute>.</span></span>  
  
 <span data-ttu-id="cffbb-130">下面的代码示例展示了如何使用 GetCustomAttributes 方法来创建数组，以引用任何给定类中的所有 `DeveloperAttribute` 实例。</span><span class="sxs-lookup"><span data-stu-id="cffbb-130">The following code example shows how to use the **GetCustomAttributes** method to create an array that references all instances of `DeveloperAttribute` in any given class.</span></span> <span data-ttu-id="cffbb-131">然后，所有属性的值都显示在控制台中。</span><span class="sxs-lookup"><span data-stu-id="cffbb-131">The values of all attributes are then displayed to the console.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#19)]
 [!code-csharp[Conceptual.Attributes.Usage#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#19)]
 [!code-vb[Conceptual.Attributes.Usage#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#19)]  
  
 <span data-ttu-id="cffbb-132">如果找不到任何属性，此代码会向用户发出警报。</span><span class="sxs-lookup"><span data-stu-id="cffbb-132">If no attributes are found, this code alerts the user.</span></span> <span data-ttu-id="cffbb-133">如果找到，就会显示两个 `DeveloperAttribute` 实例中包含的信息。</span><span class="sxs-lookup"><span data-stu-id="cffbb-133">Otherwise, the information contained in both instances of `DeveloperAttribute` is displayed.</span></span>  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes"></a>
## <a name="retrieving-multiple-instances-of-an-attribute-applied-to-different-scopes"></a><span data-ttu-id="cffbb-134">检索应用于不同范围的多个属性实例</span><span class="sxs-lookup"><span data-stu-id="cffbb-134">Retrieving Multiple Instances of an Attribute Applied to Different Scopes</span></span>  
 <span data-ttu-id="cffbb-135"><xref:System.Attribute.GetCustomAttributes%2A> 和 <xref:System.Attribute.GetCustomAttribute%2A> 方法不会搜索整个类，也不会返回相应类中的所有属性实例。</span><span class="sxs-lookup"><span data-stu-id="cffbb-135">The <xref:System.Attribute.GetCustomAttributes%2A> and <xref:System.Attribute.GetCustomAttribute%2A> methods do not search an entire class and return all instances of an attribute in that class.</span></span> <span data-ttu-id="cffbb-136">而是一次只搜索一个指定方法或成员。</span><span class="sxs-lookup"><span data-stu-id="cffbb-136">Rather, they search only one specified method or member at a time.</span></span> <span data-ttu-id="cffbb-137">如果类中的相同属性应用于每个成员，且要检索应用于这些成员的所有属性的值，必须将各个方法或成员单独提供给 GetCustomAttributes 和 GetCustomAttribute。</span><span class="sxs-lookup"><span data-stu-id="cffbb-137">If you have a class with the same attribute applied to every member and you want to retrieve the values in all the attributes applied to those members, you must supply every method or member individually to **GetCustomAttributes** and **GetCustomAttribute** .</span></span>  
  
 <span data-ttu-id="cffbb-138">下面的代码示例将类用作参数，并在类一级以及相应类的所有方法一级搜索 `DeveloperAttribute`（如前面所定义）。</span><span class="sxs-lookup"><span data-stu-id="cffbb-138">The following code example takes a class as a parameter and searches for the `DeveloperAttribute` (defined previously) on the class level and on every individual method of that class.</span></span>  
  
 [!code-cpp[Conceptual.Attributes.Usage#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#20)]
 [!code-csharp[Conceptual.Attributes.Usage#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#20)]
 [!code-vb[Conceptual.Attributes.Usage#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#20)]  
  
 <span data-ttu-id="cffbb-139">如果在方法或类一级找不到 `DeveloperAttribute` 实例，`GetAttribute` 方法会通知用户找不到属性，并显示不包含属性的方法名称或类名称。</span><span class="sxs-lookup"><span data-stu-id="cffbb-139">If no instances of the `DeveloperAttribute` are found on the method level or class level, the `GetAttribute` method notifies the user that no attributes were found and displays the name of the method or class that does not contain the attribute.</span></span> <span data-ttu-id="cffbb-140">如果找到属性，控制台中会显示 `Name`、`Level` 和 `Reviewed` 字段。</span><span class="sxs-lookup"><span data-stu-id="cffbb-140">If an attribute is found, the `Name`, `Level`, and `Reviewed` fields are displayed to the console.</span></span>  
  
 <span data-ttu-id="cffbb-141">可以使用 <xref:System.Type> 类的成员，在传递的类中获取各个方法和成员。</span><span class="sxs-lookup"><span data-stu-id="cffbb-141">You can use the members of the <xref:System.Type> class to get the individual methods and members in the passed class.</span></span> <span data-ttu-id="cffbb-142">此示例先查询 Type 对象，以获取类一级的属性信息。</span><span class="sxs-lookup"><span data-stu-id="cffbb-142">This example first queries the **Type** object to get attribute information for the class level.</span></span> <span data-ttu-id="cffbb-143">接下来，它使用 <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> 将所有方法实例都放入 <xref:System.Reflection.MemberInfo?displayProperty=nameWithType> 对象数组，以检索方法一级的属性信息。</span><span class="sxs-lookup"><span data-stu-id="cffbb-143">Next, it uses <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> to place instances of all methods into an array of <xref:System.Reflection.MemberInfo?displayProperty=nameWithType> objects to retrieve attribute information for the method level.</span></span> <span data-ttu-id="cffbb-144">还可以使用 <xref:System.Type.GetProperties%2A?displayProperty=nameWithType> 方法检查属性一级的属性，或使用 <xref:System.Type.GetConstructors%2A?displayProperty=nameWithType>方法检查构造函数一级的属性。</span><span class="sxs-lookup"><span data-stu-id="cffbb-144">You can also use the <xref:System.Type.GetProperties%2A?displayProperty=nameWithType> method to check for attributes on the property level or <xref:System.Type.GetConstructors%2A?displayProperty=nameWithType> to check for attributes on the constructor level.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cffbb-145">请参阅</span><span class="sxs-lookup"><span data-stu-id="cffbb-145">See also</span></span>

- <xref:System.Type?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=nameWithType>
- <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=nameWithType>
- [<span data-ttu-id="cffbb-146">特性</span><span class="sxs-lookup"><span data-stu-id="cffbb-146">Attributes</span></span>](index.md)
