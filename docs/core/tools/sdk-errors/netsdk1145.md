---
title: NETSDK1145：缺少目标包或 apphost 包
description: 如何在不支持 NuGet 包还原的情况下解决缺少目标包的问题
author: wli3
ms.topic: error-reference
ms.date: 09/14/2020
f1_keywords:
- NETSDK1145
ms.openlocfilehash: c343952582cafb63eae388fd216769e6c67d4741
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91805305"
---
# <a name="netsdk1145-targeting-or-apphost-pack-missing"></a><span data-ttu-id="3be94-103">NETSDK1145：缺少目标包或 apphost 包</span><span class="sxs-lookup"><span data-stu-id="3be94-103">NETSDK1145: Targeting or apphost pack missing</span></span>

<span data-ttu-id="3be94-104">**本文适用于：** ✔️ .NET 5.0.100 SDK 及更高版本</span><span class="sxs-lookup"><span data-stu-id="3be94-104">**This article applies to:** ✔️ .NET 5.0.100 SDK and later versions</span></span>

<span data-ttu-id="3be94-105">当 .NET SDK 出现错误 NETSDK1145 时，将不会安装目标包或 apphost 包，也不支持 NuGet 包还原。</span><span class="sxs-lookup"><span data-stu-id="3be94-105">When the .NET SDK issues error NETSDK1145, the targeting or apphost pack is not installed and NuGet package restore is not supported.</span></span> <span data-ttu-id="3be94-106">这通常是因为 SDK 比 Visual Studio for C++/CLI 项目中包含的 SDK 更新。</span><span class="sxs-lookup"><span data-stu-id="3be94-106">This is typically caused by having a newer SDK than the one included in Visual Studio for C++/CLI projects.</span></span> <span data-ttu-id="3be94-107">升级 Visual Studio，删除 global.json（如果它指定了某个 SDK 版本），并卸载较新的 SDK。</span><span class="sxs-lookup"><span data-stu-id="3be94-107">Upgrade Visual Studio, remove _global.json_ if it specifies a certain SDK version, and uninstall the newer SDK.</span></span> <span data-ttu-id="3be94-108">或者，可以替代目标或 apphost 版本。</span><span class="sxs-lookup"><span data-stu-id="3be94-108">Alternatively, you could override the targeting or apphost version.</span></span> <span data-ttu-id="3be94-109">从错误消息中查找包目录下存在的版本，并匹配项目的目标框架。</span><span class="sxs-lookup"><span data-stu-id="3be94-109">Find the version that exists under the pack directory from the error message and matches the target framework of the project.</span></span> <span data-ttu-id="3be94-110">将以下内容添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="3be94-110">Add the following to the project:</span></span>

<span data-ttu-id="3be94-111">对于 apphost 包</span><span class="sxs-lookup"><span data-stu-id="3be94-111">For apphost pack</span></span>

```xml
<ItemGroup>
  <KnownAppHostPack Update="@(KnownAppHostPack)">
    <AppHostPackVersion Condition="'%(TargetFramework)' == 'TARGETFRAMEWORK'">EXISTINGVERSION</AppHostPackVersion>
  </KnownAppHostPack>
</ItemGroup>
```

<span data-ttu-id="3be94-112">对于目标包</span><span class="sxs-lookup"><span data-stu-id="3be94-112">For targeting pack</span></span>

```xml
<ItemGroup>
  <KnownAppHostPack Update="@(KnownAppHostPack)">
    <AppHostPackVersion Condition="'%(TargetFramework)' == 'TARGETFRAMEWORK'">EXISTINGVERSION</AppHostPackVersion>
  </KnownAppHostPack>
</ItemGroup>
```
