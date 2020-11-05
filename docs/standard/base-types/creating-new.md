---
title: 新建 .NET 中的字符串
description: 了解如何在 .NET 中使用赋值、类构造函数或 System.String 方法创建字符串，这些方法结合了多个字符串、字符串数组或对象。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CopyTo method
- Join method
- Format method
- Concat method
- strings [.NET], creating
- Insert method
ms.assetid: 06fdf123-2fac-4459-8904-eb48ab908a30
ms.openlocfilehash: 7dedaf61f56f19343299c841bb4cee70fb9c767a
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889434"
---
# <a name="creating-new-strings-in-net"></a><span data-ttu-id="762ea-103">新建 .NET 中的字符串</span><span class="sxs-lookup"><span data-stu-id="762ea-103">Creating New Strings in .NET</span></span>

<span data-ttu-id="762ea-104">.NET 允许通过简单赋值创建字符串，并且还重载一个类构造函数，以支持使用一些不同参数来创建字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-104">.NET allows strings to be created using simple assignment, and also overloads a class constructor to support string creation using a number of different parameters.</span></span> <span data-ttu-id="762ea-105">.NET 还在 <xref:System.String?displayProperty=nameWithType> 类中提供了多个方法，可通过合并多个字符串、字符串数组或对象来新建字符串对象。</span><span class="sxs-lookup"><span data-stu-id="762ea-105">.NET also provides several methods in the <xref:System.String?displayProperty=nameWithType> class that create new string objects by combining several strings, arrays of strings, or objects.</span></span>  
  
## <a name="creating-strings-using-assignment"></a><span data-ttu-id="762ea-106">通过赋值创建字符串</span><span class="sxs-lookup"><span data-stu-id="762ea-106">Creating Strings Using Assignment</span></span>  
 <span data-ttu-id="762ea-107">新建 <xref:System.String> 对象的最简单方法是，将字符串文本分配给 <xref:System.String> 对象。</span><span class="sxs-lookup"><span data-stu-id="762ea-107">The easiest way to create a new <xref:System.String> object is simply to assign a string literal to a <xref:System.String> object.</span></span>  
  
## <a name="creating-strings-using-a-class-constructor"></a><span data-ttu-id="762ea-108">使用类构造函数创建字符串</span><span class="sxs-lookup"><span data-stu-id="762ea-108">Creating Strings Using a Class Constructor</span></span>  
 <span data-ttu-id="762ea-109">可以重载 <xref:System.String> 类构造函数，通过字符数组创建字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-109">You can use overloads of the <xref:System.String> class constructor to create strings from character arrays.</span></span> <span data-ttu-id="762ea-110">还可以通过将特定字符重复指定次数来创建新字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-110">You can also create a new string by duplicating a particular character a specified number of times.</span></span>  
  
## <a name="methods-that-return-strings"></a><span data-ttu-id="762ea-111">返回字符串的方法</span><span class="sxs-lookup"><span data-stu-id="762ea-111">Methods that Return Strings</span></span>  
 <span data-ttu-id="762ea-112">下表列出了返回新字符串对象的几个有用方法。</span><span class="sxs-lookup"><span data-stu-id="762ea-112">The following table lists several useful methods that return new string objects.</span></span>  
  
|<span data-ttu-id="762ea-113">方法名称</span><span class="sxs-lookup"><span data-stu-id="762ea-113">Method name</span></span>|<span data-ttu-id="762ea-114">使用</span><span class="sxs-lookup"><span data-stu-id="762ea-114">Use</span></span>|  
|-----------------|---------|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|<span data-ttu-id="762ea-115">从一组输入对象生成格式化的字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-115">Builds a formatted string from a set of input objects.</span></span>|  
|<xref:System.String.Concat%2A?displayProperty=nameWithType>|<span data-ttu-id="762ea-116">从两个或更多个字符串生成字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-116">Builds strings from two or more strings.</span></span>|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|<span data-ttu-id="762ea-117">通过合并字符串数组生成新字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-117">Builds a new string by combining an array of strings.</span></span>|  
|<xref:System.String.Insert%2A?displayProperty=nameWithType>|<span data-ttu-id="762ea-118">通过将一个字符串插入现有字符串的指定索引处生成新字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-118">Builds a new string by inserting a string into the specified index of an existing string.</span></span>|  
|<xref:System.String.CopyTo%2A?displayProperty=nameWithType>|<span data-ttu-id="762ea-119">将一个字符串中的指定字符复制到一个字符数组中的指定位置。</span><span class="sxs-lookup"><span data-stu-id="762ea-119">Copies specified characters in a string into a specified position in an array of characters.</span></span>|  
  
### <a name="format"></a><span data-ttu-id="762ea-120">格式</span><span class="sxs-lookup"><span data-stu-id="762ea-120">Format</span></span>  
 <span data-ttu-id="762ea-121">可以使用 String.Format 方法，创建格式化字符串，并连接表示多个对象的字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-121">You can use the **String.Format** method to create formatted strings and concatenate strings representing multiple objects.</span></span> <span data-ttu-id="762ea-122">此方法自动将传递给它的任何对象转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-122">This method automatically converts any passed object into a string.</span></span> <span data-ttu-id="762ea-123">例如，如果应用必须向用户显示 Int32 值和 DateTime 值，可以使用 Format 方法，轻松构造表示这些值的字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-123">For example, if your application must display an **Int32** value and a **DateTime** value to the user, you can easily construct a string to represent these values using the **Format** method.</span></span> <span data-ttu-id="762ea-124">有关此方法使用的格式化约定的信息，请参阅有关[复合格式化](composite-formatting.md)的部分。</span><span class="sxs-lookup"><span data-stu-id="762ea-124">For information about formatting conventions used with this method, see the section on [composite formatting](composite-formatting.md).</span></span>  
  
 <span data-ttu-id="762ea-125">下面的示例使用 Format 方法，创建使用整数变量的字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-125">The following example uses the **Format** method to create a string that uses an integer variable.</span></span>  
  
 [!code-csharp[Strings.Creating#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#1)]
 [!code-vb[Strings.Creating#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#1)]  
  
 <span data-ttu-id="762ea-126">在此示例中，<xref:System.DateTime.Now%2A?displayProperty=nameWithType> 按照与当前线程关联的区域性指定的方式，显示当前日期和时间。</span><span class="sxs-lookup"><span data-stu-id="762ea-126">In this example,<xref:System.DateTime.Now%2A?displayProperty=nameWithType> displays the current date and time in a manner specified by the culture associated with the current thread.</span></span>  
  
### <a name="concat"></a><span data-ttu-id="762ea-127">Concat</span><span class="sxs-lookup"><span data-stu-id="762ea-127">Concat</span></span>  
 <span data-ttu-id="762ea-128">使用 String.Concat 方法，可以通过两个或多个现有对象轻松新建字符串对象。</span><span class="sxs-lookup"><span data-stu-id="762ea-128">The **String.Concat** method can be used to easily create a new string object from two or more existing objects.</span></span> <span data-ttu-id="762ea-129">它提供了一种与语言无关的方法来连接字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-129">It provides a language-independent way to concatenate strings.</span></span> <span data-ttu-id="762ea-130">此方法接受派生自 System.Object 的任何类。</span><span class="sxs-lookup"><span data-stu-id="762ea-130">This method accepts any class that derives from **System.Object**.</span></span> <span data-ttu-id="762ea-131">下面的示例使用两个现有字符串对象和一个分隔符创建一个字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-131">The following example creates a string from two existing string objects and a separating character.</span></span>  
  
 [!code-csharp[Strings.Creating#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#2)]
 [!code-vb[Strings.Creating#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#2)]  
  
### <a name="join"></a><span data-ttu-id="762ea-132">联接</span><span class="sxs-lookup"><span data-stu-id="762ea-132">Join</span></span>  
 <span data-ttu-id="762ea-133">String.Join 方法通过字符串数组和分隔符字符串新建字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-133">The **String.Join** method creates a new string from an array of strings and a separator string.</span></span> <span data-ttu-id="762ea-134">如果想要将多个字符串连接在一起，构成一个可能由逗号分隔的列表，则此方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="762ea-134">This method is useful if you want to concatenate multiple strings together, making a list perhaps separated by a comma.</span></span>  
  
 <span data-ttu-id="762ea-135">下面的示例使用空格来连接字符串数组。</span><span class="sxs-lookup"><span data-stu-id="762ea-135">The following example uses a space to bind a string array.</span></span>  
  
 [!code-csharp[Strings.Creating#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#3)]
 [!code-vb[Strings.Creating#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#3)]  
  
### <a name="insert"></a><span data-ttu-id="762ea-136">Insert</span><span class="sxs-lookup"><span data-stu-id="762ea-136">Insert</span></span>  
 <span data-ttu-id="762ea-137">String.Insert 方法通过将一个字符串插入另一个字符串中的指定位置来新建字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-137">The **String.Insert** method creates a new string by inserting a string into a specified position in another string.</span></span> <span data-ttu-id="762ea-138">此方法使用从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="762ea-138">This method uses a zero-based index.</span></span> <span data-ttu-id="762ea-139">下面的示例将一个字符串插入 `MyString` 的第五个索引位置，并用此值创建新字符串。</span><span class="sxs-lookup"><span data-stu-id="762ea-139">The following example inserts a string into the fifth index position of `MyString` and creates a new string with this value.</span></span>  
  
 [!code-csharp[Strings.Creating#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#4)]
 [!code-vb[Strings.Creating#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#4)]  
  
### <a name="copyto"></a><span data-ttu-id="762ea-140">CopyTo</span><span class="sxs-lookup"><span data-stu-id="762ea-140">CopyTo</span></span>  
 <span data-ttu-id="762ea-141">String.CopyTo 方法将字符串的某些部分复制到字符数组中。</span><span class="sxs-lookup"><span data-stu-id="762ea-141">The **String.CopyTo** method copies portions of a string into an array of characters.</span></span> <span data-ttu-id="762ea-142">可以同时指定字符串的开始索引和要复制的字符数。</span><span class="sxs-lookup"><span data-stu-id="762ea-142">You can specify both the beginning index of the string and the number of characters to be copied.</span></span> <span data-ttu-id="762ea-143">此方法采用源索引、字符数组、目标索引和要复制的字符数。</span><span class="sxs-lookup"><span data-stu-id="762ea-143">This method takes the source index, an array of characters, the destination index, and the number of characters to copy.</span></span> <span data-ttu-id="762ea-144">所有索引都从零开始。</span><span class="sxs-lookup"><span data-stu-id="762ea-144">All indexes are zero-based.</span></span>  
  
 <span data-ttu-id="762ea-145">下面的示例使用 CopyTo 方法，将字符串对象中的“Hello”字词字符复制到字符数组的第一个索引位置。</span><span class="sxs-lookup"><span data-stu-id="762ea-145">The following example uses the **CopyTo** method to copy the characters of the word "Hello" from a string object to the first index position of an array of characters.</span></span>  
  
 [!code-csharp[Strings.Creating#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.Creating/cs/Example.cs#5)]
 [!code-vb[Strings.Creating#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.Creating/vb/Example.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="762ea-146">请参阅</span><span class="sxs-lookup"><span data-stu-id="762ea-146">See also</span></span>

- [<span data-ttu-id="762ea-147">基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="762ea-147">Basic String Operations</span></span>](basic-string-operations.md)
- [<span data-ttu-id="762ea-148">复合格式设置</span><span class="sxs-lookup"><span data-stu-id="762ea-148">Composite Formatting</span></span>](composite-formatting.md)
