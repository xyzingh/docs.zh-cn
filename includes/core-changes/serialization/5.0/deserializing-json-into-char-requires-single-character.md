---
ms.openlocfilehash: 8209c5336983bde13a698fbc68e6a099091071f7
ms.sourcegitcommit: a6bd4cad438fe479cbd112eae10f2cd449f06e40
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2020
ms.locfileid: "91844496"
---
### <a name="jsonserializerdeserialize-requires-single-character-string"></a>JsonSerializer.Deserialize 需要单字符的字符串

如果类型参数是 <xref:System.Char>，<xref:System.Text.Json.JsonSerializer.Deserialize%60%601(System.String,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> 的字符串参数必须包含单个字符才能成功进行反序列化。

#### <a name="change-description"></a>更改描述

在以前的 .NET 版本中，如果将多字符字符串传递到 <xref:System.Text.Json.JsonSerializer.Deserialize%60%601(System.String,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType>，并且类型参数为 <xref:System.Char>，则反序列化会成功，并且仅反序列化第一个字符。

在 .NET 5.0 和更高版本中，如果类型参数为 <xref:System.Char>，传递除单字符字符串外的任何内容都会导致引发 <xref:System.Text.Json.JsonException>。

```csharp
// .NET Core 3.0 and 3.1: Returns the first character 'a'.
// .NET 5.0 and later: Throws JsonException because payload has more than one character.
JsonSerializer.Deserialize<char>("\"abc\"");

// Correct usage.
JsonSerializer.Deserialize<char>("\"a\"");
```

#### <a name="version-introduced"></a>引入的版本

5.0

#### <a name="reason-for-change"></a>更改原因

<xref:System.Text.Json.JsonSerializer.Deserialize%60%601(System.String,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> 将表示单个 JSON 值的文本分析为泛型类型参数指定的类型的实例。 仅当提供的有效负载对指定的泛型类型参数有效时，分析才会成功。 对于 <xref:System.Char> 值类型，有效的负载是单字符字符串。

#### <a name="recommended-action"></a>建议的操作

使用 <xref:System.Text.Json.JsonSerializer.Deserialize%60%601(System.String,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> 将字符串分析为 <xref:System.Char> 类型时，请确保字符串包含单个字符。

#### <a name="category"></a>类别

序列化

#### <a name="affected-apis"></a>受影响的 API

- <xref:System.Text.Json.JsonSerializer.Deserialize%60%601(System.String,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Text.Json.JsonSerializer.Deserialize``1(System.String,System.Text.Json.JsonSerializerOptions)`

-->
