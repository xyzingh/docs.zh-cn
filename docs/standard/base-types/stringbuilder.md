---
title: 使用 .NET 中的 StringBuilder 类
description: 了解如何使用 .NET 中的 StringBuilder 类。 无需创建新对象即可使用此类来修改字符串。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Remove method
- strings [.NET], capacities
- StringBuilder object
- Replace method
- AppendFormat method
- Append method
- Insert method
- strings [.NET], StringBuilder object
ms.assetid: 5c14867c-9a99-45bc-ae7f-2686700d377a
ms.openlocfilehash: 1005da650c624b2b8f6616c163082ff95d7dc007
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888953"
---
# <a name="using-the-stringbuilder-class-in-net"></a><span data-ttu-id="53309-104">使用 .NET 中的 StringBuilder 类</span><span class="sxs-lookup"><span data-stu-id="53309-104">Using the StringBuilder Class in .NET</span></span>
<span data-ttu-id="53309-105"><xref:System.String> 对象不可变。</span><span class="sxs-lookup"><span data-stu-id="53309-105">The <xref:System.String> object is immutable.</span></span> <span data-ttu-id="53309-106">每次使用 <xref:System.String?displayProperty=nameWithType> 类中的方法之一，都要在内存中新建字符串对象，这就需要为新对象分配新空间。</span><span class="sxs-lookup"><span data-stu-id="53309-106">Every time you use one of the methods in the <xref:System.String?displayProperty=nameWithType> class, you create a new string object in memory, which requires a new allocation of space for that new object.</span></span> <span data-ttu-id="53309-107">在需要重复修改字符串的情况下，与新建 <xref:System.String> 对象关联的开销可能会非常大。</span><span class="sxs-lookup"><span data-stu-id="53309-107">In situations where you need to perform repeated modifications to a string, the overhead associated with creating a new <xref:System.String> object can be costly.</span></span> <span data-ttu-id="53309-108">若要修改字符串（而不新建对象），可以使用 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 类。</span><span class="sxs-lookup"><span data-stu-id="53309-108">The <xref:System.Text.StringBuilder?displayProperty=nameWithType> class can be used when you want to modify a string without creating a new object.</span></span> <span data-ttu-id="53309-109">例如，如果在循环中将许多字符串连接在一起，使用 <xref:System.Text.StringBuilder> 类可以提升性能。</span><span class="sxs-lookup"><span data-stu-id="53309-109">For example, using the <xref:System.Text.StringBuilder> class can boost performance when concatenating many strings together in a loop.</span></span>  
  
## <a name="importing-the-systemtext-namespace"></a><span data-ttu-id="53309-110">导入 System.Text 命名空间</span><span class="sxs-lookup"><span data-stu-id="53309-110">Importing the System.Text Namespace</span></span>  
 <span data-ttu-id="53309-111"><xref:System.Text.StringBuilder> 类位于 <xref:System.Text> 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="53309-111">The <xref:System.Text.StringBuilder> class is found in the <xref:System.Text> namespace.</span></span>  <span data-ttu-id="53309-112">为了避免必须在代码中提供完全限定的类型名称，可以导入 <xref:System.Text> 命名空间：</span><span class="sxs-lookup"><span data-stu-id="53309-112">To avoid having to provide a fully qualified type name in your code,  you can import the <xref:System.Text> namespace:</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#11)]
 [!code-csharp[Conceptual.StringBuilder#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#11)]
 [!code-vb[Conceptual.StringBuilder#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#11)]  
  
## <a name="instantiating-a-stringbuilder-object"></a><span data-ttu-id="53309-113">实例化 StringBuilder 对象</span><span class="sxs-lookup"><span data-stu-id="53309-113">Instantiating a StringBuilder Object</span></span>  
 <span data-ttu-id="53309-114">通过使用重载的构造函数方法之一初始化变量，可以新建 <xref:System.Text.StringBuilder> 类的实例，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="53309-114">You can create a new instance of the <xref:System.Text.StringBuilder> class by initializing your variable with one of the overloaded constructor methods, as illustrated in the following example.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#1)]
 [!code-csharp[Conceptual.StringBuilder#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#1)]
 [!code-vb[Conceptual.StringBuilder#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#1)]  
  
## <a name="setting-the-capacity-and-length"></a><span data-ttu-id="53309-115">设置容量和长度</span><span class="sxs-lookup"><span data-stu-id="53309-115">Setting the Capacity and Length</span></span>  
 <span data-ttu-id="53309-116">虽然 <xref:System.Text.StringBuilder> 是动态对象，支持扩展它封装的字符串中的字符数，但可以指定值，作为对象可保留的字符数上限。</span><span class="sxs-lookup"><span data-stu-id="53309-116">Although the <xref:System.Text.StringBuilder> is a dynamic object that allows you to expand the number of characters in the string that it encapsulates, you can specify a value for the maximum number of characters that it can hold.</span></span> <span data-ttu-id="53309-117">此值称为“对象容量”，不得将它与当前 <xref:System.Text.StringBuilder> 保留的字符串长度相混淆。</span><span class="sxs-lookup"><span data-stu-id="53309-117">This value is called the capacity of the object and should not be confused with the length of the string that the current <xref:System.Text.StringBuilder> holds.</span></span> <span data-ttu-id="53309-118">例如，可以使用长度为 5 的字符串“Hello”新建 <xref:System.Text.StringBuilder> 类的实例，同时可以指定此对象的最大容量为 25。</span><span class="sxs-lookup"><span data-stu-id="53309-118">For example, you might create a new instance of the <xref:System.Text.StringBuilder> class with the string "Hello", which has a length of 5, and you might specify that the object has a maximum capacity of 25.</span></span> <span data-ttu-id="53309-119">修改 <xref:System.Text.StringBuilder> 时，除非达到容量，否则对象不会为自己重新分配空间。</span><span class="sxs-lookup"><span data-stu-id="53309-119">When you modify the <xref:System.Text.StringBuilder>, it does not reallocate size for itself until the capacity is reached.</span></span> <span data-ttu-id="53309-120">当达到容量时，将自动分配新的空间且容量翻倍。</span><span class="sxs-lookup"><span data-stu-id="53309-120">When this occurs, the new space is allocated automatically and the capacity is doubled.</span></span> <span data-ttu-id="53309-121">可以使用重载的构造函数之一，指定 <xref:System.Text.StringBuilder> 类的容量。</span><span class="sxs-lookup"><span data-stu-id="53309-121">You can specify the capacity of the <xref:System.Text.StringBuilder> class using one of the overloaded constructors.</span></span> <span data-ttu-id="53309-122">下面的示例指定可以将 `myStringBuilder` 对象增加到最多 25 个空间。</span><span class="sxs-lookup"><span data-stu-id="53309-122">The following example specifies that the `myStringBuilder` object can be expanded to a maximum of 25 spaces.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#2)]
 [!code-csharp[Conceptual.StringBuilder#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#2)]
 [!code-vb[Conceptual.StringBuilder#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#2)]  
  
 <span data-ttu-id="53309-123">另外，还可以使用读/写 <xref:System.Text.StringBuilder.Capacity%2A> 属性，设置对象的长度上限。</span><span class="sxs-lookup"><span data-stu-id="53309-123">Additionally, you can use the read/write <xref:System.Text.StringBuilder.Capacity%2A> property to set the maximum length of your object.</span></span> <span data-ttu-id="53309-124">下面的示例使用 **Capacity** 属性来定义对象的最大长度。</span><span class="sxs-lookup"><span data-stu-id="53309-124">The following example uses the **Capacity** property to define the maximum object length.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#3)]
 [!code-csharp[Conceptual.StringBuilder#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#3)]
 [!code-vb[Conceptual.StringBuilder#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#3)]  
  
 <span data-ttu-id="53309-125"><xref:System.Text.StringBuilder.EnsureCapacity%2A> 方法可用于检查当前 StringBuilder 的容量。</span><span class="sxs-lookup"><span data-stu-id="53309-125">The <xref:System.Text.StringBuilder.EnsureCapacity%2A> method can be used to check the capacity of the current **StringBuilder** .</span></span> <span data-ttu-id="53309-126">如果容量大于传递的值，则不进行任何更改；但是，如果容量小于传递的值，则会更改当前的容量以使其与传递的值匹配。</span><span class="sxs-lookup"><span data-stu-id="53309-126">If the capacity is greater than the passed value, no change is made; however, if the capacity is smaller than the passed value, the current capacity is changed to match the passed value.</span></span>  
  
 <span data-ttu-id="53309-127">也可以查看或设置 <xref:System.Text.StringBuilder.Length%2A> 属性。</span><span class="sxs-lookup"><span data-stu-id="53309-127">The <xref:System.Text.StringBuilder.Length%2A> property can also be viewed or set.</span></span> <span data-ttu-id="53309-128">如果将 **Length** 属性设置为大于 **Capacity** 属性的值，则自动将 **Capacity** 属性更改为与 **Length** 属性相同的值。</span><span class="sxs-lookup"><span data-stu-id="53309-128">If you set the **Length** property to a value that is greater than the **Capacity** property, the **Capacity** property is automatically changed to the same value as the **Length** property.</span></span> <span data-ttu-id="53309-129">如果将 **Length** 属性设置为小于当前 **StringBuilder** 对象内的字符串长度的值，则会缩短该字符串。</span><span class="sxs-lookup"><span data-stu-id="53309-129">Setting the **Length** property to a value that is less than the length of the string within the current **StringBuilder** shortens the string.</span></span>  
  
## <a name="modifying-the-stringbuilder-string"></a><span data-ttu-id="53309-130">修改 StringBuilder 字符串</span><span class="sxs-lookup"><span data-stu-id="53309-130">Modifying the StringBuilder String</span></span>  
 <span data-ttu-id="53309-131">下表列出了可用于修改 **StringBuilder** 内容的方法。</span><span class="sxs-lookup"><span data-stu-id="53309-131">The following table lists the methods you can use to modify the contents of a **StringBuilder** .</span></span>  
  
|<span data-ttu-id="53309-132">方法名称</span><span class="sxs-lookup"><span data-stu-id="53309-132">Method name</span></span>|<span data-ttu-id="53309-133">使用</span><span class="sxs-lookup"><span data-stu-id="53309-133">Use</span></span>|  
|-----------------|---------|  
|<xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType>|<span data-ttu-id="53309-134">将信息追加到当前 **StringBuilder** 的末尾。</span><span class="sxs-lookup"><span data-stu-id="53309-134">Appends information to the end of the current **StringBuilder** .</span></span>|  
|<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType>|<span data-ttu-id="53309-135">用带格式文本替换字符串中传递的格式说明符。</span><span class="sxs-lookup"><span data-stu-id="53309-135">Replaces a format specifier passed in a string with formatted text.</span></span>|  
|<xref:System.Text.StringBuilder.Insert%2A?displayProperty=nameWithType>|<span data-ttu-id="53309-136">将字符串或对象插入到当前 **StringBuilder** 的指定索引中。</span><span class="sxs-lookup"><span data-stu-id="53309-136">Inserts a string or object into the specified index of the current **StringBuilder** .</span></span>|  
|<xref:System.Text.StringBuilder.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="53309-137">从当前 **StringBuilder** 中删除指定数量的字符。</span><span class="sxs-lookup"><span data-stu-id="53309-137">Removes a specified number of characters from the current **StringBuilder** .</span></span>|  
|<xref:System.Text.StringBuilder.Replace%2A?displayProperty=nameWithType>|<span data-ttu-id="53309-138">将当前 StringBuilder 中出现的所有指定字符或字符串替换为其他的指定字符或字符串。</span><span class="sxs-lookup"><span data-stu-id="53309-138">Replaces all occurrences of a specified character or string in the current **StringBuilder** with another specified character or string.</span></span>|  
  
### <a name="append"></a><span data-ttu-id="53309-139">追加</span><span class="sxs-lookup"><span data-stu-id="53309-139">Append</span></span>  
 <span data-ttu-id="53309-140">Append 方法可用于将对象的文本或字符串表示形式添加到当前 StringBuilder 表示的字符串末尾。</span><span class="sxs-lookup"><span data-stu-id="53309-140">The **Append** method can be used to add text or a string representation of an object to the end of a string represented by the current **StringBuilder** .</span></span> <span data-ttu-id="53309-141">下面的示例将 **StringBuilder** 对象初始化为“Hello World”，然后将一些文本追加到该对象的末尾。</span><span class="sxs-lookup"><span data-stu-id="53309-141">The following example initializes a **StringBuilder** to "Hello World" and then appends some text to the end of the object.</span></span> <span data-ttu-id="53309-142">将根据需要自动分配空间。</span><span class="sxs-lookup"><span data-stu-id="53309-142">Space is allocated automatically as needed.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#4)]
 [!code-csharp[Conceptual.StringBuilder#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#4)]
 [!code-vb[Conceptual.StringBuilder#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#4)]  
  
### <a name="appendformat"></a><span data-ttu-id="53309-143">AppendFormat</span><span class="sxs-lookup"><span data-stu-id="53309-143">AppendFormat</span></span>  
 <span data-ttu-id="53309-144"><xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> 方法将文本添加到 <xref:System.Text.StringBuilder> 对象末尾。</span><span class="sxs-lookup"><span data-stu-id="53309-144">The <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> method adds text to the end of the <xref:System.Text.StringBuilder> object.</span></span> <span data-ttu-id="53309-145">它调用要设置格式的一个或多个对象的 <xref:System.IFormattable> 实现，支持复合格式功能（有关详细信息，请参阅[复合格式](composite-formatting.md)）。</span><span class="sxs-lookup"><span data-stu-id="53309-145">It supports the composite formatting feature (for more information, see [Composite Formatting](composite-formatting.md)) by calling the <xref:System.IFormattable> implementation of the object or objects to be formatted.</span></span> <span data-ttu-id="53309-146">因此，它接受数字、日期和时间以及枚举值的标准格式字符串、数字以及日期和时间值的自定义格式字符串，以及为自定义类型定义的格式字符串。</span><span class="sxs-lookup"><span data-stu-id="53309-146">Therefore, it accepts the standard format strings for numeric, date and time, and enumeration values, the custom format strings for numeric and date and time values, and the format strings defined for custom types.</span></span> <span data-ttu-id="53309-147">（有关格式化的信息，请参阅[格式设置类型](formatting-types.md)。）此方法可用于自定义变量格式，并将这些值追加到 <xref:System.Text.StringBuilder>。</span><span class="sxs-lookup"><span data-stu-id="53309-147">(For information about formatting, see [Formatting Types](formatting-types.md).) You can use this method to customize the format of variables and append those values to a <xref:System.Text.StringBuilder>.</span></span> <span data-ttu-id="53309-148">下面的示例使用 <xref:System.Text.StringBuilder.AppendFormat%2A> 方法，将格式为货币值的整数值添加到 <xref:System.Text.StringBuilder> 对象末尾。</span><span class="sxs-lookup"><span data-stu-id="53309-148">The following example uses the <xref:System.Text.StringBuilder.AppendFormat%2A> method to place an integer value formatted as a currency value at the end of a <xref:System.Text.StringBuilder> object.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#5)]
 [!code-csharp[Conceptual.StringBuilder#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#5)]
 [!code-vb[Conceptual.StringBuilder#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#5)]  
  
### <a name="insert"></a><span data-ttu-id="53309-149">Insert</span><span class="sxs-lookup"><span data-stu-id="53309-149">Insert</span></span>  
 <span data-ttu-id="53309-150"><xref:System.Text.StringBuilder.Insert%2A> 方法将字符串或对象添加到当前 <xref:System.Text.StringBuilder> 对象中的指定位置。</span><span class="sxs-lookup"><span data-stu-id="53309-150">The <xref:System.Text.StringBuilder.Insert%2A> method adds a string or object to a specified position in the current <xref:System.Text.StringBuilder> object.</span></span> <span data-ttu-id="53309-151">下面的示例使用此方法，将字词插入 <xref:System.Text.StringBuilder> 对象的第六个位置。</span><span class="sxs-lookup"><span data-stu-id="53309-151">The following example uses this method to insert a word into the sixth position of a <xref:System.Text.StringBuilder> object.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#6)]
 [!code-csharp[Conceptual.StringBuilder#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#6)]
 [!code-vb[Conceptual.StringBuilder#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#6)]  
  
### <a name="remove"></a><span data-ttu-id="53309-152">删除</span><span class="sxs-lookup"><span data-stu-id="53309-152">Remove</span></span>  
 <span data-ttu-id="53309-153">可以使用 Remove方法，从当前 <xref:System.Text.StringBuilder> 对象中指定索引（从零开始编制）处开始删除指定数量的字符。</span><span class="sxs-lookup"><span data-stu-id="53309-153">You can use the **Remove** method to remove a specified number of characters from the current <xref:System.Text.StringBuilder> object, beginning at a specified zero-based index.</span></span> <span data-ttu-id="53309-154">下面的示例使用 Remove 方法缩短 <xref:System.Text.StringBuilder> 对象。</span><span class="sxs-lookup"><span data-stu-id="53309-154">The following example uses the **Remove** method to shorten a <xref:System.Text.StringBuilder> object.</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#7)]
 [!code-csharp[Conceptual.StringBuilder#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#7)]
 [!code-vb[Conceptual.StringBuilder#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#7)]  
  
### <a name="replace"></a><span data-ttu-id="53309-155">替换</span><span class="sxs-lookup"><span data-stu-id="53309-155">Replace</span></span>  
 <span data-ttu-id="53309-156">Replace 方法可用于将 <xref:System.Text.StringBuilder> 对象内的字符替换为另一个指定的字符。</span><span class="sxs-lookup"><span data-stu-id="53309-156">The **Replace** method can be used to replace characters within the <xref:System.Text.StringBuilder> object with another specified character.</span></span> <span data-ttu-id="53309-157">下面的示例使用 Replace 方法，在 <xref:System.Text.StringBuilder> 对象中搜索感叹号字符 (!) 的所有实例，并将它们替换为问号字符 (?)。</span><span class="sxs-lookup"><span data-stu-id="53309-157">The following example uses the **Replace** method to search a <xref:System.Text.StringBuilder> object for all instances of the exclamation point character (!) and replace them with the question mark character (?).</span></span>  
  
 [!code-cpp[Conceptual.StringBuilder#8](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.StringBuilder/cpp/example.cpp#8)]
 [!code-csharp[Conceptual.StringBuilder#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/Example.cs#8)]
 [!code-vb[Conceptual.StringBuilder#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/Example.vb#8)]  
  
## <a name="converting-a-stringbuilder-object-to-a-string"></a><span data-ttu-id="53309-158">将 StringBuilder 对象转换为字符串</span><span class="sxs-lookup"><span data-stu-id="53309-158">Converting a StringBuilder Object to a String</span></span>  
 <span data-ttu-id="53309-159">必须先将 <xref:System.Text.StringBuilder> 对象转换为 <xref:System.String> 对象，然后才能将 <xref:System.Text.StringBuilder> 对象表示的字符串传递给包含 <xref:System.String> 参数的方法，或在用户界面中显示它。</span><span class="sxs-lookup"><span data-stu-id="53309-159">You must convert the <xref:System.Text.StringBuilder> object to a <xref:System.String> object before you can pass the string represented by the <xref:System.Text.StringBuilder> object to a method that has a <xref:System.String> parameter or display it in the user interface.</span></span> <span data-ttu-id="53309-160">可通过调用 <xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> 方法来执行此转换。</span><span class="sxs-lookup"><span data-stu-id="53309-160">You do this conversion by calling the <xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="53309-161">下面的示例先调用许多 <xref:System.Text.StringBuilder> 方法，再调用 <xref:System.Text.StringBuilder.ToString?displayProperty=nameWithType> 方法来显示字符串。</span><span class="sxs-lookup"><span data-stu-id="53309-161">The following example calls a number of <xref:System.Text.StringBuilder> methods and then calls the <xref:System.Text.StringBuilder.ToString?displayProperty=nameWithType> method to display the string.</span></span>  
  
 [!code-csharp[Conceptual.StringBuilder#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/tostringexample1.cs#10)]
 [!code-vb[Conceptual.StringBuilder#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/tostringexample1.vb#10)]  
  
## <a name="see-also"></a><span data-ttu-id="53309-162">请参阅</span><span class="sxs-lookup"><span data-stu-id="53309-162">See also</span></span>

- <xref:System.Text.StringBuilder?displayProperty=nameWithType>
- [<span data-ttu-id="53309-163">基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="53309-163">Basic String Operations</span></span>](basic-string-operations.md)
- [<span data-ttu-id="53309-164">格式设置类型</span><span class="sxs-lookup"><span data-stu-id="53309-164">Formatting Types</span></span>](formatting-types.md)
