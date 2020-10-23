---
title: MSBuild 中断性变更
description: 列出 MSBuild for .NET Core 中的中断性变更。
ms.date: 02/10/2020
ms.openlocfilehash: 9b0fba30c8955a6099bde0dc95b4df65a151d9e6
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92159478"
---
# <a name="msbuild-breaking-changes"></a><span data-ttu-id="c2833-103">MSBuild 中断性变更</span><span class="sxs-lookup"><span data-stu-id="c2833-103">MSBuild breaking changes</span></span>

<span data-ttu-id="c2833-104">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="c2833-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="c2833-105">重大更改</span><span class="sxs-lookup"><span data-stu-id="c2833-105">Breaking change</span></span> | <span data-ttu-id="c2833-106">引入的版本</span><span class="sxs-lookup"><span data-stu-id="c2833-106">Version introduced</span></span> |
| - | - |
| [<span data-ttu-id="c2833-107">TargetFramework 从 netcoreapp 更改为 net</span><span class="sxs-lookup"><span data-stu-id="c2833-107">TargetFramework change from netcoreapp to net</span></span>](#targetframework-change-from-netcoreapp-to-net) | <span data-ttu-id="c2833-108">5.0</span><span class="sxs-lookup"><span data-stu-id="c2833-108">5.0</span></span> |
| [<span data-ttu-id="c2833-109">面向 .NET 5 时，未定义 NETCOREAPP3_1 预处理器符号</span><span class="sxs-lookup"><span data-stu-id="c2833-109">NETCOREAPP3_1 preprocessor symbol is not defined when targeting .NET 5</span></span>](#netcoreapp3_1-preprocessor-symbol-is-not-defined-when-targeting-net-5) | <span data-ttu-id="c2833-110">5.0</span><span class="sxs-lookup"><span data-stu-id="c2833-110">5.0</span></span> |
| [<span data-ttu-id="c2833-111">PublishDepsFilePath 行为变更</span><span class="sxs-lookup"><span data-stu-id="c2833-111">PublishDepsFilePath behavior change</span></span>](#publishdepsfilepath-behavior-change) | <span data-ttu-id="c2833-112">5.0</span><span class="sxs-lookup"><span data-stu-id="c2833-112">5.0</span></span> |
| [<span data-ttu-id="c2833-113">默认导入 Directory.Packages.props 文件</span><span class="sxs-lookup"><span data-stu-id="c2833-113">Directory.Packages.props files is imported by default</span></span>](#directorypackagesprops-files-is-imported-by-default) | <span data-ttu-id="c2833-114">5.0</span><span class="sxs-lookup"><span data-stu-id="c2833-114">5.0</span></span> |
| [<span data-ttu-id="c2833-115">资源清单文件名更改</span><span class="sxs-lookup"><span data-stu-id="c2833-115">Resource manifest file name change</span></span>](#resource-manifest-file-name-change) | <span data-ttu-id="c2833-116">3.0</span><span class="sxs-lookup"><span data-stu-id="c2833-116">3.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="c2833-117">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="c2833-117">.NET 5.0</span></span>

[!INCLUDE [targetframework-name-change](../../../includes/core-changes/msbuild/5.0/targetframework-name-change.md)]

***

[!INCLUDE [netcoreapp3_1-preprocessor-symbol-not-defined](../../../includes/core-changes/msbuild/5.0/netcoreapp3_1-preprocessor-symbol-not-defined.md)]

***

[!INCLUDE [publishdepsfilepath-behavior-change](../../../includes/core-changes/msbuild/5.0/publishdepsfilepath-behavior-change.md)]

***

[!INCLUDE [directory-packages-props-imported-by-default](../../../includes/core-changes/msbuild/5.0/directory-packages-props-imported-by-default.md)]

***

## <a name="net-core-30"></a><span data-ttu-id="c2833-118">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="c2833-118">.NET Core 3.0</span></span>

[!INCLUDE[Resource file names](~/includes/core-changes/msbuild/3.0/resource-manifest-name.md)]

***
