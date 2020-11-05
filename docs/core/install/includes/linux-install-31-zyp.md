---
ms.openlocfilehash: 36f1ee26def82d426b6637ae96f382fc89791a2f
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93135757"
---

### <a name="install-the-sdk"></a><span data-ttu-id="ae0d6-101">安装 SDK</span><span class="sxs-lookup"><span data-stu-id="ae0d6-101">Install the SDK</span></span>

<span data-ttu-id="ae0d6-102">.NET Core SDK 使你可以通过 .NET Core 开发应用。</span><span class="sxs-lookup"><span data-stu-id="ae0d6-102">The .NET Core SDK allows you to develop apps with .NET Core.</span></span> <span data-ttu-id="ae0d6-103">若要安装 .NET Core SDK，请运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ae0d6-103">To install the .NET Core SDK, run the following commands.</span></span>

```bash
sudo zypper install dotnet-sdk-3.1
```

### <a name="install-the-runtime"></a><span data-ttu-id="ae0d6-104">安装运行时</span><span class="sxs-lookup"><span data-stu-id="ae0d6-104">Install the runtime</span></span>

<span data-ttu-id="ae0d6-105">.NET Core 运行时允许运行使用不随附运行时的 .NET Core 所开发的应用。</span><span class="sxs-lookup"><span data-stu-id="ae0d6-105">The .NET Core Runtime allows you to run apps that were made with .NET Core that didn't include the runtime.</span></span> <span data-ttu-id="ae0d6-106">以下命令安装 ASP.NET Core 运行时，这是与 .NET Core 最兼容的运行时。</span><span class="sxs-lookup"><span data-stu-id="ae0d6-106">The following commands install the ASP.NET Core Runtime, which is the most compatible runtime for .NET Core.</span></span> <span data-ttu-id="ae0d6-107">在终端中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ae0d6-107">In your terminal, run the following commands.</span></span>

```bash
sudo zypper install aspnetcore-runtime-3.1
```

<span data-ttu-id="ae0d6-108">作为 ASP.NET Core 运行时的一种替代方法，你可以安装不包含 ASP.NET Core 支持的 .NET Core 运行时：将上一命令中的 `aspnetcore-runtime-2.1` 替换为 `dotnet-runtime-3.1`。</span><span class="sxs-lookup"><span data-stu-id="ae0d6-108">As an alternative to the ASP.NET Core Runtime, you can install the .NET Core Runtime that doesn't include ASP.NET Core support: replace `aspnetcore-runtime-2.1` in the previous command with `dotnet-runtime-3.1`.</span></span>

```bash
sudo zypper install dotnet-runtime-3.1
```
