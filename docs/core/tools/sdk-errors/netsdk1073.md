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
# <a name="netsdk1073-the-frameworkreference-was-not-recognized"></a>NETSDK1073：未识别 FrameworkReference

**本文适用于：** ✔️ .NET 2.1.100 SDK 及更高版本

此错误通常表示存在 SDK 无法找到的特定 FrameworkReference 的版本。 尝试删除 obj 和 bin 文件夹，并运行 `dotnet restore` 以重新下载最新的目标包 。

或者，由于安装时可能存在问题，因此请确保使用最新版本的 .NET 和 Visual Studio
