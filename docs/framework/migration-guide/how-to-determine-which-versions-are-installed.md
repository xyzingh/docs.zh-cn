---
title: 确定已安装的 .NET Framework 版本
description: 使用代码、regedit.exe 或 PowerShell，通过查询 Windows 注册表来检测在计算机上安装了哪些版本的 .NET Framework。
ms.date: 02/03/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining version
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
ms.openlocfilehash: faeb2c14b9c1d93b558c67a42c223702178407c0
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955585"
---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a><span data-ttu-id="5d86e-103">如何：确定已安装的 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-103">How to: Determine which .NET Framework versions are installed</span></span>

<span data-ttu-id="5d86e-104">用户可在他们的计算机上[安装](../install/index.md)和运行 .NET Framework 的多个版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-104">Users can [install](../install/index.md) and run multiple versions of .NET Framework on their computers.</span></span> <span data-ttu-id="5d86e-105">当你开发或部署应用时，你可能需要知道用户的计算机上安装了哪些 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-105">When you develop or deploy your app, you might need to know which .NET Framework versions are installed on the user's computer.</span></span> <span data-ttu-id="5d86e-106">注册表包含计算机上安装的 .NET Framework 版本列表。</span><span class="sxs-lookup"><span data-stu-id="5d86e-106">The registry contains a list of the versions of .NET Framework installed on the computer.</span></span>

<span data-ttu-id="5d86e-107">.NET Framework 由两个采用不同版本的主要组件构成：</span><span class="sxs-lookup"><span data-stu-id="5d86e-107">.NET Framework consists of two main components, which are versioned separately:</span></span>

- <span data-ttu-id="5d86e-108">一组程序集，它们是为应用提供功能的类型与资源的集合。</span><span class="sxs-lookup"><span data-stu-id="5d86e-108">A set of assemblies, which are collections of types and resources that provide the functionality for your apps.</span></span> <span data-ttu-id="5d86e-109">.NET Framework 和程序集使用相同的版本号。</span><span class="sxs-lookup"><span data-stu-id="5d86e-109">.NET Framework and the assemblies share the same version number.</span></span> <span data-ttu-id="5d86e-110">例如，.NET Framework 版本包括 4.5、4.6.1 和 4.7.2。</span><span class="sxs-lookup"><span data-stu-id="5d86e-110">For example, .NET Framework versions include 4.5, 4.6.1, and 4.7.2.</span></span>

- <span data-ttu-id="5d86e-111">公共语言运行时 (CLR)，可管理并执行应用代码。</span><span class="sxs-lookup"><span data-stu-id="5d86e-111">The common language runtime (CLR), which manages and executes your app's code.</span></span> <span data-ttu-id="5d86e-112">单个 CLR 版本通常可支持多个 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-112">A single CLR version typically supports multiple .NET Framework versions.</span></span> <span data-ttu-id="5d86e-113">例如，CLR 版本4.0.30319.xxxxx（其中 xxxxx 小于42000）支持 .NET Framework 版本 4 到 4.5.2。 </span><span class="sxs-lookup"><span data-stu-id="5d86e-113">For example, CLR version 4.0.30319.*xxxxx* where *xxxxx* is less than 42000, supports .NET Framework versions 4 through 4.5.2.</span></span> <span data-ttu-id="5d86e-114">大于或等于4.0.30319.42000 的 CLR 版本支持从 .NET Framework 4.6 开始的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-114">CLR version greater than or equal to 4.0.30319.42000 supports .NET Framework versions starting with .NET Framework 4.6.</span></span>

<span data-ttu-id="5d86e-115">可使用社区维护的工具帮助检测安装了哪些 .NET Framework 版本：</span><span class="sxs-lookup"><span data-stu-id="5d86e-115">Community-maintained tools are available to help detect which .NET Framework versions are installed:</span></span>

- [https://github.com/jmalarcon/DotNetVersions](https://github.com/jmalarcon/DotNetVersions)

  <span data-ttu-id="5d86e-116">.NET 2.0 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="5d86e-116">A .NET 2.0 command-line tool.</span></span>

- [https://github.com/EliteLoser/DotNetVersionLister](https://github.com/EliteLoser/DotNetVersionLister)

  <span data-ttu-id="5d86e-117">PowerShell 2.0 模块。</span><span class="sxs-lookup"><span data-stu-id="5d86e-117">A PowerShell 2.0 module.</span></span>

<span data-ttu-id="5d86e-118">要了解如何检测已安装的每个 .NET Framework 版本的更新，请参阅[操作说明：确定已安装的 .NET Framework 更新](how-to-determine-which-net-framework-updates-are-installed.md)。</span><span class="sxs-lookup"><span data-stu-id="5d86e-118">For information about detecting the installed updates for each version of .NET Framework, see [How to: Determine which .NET Framework updates are installed](how-to-determine-which-net-framework-updates-are-installed.md).</span></span>

## <a name="detect-net-framework-45-and-later-versions"></a><span data-ttu-id="5d86e-119">检测 .NET Framework 4.5 及更高版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-119">Detect .NET Framework 4.5 and later versions</span></span>

<span data-ttu-id="5d86e-120">计算机上安装的 .NET Framework 版本（4.5 及更高版本）列出在注册表中，位于 HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full。</span><span class="sxs-lookup"><span data-stu-id="5d86e-120">The version of .NET Framework (4.5 and later) installed on a machine is listed in the registry at **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span> <span data-ttu-id="5d86e-121">如果缺少 Full 子项，则未安装 .NET Framework 4.5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-121">If the **Full** subkey is missing, then .NET Framework 4.5 or above isn't installed.</span></span>

> [!NOTE]
> <span data-ttu-id="5d86e-122">注册表路径中的 .NET Framework Setup 子项不以句点开头。</span><span class="sxs-lookup"><span data-stu-id="5d86e-122">The **NET Framework Setup** subkey in the registry path does *not* begin with a period.</span></span>

<span data-ttu-id="5d86e-123">注册表中的 **Release** REG_DWORD 值代表已安装的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-123">The **Release** REG_DWORD value in the registry represents the version of .NET Framework installed.</span></span>

<a name="version_table"></a>

| <span data-ttu-id="5d86e-124">.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-124">.NET Framework version</span></span> | <span data-ttu-id="5d86e-125">Release 的值</span><span class="sxs-lookup"><span data-stu-id="5d86e-125">Value of **Release**</span></span> |
| ---------------------- | -------------------------- |
| <span data-ttu-id="5d86e-126">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="5d86e-126">.NET Framework 4.5</span></span>     | <span data-ttu-id="5d86e-127">所有 Windows 操作系统：378389</span><span class="sxs-lookup"><span data-stu-id="5d86e-127">All Windows operating systems: 378389</span></span> |
| <span data-ttu-id="5d86e-128">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-128">.NET Framework 4.5.1</span></span>   | <span data-ttu-id="5d86e-129">在 Windows 8.1 和 Windows Server 2012 R2 上：378675</span><span class="sxs-lookup"><span data-stu-id="5d86e-129">On Windows 8.1 and Windows Server 2012 R2: 378675</span></span><br /><span data-ttu-id="5d86e-130">在所有其他 Windows 操作系统上：378758</span><span class="sxs-lookup"><span data-stu-id="5d86e-130">On all other Windows operating systems: 378758</span></span> |
| <span data-ttu-id="5d86e-131">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="5d86e-131">.NET Framework 4.5.2</span></span>   | <span data-ttu-id="5d86e-132">所有 Windows 操作系统：379893</span><span class="sxs-lookup"><span data-stu-id="5d86e-132">All Windows operating systems: 379893</span></span> |
| <span data-ttu-id="5d86e-133">.NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="5d86e-133">.NET Framework 4.6</span></span>     | <span data-ttu-id="5d86e-134">在 Windows 10 上：393295</span><span class="sxs-lookup"><span data-stu-id="5d86e-134">On Windows 10: 393295</span></span><br /><span data-ttu-id="5d86e-135">在所有其他 Windows 操作系统上：393297</span><span class="sxs-lookup"><span data-stu-id="5d86e-135">On all other Windows operating systems: 393297</span></span> |
| <span data-ttu-id="5d86e-136">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-136">.NET Framework 4.6.1</span></span>   | <span data-ttu-id="5d86e-137">在 Windows 10 11 月更新系统上：394254</span><span class="sxs-lookup"><span data-stu-id="5d86e-137">On Windows 10 November Update systems: 394254</span></span><br /><span data-ttu-id="5d86e-138">在所有其他 Windows 操作系统（包括 Windows 10）上：394271</span><span class="sxs-lookup"><span data-stu-id="5d86e-138">On all other Windows operating systems (including Windows 10): 394271</span></span> |
| <span data-ttu-id="5d86e-139">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="5d86e-139">.NET Framework 4.6.2</span></span>   | <span data-ttu-id="5d86e-140">在 Windows 10 周年更新和 Windows Server 2016 上：394802</span><span class="sxs-lookup"><span data-stu-id="5d86e-140">On Windows 10 Anniversary Update and Windows Server 2016: 394802</span></span><br /><span data-ttu-id="5d86e-141">在所有其他 Windows 操作系统（包括其他 Windows 10 操作系统）上：394806</span><span class="sxs-lookup"><span data-stu-id="5d86e-141">On all other Windows operating systems (including other Windows 10 operating systems): 394806</span></span> |
| <span data-ttu-id="5d86e-142">.NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="5d86e-142">.NET Framework 4.7</span></span>     | <span data-ttu-id="5d86e-143">在 Windows 10 创意者更新上：460798</span><span class="sxs-lookup"><span data-stu-id="5d86e-143">On Windows 10 Creators Update: 460798</span></span><br /><span data-ttu-id="5d86e-144">在所有其他 Windows 操作系统（包括其他 Windows 10 操作系统）上：460805</span><span class="sxs-lookup"><span data-stu-id="5d86e-144">On all other Windows operating systems (including other Windows 10 operating systems): 460805</span></span> |
| <span data-ttu-id="5d86e-145">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-145">.NET Framework 4.7.1</span></span>   | <span data-ttu-id="5d86e-146">在 Windows 10 Fall Creators Update 和 Windows Server 版本 1709 上：461308</span><span class="sxs-lookup"><span data-stu-id="5d86e-146">On Windows 10 Fall Creators Update and Windows Server, version 1709: 461308</span></span><br/><span data-ttu-id="5d86e-147">在所有其他 Windows 操作系统（包括其他 Windows 10 操作系统）上：461310</span><span class="sxs-lookup"><span data-stu-id="5d86e-147">On all other Windows operating systems (including other Windows 10 operating systems): 461310</span></span> |
| <span data-ttu-id="5d86e-148">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="5d86e-148">.NET Framework 4.7.2</span></span>   | <span data-ttu-id="5d86e-149">在 Windows 10 2018 年 4 月更新和 Windows Server 版本 1803 上：461808</span><span class="sxs-lookup"><span data-stu-id="5d86e-149">On Windows 10 April 2018 Update and Windows Server, version 1803: 461808</span></span><br/><span data-ttu-id="5d86e-150">在除 Windows 10 2018 年 4 月更新和 Windows Server 版本 1803 之外的所有 Windows 操作系统上：461814</span><span class="sxs-lookup"><span data-stu-id="5d86e-150">On all Windows operating systems other than Windows 10 April 2018 Update and Windows Server, version 1803: 461814</span></span> |
| <span data-ttu-id="5d86e-151">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="5d86e-151">.NET Framework 4.8</span></span>     | <span data-ttu-id="5d86e-152">在 Windows 10 2019 年 5 月更新和 Windows 10 2019 年 11 月更新上：528040</span><span class="sxs-lookup"><span data-stu-id="5d86e-152">On Windows 10 May 2019 Update and Windows 10 November 2019 Update: 528040</span></span><br/><span data-ttu-id="5d86e-153">在 Windows 10 2020 年 5 月更新上：528372</span><span class="sxs-lookup"><span data-stu-id="5d86e-153">On Windows 10 May 2020 Update: 528372</span></span><br/><span data-ttu-id="5d86e-154">在所有其他 Windows 操作系统（包括其他 Windows 10 操作系统）上：528049</span><span class="sxs-lookup"><span data-stu-id="5d86e-154">On all other Windows operating systems (including other Windows 10 operating systems): 528049</span></span> |

### <a name="minimum-version"></a><span data-ttu-id="5d86e-155">最低版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-155">Minimum version</span></span>

<span data-ttu-id="5d86e-156">若要确定是否安装了最低版本的 .NET Framework，请使用上表中最小的 Release REG_DWORD 值来指示该版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-156">To determine whether a *minimum* version of .NET Framework is present, use the smallest **Release** REG_DWORD value for that version from the previous table.</span></span>

<span data-ttu-id="5d86e-157">例如，如果应用程序在 .NET Framework 4.8 或更高版本下运行，请测试 Release REG_DWORD 值是否大于或等于 528040。</span><span class="sxs-lookup"><span data-stu-id="5d86e-157">For example, if your application runs under .NET Framework 4.8 or a later version, test for a **Release** REG_DWORD value that is *greater than or equal to* 528040.</span></span>

| <span data-ttu-id="5d86e-158">.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-158">.NET Framework version</span></span> | <span data-ttu-id="5d86e-159">最小值</span><span class="sxs-lookup"><span data-stu-id="5d86e-159">Minimum value</span></span> |
| ---------------------- | ------------- |
| <span data-ttu-id="5d86e-160">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="5d86e-160">.NET Framework 4.5</span></span>     | <span data-ttu-id="5d86e-161">378389</span><span class="sxs-lookup"><span data-stu-id="5d86e-161">378389</span></span> |
| <span data-ttu-id="5d86e-162">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-162">.NET Framework 4.5.1</span></span>   | <span data-ttu-id="5d86e-163">378675</span><span class="sxs-lookup"><span data-stu-id="5d86e-163">378675</span></span> |
| <span data-ttu-id="5d86e-164">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="5d86e-164">.NET Framework 4.5.2</span></span>   | <span data-ttu-id="5d86e-165">379893</span><span class="sxs-lookup"><span data-stu-id="5d86e-165">379893</span></span> |
| <span data-ttu-id="5d86e-166">.NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="5d86e-166">.NET Framework 4.6</span></span>     | <span data-ttu-id="5d86e-167">393295</span><span class="sxs-lookup"><span data-stu-id="5d86e-167">393295</span></span> |
| <span data-ttu-id="5d86e-168">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-168">.NET Framework 4.6.1</span></span>   | <span data-ttu-id="5d86e-169">394254</span><span class="sxs-lookup"><span data-stu-id="5d86e-169">394254</span></span> |
| <span data-ttu-id="5d86e-170">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="5d86e-170">.NET Framework 4.6.2</span></span>   | <span data-ttu-id="5d86e-171">394802</span><span class="sxs-lookup"><span data-stu-id="5d86e-171">394802</span></span> |
| <span data-ttu-id="5d86e-172">.NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="5d86e-172">.NET Framework 4.7</span></span>     | <span data-ttu-id="5d86e-173">460798</span><span class="sxs-lookup"><span data-stu-id="5d86e-173">460798</span></span> |
| <span data-ttu-id="5d86e-174">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-174">.NET Framework 4.7.1</span></span>   | <span data-ttu-id="5d86e-175">461308</span><span class="sxs-lookup"><span data-stu-id="5d86e-175">461308</span></span> |
| <span data-ttu-id="5d86e-176">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="5d86e-176">.NET Framework 4.7.2</span></span>   | <span data-ttu-id="5d86e-177">461808</span><span class="sxs-lookup"><span data-stu-id="5d86e-177">461808</span></span> |
| <span data-ttu-id="5d86e-178">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="5d86e-178">.NET Framework 4.8</span></span>     | <span data-ttu-id="5d86e-179">528040</span><span class="sxs-lookup"><span data-stu-id="5d86e-179">528040</span></span> |

### <a name="use-registry-editor"></a><span data-ttu-id="5d86e-180">使用注册表编辑器</span><span class="sxs-lookup"><span data-stu-id="5d86e-180">Use Registry Editor</span></span>

01. <span data-ttu-id="5d86e-181">在“开始”菜单中，选择“运行”，输入“regedit”，然后选择“确定” 。</span><span class="sxs-lookup"><span data-stu-id="5d86e-181">From the **Start** menu, choose **Run**, enter *regedit*, and then select **OK**.</span></span>

   <span data-ttu-id="5d86e-182">（必须具有管理凭据才能运行 regedit。）</span><span class="sxs-lookup"><span data-stu-id="5d86e-182">(You must have administrative credentials to run regedit.)</span></span>

01. <span data-ttu-id="5d86e-183">在注册表编辑器中，打开以下子项：HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full。</span><span class="sxs-lookup"><span data-stu-id="5d86e-183">In the Registry Editor, open the following subkey: **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span> <span data-ttu-id="5d86e-184">如果“Full”子项不存在，则表示尚未安装 .NET Framework 4.5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-184">If the **Full** subkey isn't present, then you don't have .NET Framework 4.5 or later installed.</span></span>

01. <span data-ttu-id="5d86e-185">请检查名为“Release”的 REG_DWORD 条目。</span><span class="sxs-lookup"><span data-stu-id="5d86e-185">Check for a REG_DWORD entry named **Release**.</span></span> <span data-ttu-id="5d86e-186">如果存在，则已安装 .NET Framework 4.5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-186">If it exists, then you have .NET Framework 4.5 or later installed.</span></span> <span data-ttu-id="5d86e-187">其值对应于 .NET Framework 的特定版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-187">Its value corresponds to a particular version of .NET Framework.</span></span> <span data-ttu-id="5d86e-188">以下图为例，“Release”条目的值为 528040，这是 .NET Framework 4.8 的版本密钥。</span><span class="sxs-lookup"><span data-stu-id="5d86e-188">In the following figure, for example, the value of the **Release** entry is 528040, which is the release key for .NET Framework 4.8.</span></span>

   ![.NET Framework 4.5 的注册表项](./media/clr-installdir.png )

### <a name="use-powershell-to-check-for-a-minimum-version"></a><span data-ttu-id="5d86e-190">使用 PowerShell 检查最低版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-190">Use PowerShell to check for a minimum version</span></span>

<span data-ttu-id="5d86e-191">使用 PowerShell 命令检查 HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full 子项“Release”条目的值\\。</span><span class="sxs-lookup"><span data-stu-id="5d86e-191">Use PowerShell commands to check the value of the **Release** entry of the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** subkey.</span></span>

<span data-ttu-id="5d86e-192">以下示例检查“Release”条目的值，以确定是否已安装 .NET Framework 4.6.2 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-192">The following examples check the value of the **Release** entry to determine whether .NET Framework 4.6.2 or later is installed.</span></span> <span data-ttu-id="5d86e-193">如果安装了此代码，则返回 `True`，否则返回 `False`。</span><span class="sxs-lookup"><span data-stu-id="5d86e-193">This code returns `True` if it's installed and `False` otherwise.</span></span>

```powershell
(Get-ItemProperty "HKLM:SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
```

### <a name="query-the-registry-using-code"></a><span data-ttu-id="5d86e-194">使用代码查询注册表</span><span class="sxs-lookup"><span data-stu-id="5d86e-194">Query the registry using code</span></span>

01. <span data-ttu-id="5d86e-195">使用 <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> 和 <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> 方法访问 Windows 注册表中的 HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full 子项。</span><span class="sxs-lookup"><span data-stu-id="5d86e-195">Use the <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> and <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> methods to access the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** subkey in the Windows registry.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5d86e-196">如果运行的应用是 32 位且在 64 位 Windows 中运行，则注册表路径与前面列出的不同。</span><span class="sxs-lookup"><span data-stu-id="5d86e-196">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="5d86e-197">可在 HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\ 子项中找到 64 位注册表。</span><span class="sxs-lookup"><span data-stu-id="5d86e-197">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="5d86e-198">例如，.NET Framework 4.5 的注册表子项为 HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full。</span><span class="sxs-lookup"><span data-stu-id="5d86e-198">For example, the registry subkey for .NET Framework 4.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span>

01. <span data-ttu-id="5d86e-199">检查 Release REG_DWORD 值以确定已安装的版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-199">Check the **Release** REG_DWORD value to determine the installed version.</span></span> <span data-ttu-id="5d86e-200">为了向前兼容，可检查是否有一个值大于或等于 [.NET Framework 版本表](#version_table)中所列的值。</span><span class="sxs-lookup"><span data-stu-id="5d86e-200">To be forward-compatible, check for a value greater than or equal to the value listed in the [.NET Framework version table](#version_table).</span></span>

<span data-ttu-id="5d86e-201">以下示例检查注册表中“Release”条目的值，以查找已安装的 .NET Framework 4.5-4.8：</span><span class="sxs-lookup"><span data-stu-id="5d86e-201">The following example checks the value of the **Release** entry in the registry to find the versions of .NET Framework 4.5-4.8 that are installed:</span></span>

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="2":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="2":::

<span data-ttu-id="5d86e-202">此示例显示类似以下内容的输出：</span><span class="sxs-lookup"><span data-stu-id="5d86e-202">The example displays output like the following:</span></span>

```output
.NET Framework Version: 4.6.1
```

<span data-ttu-id="5d86e-203">此示例遵循版本检查的建议做法：</span><span class="sxs-lookup"><span data-stu-id="5d86e-203">This example follows the recommended practice for version checking:</span></span>

- <span data-ttu-id="5d86e-204">检查“Release”条目的值是否大于或等于已知版本密钥的值。</span><span class="sxs-lookup"><span data-stu-id="5d86e-204">It checks whether the value of the **Release** entry is *greater than or equal to* the value of the known release keys.</span></span>
- <span data-ttu-id="5d86e-205">按从最新版本到最早版本的顺序检查。</span><span class="sxs-lookup"><span data-stu-id="5d86e-205">It checks in order from most recent version to earliest version.</span></span>

## <a name="detect-net-framework-10-through-40"></a><span data-ttu-id="5d86e-206">检测 .NET Framework 1.0 到 4.0</span><span class="sxs-lookup"><span data-stu-id="5d86e-206">Detect .NET Framework 1.0 through 4.0</span></span>

<span data-ttu-id="5d86e-207">.NET Framework 1.1 到 4.0 的每个版本都作为子项列出在 HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP。</span><span class="sxs-lookup"><span data-stu-id="5d86e-207">Each version of .NET Framework from 1.1 to 4.0 is listed as a subkey at **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP**.</span></span> <span data-ttu-id="5d86e-208">下表列出了每个 .NET Framework 版本的路径。</span><span class="sxs-lookup"><span data-stu-id="5d86e-208">The following table lists the path to each .NET Framework version.</span></span> <span data-ttu-id="5d86e-209">对于大多数版本，都有 Install REG_DWORD 值 `1`，指示已安装此版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-209">For most versions, there's an **Install** REG_DWORD value of `1` to indicate this version is installed.</span></span> <span data-ttu-id="5d86e-210">在这些子项中，还有一个包含版本字符串的 Version REG_SZ 值。</span><span class="sxs-lookup"><span data-stu-id="5d86e-210">In these subkeys, there's also a **Version** REG_SZ value that contains a version string.</span></span>

> [!NOTE]
> <span data-ttu-id="5d86e-211">注册表路径中的 .NET Framework Setup 子项不以句点开头。</span><span class="sxs-lookup"><span data-stu-id="5d86e-211">The **NET Framework Setup** subkey in the registry path does *not* begin with a period.</span></span>

| <span data-ttu-id="5d86e-212">Framework 版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-212">Framework Version</span></span>  | <span data-ttu-id="5d86e-213">注册表子项</span><span class="sxs-lookup"><span data-stu-id="5d86e-213">Registry Subkey</span></span> | <span data-ttu-id="5d86e-214">“值”</span><span class="sxs-lookup"><span data-stu-id="5d86e-214">Value</span></span> |
| ------------------ | --------------- | ----- |
| <span data-ttu-id="5d86e-215">1.0</span><span class="sxs-lookup"><span data-stu-id="5d86e-215">1.0</span></span>                | <span data-ttu-id="5d86e-216">**HKLM\\Software\\Microsoft\\.NETFramework\\Policy\\v1.0\\3705**</span><span class="sxs-lookup"><span data-stu-id="5d86e-216">**HKLM\\Software\\Microsoft\\.NETFramework\\Policy\\v1.0\\3705**</span></span>     | <span data-ttu-id="5d86e-217">**Install** REG_SZ 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-217">**Install** REG_SZ equals `1`</span></span> |
| <span data-ttu-id="5d86e-218">1.1</span><span class="sxs-lookup"><span data-stu-id="5d86e-218">1.1</span></span>                | <span data-ttu-id="5d86e-219">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v1.1.4322**</span><span class="sxs-lookup"><span data-stu-id="5d86e-219">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v1.1.4322**</span></span>   | <span data-ttu-id="5d86e-220">**Install** REG_DWORD 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-220">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="5d86e-221">2.0</span><span class="sxs-lookup"><span data-stu-id="5d86e-221">2.0</span></span>                | <span data-ttu-id="5d86e-222">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v2.0.50727**</span><span class="sxs-lookup"><span data-stu-id="5d86e-222">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v2.0.50727**</span></span>  | <span data-ttu-id="5d86e-223">**Install** REG_DWORD 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-223">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="5d86e-224">3.0</span><span class="sxs-lookup"><span data-stu-id="5d86e-224">3.0</span></span>                | <span data-ttu-id="5d86e-225">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.0\\Setup**</span><span class="sxs-lookup"><span data-stu-id="5d86e-225">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.0\\Setup**</span></span> | <span data-ttu-id="5d86e-226">**InstallSuccess** REG_DWORD 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-226">**InstallSuccess** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="5d86e-227">3.5</span><span class="sxs-lookup"><span data-stu-id="5d86e-227">3.5</span></span>                | <span data-ttu-id="5d86e-228">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.5**</span><span class="sxs-lookup"><span data-stu-id="5d86e-228">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.5**</span></span>        | <span data-ttu-id="5d86e-229">**Install** REG_DWORD 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-229">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="5d86e-230">4.0 客户端配置文件</span><span class="sxs-lookup"><span data-stu-id="5d86e-230">4.0 Client Profile</span></span> | <span data-ttu-id="5d86e-231">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Client**</span><span class="sxs-lookup"><span data-stu-id="5d86e-231">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Client**</span></span>  | <span data-ttu-id="5d86e-232">**Install** REG_DWORD 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-232">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="5d86e-233">4.0 完整配置文件</span><span class="sxs-lookup"><span data-stu-id="5d86e-233">4.0 Full Profile</span></span>   | <span data-ttu-id="5d86e-234">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**</span><span class="sxs-lookup"><span data-stu-id="5d86e-234">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**</span></span>    | <span data-ttu-id="5d86e-235">**Install** REG_DWORD 等于 `1`</span><span class="sxs-lookup"><span data-stu-id="5d86e-235">**Install** REG_DWORD equals `1`</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5d86e-236">如果运行的应用是 32 位且在 64 位 Windows 中运行，则注册表路径与前面列出的不同。</span><span class="sxs-lookup"><span data-stu-id="5d86e-236">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="5d86e-237">可在 HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\ 子项中找到 64 位注册表。</span><span class="sxs-lookup"><span data-stu-id="5d86e-237">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="5d86e-238">例如，.NET Framework 3.5 的注册表子项为 HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5。</span><span class="sxs-lookup"><span data-stu-id="5d86e-238">For example, the registry subkey for .NET Framework 3.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5**.</span></span>

<span data-ttu-id="5d86e-239">请注意，.NET Framework 1.0 子项的注册表路径与其他子项不同。</span><span class="sxs-lookup"><span data-stu-id="5d86e-239">Notice that the registry path to the .NET Framework 1.0 subkey is different from the others.</span></span>

### <a name="use-registry-editor-older-framework-versions"></a><span data-ttu-id="5d86e-240">使用注册表编辑器（较旧的框架版本）</span><span class="sxs-lookup"><span data-stu-id="5d86e-240">Use Registry Editor (older framework versions)</span></span>

01. <span data-ttu-id="5d86e-241">在“开始”菜单中，选择“运行”，输入“regedit”，然后选择“确定” 。</span><span class="sxs-lookup"><span data-stu-id="5d86e-241">From the **Start** menu, choose **Run**, enter *regedit*, and then select **OK**.</span></span>

    <span data-ttu-id="5d86e-242">必须具有管理凭据才能运行 regedit。</span><span class="sxs-lookup"><span data-stu-id="5d86e-242">You must have administrative credentials to run regedit.</span></span>

01. <span data-ttu-id="5d86e-243">打开与要检查的版本匹配的子项。</span><span class="sxs-lookup"><span data-stu-id="5d86e-243">Open the subkey that matches the version you want to check.</span></span> <span data-ttu-id="5d86e-244">使用[检测 .NET Framework 1.0 到 4.0](#detect-net-framework-10-through-40)部分列出的表。</span><span class="sxs-lookup"><span data-stu-id="5d86e-244">Use the table in the [Detect .NET Framework 1.0 through 4.0](#detect-net-framework-10-through-40) section.</span></span>

    <span data-ttu-id="5d86e-245">下图显示了 .NET Framework 3.5 的子项及其 Version 值。</span><span class="sxs-lookup"><span data-stu-id="5d86e-245">The following figure shows the subkey and its **Version** value for .NET Framework 3.5.</span></span>

    <span data-ttu-id="5d86e-246">![.NET Framework 3.5 的注册表项。](./media/net-4-and-earlier.png ".NET Framework 3.5 及早期版本")</span><span class="sxs-lookup"><span data-stu-id="5d86e-246">![The registry entry for .NET Framework 3.5.](./media/net-4-and-earlier.png ".NET Framework 3.5 and earlier versions")</span></span>

### <a name="query-the-registry-using-code-older-framework-versions"></a><span data-ttu-id="5d86e-247">使用代码查询注册表（较旧的框架版本）</span><span class="sxs-lookup"><span data-stu-id="5d86e-247">Query the registry using code (older framework versions)</span></span>

<span data-ttu-id="5d86e-248">使用 <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> 类访问 Windows 注册表中的 HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP 子项。</span><span class="sxs-lookup"><span data-stu-id="5d86e-248">Use the <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> class to access the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP** subkey in the Windows registry.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d86e-249">如果运行的应用是 32 位且在 64 位 Windows 中运行，则注册表路径与前面列出的不同。</span><span class="sxs-lookup"><span data-stu-id="5d86e-249">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="5d86e-250">可在 HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\ 子项中找到 64 位注册表。</span><span class="sxs-lookup"><span data-stu-id="5d86e-250">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="5d86e-251">例如，.NET Framework 3.5 的注册表子项为 HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5。</span><span class="sxs-lookup"><span data-stu-id="5d86e-251">For example, the registry subkey for .NET Framework 3.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5**.</span></span>

<span data-ttu-id="5d86e-252">以下示例查找已安装的 .NET Framework 1-4：</span><span class="sxs-lookup"><span data-stu-id="5d86e-252">The following example finds the versions of .NET Framework 1-4 that are installed:</span></span>

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="1":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="1":::

<span data-ttu-id="5d86e-253">该示例显示类似于以下内容的输出：</span><span class="sxs-lookup"><span data-stu-id="5d86e-253">The example displays output similar to the following:</span></span>

```output
v2.0.50727  2.0.50727.4927  SP2
v3.0  3.0.30729.4926  SP2
v3.5  3.5.30729.4926  SP1
v4.0
  Client  4.0.0.0
```

## <a name="find-clr-versions"></a><span data-ttu-id="5d86e-254">查找 CLR 版本</span><span class="sxs-lookup"><span data-stu-id="5d86e-254">Find CLR versions</span></span>

<span data-ttu-id="5d86e-255">随 .NET Framework 一起安装 .NET Framework CLR 单独进行版本控制。</span><span class="sxs-lookup"><span data-stu-id="5d86e-255">The .NET Framework CLR installed with .NET Framework is versioned separately.</span></span> <span data-ttu-id="5d86e-256">可通过两种方式检测 .NET Framework CLR 的版本：</span><span class="sxs-lookup"><span data-stu-id="5d86e-256">There are two ways to detect the version of the .NET Framework CLR:</span></span>

- <span data-ttu-id="5d86e-257">**Clrver 工具**</span><span class="sxs-lookup"><span data-stu-id="5d86e-257">**The Clrver.exe tool**</span></span>

  <span data-ttu-id="5d86e-258">使用 [CLR 版本工具 (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) 确定计算机上安装了哪些版本的 CLR。</span><span class="sxs-lookup"><span data-stu-id="5d86e-258">Use the [CLR Version tool (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) to determine which versions of the CLR are installed on a computer.</span></span> <span data-ttu-id="5d86e-259">打开 [Visual Studio 开发人员命令提示](../tools/developer-command-prompt-for-vs.md)并输入 `clrver`。</span><span class="sxs-lookup"><span data-stu-id="5d86e-259">Open the [Developer Command Prompt for Visual Studio](../tools/developer-command-prompt-for-vs.md) and enter `clrver`.</span></span>

  <span data-ttu-id="5d86e-260">示例输出：</span><span class="sxs-lookup"><span data-stu-id="5d86e-260">Sample output:</span></span>

  ```console
  Versions installed on the machine:
  v2.0.50727
  v4.0.30319
  ```

- <span data-ttu-id="5d86e-261">**`Environment` 类**</span><span class="sxs-lookup"><span data-stu-id="5d86e-261">**The `Environment` class**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5d86e-262">对于 .NET Framework 4.5 及更高版本，请勿使用 <xref:System.Environment.Version%2A?displayProperty=nameWithType> 属性来检测 CLR 的版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-262">For .NET Framework 4.5 and later versions, don't use the <xref:System.Environment.Version%2A?displayProperty=nameWithType> property to detect the version of the CLR.</span></span> <span data-ttu-id="5d86e-263">而应按照[检测 .NET Framework 4.5 及更高版本](#detect-net-framework-45-and-later-versions)中所述查询注册表。</span><span class="sxs-lookup"><span data-stu-id="5d86e-263">Instead, query the registry as described in [Detect .NET Framework 4.5 and later versions](#detect-net-framework-45-and-later-versions).</span></span>

  1. <span data-ttu-id="5d86e-264">查询 <xref:System.Environment.Version?displayProperty=nameWithType> 属性以检索 <xref:System.Version> 对象。</span><span class="sxs-lookup"><span data-stu-id="5d86e-264">Query the <xref:System.Environment.Version?displayProperty=nameWithType> property to retrieve a <xref:System.Version> object.</span></span>

     <span data-ttu-id="5d86e-265">返回的 `System.Version` 对象标识当前正在执行代码的运行时版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-265">The returned `System.Version` object identifies the version of the runtime that's currently executing the code.</span></span> <span data-ttu-id="5d86e-266">它不返回可能已安装在计算机上的程序集版本或其他运行时版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-266">It doesn't return assembly versions or other versions of the runtime that may have been installed on the computer.</span></span>

     <span data-ttu-id="5d86e-267">对于 .NET Framework 版本 4、4.5、4.5.1 和 4.5.2，返回的 <xref:System.Version>  对象的字符串表示形式为 4.0.30319.xxxxx，其中 xxxxx 小于 42000。</span><span class="sxs-lookup"><span data-stu-id="5d86e-267">For .NET Framework versions 4, 4.5, 4.5.1, and 4.5.2, the string representation of the returned <xref:System.Version> object has the form 4.0.30319.*xxxxx*, where *xxxxx* is less than 42000.</span></span> <span data-ttu-id="5d86e-268">对于 .NET Framework 4.6 及更高版本，它的格式为 4.0.30319.42000。</span><span class="sxs-lookup"><span data-stu-id="5d86e-268">For .NET Framework 4.6 and later versions, it has the form 4.0.30319.42000.</span></span>

  1. <span data-ttu-id="5d86e-269">获得 Version 对象后，按如下方式查询：</span><span class="sxs-lookup"><span data-stu-id="5d86e-269">After you have the **Version** object, query it as follows:</span></span>

     - <span data-ttu-id="5d86e-270">对于主要版本标识符（例如，4 表示版本 4.0），请使用 <xref:System.Version.Major%2A?displayProperty=nameWithType> 属性。</span><span class="sxs-lookup"><span data-stu-id="5d86e-270">For the major release identifier (for example, *4* for version 4.0), use the <xref:System.Version.Major%2A?displayProperty=nameWithType> property.</span></span>

     - <span data-ttu-id="5d86e-271">对于次要版本标识符（例如，0 表示版本 4.0），请使用 <xref:System.Version.Minor%2A?displayProperty=nameWithType> 属性</span><span class="sxs-lookup"><span data-stu-id="5d86e-271">For the minor release identifier (for example, *0* for version 4.0), use the <xref:System.Version.Minor%2A?displayProperty=nameWithType> property.</span></span>

     - <span data-ttu-id="5d86e-272">对于整个版本字符串（例如，4.0.30319.18010），请使用 <xref:System.Version.ToString%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="5d86e-272">For the entire version string (for example, *4.0.30319.18010*), use the <xref:System.Version.ToString%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="5d86e-273">此方法返回一个值，该值反映正在执行代码的运行时的版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-273">This method returns a single value that reflects the version of the runtime that's executing the code.</span></span> <span data-ttu-id="5d86e-274">它不返回可能安装在计算机上的程序集版本或其他运行时版本。</span><span class="sxs-lookup"><span data-stu-id="5d86e-274">It doesn't return assembly versions or other runtime versions that may be installed on the computer.</span></span>

  <span data-ttu-id="5d86e-275">以下示例使用 <xref:System.Environment.Version%2A?displayProperty=nameWithType> 属性检索 CLR 版本信息：</span><span class="sxs-lookup"><span data-stu-id="5d86e-275">The following example uses the <xref:System.Environment.Version%2A?displayProperty=nameWithType> property to retrieve CLR version information:</span></span>

  ```csharp
  Console.WriteLine($"Version: {Environment.Version}");
  ```

  ```vb
  Console.WriteLine($"Version: {Environment.Version}")
  ```

  <span data-ttu-id="5d86e-276">该示例显示类似于以下内容的输出：</span><span class="sxs-lookup"><span data-stu-id="5d86e-276">The example displays output similar to the following:</span></span>

  ```output
  Version: 4.0.30319.18010
  ```

## <a name="see-also"></a><span data-ttu-id="5d86e-277">请参阅</span><span class="sxs-lookup"><span data-stu-id="5d86e-277">See also</span></span>

- [<span data-ttu-id="5d86e-278">如何：确定安装了哪些 .NET Framework 更新</span><span class="sxs-lookup"><span data-stu-id="5d86e-278">How to: Determine which .NET Framework updates are installed</span></span>](how-to-determine-which-net-framework-updates-are-installed.md)
- [<span data-ttu-id="5d86e-279">安装面向开发人员的 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="5d86e-279">Install .NET Framework for developers</span></span>](../install/guide-for-developers.md)
- [<span data-ttu-id="5d86e-280">.NET Framework 版本和依赖关系</span><span class="sxs-lookup"><span data-stu-id="5d86e-280">.NET Framework versions and dependencies</span></span>](versions-and-dependencies.md)
