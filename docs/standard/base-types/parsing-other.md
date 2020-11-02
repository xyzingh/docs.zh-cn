---
title: 分析 .NET 中的其他字符串
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Char data type, parsing strings
- enumerations [.NET], parsing strings
- base types, parsing strings
- parsing strings, other strings
- Boolean data type, parsing strings
ms.assetid: d139bc00-3c4e-4d78-ac9a-5c951b258d28
ms.openlocfilehash: 5a8afde40dddd69a9648439be5c0f232db23b37b
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889005"
---
# <a name="parsing-other-strings-in-net"></a><span data-ttu-id="6287f-102">分析 .NET 中的其他字符串</span><span class="sxs-lookup"><span data-stu-id="6287f-102">Parsing Other Strings in .NET</span></span>
<span data-ttu-id="6287f-103">除了数字和 <xref:System.DateTime> 字符串之外，还可以将表示类型 <xref:System.Char>、<xref:System.Boolean> 和 <xref:System.Enum> 的字符串分析为数据类型。</span><span class="sxs-lookup"><span data-stu-id="6287f-103">In addition to numeric and <xref:System.DateTime> strings, you can also parse strings that represent the types <xref:System.Char>, <xref:System.Boolean>, and <xref:System.Enum> into data types.</span></span>  
  
## <a name="char"></a><span data-ttu-id="6287f-104">Char</span><span class="sxs-lookup"><span data-stu-id="6287f-104">Char</span></span>  
 <span data-ttu-id="6287f-105">与 **Char** 数据类型关联的静态分析方法 可用于将包含单个字符的字符串转换为其 Unicode 值。</span><span class="sxs-lookup"><span data-stu-id="6287f-105">The static parse method associated with the **Char** data type is useful for converting a string that contains a single character into its Unicode value.</span></span> <span data-ttu-id="6287f-106">下面的代码示例将字符串分析为 Unicode 字符。</span><span class="sxs-lookup"><span data-stu-id="6287f-106">The following code example parses a string into a Unicode character.</span></span>  
  
 [!code-cpp[Conceptual.String.Parse#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#2)]
 [!code-csharp[Conceptual.String.Parse#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#2)]
 [!code-vb[Conceptual.String.Parse#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#2)]  
  
## <a name="boolean"></a><span data-ttu-id="6287f-107">Boolean</span><span class="sxs-lookup"><span data-stu-id="6287f-107">Boolean</span></span>  
 <span data-ttu-id="6287f-108">Boolean  数据类型包含 Parse  方法，可用于将表示 Boolean 值的字符串转换为实际 Boolean  类型。</span><span class="sxs-lookup"><span data-stu-id="6287f-108">The **Boolean** data type contains a **Parse** method that you can use to convert a string that represents a Boolean value into an actual **Boolean** type.</span></span> <span data-ttu-id="6287f-109">此方法不区分大小写，可以成功分析包含“True”或“False”的字符串。</span><span class="sxs-lookup"><span data-stu-id="6287f-109">This method is not case-sensitive and can successfully parse a string containing "True" or "False."</span></span> <span data-ttu-id="6287f-110">与 Boolean 类型关联的 Parse 方法还可以分析两端是空格的字符串。</span><span class="sxs-lookup"><span data-stu-id="6287f-110">The **Parse** method associated with the **Boolean** type can also parse strings that are surrounded by white spaces.</span></span> <span data-ttu-id="6287f-111">如果传递的是其他任何字符串，<xref:System.FormatException> 就会抛出。</span><span class="sxs-lookup"><span data-stu-id="6287f-111">If any other string is passed, a <xref:System.FormatException> is thrown.</span></span>  
  
 <span data-ttu-id="6287f-112">下面的代码示例使用 Parse  方法，将字符串转换为 Boolean 值。</span><span class="sxs-lookup"><span data-stu-id="6287f-112">The following code example uses the **Parse** method to convert a string into a Boolean value.</span></span>  
  
 [!code-cpp[Conceptual.String.Parse#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#3)]
 [!code-csharp[Conceptual.String.Parse#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#3)]
 [!code-vb[Conceptual.String.Parse#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#3)]  
  
## <a name="enumeration"></a><span data-ttu-id="6287f-113">枚举</span><span class="sxs-lookup"><span data-stu-id="6287f-113">Enumeration</span></span>  
 <span data-ttu-id="6287f-114">可以使用静态 **Parse** 方法将枚举类型初始化为字符串的值。</span><span class="sxs-lookup"><span data-stu-id="6287f-114">You can use the static **Parse** method to initialize an enumeration type to the value of a string.</span></span> <span data-ttu-id="6287f-115">此方法接受要分析的枚举类型、要分析的字符串和可选 Boolean 标志（指明分析是否区分大小写）。</span><span class="sxs-lookup"><span data-stu-id="6287f-115">This method accepts the enumeration type you are parsing, the string to parse, and an optional Boolean flag indicating whether or not the parse is case-sensitive.</span></span> <span data-ttu-id="6287f-116">所分析的字符串可以包含用逗号分隔的多个值，这些值前面或后面可以是一个或多个空白（也称为空格）。</span><span class="sxs-lookup"><span data-stu-id="6287f-116">The string you are parsing can contain several values separated by commas, which can be preceded or followed by one or more empty spaces (also called white spaces).</span></span> <span data-ttu-id="6287f-117">当字符串包含多个值时，返回的对象的值是所有指定值通过按位 OR 运算组合的值。</span><span class="sxs-lookup"><span data-stu-id="6287f-117">When the string contains multiple values, the value of the returned object is the value of all specified values combined with a bitwise OR operation.</span></span>  
  
 <span data-ttu-id="6287f-118">下面的示例使用 Parse  方法，将字符串表示形式转换为枚举值。</span><span class="sxs-lookup"><span data-stu-id="6287f-118">The following example uses the **Parse** method to convert a string representation into an enumeration value.</span></span> <span data-ttu-id="6287f-119"><xref:System.DayOfWeek> 枚举从字符串初始化为 Thursday  。</span><span class="sxs-lookup"><span data-stu-id="6287f-119">The <xref:System.DayOfWeek> enumeration is initialized to **Thursday** from a string.</span></span>  
  
 [!code-cpp[Conceptual.String.Parse#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#4)]
 [!code-csharp[Conceptual.String.Parse#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#4)]
 [!code-vb[Conceptual.String.Parse#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="6287f-120">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6287f-120">See also</span></span>

- [<span data-ttu-id="6287f-121">Parsing Strings</span><span class="sxs-lookup"><span data-stu-id="6287f-121">Parsing Strings</span></span>](parsing-strings.md)
- [<span data-ttu-id="6287f-122">格式设置类型</span><span class="sxs-lookup"><span data-stu-id="6287f-122">Formatting Types</span></span>](formatting-types.md)
- [<span data-ttu-id="6287f-123">.NET 中的类型转换</span><span class="sxs-lookup"><span data-stu-id="6287f-123">Type Conversion in the .NET</span></span>](type-conversion.md)
