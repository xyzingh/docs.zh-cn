---
title: NETSDK1005 和 NETSDK1047：资产文件缺少目标
description: 如何解决资产文件缺少目标的问题。
author: sfoslund
ms.topic: error-reference
ms.date: 10/09/2020
f1_keywords:
- NETSDK1005
- NETSDK1047
ms.openlocfilehash: 6c22fd8c79c2ac6e024b46b4f67e08011d42efc6
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91957086"
---
# <a name="netsdk1005-and-netsdk1047-asset-file-is-missing-target"></a>NETSDK1005 和 NETSDK1047：资产文件缺少目标

**本文适用于：** ✔️ .NET 2.1.100 SDK 及更高版本

当 .NET SDK 发出错误 NETSDK1005 或 NETSDK1047 时，项目的资产文件缺失某个目标框架的相关信息。 通常，确保还原正常运行并将缺失的目标值包含在项目的 `TargetFrameworks` 属性中即可解决此问题。

> [!NOTE]
> Visual Studio 16.8 预览版与 .NET 5 预览版 8 的早期版本一起使用时存在一个已知问题，会导致此错误。 具体来讲，如果缺失目标 `net5.0-windows7.0` 或 `net5.0`，请确保 Visual Studio 和 .NET 5 SDK 已更新到最新版本。
