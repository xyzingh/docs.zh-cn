---
title: .NET 中的泛型集合
ms.date: 02/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET], collections
- generic collections [.NET]
- generic types [.NET]
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
ms.openlocfilehash: 956db9ace4ae00062accdd6e80c7911aaac7523f
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064244"
---
# <a name="generic-collections-in-net"></a><span data-ttu-id="eb26a-102">.NET 中的泛型集合</span><span class="sxs-lookup"><span data-stu-id="eb26a-102">Generic collections in .NET</span></span>

 <span data-ttu-id="eb26a-103">.NET 类库提供了许多 <xref:System.Collections.Generic> 和 <xref:System.Collections.ObjectModel> 命名空间中的泛型集合类。</span><span class="sxs-lookup"><span data-stu-id="eb26a-103">The .NET class library provides a number of generic collection classes in the <xref:System.Collections.Generic> and <xref:System.Collections.ObjectModel> namespaces.</span></span> <span data-ttu-id="eb26a-104">若要详细了解这些类，请参阅[常用集合类型](../collections/commonly-used-collection-types.md)。</span><span class="sxs-lookup"><span data-stu-id="eb26a-104">For more detailed information about these classes, see [Commonly Used Collection Types](../collections/commonly-used-collection-types.md).</span></span>  
  
## <a name="systemcollectionsgeneric"></a><span data-ttu-id="eb26a-105">System.Collections.Generic</span><span class="sxs-lookup"><span data-stu-id="eb26a-105">System.Collections.Generic</span></span>

 <span data-ttu-id="eb26a-106">许多泛型集合类型均为非泛型类型的直接模拟。</span><span class="sxs-lookup"><span data-stu-id="eb26a-106">Many of the generic collection types are direct analogs of nongeneric types.</span></span> <span data-ttu-id="eb26a-107"><xref:System.Collections.Generic.Dictionary%602> 是 <xref:System.Collections.Hashtable> 的泛型版本；它使用枚举的泛型结构 <xref:System.Collections.Generic.KeyValuePair%602> 而不是 <xref:System.Collections.DictionaryEntry>。</span><span class="sxs-lookup"><span data-stu-id="eb26a-107"><xref:System.Collections.Generic.Dictionary%602> is a generic version of <xref:System.Collections.Hashtable>; it uses the generic structure <xref:System.Collections.Generic.KeyValuePair%602> for enumeration instead of <xref:System.Collections.DictionaryEntry>.</span></span>  
  
 <span data-ttu-id="eb26a-108"><xref:System.Collections.Generic.List%601> 是 <xref:System.Collections.ArrayList> 的泛型版本。</span><span class="sxs-lookup"><span data-stu-id="eb26a-108"><xref:System.Collections.Generic.List%601> is a generic version of <xref:System.Collections.ArrayList>.</span></span> <span data-ttu-id="eb26a-109">存在响应非泛型版本的泛型 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601> 类。</span><span class="sxs-lookup"><span data-stu-id="eb26a-109">There are generic <xref:System.Collections.Generic.Queue%601> and <xref:System.Collections.Generic.Stack%601> classes that correspond to the nongeneric versions.</span></span>  
  
 <span data-ttu-id="eb26a-110">存在 <xref:System.Collections.Generic.SortedList%602> 的泛型和非泛型版本。</span><span class="sxs-lookup"><span data-stu-id="eb26a-110">There are generic and nongeneric versions of <xref:System.Collections.Generic.SortedList%602>.</span></span> <span data-ttu-id="eb26a-111">这两个版本均为字典和列表的混合。</span><span class="sxs-lookup"><span data-stu-id="eb26a-111">Both versions are hybrids of a dictionary and a list.</span></span> <span data-ttu-id="eb26a-112"><xref:System.Collections.Generic.SortedDictionary%602> 泛型类是一个纯字典，并且没有任何非泛型对应项。</span><span class="sxs-lookup"><span data-stu-id="eb26a-112">The <xref:System.Collections.Generic.SortedDictionary%602> generic class is a pure dictionary and has no nongeneric counterpart.</span></span>  
  
 <span data-ttu-id="eb26a-113"><xref:System.Collections.Generic.LinkedList%601> 泛型类是真正的链接列表。</span><span class="sxs-lookup"><span data-stu-id="eb26a-113">The <xref:System.Collections.Generic.LinkedList%601> generic class is a true linked list.</span></span> <span data-ttu-id="eb26a-114">它没有任何非泛型对应项。</span><span class="sxs-lookup"><span data-stu-id="eb26a-114">It has no nongeneric counterpart.</span></span>  
  
## <a name="systemcollectionsobjectmodel"></a><span data-ttu-id="eb26a-115">System.Collections.ObjectModel</span><span class="sxs-lookup"><span data-stu-id="eb26a-115">System.Collections.ObjectModel</span></span>

 <span data-ttu-id="eb26a-116"><xref:System.Collections.ObjectModel.Collection%601> 泛型类提供用于派生自己的泛型集合类型的基类。</span><span class="sxs-lookup"><span data-stu-id="eb26a-116">The <xref:System.Collections.ObjectModel.Collection%601> generic class provides a base class for deriving your own generic collection types.</span></span> <span data-ttu-id="eb26a-117"><xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 类提供了任何从实现 <xref:System.Collections.Generic.IList%601> 泛型接口的类型生成只读集合的简便方法。</span><span class="sxs-lookup"><span data-stu-id="eb26a-117">The <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> class provides an easy way to produce a read-only collection from any type that implements the <xref:System.Collections.Generic.IList%601> generic interface.</span></span> <span data-ttu-id="eb26a-118"><xref:System.Collections.ObjectModel.KeyedCollection%602> 泛型类提供了存储包含其自己的键的对象的方法。</span><span class="sxs-lookup"><span data-stu-id="eb26a-118">The <xref:System.Collections.ObjectModel.KeyedCollection%602> generic class provides a way to store objects that contain their own keys.</span></span>  
  
## <a name="other-generic-types"></a><span data-ttu-id="eb26a-119">其他泛型类型</span><span class="sxs-lookup"><span data-stu-id="eb26a-119">Other generic types</span></span>

 <span data-ttu-id="eb26a-120"><xref:System.Nullable%601> 泛型结构允许使用值类型，如同它们可分配 `null`。</span><span class="sxs-lookup"><span data-stu-id="eb26a-120">The <xref:System.Nullable%601> generic structure allows you to use value types as if they could be assigned `null`.</span></span> <span data-ttu-id="eb26a-121">这在处理数据库查询时很有用，其中字段包含可能丢失的值类型。</span><span class="sxs-lookup"><span data-stu-id="eb26a-121">This can be useful when working with database queries, where fields that contain value types can be missing.</span></span> <span data-ttu-id="eb26a-122">泛型类型参数可为任意值类型。</span><span class="sxs-lookup"><span data-stu-id="eb26a-122">The generic type parameter can be any value type.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="eb26a-123">在 C# 和 Visual Basic 中，无需显式使用 <xref:System.Nullable%601>，因为语言具有可以为 null 类型的语法。</span><span class="sxs-lookup"><span data-stu-id="eb26a-123">In C# and Visual Basic, it is not necessary to use <xref:System.Nullable%601> explicitly because the language has syntax for nullable types.</span></span> <span data-ttu-id="eb26a-124">请参阅[可为 null 的值类型（C# 引用）](../../csharp/language-reference/builtin-types/nullable-value-types.md)和[可为 null 的值类型 (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="eb26a-124">See [Nullable value types (C# reference)](../../csharp/language-reference/builtin-types/nullable-value-types.md) and [Nullable value types (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md).</span></span>
  
 <span data-ttu-id="eb26a-125"><xref:System.ArraySegment%601> 泛型结构提供了分隔任何类型的从零开始的一维数组内的一系列元素的方法。</span><span class="sxs-lookup"><span data-stu-id="eb26a-125">The <xref:System.ArraySegment%601> generic structure provides a way to delimit a range of elements within a one-dimensional, zero-based array of any type.</span></span> <span data-ttu-id="eb26a-126">泛型类型参数是数组中元素的类型。</span><span class="sxs-lookup"><span data-stu-id="eb26a-126">The generic type parameter is the type of the array's elements.</span></span>  
  
 <span data-ttu-id="eb26a-127">如果你的事件采用 .NET 所使用的事件处理模式，则 <xref:System.EventHandler%601> 泛型委托不需要声明委托类型来处理事件。</span><span class="sxs-lookup"><span data-stu-id="eb26a-127">The <xref:System.EventHandler%601> generic delegate eliminates the need to declare a delegate type to handle events, if your event follows the event-handling pattern used by .NET.</span></span> <span data-ttu-id="eb26a-128">例如，假设已创建从 <xref:System.EventArgs> 派生的 `MyEventArgs` 类，以包含事件的数据。</span><span class="sxs-lookup"><span data-stu-id="eb26a-128">For example, suppose you have created a `MyEventArgs` class, derived from <xref:System.EventArgs>, to hold the data for your event.</span></span> <span data-ttu-id="eb26a-129">则可以声明此事件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eb26a-129">You can then declare the event as follows:</span></span>  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## <a name="see-also"></a><span data-ttu-id="eb26a-130">请参阅</span><span class="sxs-lookup"><span data-stu-id="eb26a-130">See also</span></span>

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [<span data-ttu-id="eb26a-131">泛型</span><span class="sxs-lookup"><span data-stu-id="eb26a-131">Generics</span></span>](index.md)
- [<span data-ttu-id="eb26a-132">用于控制数组和列表的泛型委托</span><span class="sxs-lookup"><span data-stu-id="eb26a-132">Generic Delegates for Manipulating Arrays and Lists</span></span>](delegates-for-manipulating-arrays-and-lists.md)
- [<span data-ttu-id="eb26a-133">泛型接口</span><span class="sxs-lookup"><span data-stu-id="eb26a-133">Generic Interfaces</span></span>](interfaces.md)
