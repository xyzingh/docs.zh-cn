---
title: 序列化中断性变更
description: 列出 .NET Core 和 .NET 5.0 及更高版本中序列化类别的中断性变更。
ms.date: 07/30/2020
ms.openlocfilehash: 67608c8e7a9745c060b7eb179fe5a956ede9f80f
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92332870"
---
# <a name="serialization-breaking-changes"></a>序列化中断性变更

本页记录了以下中断性变更：

| 重大更改 | 引入的版本 |
| - | - |
| [ASP.NET Core 应用允许反序列化带引号的数字](#aspnet-core-apps-allow-deserializing-quoted-numbers) | 5.0 |
| [对键值对进行序列化和反序列化时，使用“PropertyNamingPolicy”、“PropertyNameCaseInsensitive”和“Encoder”选项](#propertynamingpolicy-propertynamecaseinsensitive-and-encoder-options-are-honored-when-serializing-and-deserializing-key-value-pairs) | 5.0 |
| [非公共的无参数构造函数不用于反序列化](#non-public-parameterless-constructors-not-used-for-deserialization) | 5.0 |
| [JsonSerializer.Serialize 在类型参数为 null 时引发 ArgumentNullException](#jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null) | 5.0 |
| [JsonSerializer.Deserialize 需要单字符的字符串](#jsonserializerdeserialize-requires-single-character-string) | 5.0 |
| [BinaryFormatter.Deserialize 重新包装 SerializationException 中的一些异常](#binaryformatterdeserialize-rewraps-some-exceptions-in-serializationexception) | 5.0 |

## <a name="net-50"></a>.NET 5.0

[!INCLUDE [jsonserializer-allows-reading-numbers-as-strings](../../../includes/core-changes/serialization/5.0/jsonserializer-allows-reading-numbers-as-strings.md)]

***

[!INCLUDE [options-honored-when-serializing-key-value-pairs](../../../includes/core-changes/serialization/5.0/options-honored-when-serializing-key-value-pairs.md)]

**_

[!INCLUDE [non-public-parameterless-constructors-not-used-for-deserialization](../../../includes/core-changes/serialization/5.0/non-public-parameterless-constructors-not-used-for-deserialization.md)]

_*_

[!INCLUDE [jsonserializer-serialize-throws-argumentnullexception-for-null-type](../../../includes/core-changes/serialization/5.0/jsonserializer-serialize-throws-argumentnullexception-for-null-type.md)]

_*_

[!INCLUDE [deserializing-json-into-char-requires-single-character](../../../includes/core-changes/serialization/5.0/deserializing-json-into-char-requires-single-character.md)]

_*_

[!INCLUDE [binaryformatter-deserialize-rewraps-exceptions](../../../includes/core-changes/serialization/5.0/binaryformatter-deserialize-rewraps-exceptions.md)]

_**
