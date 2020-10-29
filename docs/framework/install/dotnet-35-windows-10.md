---
title: 在 Windows 10、8.1、8 上安装 .NET Framework 3.5
description: 了解如何在 Windows 10、Windows 8.1 和 Windows 8 上安装 .NET Framework 3.5。
ms.date: 07/16/2018
ms.openlocfilehash: a385c46d2b3b384bc0a413d1dfa80e88ba7fb00a
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223811"
---
# <a name="install-the-net-framework-35-on-windows-10-windows-81-and-windows-8"></a><span data-ttu-id="ef158-103">在 Windows 10、Windows 8.1 和 Windows 8 上安装 .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="ef158-103">Install the .NET Framework 3.5 on Windows 10, Windows 8.1, and Windows 8</span></span>

<span data-ttu-id="ef158-104">必须安装 .NET Framework 3.5，才能在 Windows 10、Windows 8.1 和 Windows 8 上运行应用。</span><span class="sxs-lookup"><span data-stu-id="ef158-104">You may need the .NET Framework 3.5 to run an app on Windows 10, Windows 8.1, and Windows 8.</span></span> <span data-ttu-id="ef158-105">对于旧版 Windows，也可以按照以下说明操作。</span><span class="sxs-lookup"><span data-stu-id="ef158-105">You can also use these instructions for earlier Windows versions.</span></span>

## <a name="download-the-offline-installer"></a><span data-ttu-id="ef158-106">下载脱机安装程序</span><span class="sxs-lookup"><span data-stu-id="ef158-106">Download the offline installer</span></span>

<span data-ttu-id="ef158-107">.NET Framework 3.5 SP1 脱机安装程序可在 [.NET Framework 3.5 SP1 下载页](https://dotnet.microsoft.com/download/dotnet-framework/net35-sp1)上找到，并且适用于 Windows 10 之前的 Windows 版本。</span><span class="sxs-lookup"><span data-stu-id="ef158-107">The .NET Framework 3.5 SP1 offline installer is available on the [.NET Framework 3.5 SP1 Download page](https://dotnet.microsoft.com/download/dotnet-framework/net35-sp1) and is available for Windows versions prior to Windows 10.</span></span>

## <a name="install-the-net-framework-35-on-demand"></a><span data-ttu-id="ef158-108">按需安装.NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="ef158-108">Install the .NET Framework 3.5 on Demand</span></span>

<span data-ttu-id="ef158-109">如果尝试运行的应用要求安装 .NET Framework 3.5，则会看到以下配置对话框。</span><span class="sxs-lookup"><span data-stu-id="ef158-109">You may see the following configuration dialog if you try to run an app that requires the .NET Framework 3.5.</span></span> <span data-ttu-id="ef158-110">选择“安装此功能”  ，启用 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="ef158-110">Choose **Install this feature** to enable the .NET Framework 3.5.</span></span> <span data-ttu-id="ef158-111">此选项需要 Internet 连接。</span><span class="sxs-lookup"><span data-stu-id="ef158-111">This option requires an Internet connection.</span></span>

![.NET Framework 安装对话框的屏幕截图。](./media/dotnet-35-windows-10/dotnet-framework-installation-dialog.png)

### <a name="why-am-i-getting-this-pop-up"></a><span data-ttu-id="ef158-113">为什么我会看到此弹出项？</span><span class="sxs-lookup"><span data-stu-id="ef158-113">Why am I getting this pop-up?</span></span>

<span data-ttu-id="ef158-114">.NET Framework 是由 Microsoft 创建，用于提供应用程序运行环境。</span><span class="sxs-lookup"><span data-stu-id="ef158-114">The .NET Framework is created by Microsoft and provides an environment for running applications.</span></span> <span data-ttu-id="ef158-115">有多种不同版本。</span><span class="sxs-lookup"><span data-stu-id="ef158-115">There are different versions available.</span></span> <span data-ttu-id="ef158-116">许多公司都开发使用 .NET Framework 运行的应用程序，并且这些应用都定目标到具体版本。</span><span class="sxs-lookup"><span data-stu-id="ef158-116">Many companies develop their apps to run using the .NET Framework, and these apps target a specific version.</span></span> <span data-ttu-id="ef158-117">如果看到此弹出项，表明尝试运行的应用程序需要 .NET Framework 版本 3.5，但未在系统上安装此版本。</span><span class="sxs-lookup"><span data-stu-id="ef158-117">If you see this pop-up, you're trying to run an application that requires the .NET Framework version 3.5, but that version is not installed on your system.</span></span>

## <a name="enable-the-net-framework-35-in-control-panel"></a><span data-ttu-id="ef158-118">在控制面板中启用 .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="ef158-118">Enable the .NET Framework 3.5 in Control Panel</span></span>

<span data-ttu-id="ef158-119">可以通过 Windows 控制面板启用 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="ef158-119">You can enable the .NET Framework 3.5 through the Windows Control Panel.</span></span> <span data-ttu-id="ef158-120">此选项需要 Internet 连接。</span><span class="sxs-lookup"><span data-stu-id="ef158-120">This option requires an Internet connection.</span></span>

1. <span data-ttu-id="ef158-121">按下键盘上的 Windows 徽标键 ![Windows 徽标键徽标的屏幕截图](./media/dotnet-35-windows-10/windows-keyboard-logo.png)，</span><span class="sxs-lookup"><span data-stu-id="ef158-121">Press the Windows key ![Screenshot of the Windows key logo.](./media/dotnet-35-windows-10/windows-keyboard-logo.png)</span></span> <span data-ttu-id="ef158-122">键入“Windows 功能”，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="ef158-122">on your keyboard, type "Windows Features", and press Enter.</span></span> <span data-ttu-id="ef158-123">随即显示“打开或关闭 Windows 功能”对话框  。</span><span class="sxs-lookup"><span data-stu-id="ef158-123">The **Turn Windows features on or off** dialog box appears.</span></span>

2. <span data-ttu-id="ef158-124">如果弹出提示，选择“.NET Framework 3.5 (包括 .NET 2.0 和 3.0)” 复选框，选择“确定”，然后重启计算机   。</span><span class="sxs-lookup"><span data-stu-id="ef158-124">Select the **.NET Framework 3.5 (includes .NET 2.0 and 3.0)** check box, select **OK** , and reboot your computer if prompted.</span></span>

   ![显示通过控制面板安装 .NET 的屏幕截图。](./media/dotnet-35-windows-10/dotnet-control-panel.png)

   <span data-ttu-id="ef158-126">无需选择“Windows Communication Foundation (WCF) HTTP 激活”  和“Windows Communication Foundation (WCF) 非 HTTP 激活”  的子项，除非是需要使用此功能的开发者或服务器管理员。</span><span class="sxs-lookup"><span data-stu-id="ef158-126">You don't need to select the child items for **Windows Communication Foundation (WCF) HTTP Activation** and **Windows Communication Foundation (WCF) Non-HTTP Activation** unless you're a developer or server administrator who requires this functionality.</span></span>

## <a name="troubleshoot-the-installation-of-the-net-framework-35"></a><span data-ttu-id="ef158-127">.NET Framework 3.5 安装疑难解答</span><span class="sxs-lookup"><span data-stu-id="ef158-127">Troubleshoot the installation of the .NET Framework 3.5</span></span>

<span data-ttu-id="ef158-128">安装过程中，你可能会遇到错误 0x800f0906、0x800f0907、0x800f081f 或 0x800F0922，此时请参阅 [.NET Framework 3.5 安装错误：0x800f0906、0x800f0907 或 0x800f081f](https://support.microsoft.com/help/2734782/net-framework-3-5-installation-error-0x800f0906--0x800f081f--0x800f09)，了解如何解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="ef158-128">During installation, you may encounter error 0x800f0906, 0x800f0907, 0x800f081f, or 0x800F0922, in which case refer to [.NET Framework 3.5 installation error: 0x800f0906, 0x800f0907, or 0x800f081f](https://support.microsoft.com/help/2734782/net-framework-3-5-installation-error-0x800f0906--0x800f081f--0x800f09) to see how to resolve these issues.</span></span>

<span data-ttu-id="ef158-129">如果仍无法解决安装问题，或未连接到 Internet，可以尝试使用 Windows 安装介质进行安装。</span><span class="sxs-lookup"><span data-stu-id="ef158-129">If you still can't resolve your installation issue or you don't have an Internet connection, you can try installing it using your Windows installation media.</span></span> <span data-ttu-id="ef158-130">有关详细信息，请参阅[使用部署映像服务和管理 (DISM) 部署 .NET Framework 3.5](/windows-hardware/manufacture/desktop/deploy-net-framework-35-by-using-deployment-image-servicing-and-management--dism)。</span><span class="sxs-lookup"><span data-stu-id="ef158-130">For more information, see [Deploy .NET Framework 3.5 by using Deployment Image Servicing and Management (DISM)](/windows-hardware/manufacture/desktop/deploy-net-framework-35-by-using-deployment-image-servicing-and-management--dism).</span></span> <span data-ttu-id="ef158-131">如果使用的是 Windows 7、Windows 8.1 或最新的 Windows 10 版本，但没有安装媒体，请在此处创建最新的安装媒体：[为 Windows 创建安装媒体](https://support.microsoft.com/help/15088/windows-create-installation-media)。</span><span class="sxs-lookup"><span data-stu-id="ef158-131">If you're using Windows 7, Windows 8.1, or the latest Windows 10 version but you don't have the installation media, create an up-to-date installation media here: [Create installation media for Windows](https://support.microsoft.com/help/15088/windows-create-installation-media).</span></span> <span data-ttu-id="ef158-132">有关 Windows 10 按需功能的附加信息：[按需功能](/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)。</span><span class="sxs-lookup"><span data-stu-id="ef158-132">Additional information about Windows 10 Features on Demand: [Features on Demand](/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities).</span></span>

> [!WARNING]
> <span data-ttu-id="ef158-133">如果不依赖 Windows 更新作为源来安装 .NET Framework 3.5，则必须确保严格使用来自相同的、对应的 Windows 操作系统版本的源。</span><span class="sxs-lookup"><span data-stu-id="ef158-133">If you're not relying on Windows Update as the source for installing the .NET Framework 3.5, you must ensure to strictly use sources from the same corresponding Windows operating system version.</span></span> <span data-ttu-id="ef158-134">使用来自不同 Windows 操作系统版本的源将安装与 .NET Framework 3.5 不匹配的版本，或导致安装失败，使系统处于不受支持和无法提供服务的状态。</span><span class="sxs-lookup"><span data-stu-id="ef158-134">Using sources from a different Windows operating system version will either install a mismatched version of .NET Framework 3.5 or cause the installation to fail, leaving the system in an unsupported and unserviceable state.</span></span>
