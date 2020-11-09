---
title: 使用 Visual Studio for Mac 创建 .NET Core 控制台应用程序
description: 了解如何使用 Visual Studio for Mac 创建 .NET Core 控制台应用程序。
ms.date: 06/02/2020
ms.openlocfilehash: 0248e48865541a7c73b9e219a06a57996c5cf601
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400521"
---
# <a name="tutorial-create-a-net-core-console-application-using-visual-studio-for-mac"></a><span data-ttu-id="98f8e-103">教程：使用 Visual Studio for Mac 创建 .NET Core 控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="98f8e-103">Tutorial: Create a .NET Core console application using Visual Studio for Mac</span></span>

<span data-ttu-id="98f8e-104">本教程演示如何使用 Visual Studio for Mac 创建和运行 .NET Core 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="98f8e-104">This tutorial shows how to create and run a .NET Core console application using Visual Studio for Mac.</span></span>

> [!NOTE]
> <span data-ttu-id="98f8e-105">你的反馈非常有价值。</span><span class="sxs-lookup"><span data-stu-id="98f8e-105">Your feedback is highly valued.</span></span> <span data-ttu-id="98f8e-106">有两种方法可以向开发团队提供有关 Visual Studio for Mac 的反馈：</span><span class="sxs-lookup"><span data-stu-id="98f8e-106">There are two ways you can provide feedback to the development team on Visual Studio for Mac:</span></span>
>
> * <span data-ttu-id="98f8e-107">在 Visual Studio for Mac 中，从菜单中选择“帮助” > “报告问题”，或从欢迎屏幕中选择“报告问题”，将打开一个窗口，以供填写 bug 报告。</span><span class="sxs-lookup"><span data-stu-id="98f8e-107">In Visual Studio for Mac, select **Help** > **Report a Problem** from the menu or **Report a Problem** from the Welcome screen, which will open a window for filing a bug report.</span></span> <span data-ttu-id="98f8e-108">可在[开发人员社区](https://aka.ms/feedback/report?space=41)门户中跟踪自己的反馈。</span><span class="sxs-lookup"><span data-stu-id="98f8e-108">You can track your feedback in the [Developer Community](https://aka.ms/feedback/report?space=41) portal.</span></span>
> * <span data-ttu-id="98f8e-109">若要提出建议，从菜单中选择“帮助” > “提供建议”，或从欢迎屏幕中选择“提供建议”，转到 [Visual Studio for Mac 开发人员社区网页](https://aka.ms/feedback/suggest?space=41)。</span><span class="sxs-lookup"><span data-stu-id="98f8e-109">To make a suggestion, select **Help** > **Provide a Suggestion** from the menu or **Provide a Suggestion** from the Welcome screen, which will take you to the [Visual Studio for Mac Developer Community webpage](https://aka.ms/feedback/suggest?space=41).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98f8e-110">先决条件</span><span class="sxs-lookup"><span data-stu-id="98f8e-110">Prerequisites</span></span>

* <span data-ttu-id="98f8e-111">[Visual Studio for Mac 版本 8.6 或更高版本](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。</span><span class="sxs-lookup"><span data-stu-id="98f8e-111">[Visual Studio for Mac version 8.6 or later](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link).</span></span> <span data-ttu-id="98f8e-112">选择用于安装 .NET Core 的选项。</span><span class="sxs-lookup"><span data-stu-id="98f8e-112">Select the option to install .NET Core.</span></span> <span data-ttu-id="98f8e-113">安装 Xamarin 对于 .NET Core 开发而言是可选项。</span><span class="sxs-lookup"><span data-stu-id="98f8e-113">Installing Xamarin is optional for .NET Core development.</span></span> <span data-ttu-id="98f8e-114">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="98f8e-114">For more information, see the following resources:</span></span>

  * <span data-ttu-id="98f8e-115">[教程：安装 Visual Studio for Mac](/visualstudio/mac/installation)。</span><span class="sxs-lookup"><span data-stu-id="98f8e-115">[Tutorial: Install Visual Studio for Mac](/visualstudio/mac/installation).</span></span>
  * <span data-ttu-id="98f8e-116">[支持的 macOS 版本](../install/windows.md)。</span><span class="sxs-lookup"><span data-stu-id="98f8e-116">[Supported macOS versions](../install/windows.md).</span></span>
  * <span data-ttu-id="98f8e-117">[Visual Studio for Mac 支持的 .NET Core 版本](/visualstudio/mac/net-core-support)。</span><span class="sxs-lookup"><span data-stu-id="98f8e-117">[.NET Core versions supported by Visual Studio for Mac](/visualstudio/mac/net-core-support).</span></span>

## <a name="create-the-app"></a><span data-ttu-id="98f8e-118">创建应用</span><span class="sxs-lookup"><span data-stu-id="98f8e-118">Create the app</span></span>

<span data-ttu-id="98f8e-119">创建一个名为“HelloWorld”的 .NET Core 控制台应用项目。</span><span class="sxs-lookup"><span data-stu-id="98f8e-119">Create a .NET Core console app project named "HelloWorld".</span></span>

1. <span data-ttu-id="98f8e-120">启动 Visual Studio for Mac。</span><span class="sxs-lookup"><span data-stu-id="98f8e-120">Start Visual Studio for Mac.</span></span>

1. <span data-ttu-id="98f8e-121">在“开始”窗口中，选择“新建”。</span><span class="sxs-lookup"><span data-stu-id="98f8e-121">Select **New** in the start window.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-project.png" alt-text="Visual Studio for Mac 开始屏幕上的“新建”按钮":::

1. <span data-ttu-id="98f8e-123">在“新建项目”对话框中，选择“Web 和控制台”节点下的“应用”。</span><span class="sxs-lookup"><span data-stu-id="98f8e-123">In the **New Project** dialog, select **App** under the **Web and Console** node.</span></span> <span data-ttu-id="98f8e-124">选择“控制台应用程序”模板，然后选择“下一步” 。</span><span class="sxs-lookup"><span data-stu-id="98f8e-124">Select the **Console Application** template, and select **Next**.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-dialog.png" alt-text="新项目模板列表":::

1. <span data-ttu-id="98f8e-126">在“配置新的控制台应用程序”对话框的“目标框架”下拉列表中，选择“.NET Core 3.1”，然后选择“下一步”   。</span><span class="sxs-lookup"><span data-stu-id="98f8e-126">In the **Target Framework** drop-down of the **Configure your new Console Application** dialog, select **.NET Core 3.1** , and select **Next**.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/target-framework.png" alt-text="选择目标框架":::

1. <span data-ttu-id="98f8e-128">键入“HelloWorld”作为“项目名称”，然后选择“创建” 。</span><span class="sxs-lookup"><span data-stu-id="98f8e-128">Type "HelloWorld" for the **Project Name** , and select **Create**.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-new-options.png" alt-text="“配置新的控制台应用程序”对话框":::

<span data-ttu-id="98f8e-130">用于创建简单的“Hello World”应用程序的模板。</span><span class="sxs-lookup"><span data-stu-id="98f8e-130">The template creates a simple "Hello World" application.</span></span> <span data-ttu-id="98f8e-131">它会调用 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 方法来显示“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="98f8e-131">It calls the <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> method to display "Hello World!"</span></span> <span data-ttu-id="98f8e-132">（在终端窗口中）。</span><span class="sxs-lookup"><span data-stu-id="98f8e-132">in the terminal window.</span></span>

<span data-ttu-id="98f8e-133">模板代码将定义类 `Program`，其中包含一个将 <xref:System.String> 数组用作参数的方法 `Main`：</span><span class="sxs-lookup"><span data-stu-id="98f8e-133">The template code defines a class, `Program`, with a single method, `Main`, that takes a <xref:System.String> array as an argument:</span></span>

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

<span data-ttu-id="98f8e-134">`Main` 是应用程序入口点，同时也是在应用程序启动时由运行时自动调用的方法。</span><span class="sxs-lookup"><span data-stu-id="98f8e-134">`Main` is the application entry point, the method that's called automatically by the runtime when it launches the application.</span></span> <span data-ttu-id="98f8e-135">`args` 数组中包含在应用程序启动时提供的所有命令行参数。</span><span class="sxs-lookup"><span data-stu-id="98f8e-135">Any command-line arguments supplied when the application is launched are available in the `args` array.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="98f8e-136">运行应用</span><span class="sxs-lookup"><span data-stu-id="98f8e-136">Run the app</span></span>

1. <span data-ttu-id="98f8e-137">按 <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) 以运行应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="98f8e-137">Press <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) to run the app without debugging.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/visual-studio-mac-output.png" alt-text="终端显示 Hello World!":::

1. <span data-ttu-id="98f8e-139">关闭终端窗口。</span><span class="sxs-lookup"><span data-stu-id="98f8e-139">Close the **Terminal** window.</span></span>

## <a name="enhance-the-app"></a><span data-ttu-id="98f8e-140">增强应用</span><span class="sxs-lookup"><span data-stu-id="98f8e-140">Enhance the app</span></span>

<span data-ttu-id="98f8e-141">改进应用程序，使其提示用户输入名字，并将其与日期和时间一同显示。</span><span class="sxs-lookup"><span data-stu-id="98f8e-141">Enhance the application to prompt the user for their name and display it along with the date and time.</span></span>

1. <span data-ttu-id="98f8e-142">在 Program.cs 中，将 `Main` 方法的内容（是调用 `Console.WriteLine` 的行）替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="98f8e-142">In *Program.cs* , replace the contents of the `Main` method, which is the line that calls `Console.WriteLine`, with the following code:</span></span>

   :::code language="csharp" source="./snippets/with-visual-studio/csharp/Program.cs" id="MainMethod":::

   <span data-ttu-id="98f8e-143">此代码会在控制台窗口中显示一条提示，然后等待用户输入字符串并按 <kbd>Enter</kbd>。</span><span class="sxs-lookup"><span data-stu-id="98f8e-143">This code displays a prompt in the console window and waits until the user enters a string followed by the <kbd>enter</kbd> key.</span></span> <span data-ttu-id="98f8e-144">它会将此字符串存储到名为 `name` 的变量中。</span><span class="sxs-lookup"><span data-stu-id="98f8e-144">It stores this string in a variable named `name`.</span></span> <span data-ttu-id="98f8e-145">它还会检索 <xref:System.DateTime.Now?displayProperty=nameWithType> 属性的值（其中包含当前的本地时间），并将此值赋给 `date` 变量。</span><span class="sxs-lookup"><span data-stu-id="98f8e-145">It also retrieves the value of the <xref:System.DateTime.Now?displayProperty=nameWithType> property, which contains the current local time, and assigns it to a variable named `date`.</span></span> <span data-ttu-id="98f8e-146">同时会在控制台窗口中显示这些值。</span><span class="sxs-lookup"><span data-stu-id="98f8e-146">And it displays these values in the console window.</span></span> <span data-ttu-id="98f8e-147">最后会在控制台窗口中显示一条提示，并调用 <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> 方法来等待用户输入。</span><span class="sxs-lookup"><span data-stu-id="98f8e-147">Finally, it displays a prompt in the console window and calls the <xref:System.Console.ReadKey(System.Boolean)?displayProperty=nameWithType> method to wait for user input.</span></span>

   <span data-ttu-id="98f8e-148">`\n` 表示一个换行符。</span><span class="sxs-lookup"><span data-stu-id="98f8e-148">The `\n` represents a newline character.</span></span>

   <span data-ttu-id="98f8e-149">字符串前面的美元符号 (`$`) 使你可以将表达式（如变量名称）放入字符串中的大括号内。</span><span class="sxs-lookup"><span data-stu-id="98f8e-149">The dollar sign (`$`) in front of a string lets you put expressions such as variable names in curly braces in the string.</span></span> <span data-ttu-id="98f8e-150">表达式值将代替表达式插入到字符串中。</span><span class="sxs-lookup"><span data-stu-id="98f8e-150">The expression value is inserted into the string in place of the expression.</span></span> <span data-ttu-id="98f8e-151">此语法称为[内插字符串](../../csharp/language-reference/tokens/interpolated.md)。</span><span class="sxs-lookup"><span data-stu-id="98f8e-151">This syntax is referred to as [interpolated strings](../../csharp/language-reference/tokens/interpolated.md).</span></span>

1. <span data-ttu-id="98f8e-152">按 <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) 以运行应用。</span><span class="sxs-lookup"><span data-stu-id="98f8e-152">Press <kbd>⌥</kbd><kbd>⌘</kbd><kbd>↵</kbd> (<kbd>option</kbd>+<kbd>command</kbd>+<kbd>enter</kbd>) to run the app.</span></span>

1. <span data-ttu-id="98f8e-153">输入名称并按 <kbd>Enter</kbd>，从而响应提示。</span><span class="sxs-lookup"><span data-stu-id="98f8e-153">Respond to the prompt by entering a name and pressing <kbd>enter</kbd>.</span></span>

   :::image type="content" source="media/with-visual-studio-mac/hello-world-update.png" alt-text="终端显示经过修改的程序输出":::

1. <span data-ttu-id="98f8e-155">关闭终端。</span><span class="sxs-lookup"><span data-stu-id="98f8e-155">Close the terminal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98f8e-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="98f8e-156">Next steps</span></span>

<span data-ttu-id="98f8e-157">在本教程中，你创建了一个 .NET Core 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="98f8e-157">In this tutorial, you created a .NET Core console application.</span></span> <span data-ttu-id="98f8e-158">在下一教程中，你将调试该应用。</span><span class="sxs-lookup"><span data-stu-id="98f8e-158">In the next tutorial, you debug the app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98f8e-159">使用 Visual Studio for Mac 调试 .NET Core 控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="98f8e-159">Debug a .NET Core console application using Visual Studio for Mac</span></span>](debugging-with-visual-studio-mac.md)
