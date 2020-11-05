---
ms.openlocfilehash: 56f5d27eb9be2f8eb3e335c5ec161dba1bcfdb1e
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93135599"
---

### <a name="install-the-sdk"></a>安装 SDK

.NET Core SDK 使你可以通过 .NET Core 开发应用。 如果安装 .NET Core SDK，则无需安装相应的运行时。 若要安装 .NET Core SDK，请运行以下命令：

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-3.1
```

> [!IMPORTANT]
> 如果收到类似于“找不到包 dotnet-sdk-3.1”的错误消息，请参阅 [APT 疑难解答](#apt-troubleshooting)部分。

### <a name="install-the-runtime"></a>安装运行时

.NET Core 运行时允许运行使用不随附运行时的 .NET Core 所开发的应用。 以下命令安装 ASP.NET Core 运行时，这是与 .NET Core 最兼容的运行时。 在终端中，运行以下命令。

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-3.1
```

> [!IMPORTANT]
> 如果收到类似于“找不到包 aspnetcore-runtime-3.1”的错误消息，请参阅 [APT 疑难解答](#apt-troubleshooting)部分。

作为 ASP.NET Core 运行时的一种替代方法，你可以安装不包含 ASP.NET Core 支持的 .NET Core 运行时：将上一命令中的 `aspnetcore-runtime-3.1` 替换为 `dotnet-runtime-3.1`。

```bash
sudo apt-get install -y dotnet-runtime-3.1
```
