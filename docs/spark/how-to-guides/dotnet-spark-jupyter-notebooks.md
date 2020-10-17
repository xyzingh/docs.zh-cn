---
title: 使用 Jupyter Notebook
titleSuffix: .NET for Apache Spark
description: 在 Jupyter Notebook、Jupyter Lab 或 Visual Studio Code (VS Code) 等交互式环境中使用 .NET for Apache Spark
ms.author: luquinta
author: luisquintanilla
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc, how-to
ms.openlocfilehash: 38263c5ce4d1686777f33f5a9742d530eafa9d89
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955688"
---
# <a name="use-net-for-apache-spark-in-jupyter-notebooks"></a><span data-ttu-id="77fad-103">在 Jupyter 笔记本中使用 .NET for Apache Spark</span><span class="sxs-lookup"><span data-stu-id="77fad-103">Use .NET for Apache Spark in Jupyter notebooks</span></span>

<span data-ttu-id="77fad-104">本文介绍如何在 Jupyter Notebook 和 Visual Studio Code (VS Code) 中使用 .NET Interactive 以交互方式运行 .NET for Apache Spark。</span><span class="sxs-lookup"><span data-stu-id="77fad-104">In this article, you learn how to run .NET for Apache Spark jobs interactively in Jupyter Notebook and Visual Studio Code (VS Code) with .NET Interactive.</span></span>

## <a name="about-jupyter"></a><span data-ttu-id="77fad-105">关于 Jupyter</span><span class="sxs-lookup"><span data-stu-id="77fad-105">About Jupyter</span></span>

<span data-ttu-id="77fad-106">[Jupyter](https://jupyter.org/) 是一种开源的跨平台计算环境，可让用户以交互方式构建和开发应用程序。</span><span class="sxs-lookup"><span data-stu-id="77fad-106">[Jupyter](https://jupyter.org/) is an open-source, cross-platform computing environment that provides a way for users to prototype and develop applications interactively.</span></span> <span data-ttu-id="77fad-107">你可以通过各种界面（例如 Jupyter Notebook、Jupyter Lab 和 VS Code）与 Jupyter 交互。</span><span class="sxs-lookup"><span data-stu-id="77fad-107">You can interact with Jupyter through a wide variety of interfaces such as Jupyter Notebook, Jupyter Lab, and VS Code.</span></span>

<span data-ttu-id="77fad-108">在 .NET 上下文中，.net Core 全局工具 [.NET Interactive](https://github.com/dotnet/interactive) 提供了一个用于在 Jupyter Notebook 等交互式计算环境中编写 .NET 代码 (C#/F#) 的内核。</span><span class="sxs-lookup"><span data-stu-id="77fad-108">In the context of .NET, [.NET Interactive](https://github.com/dotnet/interactive), a .NET Core global tool, provides a kernel for writing .NET code (C#/F#) in interactive computing environments such as Jupyter Notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77fad-109">先决条件</span><span class="sxs-lookup"><span data-stu-id="77fad-109">Prerequisites</span></span>

- [<span data-ttu-id="77fad-110">.NET Core 3.1 SDK</span><span class="sxs-lookup"><span data-stu-id="77fad-110">.NET Core 3.1 SDK</span></span>](https://docs.microsoft.com/dotnet/core/install/)
- <span data-ttu-id="77fad-111">Apache Spark[](https://spark.apache.org/downloads.html)</span><span class="sxs-lookup"><span data-stu-id="77fad-111">[Apache Spark](https://spark.apache.org/downloads.html)</span></span>
- [<span data-ttu-id="77fad-112">Apache Spark .NET 工作器</span><span class="sxs-lookup"><span data-stu-id="77fad-112">Apache Spark .NET Worker</span></span>](https://github.com/dotnet/spark/releases)

<span data-ttu-id="77fad-113">请参阅[入门教程](../tutorials/get-started.md)，详细了解如何设置 .NET for Apache Spark 环境。</span><span class="sxs-lookup"><span data-stu-id="77fad-113">See the [getting started tutorial](../tutorials/get-started.md) for more information on setting up your .NET for Apache Spark environment.</span></span>

## <a name="prepare-environment"></a><span data-ttu-id="77fad-114">准备环境</span><span class="sxs-lookup"><span data-stu-id="77fad-114">Prepare environment</span></span>

<span data-ttu-id="77fad-115">若要使用 Jupyter Notebook，需要完成两项操作。</span><span class="sxs-lookup"><span data-stu-id="77fad-115">To work with Jupyter Notebooks, you'll need two things.</span></span>

1. <span data-ttu-id="77fad-116">安装 [.NET Interactive 全局 .NET 工具](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)</span><span class="sxs-lookup"><span data-stu-id="77fad-116">Install the [.NET Interactive global .NET tool](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)</span></span>
1. <span data-ttu-id="77fad-117">下载 `Microsoft.Spark` NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="77fad-117">Download the `Microsoft.Spark` NuGet package.</span></span>
    1. <span data-ttu-id="77fad-118">导航到 [Microsoft.Spark](https://www.nuget.org/packages/Microsoft.Spark/) NuGet 包页面。</span><span class="sxs-lookup"><span data-stu-id="77fad-118">Navigate to the [Microsoft.Spark](https://www.nuget.org/packages/Microsoft.Spark/) NuGet package page.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="77fad-119">默认下载最新版本的包。</span><span class="sxs-lookup"><span data-stu-id="77fad-119">By default, the latest version of the package is downloaded.</span></span> <span data-ttu-id="77fad-120">**请确保下载的版本与 Apache Spark .NET 工作器版本相同。**</span><span class="sxs-lookup"><span data-stu-id="77fad-120">**Make sure that the version you download is the same as your Apache Spark .NET Worker.**</span></span>

    1. <span data-ttu-id="77fad-121">在“信息”窗格中，选择“下载包”以下载最新版本的包 。</span><span class="sxs-lookup"><span data-stu-id="77fad-121">In the **Info** pane, select **Download package** to download the latest version of the package.</span></span> <span data-ttu-id="77fad-122">包的名称类似于 microsoft.spark.[PACKAGE-VERSION].nupkg。</span><span class="sxs-lookup"><span data-stu-id="77fad-122">The name of the package is similar to  *microsoft.spark.[PACKAGE-VERSION].nupkg*.</span></span>
    1. <span data-ttu-id="77fad-123">解压缩下载的包。</span><span class="sxs-lookup"><span data-stu-id="77fad-123">Unzip the downloaded package.</span></span> <span data-ttu-id="77fad-124">解压缩的目录应包含名为 jars 的子目录。</span><span class="sxs-lookup"><span data-stu-id="77fad-124">The unzipped directory should contain a subdirectory called *jars*.</span></span> <span data-ttu-id="77fad-125">记下该路径，因为稍后将使用它。</span><span class="sxs-lookup"><span data-stu-id="77fad-125">Take note of the path since it's used at a later time.</span></span>

## <a name="start-net-for-apache-spark"></a><span data-ttu-id="77fad-126">启动 .NET for Apache Spark</span><span class="sxs-lookup"><span data-stu-id="77fad-126">Start .NET for Apache Spark</span></span>

<span data-ttu-id="77fad-127">运行以下命令，在调试模式下启动 .NET for Apache Spark。</span><span class="sxs-lookup"><span data-stu-id="77fad-127">Run the following command to start .NET for Apache Spark in debug mode.</span></span> <span data-ttu-id="77fad-128">此 `spark-submit` 命令启动一个进程，并等待来自 [SparkSession](xref:Microsoft.Spark.Sql.SparkSession) 的连接。</span><span class="sxs-lookup"><span data-stu-id="77fad-128">This `spark-submit` command starts a process and waits for connections from a [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).</span></span> <span data-ttu-id="77fad-129">确保为正在使用的相应版本的 .NET for Apache Spark 提供 `microsoft-spark-<version>.jar` 路径。</span><span class="sxs-lookup"><span data-stu-id="77fad-129">Make sure to provide the path to the `microsoft-spark-<version>.jar` for the respective version of .NET for Apache Spark you're using.</span></span>

<span data-ttu-id="77fad-130">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="77fad-130">**Ubuntu**</span></span>

```bash
spark-submit \
    --class org.apache.spark.deploy.dotnet.DotnetRunner \
    --master local \
    <path-to-microsoft-spark-jar> \
    debug
```

<span data-ttu-id="77fad-131">**Windows**</span><span class="sxs-lookup"><span data-stu-id="77fad-131">**Windows**</span></span>

```cmd
spark-submit ^
    --class org.apache.spark.deploy.dotnet.DotnetRunner ^
    --master local ^
    <path-to-microsoft-spark-jar> ^
    debug
```

## <a name="create-a-notebook"></a><span data-ttu-id="77fad-132">创建笔记本</span><span class="sxs-lookup"><span data-stu-id="77fad-132">Create a notebook</span></span>

<span data-ttu-id="77fad-133">你可以使用不同的界面与 Jupyter 交互。</span><span class="sxs-lookup"><span data-stu-id="77fad-133">You can use different interfaces to interact with Jupyter.</span></span> <span data-ttu-id="77fad-134">若要使用基于浏览器的界面，请使用 Jupyter Notebook 或 Jupyter Lab。</span><span class="sxs-lookup"><span data-stu-id="77fad-134">For a browser-based interface, use Jupyter Notebooks or Jupyter Lab.</span></span> <span data-ttu-id="77fad-135">若要体验本地编辑器，请使用 VS Code。</span><span class="sxs-lookup"><span data-stu-id="77fad-135">For a local editor experience, use VS Code.</span></span>

### <a name="jupyter-notebooks--jupyter-lab"></a><span data-ttu-id="77fad-136">Jupyter Notebooks 和 Jupyter Lab</span><span class="sxs-lookup"><span data-stu-id="77fad-136">Jupyter Notebooks & Jupyter Lab</span></span>

1. <span data-ttu-id="77fad-137">在另一个命令提示符处，使用以下命令之一启动 Jupyter Notebook 或 Jupyter Lab：</span><span class="sxs-lookup"><span data-stu-id="77fad-137">In another command prompt, start Jupyter Notebook or Jupyter Lab using one of the commands below:</span></span>

    <span data-ttu-id="77fad-138">**Jupyter 笔记本**</span><span class="sxs-lookup"><span data-stu-id="77fad-138">**Jupyter Notebook**</span></span>

    ```bash
    jupyter notebook
    ```

    <span data-ttu-id="77fad-139">**Jupyter Lab**</span><span class="sxs-lookup"><span data-stu-id="77fad-139">**Jupyter Lab**</span></span>

    ```bash
    jupyter lab
    ```

    <span data-ttu-id="77fad-140">这些命令将使用 Jupyter Notebook 或 Jupyter Lab 界面启动浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="77fad-140">These commands launch a browser window with the Jupyter Notebook or Jupyter Lab interface.</span></span>

1. <span data-ttu-id="77fad-141">在浏览器中，创建新笔记本。</span><span class="sxs-lookup"><span data-stu-id="77fad-141">In the browser, create a new notebook.</span></span>

    <span data-ttu-id="77fad-142">**Jupyter 笔记本**</span><span class="sxs-lookup"><span data-stu-id="77fad-142">**Jupyter Notebook**</span></span>

    <span data-ttu-id="77fad-143">选择“新建”>“.NET (C#)”或“新建”>“.NET (F#)” </span><span class="sxs-lookup"><span data-stu-id="77fad-143">Select **New > .NET (C#)** or **New > .NET (F#)**</span></span>

    <span data-ttu-id="77fad-144">**Jupyter Lab**</span><span class="sxs-lookup"><span data-stu-id="77fad-144">**Jupyter Lab**</span></span>

    <span data-ttu-id="77fad-145">在启动器窗口中，选择 .NET (C#) 或 .NET (F#) </span><span class="sxs-lookup"><span data-stu-id="77fad-145">In the Launcher window, select **.NET (C#)** or **.NET (F#)**</span></span>

### <a name="visual-studio-code-preview"></a><span data-ttu-id="77fad-146">Visual Studio Code（预览）</span><span class="sxs-lookup"><span data-stu-id="77fad-146">Visual Studio Code (preview)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77fad-147">若要在 VS Code 中使用 Jupyter Notebook，必须安装以下各项：</span><span class="sxs-lookup"><span data-stu-id="77fad-147">To use Jupyter Notebooks in VS Code, you have to install:</span></span>
>
>- [<span data-ttu-id="77fad-148">VS Code Insiders</span><span class="sxs-lookup"><span data-stu-id="77fad-148">VS Code Insiders</span></span>](https://code.visualstudio.com/insiders/)
>- [<span data-ttu-id="77fad-149"> 扩展</span><span class="sxs-lookup"><span data-stu-id="77fad-149">.NET Interactive Notebooks extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)

1. <span data-ttu-id="77fad-150">打开 VS Code。</span><span class="sxs-lookup"><span data-stu-id="77fad-150">Open VS Code.</span></span>
1. <span data-ttu-id="77fad-151">打开命令面板“查看”>“命令面板”。</span><span class="sxs-lookup"><span data-stu-id="77fad-151">Open the command palette **View > Command Palette**.</span></span>

    <span data-ttu-id="77fad-152">出现命令面板时，输入以下命令以创建新的 .NET Interactive 笔记本：</span><span class="sxs-lookup"><span data-stu-id="77fad-152">When the command palette appears, enter the following command to create a new .NET Interactive notebook:</span></span>

    ```text
    >.NET Interactive: Create new blank notebook
    ```

    <span data-ttu-id="77fad-153">或者，如果想要使用 ipynb 扩展打开现有的 .NET 交互式笔记本，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="77fad-153">Alternatively, if you want to open an existing .NET Interactive notebook with the *.ipynb* extension, use the following command:</span></span>

    ```text
    >.NET Interactive: Open notebook
    ```

## <a name="initialize-a-spark-session"></a><span data-ttu-id="77fad-154">初始化 Spark 会话</span><span class="sxs-lookup"><span data-stu-id="77fad-154">Initialize a Spark Session</span></span>

1. <span data-ttu-id="77fad-155">打开笔记本时，请安装 `Microsoft.Spark` NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="77fad-155">When the notebook opens, install the `Microsoft.Spark` NuGet package.</span></span> <span data-ttu-id="77fad-156">请确保安装的版本与 .NET 工作器版本相同。</span><span class="sxs-lookup"><span data-stu-id="77fad-156">Make sure the version you install is the same as the .NET Worker.</span></span>

    ```text
    #r "nuget:Microsoft.Spark, 0.12.1"
    ```

1. <span data-ttu-id="77fad-157">向笔记本添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="77fad-157">Add the following using statement to the notebook.</span></span>

    ```csharp
    using Microsoft.Spark.Sql;
    ```

1. <span data-ttu-id="77fad-158">初始化 [SparkSession](xref:Microsoft.Spark.Sql.SparkSession)。</span><span class="sxs-lookup"><span data-stu-id="77fad-158">Initialize your [SparkSession](xref:Microsoft.Spark.Sql.SparkSession).</span></span>

    ```csharp
    var sparkSession =
    SparkSession
        .Builder()
        .AppName("dotnet-interactive-spark")
        .GetOrCreate();
    ```

<span data-ttu-id="77fad-159">笔记本应与下图中的类似。</span><span class="sxs-lookup"><span data-stu-id="77fad-159">The notebook should look similar to the one in the following image.</span></span> <span data-ttu-id="77fad-160">此示例使用 VS Code，但 Jupyter Notebook 和 Jupyter Lab 应大致相同。</span><span class="sxs-lookup"><span data-stu-id="77fad-160">This example uses VS Code, but Jupyter Notebook and Jupyter Lab should look about the same.</span></span>

> [!div class="mx-imgBorder"]
<span data-ttu-id="77fad-161">![.NET for Apache Spark Jupyter Notebook VS Code](media/dotnet-spark-jupyter-notebooks/jupyter-notebooks-dotnet-spark-vscode.png)</span><span class="sxs-lookup"><span data-stu-id="77fad-161">![.NET for Apache Spark Jupyter Notebook VS Code](media/dotnet-spark-jupyter-notebooks/jupyter-notebooks-dotnet-spark-vscode.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="77fad-162">后续步骤</span><span class="sxs-lookup"><span data-stu-id="77fad-162">Next Steps</span></span>

- [<span data-ttu-id="77fad-163">.NET for Apache Spark 入门</span><span class="sxs-lookup"><span data-stu-id="77fad-163">Get started with .NET for Apache Spark</span></span>](../tutorials/get-started.md)
- [<span data-ttu-id="77fad-164">使用 .NET for Apache Spark 和 ML.NET 预测情绪</span><span class="sxs-lookup"><span data-stu-id="77fad-164">Predict sentiment using .NET for Apache Spark and ML.NET</span></span>](../tutorials/ml-sentiment-analysis.md)
- <span data-ttu-id="77fad-165">如需详细了解 .NET Interactive，请参阅 [.NET 交互文档](https://github.com/dotnet/interactive/blob/main/docs/README.md)。</span><span class="sxs-lookup"><span data-stu-id="77fad-165">For more information on .NET Interactive, see the [.NET Interactive documentation](https://github.com/dotnet/interactive/blob/main/docs/README.md).</span></span>
