---
title: 修整和删除 .NET 中的字符串字符
description: 了解如何在字符串的开头或结尾修整空格，或者从 .NET 的字符串中的指定位置删除任意数量的空格或字符。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET], removing characters
- Remove method
- TrimEnd method
- Trim method
- trimming characters
- TrimStart method
- removing characters
ms.assetid: ab248dab-70d4-4413-81c6-542d153fd195
ms.openlocfilehash: d0057d503474f3f6ff886acda3ce1d72fb3ebe21
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888589"
---
# <a name="trimming-and-removing-characters-from-strings-in-net"></a><span data-ttu-id="95926-103">修整和删除 .NET 中的字符串字符</span><span class="sxs-lookup"><span data-stu-id="95926-103">Trimming and Removing Characters from Strings in .NET</span></span>
<span data-ttu-id="95926-104">如果将句子分析成单个单词，最后得到的结果可能是任意一端带有空白（也称为空格）的单词。</span><span class="sxs-lookup"><span data-stu-id="95926-104">If you are parsing a sentence into individual words, you might end up with words that have blank spaces (also called white spaces) on either end of the word.</span></span> <span data-ttu-id="95926-105">在这种情形下，可以使用 **System.String** 类中的其中一种剪裁方法，从字符串中的指定位置移除任何数量的空格或其他字符。</span><span class="sxs-lookup"><span data-stu-id="95926-105">In this situation, you can use one of the trim methods in the **System.String** class to remove any number of spaces or other characters from a specified position in the string.</span></span> <span data-ttu-id="95926-106">下表描述了可用的剪裁方法。</span><span class="sxs-lookup"><span data-stu-id="95926-106">The following table describes the available trim methods.</span></span>  
  
|<span data-ttu-id="95926-107">方法名称</span><span class="sxs-lookup"><span data-stu-id="95926-107">Method name</span></span>|<span data-ttu-id="95926-108">使用</span><span class="sxs-lookup"><span data-stu-id="95926-108">Use</span></span>|  
|-----------------|---------|  
|<xref:System.String.Trim%2A?displayProperty=nameWithType>|<span data-ttu-id="95926-109">从字符串的开头和结尾移除空白或者指定的字符</span><span class="sxs-lookup"><span data-stu-id="95926-109">Removes white spaces or characters specified in an array of characters from the beginning and end of a string.</span></span>|  
|<xref:System.String.TrimEnd%2A?displayProperty=nameWithType>|<span data-ttu-id="95926-110">从字符串的结尾移除在字符数组中指定的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-110">Removes characters specified in an array of characters from the end of a string.</span></span>|  
|<xref:System.String.TrimStart%2A?displayProperty=nameWithType>|<span data-ttu-id="95926-111">从字符串的开头移除在字符数组中指定的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-111">Removes characters specified in an array of characters from the beginning of a string.</span></span>|  
|<xref:System.String.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="95926-112">从字符串中的指定索引位置移除指定数量的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-112">Removes a specified number of characters from a specified index position in a string.</span></span>|  
  
## <a name="trim"></a><span data-ttu-id="95926-113">Trim</span><span class="sxs-lookup"><span data-stu-id="95926-113">Trim</span></span>

 <span data-ttu-id="95926-114">通过使用 <xref:System.String.Trim%2A?displayProperty=nameWithType> 方法，可以方便地从字符串两端移除空白，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="95926-114">You can easily remove white spaces from both ends of a string by using the <xref:System.String.Trim%2A?displayProperty=nameWithType> method, as shown in the following example.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#17)]
 [!code-csharp[Conceptual.String.BasicOps#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#17)]
 [!code-vb[Conceptual.String.BasicOps#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#17)]  
  
 <span data-ttu-id="95926-115">还可以从字符串的开始和结尾移除指定的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-115">You can also remove characters that you specify in a character array from the beginning and end of a string.</span></span> <span data-ttu-id="95926-116">下面的示例将移除空白字符、句点和星号。</span><span class="sxs-lookup"><span data-stu-id="95926-116">The following example removes white-space characters, periods, and asterisks.</span></span>  
  
 [!code-csharp[Conceptual.String.BasicOps#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trim2.cs#22)]
 [!code-vb[Conceptual.String.BasicOps#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trim2.vb#22)]  
  
## <a name="trimend"></a><span data-ttu-id="95926-117">TrimEnd</span><span class="sxs-lookup"><span data-stu-id="95926-117">TrimEnd</span></span>

 <span data-ttu-id="95926-118">**String.TrimEnd** 方法从字符串的结尾移除字符，同时创建新的字符串对象。</span><span class="sxs-lookup"><span data-stu-id="95926-118">The **String.TrimEnd** method removes characters from the end of a string, creating a new string object.</span></span> <span data-ttu-id="95926-119">通过向此方法传递一个字符数组来指定要移除的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-119">An array of characters is passed to this method to specify the characters to be removed.</span></span> <span data-ttu-id="95926-120">字符数组中的元素顺序并不影响剪裁操作。</span><span class="sxs-lookup"><span data-stu-id="95926-120">The order of the elements in the character array does not affect the trim operation.</span></span> <span data-ttu-id="95926-121">找到未在数组中指定的字符时，剪裁停止。</span><span class="sxs-lookup"><span data-stu-id="95926-121">The trim stops when a character not specified in the array is found.</span></span>  
  
 <span data-ttu-id="95926-122">下面的示例使用 TrimEnd 方法，删除字符串的最后几个字母。</span><span class="sxs-lookup"><span data-stu-id="95926-122">The following example removes the last letters of a string using the **TrimEnd** method.</span></span> <span data-ttu-id="95926-123">在此示例中，`'r'` 字符和 `'W'` 字符的位置交换，说明数组中字符的顺序并不重要。</span><span class="sxs-lookup"><span data-stu-id="95926-123">In this example, the position of the `'r'` character and the `'W'` character are reversed to illustrate that the order of characters in the array does not matter.</span></span> <span data-ttu-id="95926-124">请注意，此代码移除 `MyString` 的最后一个单词和第一个单词的一部分。</span><span class="sxs-lookup"><span data-stu-id="95926-124">Notice that this code removes the last word of `MyString` plus part of the first.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#18)]
 [!code-csharp[Conceptual.String.BasicOps#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#18)]
 [!code-vb[Conceptual.String.BasicOps#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#18)]  
  
 <span data-ttu-id="95926-125">此代码向控制台显示 `He`。</span><span class="sxs-lookup"><span data-stu-id="95926-125">This code displays `He` to the console.</span></span>  
  
 <span data-ttu-id="95926-126">下面的示例使用 **TrimEnd** 方法移除字符串的最后一个单词。</span><span class="sxs-lookup"><span data-stu-id="95926-126">The following example removes the last word of a string using the **TrimEnd** method.</span></span> <span data-ttu-id="95926-127">在此代码中，单词 `Hello` 后跟一个逗号，而由于在要剪裁的字符数组中未指定逗号，因此剪裁在逗号处结束。</span><span class="sxs-lookup"><span data-stu-id="95926-127">In this code, a comma follows the word `Hello` and, because the comma is not specified in the array of characters to trim, the trim ends at the comma.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#19)]
 [!code-csharp[Conceptual.String.BasicOps#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#19)]
 [!code-vb[Conceptual.String.BasicOps#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#19)]  
  
 <span data-ttu-id="95926-128">此代码向控制台显示 `Hello,`。</span><span class="sxs-lookup"><span data-stu-id="95926-128">This code displays `Hello,` to the console.</span></span>  
  
## <a name="trimstart"></a><span data-ttu-id="95926-129">TrimStart</span><span class="sxs-lookup"><span data-stu-id="95926-129">TrimStart</span></span>

 <span data-ttu-id="95926-130">**String.TrimStart** 方法类似于 **String.TrimEnd** 方法，不同之处在于它通过从现有字符串对象的开头移除字符来创建新的字符串。</span><span class="sxs-lookup"><span data-stu-id="95926-130">The **String.TrimStart** method is similar to the **String.TrimEnd** method except that it creates a new string by removing characters from the beginning of an existing string object.</span></span> <span data-ttu-id="95926-131">通过向 **TrimStart** 方法传递一个字符数组来指定要移除的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-131">An array of characters is passed to the **TrimStart** method to specify the characters to be removed.</span></span> <span data-ttu-id="95926-132">与 **TrimEnd** 方法一样，字符数组中元素的顺序并不影响剪裁操作。</span><span class="sxs-lookup"><span data-stu-id="95926-132">As with the **TrimEnd** method, the order of the elements in the character array does not affect the trim operation.</span></span> <span data-ttu-id="95926-133">找到未在数组中指定的字符时，剪裁停止。</span><span class="sxs-lookup"><span data-stu-id="95926-133">The trim stops when a character not specified in the array is found.</span></span>  
  
 <span data-ttu-id="95926-134">下面的示例移除字符串的第一个单词。</span><span class="sxs-lookup"><span data-stu-id="95926-134">The following example removes the first word of a string.</span></span> <span data-ttu-id="95926-135">在此示例中，`'l'` 字符和 `'H'` 字符的位置交换，说明数组中字符的顺序并不重要。</span><span class="sxs-lookup"><span data-stu-id="95926-135">In this example, the position of the `'l'` character and the `'H'` character are reversed to illustrate that the order of characters in the array does not matter.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#20)]
 [!code-csharp[Conceptual.String.BasicOps#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#20)]
 [!code-vb[Conceptual.String.BasicOps#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#20)]  
  
 <span data-ttu-id="95926-136">此代码向控制台显示 `World!`。</span><span class="sxs-lookup"><span data-stu-id="95926-136">This code displays `World!` to the console.</span></span>  
  
## <a name="remove"></a><span data-ttu-id="95926-137">删除</span><span class="sxs-lookup"><span data-stu-id="95926-137">Remove</span></span>

 <span data-ttu-id="95926-138"><xref:System.String.Remove%2A?displayProperty=nameWithType> 方法从现有字符串的指定位置开始移除指定数量的字符。</span><span class="sxs-lookup"><span data-stu-id="95926-138">The <xref:System.String.Remove%2A?displayProperty=nameWithType> method removes a specified number of characters that begin at a specified position in an existing string.</span></span> <span data-ttu-id="95926-139">此方法采用从零开始的索引。</span><span class="sxs-lookup"><span data-stu-id="95926-139">This method assumes a zero-based index.</span></span>  
  
 <span data-ttu-id="95926-140">下面的示例在字符串从零开始的索引中第五个位置开始移除十个字符。</span><span class="sxs-lookup"><span data-stu-id="95926-140">The following example removes ten characters from a string beginning at position five of a zero-based index of the string.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#21)]
 [!code-csharp[Conceptual.String.BasicOps#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#21)]
 [!code-vb[Conceptual.String.BasicOps#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#21)]  
  
## <a name="replace"></a><span data-ttu-id="95926-141">替换</span><span class="sxs-lookup"><span data-stu-id="95926-141">Replace</span></span>

 <span data-ttu-id="95926-142">通过调用 <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=nameWithType> 方法并指定空字符串 (<xref:System.String.Empty?displayProperty=nameWithType>) 作为替代，也可以从字符串中移除指定字符或子字符串。</span><span class="sxs-lookup"><span data-stu-id="95926-142">You can also remove a specified character or substring from a string by calling the <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=nameWithType> method and specifying an empty string (<xref:System.String.Empty?displayProperty=nameWithType>) as the replacement.</span></span> <span data-ttu-id="95926-143">下面的示例从字符串中移除所有逗号。</span><span class="sxs-lookup"><span data-stu-id="95926-143">The following example removes all commas from a string.</span></span>  
  
 [!code-csharp[Conceptual.String.BasicOps#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/replace1.cs#23)]
 [!code-vb[Conceptual.String.BasicOps#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/replace1.vb#23)]  
  
## <a name="see-also"></a><span data-ttu-id="95926-144">请参阅</span><span class="sxs-lookup"><span data-stu-id="95926-144">See also</span></span>

- [<span data-ttu-id="95926-145">基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="95926-145">Basic String Operations</span></span>](basic-string-operations.md)
