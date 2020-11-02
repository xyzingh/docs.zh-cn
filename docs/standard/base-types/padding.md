---
title: 填充 .NET 中的字符串
description: 了解如何填充 .NET 中的字符串。 使用 String.PadLeft 和 String.PadRight 方法添加前导或尾随字符，以达到指定的总长度。
ms.date: 03/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET], padding
- white space
- PadRight method
- PadLeft method
- padding strings
ms.assetid: 84a9f142-3244-4c90-ba02-21af9bbaff71
ms.openlocfilehash: f90a95f0ceb5ad7cc32d451897544fffe56afb6d
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889044"
---
# <a name="padding-strings-in-net"></a><span data-ttu-id="1e04f-104">填充 .NET 中的字符串</span><span class="sxs-lookup"><span data-stu-id="1e04f-104">Padding Strings in .NET</span></span>

<span data-ttu-id="1e04f-105">使用下面的 <xref:System.String> 方法之一，在原始字符串中填充前导或尾随字符，以达到指定总长度，从而新建字符串。</span><span class="sxs-lookup"><span data-stu-id="1e04f-105">Use one of the following <xref:System.String> methods to create a new string that consists of an original string that is padded with leading or trailing characters to a specified total length.</span></span> <span data-ttu-id="1e04f-106">填充字符可以是空格或指定字符。</span><span class="sxs-lookup"><span data-stu-id="1e04f-106">The padding character can be a space or a specified character.</span></span> <span data-ttu-id="1e04f-107">生成的字符串可能显示为右对齐或左对齐。</span><span class="sxs-lookup"><span data-stu-id="1e04f-107">The resulting string appears to be either right-aligned or left-aligned.</span></span> <span data-ttu-id="1e04f-108">如果原始字符串的长度已经等于或大于所需总长度，则填充方法返回未经更改的原始字符串；有关详细信息，请参阅 <xref:System.String.PadLeft%2A?displayProperty=nameWithType> 和 <xref:System.String.PadRight%2A?displayProperty=nameWithType> 方法的两个重载的“返回”部分。</span><span class="sxs-lookup"><span data-stu-id="1e04f-108">If the original string's length is already equal to or greater than the desired total length, the padding methods return the original string unchanged; for more information, see the **Returns** sections of the two overloads of the <xref:System.String.PadLeft%2A?displayProperty=nameWithType> and <xref:System.String.PadRight%2A?displayProperty=nameWithType> methods.</span></span>
  
|<span data-ttu-id="1e04f-109">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e04f-109">Method name</span></span>|<span data-ttu-id="1e04f-110">使用</span><span class="sxs-lookup"><span data-stu-id="1e04f-110">Use</span></span>|  
|-----------------|---------|  
|<xref:System.String.PadLeft%2A?displayProperty=nameWithType>|<span data-ttu-id="1e04f-111">使用前导字符将字符串填充到指定总长度。</span><span class="sxs-lookup"><span data-stu-id="1e04f-111">Pads a string with leading characters to a specified total length.</span></span>|  
|<xref:System.String.PadRight%2A?displayProperty=nameWithType>|<span data-ttu-id="1e04f-112">使用尾随字符将字符串填充到指定总长度。</span><span class="sxs-lookup"><span data-stu-id="1e04f-112">Pads a string with trailing characters to a specified total length.</span></span>|  
  
## <a name="padleft"></a><span data-ttu-id="1e04f-113">PadLeft</span><span class="sxs-lookup"><span data-stu-id="1e04f-113">PadLeft</span></span>  
 <span data-ttu-id="1e04f-114"><xref:System.String.PadLeft%2A?displayProperty=nameWithType> 方法将足够多的前导填充字符连接到原始字符串，以达到指定总长度，从而新建字符串。</span><span class="sxs-lookup"><span data-stu-id="1e04f-114">The <xref:System.String.PadLeft%2A?displayProperty=nameWithType> method creates a new string by concatenating enough leading pad characters to an original string to achieve a specified total length.</span></span> <span data-ttu-id="1e04f-115"><xref:System.String.PadLeft%28System.Int32%29?displayProperty=nameWithType> 方法使用空格作为填充字符，<xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> 方法支持指定自己的填充字符。</span><span class="sxs-lookup"><span data-stu-id="1e04f-115">The <xref:System.String.PadLeft%28System.Int32%29?displayProperty=nameWithType> method uses white space as the padding character and the <xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> method enables you to specify your own padding character.</span></span>  
  
 <span data-ttu-id="1e04f-116">下面的代码示例使用 <xref:System.String.PadLeft%2A> 方法新建长度为 20 个字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="1e04f-116">The following code example uses the <xref:System.String.PadLeft%2A> method to create a new string that is twenty characters long.</span></span> <span data-ttu-id="1e04f-117">该示例向控制台显示“`--------Hello World!`”。</span><span class="sxs-lookup"><span data-stu-id="1e04f-117">The example displays "`--------Hello World!`" to the console.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#3)]
 [!code-csharp[Conceptual.String.BasicOps#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#3)]
 [!code-vb[Conceptual.String.BasicOps#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#3)]  
  
## <a name="padright"></a><span data-ttu-id="1e04f-118">PadRight</span><span class="sxs-lookup"><span data-stu-id="1e04f-118">PadRight</span></span>  
 <span data-ttu-id="1e04f-119"><xref:System.String.PadRight%2A?displayProperty=nameWithType> 方法将足够多的尾随填充字符连接到原始字符串，以达到指定总长度，从而新建字符串。</span><span class="sxs-lookup"><span data-stu-id="1e04f-119">The <xref:System.String.PadRight%2A?displayProperty=nameWithType> method creates a new string by concatenating enough trailing pad characters to an original string to achieve a specified total length.</span></span> <span data-ttu-id="1e04f-120"><xref:System.String.PadRight%28System.Int32%29?displayProperty=nameWithType> 方法使用空格作为填充字符，<xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> 方法支持指定自己的填充字符。</span><span class="sxs-lookup"><span data-stu-id="1e04f-120">The <xref:System.String.PadRight%28System.Int32%29?displayProperty=nameWithType> method uses white space as the padding character and the <xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> method enables you to specify your own padding character.</span></span>  
  
 <span data-ttu-id="1e04f-121">下面的代码示例使用 <xref:System.String.PadRight%2A> 方法新建长度为 20 个字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="1e04f-121">The following code example uses the <xref:System.String.PadRight%2A> method to create a new string that is twenty characters long.</span></span> <span data-ttu-id="1e04f-122">该示例向控制台显示“`Hello World!--------`”。</span><span class="sxs-lookup"><span data-stu-id="1e04f-122">The example displays "`Hello World!--------`" to the console.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#4)]
 [!code-csharp[Conceptual.String.BasicOps#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#4)]
 [!code-vb[Conceptual.String.BasicOps#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="1e04f-123">请参阅</span><span class="sxs-lookup"><span data-stu-id="1e04f-123">See also</span></span>

- [<span data-ttu-id="1e04f-124">基本字符串操作</span><span class="sxs-lookup"><span data-stu-id="1e04f-124">Basic String Operations</span></span>](basic-string-operations.md)
