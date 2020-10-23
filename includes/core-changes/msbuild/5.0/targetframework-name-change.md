---
ms.openlocfilehash: 1ddc2cea19872b44ff9659bcebd76117587ea89a
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159479"
---
### <a name="targetframework-change-from-netcoreapp-to-net"></a>TargetFramework 从 netcoreapp 更改为 net

MSBuild `TargetFramework` 属性的值已从 `netcoreapp3.1` 更改为 `net5.0`。 这可能会破坏依赖于分析 `TargetFramework` 的值的代码。

#### <a name="version-introduced"></a>引入的版本

5.0

#### <a name="change-description"></a>更改描述

在 .NET Core 1.0 - 3.1 中，MSBuild `TargetFramework` 属性的值以 `netcoreapp` 开头（例如，对于面向 .NET Core 3.1 的应用，为 `netcoreapp3.1`）。 从 .NET 5.0 开始，此值简化为仅以 `net` 开头（例如，对于 .NET 5.0，为 `net5.0`）。

有关详细信息，请参阅 [.NET Standard 的未来](https://devblogs.microsoft.com/dotnet/the-future-of-net-standard/)和 [.NET 5 中的目标框架名称](https://github.com/dotnet/designs/blob/main/accepted/2020/net5/net5.md)。

#### <a name="reason-for-change"></a>更改原因

- 简化 `TargetFramework` 值。
- 使项目能够在 `TargetFramework` 属性中包含 `TargetPlatform`。

#### <a name="recommended-action"></a>建议的操作

如果你有用于分析 `TargetFramework` 的值的逻辑，则需要对其进行更新。 例如，以下 MSBuild 条件依赖于 `TargetFramework` 的值。

```xml
<PropertyGroup Condition="$(TargetFramework.StartsWith('netcoreapp'))">
```

为满足此要求，可更新代码，改为比较目标框架标识符。

```xml
<PropertyGroup Condition="'$([MSBuild]::GetTargetFrameworkIdentifier('$(TargetFramework)'))' == '.NETCoreApp'">
```

#### <a name="category"></a>类别

MSBuild

#### <a name="affected-apis"></a>受影响的 API

不可用

<!--

#### Affected APIs

Not detectable via API analysis.

-->
