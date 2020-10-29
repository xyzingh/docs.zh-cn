---
title: SYSLIB0011 警告
description: 了解有关生成编译时警告 SYSLIB0011 的过时信息。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 2b363e565ce1143c162679c6b74621885378d7ff
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333044"
---
# <a name="syslib0011-binaryformatter-serialization-is-obsolete"></a>SYSLIB0011：BinaryFormatter 序列化已过时

由于 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 存在[安全漏洞](../../standard/serialization/binaryformatter-security-guide.md#binaryformatter-security-vulnerabilities)，从 .NET 5.0 开始，以下 API 标记为已过时。 在代码中使用这些 API 会在编译时生成警告 `SYSLIB0011`。

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>

## <a name="workaround"></a>解决方法

请考虑使用 <xref:System.Text.Json.JsonSerializer> 或 <xref:System.Xml.Serialization.XmlSerializer>，而不是 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>。

若要详细了解建议的操作，请参阅[修复 BinaryFormatter 过时和禁用错误](https://aka.ms/binaryformatter)。

## <a name="see-also"></a>另请参阅

- [修复 BinaryFormatter 过时和禁用错误](https://aka.ms/binaryformatter)
- [BinaryFormatter 序列化方法已过时，并且已在 ASP.NET 应用中禁用](corefx.md#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps)
