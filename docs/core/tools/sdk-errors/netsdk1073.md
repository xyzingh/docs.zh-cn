---
title: NETSDK1073：未识别 FrameworkReference
description: 如何解决找不到 FrameworkReference 的问题。
author: marcpopMSFT
ms.topic: error-reference
ms.date: 10/9/2020
f1_keywords:
- NETSDK1073
ms.openlocfilehash: 59b5f63dcfe0115feabc2d87d24a09c6a650cc62
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91957083"
---
# <a name="netsdk1073-the-frameworkreference-was-not-recognized"></a><span data-ttu-id="7a7a2-103">NETSDK1073：未识别 FrameworkReference</span><span class="sxs-lookup"><span data-stu-id="7a7a2-103">NETSDK1073: The FrameworkReference was not recognized</span></span>

<span data-ttu-id="7a7a2-104">**本文适用于：** ✔️ .NET 2.1.100 SDK 及更高版本</span><span class="sxs-lookup"><span data-stu-id="7a7a2-104">**This article applies to:** ✔️ .NET 2.1.100 SDK and later versions</span></span>

<span data-ttu-id="7a7a2-105">此错误通常表示存在 SDK 无法找到的特定 FrameworkReference 的版本。</span><span class="sxs-lookup"><span data-stu-id="7a7a2-105">This error typically means there is a version of a particular FrameworkReference that the SDK cannot find.</span></span> <span data-ttu-id="7a7a2-106">尝试删除 obj 和 bin 文件夹，并运行 `dotnet restore` 以重新下载最新的目标包 。</span><span class="sxs-lookup"><span data-stu-id="7a7a2-106">Try deleting your *obj* and *bin* folders and running `dotnet restore` to redownload the latest targeting packs.</span></span>

<span data-ttu-id="7a7a2-107">或者，由于安装时可能存在问题，因此请确保使用最新版本的 .NET 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a7a2-107">Alternatively, there could be an issue with your install, so ensure you're on the latest versions of .NET and Visual Studio</span></span>
