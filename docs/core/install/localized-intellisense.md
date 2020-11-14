---
title: 安装本地化的 IntelliSense 文件
description: 了解如何设置开发计算机，以便在 Visual Studio 中为 .NET 5+ 项目（包含 .NET Core）使用本地化的 IntelliSense 文件。
ms.date: 11/06/2020
ms.openlocfilehash: 45eeae12ca79179cacb3d48fca28118de70e0a4f
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "94506761"
---
# <a name="how-to-install-localized-intellisense-files-for-net"></a><span data-ttu-id="af055-103">如何为 .NET 安装本地化的 IntelliSense 文件</span><span class="sxs-lookup"><span data-stu-id="af055-103">How to install localized IntelliSense files for .NET</span></span>

<span data-ttu-id="af055-104">[IntelliSense](/visualstudio/ide/using-intellisense) 是一种代码完成辅助工具，可以在不同的集成开发环境 (IDE) 中使用，例如 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="af055-104">[IntelliSense](/visualstudio/ide/using-intellisense) is a code-completion aid that's available in different integrated development environments (IDEs), such as Visual Studio.</span></span> <span data-ttu-id="af055-105">默认情况下，在开发 .NET 项目时，SDK 仅包含英语版本的 IntelliSense 文件。</span><span class="sxs-lookup"><span data-stu-id="af055-105">By default, when you're developing .NET projects, the SDK only includes the English version of the IntelliSense files.</span></span> <span data-ttu-id="af055-106">本文介绍：</span><span class="sxs-lookup"><span data-stu-id="af055-106">This article explains:</span></span>

- <span data-ttu-id="af055-107">如何安装这些文件的本地化版本。</span><span class="sxs-lookup"><span data-stu-id="af055-107">How to install the localized version of those files.</span></span>
- <span data-ttu-id="af055-108">如何修改 Visual Studio 安装以使用其他语言。</span><span class="sxs-lookup"><span data-stu-id="af055-108">How to modify the Visual Studio installation to use a different language.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af055-109">系统必备</span><span class="sxs-lookup"><span data-stu-id="af055-109">Prerequisites</span></span>

- <span data-ttu-id="af055-110">[.NET Core 3.0 SDK](https://dotnet.microsoft.com/download/dotnet-core) 或更高版本，例如 [.NET 5 SDK](https://dotnet.microsoft.com/download/dotnet/5.0)。</span><span class="sxs-lookup"><span data-stu-id="af055-110">[.NET Core 3.0 SDK](https://dotnet.microsoft.com/download/dotnet-core) or a later version, such as [.NET 5 SDK](https://dotnet.microsoft.com/download/dotnet/5.0).</span></span>
- <span data-ttu-id="af055-111">[Visual Studio 2019 版本 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="af055-111">[Visual Studio 2019 version 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) or a later version.</span></span>

## <a name="download-and-install-the-localized-intellisense-files"></a><span data-ttu-id="af055-112">下载并安装本地化的 IntelliSense 文件</span><span class="sxs-lookup"><span data-stu-id="af055-112">Download and install the localized IntelliSense files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af055-113">此过程需具有管理员权限，才能将 IntelliSense 文件复制到 .NET 安装文件夹中。</span><span class="sxs-lookup"><span data-stu-id="af055-113">This procedure requires that you have administrator permission to copy the IntelliSense files to the .NET installation folder.</span></span>

1. <span data-ttu-id="af055-114">转到[下载 IntelliSense 文件](https://dotnet.microsoft.com/download/intellisense)页面。</span><span class="sxs-lookup"><span data-stu-id="af055-114">Go to the [Download IntelliSense files](https://dotnet.microsoft.com/download/intellisense) page.</span></span>

1. <span data-ttu-id="af055-115">下载要使用的语言和版本的 IntelliSense 文件。</span><span class="sxs-lookup"><span data-stu-id="af055-115">Download the IntelliSense file for the language and version you'd like to use.</span></span>

1. <span data-ttu-id="af055-116">提取 zip 文件的内容。</span><span class="sxs-lookup"><span data-stu-id="af055-116">Extract the contents of the zip file.</span></span>

1. <span data-ttu-id="af055-117">导航到 .NET Intellisense 文件夹。</span><span class="sxs-lookup"><span data-stu-id="af055-117">Navigate to the .NET Intellisense folder.</span></span>

   1. <span data-ttu-id="af055-118">导航到 .NET 安装文件夹。</span><span class="sxs-lookup"><span data-stu-id="af055-118">Navigate to the .NET installation folder.</span></span> <span data-ttu-id="af055-119">默认情况下，它位于 %ProgramFiles%\dotnet\packs 下  。</span><span class="sxs-lookup"><span data-stu-id="af055-119">By default, it's under *%ProgramFiles%\dotnet\packs*.</span></span>
   1. <span data-ttu-id="af055-120">选择要为其安装 IntelliSense 的 SDK，然后导航到关联的路径。</span><span class="sxs-lookup"><span data-stu-id="af055-120">Choose which SDK you want to install the IntelliSense for, and navigate to the associated path.</span></span> <span data-ttu-id="af055-121">有下列选项：</span><span class="sxs-lookup"><span data-stu-id="af055-121">You have the following options:</span></span>

      | <span data-ttu-id="af055-122">SDK 类型</span><span class="sxs-lookup"><span data-stu-id="af055-122">SDK type</span></span>              | <span data-ttu-id="af055-123">路径</span><span class="sxs-lookup"><span data-stu-id="af055-123">Path</span></span>                               |
      |-----------------------|------------------------------------|
      | <span data-ttu-id="af055-124">.NET 5+ 和 .NET Core</span><span class="sxs-lookup"><span data-stu-id="af055-124">.NET 5+ and .NET Core</span></span> | <span data-ttu-id="af055-125">Microsoft.NETCore.App.Ref </span><span class="sxs-lookup"><span data-stu-id="af055-125">*Microsoft.NETCore.App.Ref*</span></span>        |
      | <span data-ttu-id="af055-126">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="af055-126">Windows Desktop</span></span>       | <span data-ttu-id="af055-127">Microsoft.WindowsDesktop.App.Ref </span><span class="sxs-lookup"><span data-stu-id="af055-127">*Microsoft.WindowsDesktop.App.Ref*</span></span> |
      | <span data-ttu-id="af055-128">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="af055-128">.NET Standard</span></span>         | <span data-ttu-id="af055-129">NETStandard.Library.Ref </span><span class="sxs-lookup"><span data-stu-id="af055-129">*NETStandard.Library.Ref*</span></span>          |

   1. <span data-ttu-id="af055-130">导航到要为其安装本地化 IntelliSense 的版本。</span><span class="sxs-lookup"><span data-stu-id="af055-130">Navigate to the version you want to install the localized IntelliSense for.</span></span> <span data-ttu-id="af055-131">例如，5.0.0。</span><span class="sxs-lookup"><span data-stu-id="af055-131">For example, *5.0.0*.</span></span>
   1. <span data-ttu-id="af055-132">打开 ref 文件夹  。</span><span class="sxs-lookup"><span data-stu-id="af055-132">Open the *ref* folder.</span></span>
   1. <span data-ttu-id="af055-133">打开 moniker 文件夹。</span><span class="sxs-lookup"><span data-stu-id="af055-133">Open the moniker folder.</span></span> <span data-ttu-id="af055-134">例如 net5.0。</span><span class="sxs-lookup"><span data-stu-id="af055-134">For example, *net5.0*.</span></span>

   <span data-ttu-id="af055-135">因此，要导航到的完整路径看起来将类似于 C:\Program Files\dotnet\packs\Microsoft.NETCore.App.Ref\5.0.0\ref\net5.0。</span><span class="sxs-lookup"><span data-stu-id="af055-135">So, the full path that you'd navigate to would look similar to *C:\Program Files\dotnet\packs\Microsoft.NETCore.App.Ref\5.0.0\ref\net5.0*.</span></span>

1. <span data-ttu-id="af055-136">在刚打开的 moniker 文件夹中创建一个子文件夹。</span><span class="sxs-lookup"><span data-stu-id="af055-136">Create a subfolder inside the moniker folder you just opened.</span></span> <span data-ttu-id="af055-137">文件夹名称指示要使用的语言。</span><span class="sxs-lookup"><span data-stu-id="af055-137">The name of the folder indicates which language you want to use.</span></span> <span data-ttu-id="af055-138">下表指定了不同的选项：</span><span class="sxs-lookup"><span data-stu-id="af055-138">The following table specifies the different options:</span></span>

   | <span data-ttu-id="af055-139">语言</span><span class="sxs-lookup"><span data-stu-id="af055-139">Language</span></span>              | <span data-ttu-id="af055-140">文件夹名称</span><span class="sxs-lookup"><span data-stu-id="af055-140">Folder name</span></span> |
   | --------------------- | ----------- |
   | <span data-ttu-id="af055-141">巴西葡萄牙语</span><span class="sxs-lookup"><span data-stu-id="af055-141">Brazilian Portuguese</span></span>  | <span data-ttu-id="af055-142">pt-br </span><span class="sxs-lookup"><span data-stu-id="af055-142">*pt-br*</span></span>     |
   | <span data-ttu-id="af055-143">中文（简体）</span><span class="sxs-lookup"><span data-stu-id="af055-143">Chinese (simplified)</span></span>  | <span data-ttu-id="af055-144">zh-hans </span><span class="sxs-lookup"><span data-stu-id="af055-144">*zh-hans*</span></span>   |
   | <span data-ttu-id="af055-145">中文（繁体）</span><span class="sxs-lookup"><span data-stu-id="af055-145">Chinese (traditional)</span></span> | <span data-ttu-id="af055-146">zh-hant </span><span class="sxs-lookup"><span data-stu-id="af055-146">*zh-hant*</span></span>   |
   | <span data-ttu-id="af055-147">法语</span><span class="sxs-lookup"><span data-stu-id="af055-147">French</span></span>                | <span data-ttu-id="af055-148">fr </span><span class="sxs-lookup"><span data-stu-id="af055-148">*fr*</span></span>        |
   | <span data-ttu-id="af055-149">德语</span><span class="sxs-lookup"><span data-stu-id="af055-149">German</span></span>                | <span data-ttu-id="af055-150">de </span><span class="sxs-lookup"><span data-stu-id="af055-150">*de*</span></span>        |
   | <span data-ttu-id="af055-151">意大利语</span><span class="sxs-lookup"><span data-stu-id="af055-151">Italian</span></span>               | <span data-ttu-id="af055-152">it </span><span class="sxs-lookup"><span data-stu-id="af055-152">*it*</span></span>        |
   | <span data-ttu-id="af055-153">日语</span><span class="sxs-lookup"><span data-stu-id="af055-153">Japanese</span></span>              | <span data-ttu-id="af055-154">ja </span><span class="sxs-lookup"><span data-stu-id="af055-154">*ja*</span></span>        |
   | <span data-ttu-id="af055-155">朝鲜语</span><span class="sxs-lookup"><span data-stu-id="af055-155">Korean</span></span>                | <span data-ttu-id="af055-156">ko </span><span class="sxs-lookup"><span data-stu-id="af055-156">*ko*</span></span>        |
   | <span data-ttu-id="af055-157">俄语</span><span class="sxs-lookup"><span data-stu-id="af055-157">Russian</span></span>               | <span data-ttu-id="af055-158">ru </span><span class="sxs-lookup"><span data-stu-id="af055-158">*ru*</span></span>        |
   | <span data-ttu-id="af055-159">西班牙语</span><span class="sxs-lookup"><span data-stu-id="af055-159">Spanish</span></span>               | <span data-ttu-id="af055-160">es </span><span class="sxs-lookup"><span data-stu-id="af055-160">*es*</span></span>        |

1. <span data-ttu-id="af055-161">将在步骤 3 中提取的 .xml 文件复制到此新文件夹。</span><span class="sxs-lookup"><span data-stu-id="af055-161">Copy the *.xml* files you extracted in step 3 to this new folder.</span></span> <span data-ttu-id="af055-162">.xml 文件按 SDK 文件夹细分，因此，请将它们复制到步骤 4 中选择的相应 SDK。</span><span class="sxs-lookup"><span data-stu-id="af055-162">The *.xml* files are broken down by SDK folders, so copy them to the matching SDK you chose in step 4.</span></span>

## <a name="modify-visual-studio-language"></a><span data-ttu-id="af055-163">修改 Visual Studio 语言</span><span class="sxs-lookup"><span data-stu-id="af055-163">Modify Visual Studio language</span></span>

<span data-ttu-id="af055-164">要使 Visual Studio 使用其他语言的 IntelliSense，请安装适当的语言包。</span><span class="sxs-lookup"><span data-stu-id="af055-164">For Visual Studio to use a different language for IntelliSense, install the appropriate language pack.</span></span> <span data-ttu-id="af055-165">这可以在[安装过程中](/visualstudio/install/install-visual-studio#step-6---install-language-packs-optional)完成，也可以之后通过修改 Visual Studio 安装来完成。</span><span class="sxs-lookup"><span data-stu-id="af055-165">This can be done [during installation](/visualstudio/install/install-visual-studio#step-6---install-language-packs-optional) or at a later time by modifying the Visual Studio installation.</span></span> <span data-ttu-id="af055-166">如果已将 Visual Studio 配置为所需的语言，那么 IntelliSense 安装已准备就绪。</span><span class="sxs-lookup"><span data-stu-id="af055-166">If you already have Visual Studio configured to the language of your choice, your IntelliSense installation is ready.</span></span>

### <a name="install-the-language-pack"></a><span data-ttu-id="af055-167">安装语言包</span><span class="sxs-lookup"><span data-stu-id="af055-167">Install the language pack</span></span>

<span data-ttu-id="af055-168">如果在安装过程中未安装所需的语言包，请按以下步骤更新 Visual Studio 来安装语言包：</span><span class="sxs-lookup"><span data-stu-id="af055-168">If you didn't install the desired language pack during setup, update Visual Studio as follows to install the language pack:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af055-169">若要安装、更新或修改 Visual Studio，必须使用具有管理员权限的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="af055-169">To install, update, or modify Visual Studio, you must log on with an account that has administrator permission.</span></span> <span data-ttu-id="af055-170">有关详细信息，请参阅[用户权限与 Visual Studio](/visualstudio/ide/user-permissions-and-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="af055-170">For more information, see [User permissions and Visual Studio](/visualstudio/ide/user-permissions-and-visual-studio).</span></span>

1. <span data-ttu-id="af055-171">在计算机上找到 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="af055-171">Find the Visual Studio Installer on your computer.</span></span>

   <span data-ttu-id="af055-172">例如，在运行 Windows 10 的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出    。</span><span class="sxs-lookup"><span data-stu-id="af055-172">For example, on a computer running Windows 10, select **Start** , and then scroll to the letter **V** , where it's listed as **Visual Studio Installer**.</span></span>

   ![在 Windows 中打开 Visual Studio 安装程序](./media/localized-intellisense/vs-installer-windows-start.png)

   > [!NOTE]
   > <span data-ttu-id="af055-174">还可以在以下位置中找到 Visual Studio 安装程序：</span><span class="sxs-lookup"><span data-stu-id="af055-174">You can also find the Visual Studio Installer in the following location:</span></span>
   >
   > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

   <span data-ttu-id="af055-175">可能需要先更新安装程序，然后才能继续操作。</span><span class="sxs-lookup"><span data-stu-id="af055-175">You might have to update the installer before continuing.</span></span> <span data-ttu-id="af055-176">如果是这样，请按照提示操作。</span><span class="sxs-lookup"><span data-stu-id="af055-176">If so, follow the prompts.</span></span>

1. <span data-ttu-id="af055-177">在安装程序中，查找要为其添加语言包的 Visual Studio 版本，然后选择“修改”  。</span><span class="sxs-lookup"><span data-stu-id="af055-177">In the installer, look for the edition of Visual Studio that you want to add the language pack to, and then choose **Modify**.</span></span>

   ![更新或修改 Visual Studio](./media/localized-intellisense/vs-installer-modify.png)

   > [!IMPORTANT]
   > <span data-ttu-id="af055-179">如果未看到“修改”按钮，但看到了“更新”按钮，则需要先更新 Visual Studio，才能修改安装   。</span><span class="sxs-lookup"><span data-stu-id="af055-179">If you don't see a **Modify** button but you see an **Update** one instead, you need to update your Visual Studio before you can modify your installation.</span></span>
   > <span data-ttu-id="af055-180">更新完成后，应会显示“修改”按钮  。</span><span class="sxs-lookup"><span data-stu-id="af055-180">After the update is finished, the **Modify** button should appear.</span></span>

1. <span data-ttu-id="af055-181">在“语言包”选项卡中，选择或取消选择要安装或卸载的语言  。</span><span class="sxs-lookup"><span data-stu-id="af055-181">In the **Language packs** tab, select or deselect the languages you want to install or uninstall.</span></span>

   ![Visual Studio 语言包选项卡](./media/localized-intellisense/vs-modify-language-packs.png)

1. <span data-ttu-id="af055-183">选择“修改”  。</span><span class="sxs-lookup"><span data-stu-id="af055-183">Choose **Modify**.</span></span> <span data-ttu-id="af055-184">更新开始。</span><span class="sxs-lookup"><span data-stu-id="af055-184">The update starts.</span></span>

### <a name="modify-language-settings-in-visual-studio"></a><span data-ttu-id="af055-185">修改 Visual Studio 中的语言设置</span><span class="sxs-lookup"><span data-stu-id="af055-185">Modify language settings in Visual Studio</span></span>

<span data-ttu-id="af055-186">安装所需的语言包后，请修改 Visual Studio 设置以使用其他语言：</span><span class="sxs-lookup"><span data-stu-id="af055-186">Once you've installed the desired language packs, modify your Visual Studio settings to use a different language:</span></span>

1. <span data-ttu-id="af055-187">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="af055-187">Open Visual Studio.</span></span>

1. <span data-ttu-id="af055-188">在“启动”窗口中，选择“继续但无需代码”  。</span><span class="sxs-lookup"><span data-stu-id="af055-188">On the start window, choose **Continue without code**.</span></span>

1. <span data-ttu-id="af055-189">在菜单栏上，选择“工具”   >   “选项”。</span><span class="sxs-lookup"><span data-stu-id="af055-189">On the menu bar, select **Tools** > **Options**.</span></span> <span data-ttu-id="af055-190">“选项”对话框随即打开。</span><span class="sxs-lookup"><span data-stu-id="af055-190">The Options dialog opens.</span></span>

1. <span data-ttu-id="af055-191">在“环境”节点下，选择“国际设置”   。</span><span class="sxs-lookup"><span data-stu-id="af055-191">Under the **Environment** node, choose **International Settings**.</span></span>

1. <span data-ttu-id="af055-192">在“语言”下拉列表中，选择所需的语言  。</span><span class="sxs-lookup"><span data-stu-id="af055-192">On the **Language** drop-down, select the desired language.</span></span> <span data-ttu-id="af055-193">选择 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="af055-193">Choose **OK**.</span></span>

1. <span data-ttu-id="af055-194">随即会显示一个对话框，告知必须重启 Visual Studio 才能使所做的更改生效。</span><span class="sxs-lookup"><span data-stu-id="af055-194">A dialog informs you that you have to restart Visual Studio for the changes to take effect.</span></span> <span data-ttu-id="af055-195">选择 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="af055-195">Choose **OK**.</span></span>

1. <span data-ttu-id="af055-196">重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="af055-196">Restart Visual Studio.</span></span>

<span data-ttu-id="af055-197">之后，当打开面向刚安装的 IntelliSense 文件版本的 .NET 项目时，IntelliSense 应会按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="af055-197">After this, your IntelliSense should work as expected when you open a .NET project that targets the version of the IntelliSense files you just installed.</span></span>

## <a name="see-also"></a><span data-ttu-id="af055-198">另请参阅</span><span class="sxs-lookup"><span data-stu-id="af055-198">See also</span></span>

- [<span data-ttu-id="af055-199">Visual Studio 中的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="af055-199">IntelliSense in Visual Studio</span></span>](/visualstudio/ide/using-intellisense)
