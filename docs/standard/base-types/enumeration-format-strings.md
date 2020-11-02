---
title: 枚举格式字符串
description: 使用 .NET 中的 Enum.ToString 方法创建枚举格式字符串。 格式化枚举成员的数字、十六进制或字符串值。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- format specifiers, enumeration format strings
- enumeration format strings
- formatting [.NET], enumeration
ms.assetid: dd1ff672-1052-42cf-8666-4924fb6cd1a1
ms.openlocfilehash: e4d8ca27d99c211653269b2477be8f5632b78229
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888654"
---
# <a name="enumeration-format-strings"></a><span data-ttu-id="07161-104">枚举格式字符串</span><span class="sxs-lookup"><span data-stu-id="07161-104">Enumeration format strings</span></span>

<span data-ttu-id="07161-105">可以使用 <xref:System.Enum.ToString%2A?displayProperty=nameWithType> 方法，新建表示枚举成员的数字值、十六进制值或字符串值的字符串对象。</span><span class="sxs-lookup"><span data-stu-id="07161-105">You can use the <xref:System.Enum.ToString%2A?displayProperty=nameWithType> method to create a new string object that represents the numeric, hexadecimal, or string value of an enumeration member.</span></span> <span data-ttu-id="07161-106">此方法采用枚举格式设置字符串之一来指定要返回的值。</span><span class="sxs-lookup"><span data-stu-id="07161-106">This method takes one of the enumeration formatting strings to specify the value that you want returned.</span></span>

<span data-ttu-id="07161-107">以下各部分列出了枚举格式设置字符串和它们返回的值。</span><span class="sxs-lookup"><span data-stu-id="07161-107">The following sections list the enumeration formatting strings and the values they return.</span></span> <span data-ttu-id="07161-108">这些格式说明符不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="07161-108">These format specifiers are not case-sensitive.</span></span>

## <a name="g-or-g"></a><span data-ttu-id="07161-109">G 或 g</span><span class="sxs-lookup"><span data-stu-id="07161-109">G or g</span></span>

<span data-ttu-id="07161-110">如有可能，将枚举项显示为字符串值，否则显示当前实例的整数值。</span><span class="sxs-lookup"><span data-stu-id="07161-110">Displays the enumeration entry as a string value, if possible, and otherwise displays the integer value of the current instance.</span></span> <span data-ttu-id="07161-111">如果枚举使用 **Flags** 属性集进行定义，则每个有效项的字符串值会连接在一起（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="07161-111">If the enumeration is defined with the **Flags** attribute set, the string values of each valid entry are concatenated together, separated by commas.</span></span> <span data-ttu-id="07161-112">如果未设置 **Flags** 属性，则将无效值显示为数字项。</span><span class="sxs-lookup"><span data-stu-id="07161-112">If the **Flags** attribute is not set, an invalid value is displayed as a numeric entry.</span></span> <span data-ttu-id="07161-113">下面的示例演示 G 格式说明符。</span><span class="sxs-lookup"><span data-stu-id="07161-113">The following example illustrates the G format specifier.</span></span>

[!code-csharp[Formatting.Enum#1](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#1)]
[!code-vb[Formatting.Enum#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#1)]

## <a name="f-or-f"></a><span data-ttu-id="07161-114">F 或 f</span><span class="sxs-lookup"><span data-stu-id="07161-114">F or f</span></span>

<span data-ttu-id="07161-115">如有可能，将枚举项显示为字符串值。</span><span class="sxs-lookup"><span data-stu-id="07161-115">Displays the enumeration entry as a string value, if possible.</span></span> <span data-ttu-id="07161-116">如果值可以完全显示为枚举中项的总和（即使未提供 **Flags** 属性），则每个有效项的字符串值会连接在一起（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="07161-116">If the value can be completely displayed as a summation of the entries in the enumeration (even if the **Flags** attribute is not present), the string values of each valid entry are concatenated together, separated by commas.</span></span> <span data-ttu-id="07161-117">如果值不能由枚举项完全确定，则值会格式化为整数值。</span><span class="sxs-lookup"><span data-stu-id="07161-117">If the value cannot be completely determined by the enumeration entries, then the value is formatted as the integer value.</span></span> <span data-ttu-id="07161-118">下面的示例演示 F 格式说明符。</span><span class="sxs-lookup"><span data-stu-id="07161-118">The following example illustrates the F format specifier.</span></span>

[!code-csharp[Formatting.Enum#2](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#2)]
[!code-vb[Formatting.Enum#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#2)]

## <a name="d-or-d"></a><span data-ttu-id="07161-119">D 或 d</span><span class="sxs-lookup"><span data-stu-id="07161-119">D or d</span></span>

<span data-ttu-id="07161-120">以尽可能短的表示形式将枚举项显示为整数值。</span><span class="sxs-lookup"><span data-stu-id="07161-120">Displays the enumeration entry as an integer value in the shortest representation possible.</span></span> <span data-ttu-id="07161-121">下面的示例演示 D 格式说明符。</span><span class="sxs-lookup"><span data-stu-id="07161-121">The following example illustrates the D format specifier.</span></span>

[!code-csharp[Formatting.Enum#3](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#3)]
[!code-vb[Formatting.Enum#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#3)]

## <a name="x-or-x"></a><span data-ttu-id="07161-122">X 或 x</span><span class="sxs-lookup"><span data-stu-id="07161-122">X or x</span></span>

<span data-ttu-id="07161-123">将枚举项显示为十六进制值。</span><span class="sxs-lookup"><span data-stu-id="07161-123">Displays the enumeration entry as a hexadecimal value.</span></span> <span data-ttu-id="07161-124">根据需要以前导零表示此值，以确保在枚举类型的[基础数值类型](xref:System.Enum.GetUnderlyingType%2A)中，结果字符串的每个字节都有两个字符。</span><span class="sxs-lookup"><span data-stu-id="07161-124">The value is represented with leading zeros as necessary, to ensure that the result string has two characters for each byte in the enumeration type's [underlying numeric type](xref:System.Enum.GetUnderlyingType%2A).</span></span> <span data-ttu-id="07161-125">下面的示例演示 X 格式说明符。</span><span class="sxs-lookup"><span data-stu-id="07161-125">The following example illustrates the X format specifier.</span></span> <span data-ttu-id="07161-126">在示例中，这两者的基础类型 <xref:System.ConsoleColor> 和 <xref:System.IO.FileAttributes> 为 <xref:System.Int32>，或 32 位（或 4 字节）整数，它将生成 8 个字符的结果字符串。</span><span class="sxs-lookup"><span data-stu-id="07161-126">In the example, the underlying type of both <xref:System.ConsoleColor> and <xref:System.IO.FileAttributes> is <xref:System.Int32>, or a 32-bit (or 4-byte) integer, which produces an 8-character result string.</span></span>

[!code-csharp[Formatting.Enum#4](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#4)]
[!code-vb[Formatting.Enum#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#4)]

## <a name="example"></a><span data-ttu-id="07161-127">示例</span><span class="sxs-lookup"><span data-stu-id="07161-127">Example</span></span>

<span data-ttu-id="07161-128">下面的示例定义一个名为 `Colors` 的枚举，它由三个项组成：`Red`、`Blue` 和 `Green`。</span><span class="sxs-lookup"><span data-stu-id="07161-128">The following example defines an enumeration called `Colors` that consists of three entries: `Red`, `Blue`, and `Green`.</span></span>

[!code-csharp[Formatting.Enum#5](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#5)]
[!code-vb[Formatting.Enum#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#5)]

<span data-ttu-id="07161-129">定义该枚举之后，可以按以下方式声明实例。</span><span class="sxs-lookup"><span data-stu-id="07161-129">After the enumeration is defined, an instance can be declared in the following manner.</span></span>

[!code-csharp[Formatting.Enum#6](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#6)]
[!code-vb[Formatting.Enum#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#6)]

<span data-ttu-id="07161-130">`Color.ToString(System.String)` 方法随后可以用于以不同方式显示枚举值（具体取决于传递给它的格式说明符）。</span><span class="sxs-lookup"><span data-stu-id="07161-130">The `Color.ToString(System.String)` method can then be used to display the enumeration value in different ways, depending on the format specifier passed to it.</span></span>

[!code-csharp[Formatting.Enum#7](~/samples/snippets/csharp/VS_Snippets_CLR/Formatting.Enum/cs/enum1.cs#7)]
[!code-vb[Formatting.Enum#7](~/samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Enum/vb/enum1.vb#7)]

## <a name="see-also"></a><span data-ttu-id="07161-131">请参阅</span><span class="sxs-lookup"><span data-stu-id="07161-131">See also</span></span>

- [<span data-ttu-id="07161-132">格式设置类型</span><span class="sxs-lookup"><span data-stu-id="07161-132">Formatting Types</span></span>](formatting-types.md)
