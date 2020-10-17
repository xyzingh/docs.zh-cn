---
title: dotnet nuget verify 命令
description: dotnet nuget verify 命令可验证已签名的包。
author: kartheekp-ms
ms.date: 10/08/2020
ms.openlocfilehash: 6cb368e2b6c203f3774b4450c0831c5d6b2dc0e8
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91957085"
---
# <a name="dotnet-nuget-verify"></a><span data-ttu-id="4d84f-103">dotnet nuget verify</span><span class="sxs-lookup"><span data-stu-id="4d84f-103">dotnet nuget verify</span></span>

<span data-ttu-id="4d84f-104">**本文适用于：** ✔️ .NET 5.0.100-rc.2.x SDK 及更高版本</span><span class="sxs-lookup"><span data-stu-id="4d84f-104">**This article applies to:** ✔️ .NET 5.0.100-rc.2.x SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="4d84f-105">名称</span><span class="sxs-lookup"><span data-stu-id="4d84f-105">Name</span></span>

<span data-ttu-id="4d84f-106">`dotnet nuget verify` -验证已签名的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4d84f-106">`dotnet nuget verify` - Verifies a signed NuGet package.</span></span>

## <a name="synopsis"></a><span data-ttu-id="4d84f-107">摘要</span><span class="sxs-lookup"><span data-stu-id="4d84f-107">Synopsis</span></span>

```dotnetcli
dotnet nuget verify [<package-path(s)>]
    [--all]
    [--certificate-fingerprint <FINGERPRINT>]
    [-v|--verbosity <LEVEL>]

dotnet nuget verify -h|--help
```

## <a name="description"></a><span data-ttu-id="4d84f-108">描述</span><span class="sxs-lookup"><span data-stu-id="4d84f-108">Description</span></span>

<span data-ttu-id="4d84f-109">`dotnet nuget verify` 命令验证已签名的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4d84f-109">The `dotnet nuget verify` command verifies a signed NuGet package.</span></span>

## <a name="arguments"></a><span data-ttu-id="4d84f-110">参数</span><span class="sxs-lookup"><span data-stu-id="4d84f-110">Arguments</span></span>

- **`package-path(s)`**

  <span data-ttu-id="4d84f-111">指定要验证的包的文件路径。</span><span class="sxs-lookup"><span data-stu-id="4d84f-111">Specifies the file path to the package(s) to be verified.</span></span> <span data-ttu-id="4d84f-112">可以传入多个位置参数以验证多个包。</span><span class="sxs-lookup"><span data-stu-id="4d84f-112">Multiple position arguments can be passed in to verify multiple packages.</span></span>

## <a name="options"></a><span data-ttu-id="4d84f-113">选项</span><span class="sxs-lookup"><span data-stu-id="4d84f-113">Options</span></span>

- **`--all`**

  <span data-ttu-id="4d84f-114">指定应对包执行的所有可能的验证。</span><span class="sxs-lookup"><span data-stu-id="4d84f-114">Specifies that all verifications possible should be performed on the package(s).</span></span> <span data-ttu-id="4d84f-115">默认情况下，只验证 `signatures`。</span><span class="sxs-lookup"><span data-stu-id="4d84f-115">By default, only `signatures` are verified.</span></span>

> [!NOTE]
> <span data-ttu-id="4d84f-116">此命令当前仅支持 `signature` 验证。</span><span class="sxs-lookup"><span data-stu-id="4d84f-116">This command currently supports only `signature` verification.</span></span>

- **`--certificate-fingerprint <FINGERPRINT>`**

  <span data-ttu-id="4d84f-117">验证签名者证书是否与指定的其中一个 `SHA256` 指纹匹配。</span><span class="sxs-lookup"><span data-stu-id="4d84f-117">Verify that the signer certificate matches with one of the specified `SHA256` fingerprints.</span></span> <span data-ttu-id="4d84f-118">可以多次提供此选项以提供多个指纹。</span><span class="sxs-lookup"><span data-stu-id="4d84f-118">This option can be supplied multiple times to provide multiple fingerprints.</span></span>

* **`-v|--verbosity <LEVEL>`**

  <span data-ttu-id="4d84f-119">设置 MSBuild 详细级别。</span><span class="sxs-lookup"><span data-stu-id="4d84f-119">Sets the MSBuild verbosity level.</span></span> <span data-ttu-id="4d84f-120">允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="4d84f-120">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="4d84f-121">默认值为 `normal`。</span><span class="sxs-lookup"><span data-stu-id="4d84f-121">The default is `normal`.</span></span>

* **`-h|--help`**

  <span data-ttu-id="4d84f-122">打印出有关命令的简短帮助。</span><span class="sxs-lookup"><span data-stu-id="4d84f-122">Prints out a short help for the command.</span></span>

## <a name="examples"></a><span data-ttu-id="4d84f-123">示例</span><span class="sxs-lookup"><span data-stu-id="4d84f-123">Examples</span></span>

- <span data-ttu-id="4d84f-124">验证 foo.nupkg：</span><span class="sxs-lookup"><span data-stu-id="4d84f-124">Verify *foo.nupkg*:</span></span>

  ```dotnetcli
  dotnet nuget verify foo.nupkg
  ```

- <span data-ttu-id="4d84f-125">验证多个 NuGet 包 - foo.nupkg 和指定目录中的所有 .nupkg 文件 ：</span><span class="sxs-lookup"><span data-stu-id="4d84f-125">Verify multiple NuGet packages - *foo.nupkg* and *all .nupkg files in the directory specified*:</span></span>

  ```dotnetcli
  dotnet nuget verify foo.nupkg c:\mydir\*.nupkg
  ```

- <span data-ttu-id="4d84f-126">验证 foo.nupkg 签名是否与指定的证书指纹匹配：</span><span class="sxs-lookup"><span data-stu-id="4d84f-126">Verify *foo.nupkg* signature matches with the specified certificate fingerprint:</span></span>

  ```dotnetcli
  dotnet nuget verify foo.nupkg --certificate-fingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039
  ```

- <span data-ttu-id="4d84f-127">验证 foo.nupkg 签名是否与指定的其中一个证书指纹匹配：</span><span class="sxs-lookup"><span data-stu-id="4d84f-127">Verify *foo.nupkg* signature matches with one of the specified certificate fingerprints:</span></span>

  ```dotnetcli
  dotnet nuget verify foo.nupkg --certificate-fingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 --certificate-fingerprint EC10992GG5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E027
  ```
