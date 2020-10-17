---
ms.openlocfilehash: 0d6847b7a937094f36efae70ae450cc37824221d
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955547"
---
### <a name="assembly-related-api-behavior-changes-for-single-file-publishing-format"></a>适用于单文件发布格式的与程序集相关 API 行为更改

与程序集的文件位置相关的多个 API 在以单文件发布格式调用时行为发生更改。

#### <a name="change-description"></a>更改描述

在针对 .NET 5.0 及更高版本的单文件发布中，从内存中加载捆绑程序集，而不是提取到磁盘。 对于单文件发布的应用，这意味着某些与位置相关的 API 在 .NET 5.0 及更高版本上返回的值与在以前版本的 .NET 上返回的值不同。 更改如下：

| API | 以前的版本 | .NET 5.0 及更高版本 |
| - | - | - |
| <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> | 返回提取的 DLL 文件路径 | 为捆绑的程序集返回空字符串 |
| <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> | 返回提取的 DLL 文件路径 | 引发捆绑的程序集的异常 |
| <xref:System.Reflection.Assembly.GetFile(System.String)?displayProperty=nameWithType> | 为捆绑的程序集返回 `null` | 引发捆绑的程序集的异常 |
| `Environment.GetCommandLineArgs()[0]` | 值是入口点 DLL 的名称 | 值是主机可执行文件的名称 |
| <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType> | 值是临时提取目录 | 值是主机可执行文件的包含目录 |

#### <a name="version-introduced"></a>引入的版本

5.0

#### <a name="recommended-action"></a>建议操作

作为单个文件发布时，避免依赖程序集的文件位置。

#### <a name="category"></a>类别

- Core .NET 库

#### <a name="affected-apis"></a>受影响的 API

- <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.GetFile(System.String)?displayProperty=nameWithType>
- <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType>
- <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.Reflection.Assembly.Location`
- `P:System.Reflection.Assembly.CodeBase`
- `M:System.Reflection.Assembly.GetFile(System.String)`
- `M:System.Environment.GetCommandLineArgs`
- `P:System.AppContext.BaseDirectory`

-->
