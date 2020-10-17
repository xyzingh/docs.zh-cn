---
title: NETSDK1059：项目包含已过时的 .NET CLI 工具
description: 如何解决项目包含已过时的 .NET CLI 工具的问题。
author: sfoslund
ms.topic: error-reference
ms.date: 10/09/2020
f1_keywords:
- NETSDK1059
ms.openlocfilehash: 2960b9255dab9e61a84e49bc029666753d8c9a1e
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91957084"
---
# <a name="netsdk1059-project-contains-obsolete-net-cli-tool"></a>NETSDK1059：项目包含已过时的 .NET CLI 工具

**本文适用于：** ✔️ .NET 2.1.100 SDK 及更高版本

当 .NET SDK 发出警告 NETSDK1059 时，表示项目包含已过时的 .NET CLI 工具。 自 .NET 2.1 起，这些工具包含在 .NET SDK 中，无需由项目显式引用。 要详细了解如何迁移到 .NET 2.1，请参阅[此处](https://aka.ms/dotnetclitools-in-box)。
