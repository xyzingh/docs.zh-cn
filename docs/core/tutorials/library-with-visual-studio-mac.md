---
title: 使用 Visual Studio for Mac 创建 .NET Standard 类库
description: 了解如何使用 Visual Studio for Mac 创建 .NET Standard 类库。
ms.date: 06/08/2020
ms.openlocfilehash: a78cc68d29095e4fefcaf1d3b2158d673b8892ec
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400560"
---
# <a name="tutorial-create-a-net-standard-library-using-visual-studio-for-mac"></a><span data-ttu-id="9c6a3-103">教程：使用 Visual Studio for Mac 创建 .NET Standard 库</span><span class="sxs-lookup"><span data-stu-id="9c6a3-103">Tutorial: Create a .NET Standard library using Visual Studio for Mac</span></span>

<span data-ttu-id="9c6a3-104">在本教程中，将创建包含一个字符串处理方法的类库。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-104">In this tutorial, you create a class library that contains a single string-handling method.</span></span> <span data-ttu-id="9c6a3-105">我们把它作为[扩展方法](../../csharp/programming-guide/classes-and-structs/extension-methods.md)进行实现，这样就可以把它作为 <xref:System.String> 类成员进行调用。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-105">You implement it as an [extension method](../../csharp/programming-guide/classes-and-structs/extension-methods.md) so that you can call it as if it were a member of the <xref:System.String> class.</span></span>

<span data-ttu-id="9c6a3-106">类库定义的是可以由应用程序调用的类型和方法。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-106">A *class library* defines types and methods that are called by an application.</span></span> <span data-ttu-id="9c6a3-107">面向 .NET Standard 2.1 的类库可由面向任何支持 .NET Standard 版本 2.1 的 .NET 实现的应用程序使用。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-107">A class library that targets .NET Standard 2.1 can be used by an application that targets any .NET implementation that supports version 2.1 of .NET Standard.</span></span> <span data-ttu-id="9c6a3-108">完成类库后，可以将其作为第三方组件进行分发，或作为与一个或多个应用程序捆绑在一起的组件进行分发。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-108">When you finish your class library, you can distribute it as a third-party component or as a bundled component with one or more applications.</span></span>

> [!NOTE]
> <span data-ttu-id="9c6a3-109">你的反馈非常有价值。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-109">Your feedback is highly valued.</span></span> <span data-ttu-id="9c6a3-110">有两种方法可以向开发团队提供有关 Visual Studio for Mac 的反馈：</span><span class="sxs-lookup"><span data-stu-id="9c6a3-110">There are two ways you can provide feedback to the development team on Visual Studio for Mac:</span></span>
>
> - <span data-ttu-id="9c6a3-111">在 Visual Studio for Mac 中，从菜单选择“帮助” > “报告问题”，或从欢迎屏幕中选择“报告问题”，将打开一个窗口，以供填写 bug 报告。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-111">In Visual Studio for Mac, select **Help** > **Report a Problem** from the menu or **Report a Problem** from the Welcome screen, which opens a window for filing a bug report.</span></span> <span data-ttu-id="9c6a3-112">可在[开发人员社区](https://aka.ms/feedback/report?space=41)门户中跟踪自己的反馈。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-112">You can track your feedback in the [Developer Community](https://aka.ms/feedback/report?space=41) portal.</span></span>
> - <span data-ttu-id="9c6a3-113">若要提出建议，从菜单中选择“帮助” > “提供建议”，或从欢迎屏幕中选择“提供建议”，转到 [Visual Studio for Mac 开发人员社区网页](https://aka.ms/feedback/suggest?space=41)。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-113">To make a suggestion, select **Help** > **Provide a Suggestion** from the menu or **Provide a Suggestion** from the Welcome screen, which takes you to the [Visual Studio for Mac Developer Community webpage](https://aka.ms/feedback/suggest?space=41).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c6a3-114">先决条件</span><span class="sxs-lookup"><span data-stu-id="9c6a3-114">Prerequisites</span></span>

* <span data-ttu-id="9c6a3-115">[安装 Visual Studio for Mac 版本 8.6 或更高版本](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-115">[Install Visual Studio for Mac version 8.6 or later](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link).</span></span> <span data-ttu-id="9c6a3-116">选择用于安装 .NET Core 的选项。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-116">Select the option to install .NET Core.</span></span> <span data-ttu-id="9c6a3-117">安装 Xamarin 对于 .NET Core 开发而言是可选项。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-117">Installing Xamarin is optional for .NET Core development.</span></span> <span data-ttu-id="9c6a3-118">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="9c6a3-118">For more information, see the following resources:</span></span>

  * <span data-ttu-id="9c6a3-119">[教程：安装 Visual Studio for Mac](/visualstudio/mac/installation)。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-119">[Tutorial: Install Visual Studio for Mac](/visualstudio/mac/installation).</span></span>
  * <span data-ttu-id="9c6a3-120">[支持的 macOS 版本](../install/macos.md)。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-120">[Supported macOS versions](../install/macos.md).</span></span>
  * <span data-ttu-id="9c6a3-121">[Visual Studio for Mac 支持的 .NET Core 版本](/visualstudio/mac/net-core-support)。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-121">[.NET Core versions supported by Visual Studio for Mac](/visualstudio/mac/net-core-support).</span></span>

## <a name="create-a-solution-with-a-class-library-project"></a><span data-ttu-id="9c6a3-122">创建包含类库项目的解决方案</span><span class="sxs-lookup"><span data-stu-id="9c6a3-122">Create a solution with a class library project</span></span>

<span data-ttu-id="9c6a3-123">Visual Studio 解决方案用作一个或多个项目的容器。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-123">A Visual Studio solution serves as a container for one or more projects.</span></span> <span data-ttu-id="9c6a3-124">创建解决方案和解决方案中的类库项目。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-124">Create a solution and a class library project in the solution.</span></span> <span data-ttu-id="9c6a3-125">稍后将其他相关项目添加到同一个解决方案中。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-125">You'll add additional, related projects to the same solution later.</span></span>

1. <span data-ttu-id="9c6a3-126">启动 Visual Studio for Mac。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-126">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="9c6a3-127">在“开始”窗口中，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-127">In the start window, select **New Project**.</span></span>

1. <span data-ttu-id="9c6a3-128">在“多平台”节点下的“新建项目”对话框中，依次选择“库”、“.NET Standard 库”模板和“下一步”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-128">In the **New Project** dialog under the **Multi-Platform** node, select **Library** , then select the **.NET Standard Library** template, and select **Next**.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="“新建项目”对话框":::

1. <span data-ttu-id="9c6a3-130">在“配置新的 .NET Standard 库”对话框中，选择“.NET Standard 2.1”，然后选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-130">In the **Configure your new .NET Standard Library** dialog, choose ".NET Standard 2.1", and select **Next**.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/choose-net-std-21.png" alt-text="选择 .NET Standard 2.1":::

1. <span data-ttu-id="9c6a3-132">将项目命名为“StringLibrary”，并将解决方案命名为“ClassLibraryProjects”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-132">Name the project "StringLibrary" and the solution "ClassLibraryProjects".</span></span> <span data-ttu-id="9c6a3-133">使“在解决方案目录中创建项目目录”保持选中状态。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-133">Leave **Create a project directory within the solution directory** selected.</span></span> <span data-ttu-id="9c6a3-134">选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-134">Select **Create**.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-new-project-options.png" alt-text="Visual Studio for Mac“新建项目”对话框选项":::

1. <span data-ttu-id="9c6a3-136">从主菜单中，选择“视图” > “边栏” > “解决方案”，然后选择“停靠”图标使此边栏保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-136">From the main menu, select **View** > **Pads** > **Solution** , and select the dock icon to keep the pad open.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/solution-dock-icon.png" alt-text="“解决方案”边栏的“停靠”图标":::

1. <span data-ttu-id="9c6a3-138">在“解决方案”边栏中，展开 `StringLibrary` 节点以显示模板提供的类文件 *Class1.cs* 。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-138">In the **Solution** pad, expand the `StringLibrary` node to reveal the class file provided by the template, *Class1.cs*.</span></span> <span data-ttu-id="9c6a3-139">按住 <kbd>Ctrl</kbd> 并单击该文件，从上下文菜单中选择“重命名”，然后将该文件重命名为“StringLibrary.cs”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-139"><kbd>ctrl</kbd>-click the file, select **Rename** from the context menu, and rename the file to *StringLibrary.cs*.</span></span> <span data-ttu-id="9c6a3-140">打开文件并将内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9c6a3-140">Open the file and replace the contents with the following code:</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

1. <span data-ttu-id="9c6a3-141">按 <kbd>⌘</kbd><kbd>S</kbd> (<kbd>command</kbd>+<kbd>S</kbd>) 以保存文件。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-141">Press <kbd>⌘</kbd><kbd>S</kbd> (<kbd>command</kbd>+<kbd>S</kbd>) to save the file.</span></span>

1. <span data-ttu-id="9c6a3-142">在 IDE 窗口底部边距处选择“错误”，打开“错误”面板。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-142">Select **Errors** in the margin at the bottom of the IDE window to open the **Errors** panel.</span></span> <span data-ttu-id="9c6a3-143">选择“生成输出”按钮。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-143">Select the **Build Output** button.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-error-button.png" alt-text="显示“错误”按钮的 Visual Studio Mac IDE 底部边距处":::

1. <span data-ttu-id="9c6a3-145">从菜单中选择“生成” > “生成所有”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-145">Select **Build** > **Build All** from the menu.</span></span>

   <span data-ttu-id="9c6a3-146">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-146">The solution builds.</span></span> <span data-ttu-id="9c6a3-147">生成输出面板显示生成成功。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-147">The build output panel shows that the build is successful.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-build-panel.png" alt-text="“错误”面板的 Visual Studio Mac 生成输出面板，其中显示生成成功消息":::

## <a name="add-a-console-app-to-the-solution"></a><span data-ttu-id="9c6a3-149">向解决方案添加控制台应用</span><span class="sxs-lookup"><span data-stu-id="9c6a3-149">Add a console app to the solution</span></span>

<span data-ttu-id="9c6a3-150">添加使用类库的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-150">Add a console application that uses the class library.</span></span> <span data-ttu-id="9c6a3-151">应用将提示用户输入字符串，并报告字符串是否以大写字符开头。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-151">The app will prompt the user to enter a string and report whether the string begins with an uppercase character.</span></span>

1. <span data-ttu-id="9c6a3-152">在“解决方案”边栏中，按住 <kbd>Ctrl</kbd> 并单击 `ClassLibraryProjects` 解决方案。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-152">In the **Solution** pad, <kbd>ctrl</kbd>-click the `ClassLibraryProjects` solution.</span></span> <span data-ttu-id="9c6a3-153">通过从“Web 和控制台” > “应用”模板中选择模板来添加新的“控制台应用程序”项目，然后选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-153">Add a new **Console Application** project by selecting the template from the **Web and Console** > **App** templates, and select **Next**.</span></span>

1. <span data-ttu-id="9c6a3-154">选择“.NET Core 3.1”作为“目标框架”，然后选择“下一步”  。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-154">Select **.NET Core 3.1** as the **Target Framework** and select **Next**.</span></span>

1. <span data-ttu-id="9c6a3-155">将项目命名为“ShowCase”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-155">Name the project **ShowCase**.</span></span> <span data-ttu-id="9c6a3-156">选择“创建”以在解决方案中创建项目。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-156">Select **Create** to create the project in the solution.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/add-showcase-project.png" alt-text="添加 ShowCase 项目":::

1. <span data-ttu-id="9c6a3-158">打开 *Program.cs* 文件。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-158">Open the *Program.cs* file.</span></span> <span data-ttu-id="9c6a3-159">将代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9c6a3-159">Replace the code with the following code:</span></span>

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   <span data-ttu-id="9c6a3-160">该程序会提示用户输入字符串。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-160">The program prompts the user to enter a string.</span></span> <span data-ttu-id="9c6a3-161">它会指明字符串是否以大写字符开头。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-161">It indicates whether the string starts with an uppercase character.</span></span> <span data-ttu-id="9c6a3-162">如果用户没有输入字符串就按 <kbd>Enter</kbd> 键，那么应用程序会终止，控制台窗口会关闭。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-162">If the user presses the <kbd>enter</kbd> key without entering a string, the application ends, and the console window closes.</span></span>

   <span data-ttu-id="9c6a3-163">该代码使用 `row` 变量来维护写入到控制台窗口的数据行数计数。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-163">The code uses the `row` variable to maintain a count of the number of rows of data written to the console window.</span></span> <span data-ttu-id="9c6a3-164">如果大于或等于 25，该代码将清除控制台窗口，并向用户显示一条消息。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-164">Whenever it's greater than or equal to 25, the code clears the console window and displays a message to the user.</span></span>

## <a name="add-a-project-reference"></a><span data-ttu-id="9c6a3-165">添加项目引用</span><span class="sxs-lookup"><span data-stu-id="9c6a3-165">Add a project reference</span></span>

<span data-ttu-id="9c6a3-166">最初，新的控制台应用项目无权访问类库。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-166">Initially, the new console app project doesn't have access to the class library.</span></span> <span data-ttu-id="9c6a3-167">若要允许该项目调用类库中的方法，可以创建对类库项目的项目引用。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-167">To allow it to call methods in the class library, create a project reference to the class library project.</span></span>

1. <span data-ttu-id="9c6a3-168">在“解决方案”边栏中，按住 <kbd>Ctrl</kbd> 并单击新“ShowCase”项目的“依赖项”节点。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-168">In the **Solutions** pad, <kbd>ctrl</kbd>-click the **Dependencies** node of the new **ShowCase** project.</span></span> <span data-ttu-id="9c6a3-169">在上下文菜单中，选择“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-169">In the context menu, select **Add Reference**.</span></span>

1. <span data-ttu-id="9c6a3-170">在“引用”对话框中，选择“StringLibrary”，然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-170">In the **References** dialog, select **StringLibrary** and select **OK**.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="9c6a3-171">运行应用</span><span class="sxs-lookup"><span data-stu-id="9c6a3-171">Run the app</span></span>

1. <span data-ttu-id="9c6a3-172">按住 <kbd>Ctrl</kbd> 并单击 ShowCase 项目，然后从上下文菜单中选择“运行项目”。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-172"><kbd>ctrl</kbd>-click on the ShowCase project and select **Run project** from the context menu.</span></span>

1. <span data-ttu-id="9c6a3-173">输入字符串并按 <kbd>Enter</kbd> 以试用程序，然后按 <kbd>Enter</kbd> 退出。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-173">Try out the program by entering strings and pressing <kbd>enter</kbd>, then press <kbd>enter</kbd> to exit.</span></span>

   :::image type="content" source="media/library-with-visual-studio-mac/visual-studio-mac-console-window.png" alt-text="Visual Studio for Mac 控制台窗口，显示正在运行的应用":::

## <a name="additional-resources"></a><span data-ttu-id="9c6a3-175">其他资源</span><span class="sxs-lookup"><span data-stu-id="9c6a3-175">Additional resources</span></span>

* [<span data-ttu-id="9c6a3-176">使用 .NET Core CLI 开发库</span><span class="sxs-lookup"><span data-stu-id="9c6a3-176">Develop libraries with the .NET Core CLI</span></span>](libraries.md)
* <span data-ttu-id="9c6a3-177">[.NET Standard 版本及其支持的平台](../../standard/net-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-177">[.NET Standard versions and the platforms they support](../../standard/net-standard.md).</span></span>
* [<span data-ttu-id="9c6a3-178">Visual Studio 2019 for Mac 发行说明</span><span class="sxs-lookup"><span data-stu-id="9c6a3-178">Visual Studio 2019 for Mac Release Notes</span></span>](/visualstudio/releasenotes/vs2019-mac-relnotes)

## <a name="next-steps"></a><span data-ttu-id="9c6a3-179">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9c6a3-179">Next steps</span></span>

<span data-ttu-id="9c6a3-180">在本教程中，你创建了一个解决方案和一个库项目，并添加了一个使用该库的控制台应用项目。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-180">In this tutorial, you created a solution and a library project, and added a console app project that uses the library.</span></span> <span data-ttu-id="9c6a3-181">在下一教程中，将向解决方案中添加单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="9c6a3-181">In the next tutorial, you add a unit test project to the solution.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c6a3-182">在 Visual Studio for Mac 中使用 .NET Core 测试 .NET Standard 库</span><span class="sxs-lookup"><span data-stu-id="9c6a3-182">Test a .NET Standard library with .NET Core using Visual Studio for Mac</span></span>](testing-library-with-visual-studio-mac.md)
