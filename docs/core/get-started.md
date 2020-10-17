---
title: .NET 入门
description: 创建 Hello World .NET 应用。
author: adegeo
ms.author: adegeo
ms.date: 09/29/2020
ms.custom: vs-dotnet
ms.openlocfilehash: 6ad2b96e668c52ee80b707e31a63eac2433f3c9e
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756086"
---
# <a name="get-started-with-net"></a><span data-ttu-id="ccd4c-103">.NET 入门</span><span class="sxs-lookup"><span data-stu-id="ccd4c-103">Get started with .NET</span></span>

<span data-ttu-id="ccd4c-104">本文介绍如何创建和运行“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="ccd4c-104">This article teaches you how to create and run a "Hello World!"</span></span> <span data-ttu-id="ccd4c-105">.NET 应用。</span><span class="sxs-lookup"><span data-stu-id="ccd4c-105">.NET app.</span></span>

<span data-ttu-id="ccd4c-106">如果不确定什么是 .NET，请从 [.NET 简介](introduction.md)开始。</span><span class="sxs-lookup"><span data-stu-id="ccd4c-106">If you're unsure what .NET is, start with the [.NET introduction](introduction.md).</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ccd4c-107">创建应用程序</span><span class="sxs-lookup"><span data-stu-id="ccd4c-107">Create an application</span></span>

<span data-ttu-id="ccd4c-108">首先，在计算机上下载并安装 [.NET SDK](https://dotnet.microsoft.com/download/dotnet-core)。</span><span class="sxs-lookup"><span data-stu-id="ccd4c-108">First, download and install the [.NET SDK](https://dotnet.microsoft.com/download/dotnet-core) on your computer.</span></span>

<span data-ttu-id="ccd4c-109">然后，打开某一终端，如 PowerShell、命令提示符或 Bash  。</span><span class="sxs-lookup"><span data-stu-id="ccd4c-109">Next, open a terminal such as **PowerShell**, **Command Prompt**, or **bash**.</span></span> <span data-ttu-id="ccd4c-110">输入以下 `dotnet` 命令，创建并运行 C# 应用程序：</span><span class="sxs-lookup"><span data-stu-id="ccd4c-110">Enter the following `dotnet` commands to create and run a C# application:</span></span>

```dotnetcli
dotnet new console --output sample1
dotnet run --project sample1
```

<span data-ttu-id="ccd4c-111">可以看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="ccd4c-111">You see the following output:</span></span>

```output
Hello World!
```

<span data-ttu-id="ccd4c-112">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="ccd4c-112">Congratulations!</span></span> <span data-ttu-id="ccd4c-113">你现已创建了一个简单的 .NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccd4c-113">You've created a simple .NET application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd4c-114">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ccd4c-114">Next steps</span></span>

<span data-ttu-id="ccd4c-115">按照[分步教程](../standard/get-started.md)或观看 YouTube 上的 [.NET 101 视频](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oWoazjhXQzBKMrFuArxpW80)，开始开发 .NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccd4c-115">Get started developing .NET applications by following a [step-by-step tutorial](../standard/get-started.md) or by watching [.NET 101 videos](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oWoazjhXQzBKMrFuArxpW80) on YouTube.</span></span>
