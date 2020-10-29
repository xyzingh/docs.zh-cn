---
title: SYSLIB0007 警告
description: 了解有关生成编译时警告 SYSLIB0007 的过时信息。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: d5410a3b3d33515e2ee6f578cad2f4deaec9c25d
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333052"
---
# <a name="syslib0007-default-implementations-of-cryptography-algorithms-not-supported"></a>SYSLIB0007：不支持加密算法的默认实现

.NET Framework 中的加密配置系统不允许适当的加密灵活性，且不存在于 .NET Core 和 .NET 5+ 中。 .NET 的后向兼容性要求也禁止框架更新某些加密 API 以跟上加密技术的发展。 因此从 .NET 5.0 开始，以下 API 标记为已过时。 使用这些 API 会在编译时生成警告 `SYSLIB0007`。

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HMAC.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=fullName>

## <a name="workaround"></a>解决方法

- 建议采取的操作是用对特定算法（例如 <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType>）的工厂方法的调用替换对现已过时的 API 的调用。 这样，便可以完全控制要实例化哪些算法。

- 如果需要保持与使用现已过时的 API 的 .NET Framework 应用生成的现有有效负载的兼容性，请使用下表中建议的替换项。 该表提供了从 .NET Framework 默认算法到其 .NET 5+ 等效项的映射。

  | .NET framework | .NET Core/.NET 5.0+ 兼容替换项 | 备注 |
  | - | - | - |
  | <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.RSA.Create?displayProperty=nameWithType> | |
  | <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.SHA1.Create?displayProperty=nameWithType> | SHA-1 算法被认为已无效。 如果可能，请考虑使用更强大的算法。 请咨询安全顾问以获取进一步的指导。 |
  | <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | 对于大多数新式应用程序，不建议使用 HMACSHA1 算法。 如果可能，请考虑使用更强大的算法。 请咨询安全顾问以获取进一步的指导。 |
  | <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | 对于大多数新式应用程序，不建议使用 HMACSHA1 算法。 如果可能，请考虑使用更强大的算法。 请咨询安全顾问以获取进一步的指导。 |
  | <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> |

## <a name="see-also"></a>另请参阅

- [加密中断性变更](cryptography.md#instantiating-default-implementations-of-cryptographic-abstractions-is-not-supported)
