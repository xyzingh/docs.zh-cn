---
title: 将 .NET for Apache Spark 应用程序部署到 Azure HDInsight
description: 了解如何将 .NET for Apache Spark 应用程序部署到 HDInsight。
ms.date: 10/09/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: c745231f76142c11002ac6663906c8c44c69cdae
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223360"
---
# <a name="tutorial-deploy-a-net-for-apache-spark-application-to-azure-hdinsight"></a><span data-ttu-id="d0499-103">教程：将 .NET for Apache Spark 应用程序部署到 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0499-103">Tutorial: Deploy a .NET for Apache Spark application to Azure HDInsight</span></span>

<span data-ttu-id="d0499-104">本教程介绍如何通过 Azure HDInsight 群集将 .NET for Apache Spark 应用部署到云中。</span><span class="sxs-lookup"><span data-stu-id="d0499-104">This tutorial teaches you how to deploy your .NET for Apache Spark app to the cloud through an Azure HDInsight cluster.</span></span> <span data-ttu-id="d0499-105">由于 HDInsight 中的 Spark 群集与 Azure 存储和 Azure Data Lake Storage 兼容，因此使用 HDInsight，你可以更加容易地在 Azure 中创建和配置 Spark 群集。</span><span class="sxs-lookup"><span data-stu-id="d0499-105">HDInsight makes it easier to create and configure a Spark cluster in Azure since Spark clusters in HDInsight are compatible with Azure Storage and Azure Data Lake Storage.</span></span>

<span data-ttu-id="d0499-106">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="d0499-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="d0499-107">使用 Azure 存储资源管理器访问存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d0499-107">Access your storage accounts using Azure Storage Explorer.</span></span>
> * <span data-ttu-id="d0499-108">创建 Azure HDInsight 群集。</span><span class="sxs-lookup"><span data-stu-id="d0499-108">Create an Azure HDInsight cluster.</span></span>
> * <span data-ttu-id="d0499-109">发布 .NET for Apache Spark 应用。</span><span class="sxs-lookup"><span data-stu-id="d0499-109">Publish your .NET for Apache Spark app.</span></span>
> * <span data-ttu-id="d0499-110">创建并运行 HDInsight 脚本操作。</span><span class="sxs-lookup"><span data-stu-id="d0499-110">Create and run an HDInsight script action.</span></span>
> * <span data-ttu-id="d0499-111">在 HDInsight 群集上运行 .NET for Apache Spark 应用。</span><span class="sxs-lookup"><span data-stu-id="d0499-111">Run a .NET for Apache Spark app on an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0499-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="d0499-112">Prerequisites</span></span>

<span data-ttu-id="d0499-113">开始之前，请完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="d0499-113">Before you start, do the following tasks:</span></span>

* <span data-ttu-id="d0499-114">如果还没有 Azure 订阅，可以创建一个[免费帐户](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="d0499-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/dotnet/).</span></span>
* <span data-ttu-id="d0499-115">登录 [Azure 门户](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d0499-115">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
* <span data-ttu-id="d0499-116">在 [Windows](https://go.microsoft.com/fwlink/?LinkId=708343&clcid=0x409)、[Linux](https://go.microsoft.com/fwlink/?LinkId=722418&clcid=0x409) 或 [MacOS](https://go.microsoft.com/fwlink/?LinkId=708342&clcid=0x409) 计算机上安装 Azure 存储资源管理器。</span><span class="sxs-lookup"><span data-stu-id="d0499-116">Install Azure Storage Explorer on your [Windows](https://go.microsoft.com/fwlink/?LinkId=708343&clcid=0x409), [Linux](https://go.microsoft.com/fwlink/?LinkId=722418&clcid=0x409), or [MacOS](https://go.microsoft.com/fwlink/?LinkId=708342&clcid=0x409) computer.</span></span>
* <span data-ttu-id="d0499-117">完成 [.NET for Apache Spark - 10 分钟入门](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro)教程。</span><span class="sxs-lookup"><span data-stu-id="d0499-117">Complete the [.NET for Apache Spark - Get Started in 10-Minutes](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) tutorial.</span></span>

## <a name="access-your-storage-accounts"></a><span data-ttu-id="d0499-118">访问存储帐户</span><span class="sxs-lookup"><span data-stu-id="d0499-118">Access your storage accounts</span></span>

1. <span data-ttu-id="d0499-119">打开 Azure 存储资源管理器。</span><span class="sxs-lookup"><span data-stu-id="d0499-119">Open Azure Storage Explorer.</span></span>

2. <span data-ttu-id="d0499-120">在左侧菜单上选择“添加帐户”，并登录到 Azure 帐户  。</span><span class="sxs-lookup"><span data-stu-id="d0499-120">Select **Add Account** on the left menu, and sign in to your Azure account.</span></span>

    ![从存储资源管理器登录 Azure 帐户](./media/hdinsight-deployment/signin-azure-storage-explorer.png)

   <span data-ttu-id="d0499-122">登录后，应会看到你所拥有的所有存储帐户以及上传到存储帐户的所有资源。</span><span class="sxs-lookup"><span data-stu-id="d0499-122">After you sign in, you should see all storage accounts you have and any resources you have uploaded to your storage accounts.</span></span>

## <a name="create-an-hdinsight-cluster"></a><span data-ttu-id="d0499-123">创建 HDInsight 群集</span><span class="sxs-lookup"><span data-stu-id="d0499-123">Create an HDInsight cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0499-124">HDInsight 群集基于分钟按比例收费，即使你未使用它们也是如此。</span><span class="sxs-lookup"><span data-stu-id="d0499-124">Billing for HDInsight clusters is prorated per minute, even if you're not using them.</span></span> <span data-ttu-id="d0499-125">请务必在使用完之后删除群集。</span><span class="sxs-lookup"><span data-stu-id="d0499-125">Be sure to delete your cluster after you have finished using it.</span></span> <span data-ttu-id="d0499-126">有关详细信息，请参阅本教程的[清理资源](#clean-up-resources)部分。</span><span class="sxs-lookup"><span data-stu-id="d0499-126">For more information, see the [Clean up resources](#clean-up-resources) section of this tutorial.</span></span>

1. <span data-ttu-id="d0499-127">访问 [Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d0499-127">Visit the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d0499-128">选择“+ 创建资源”。 </span><span class="sxs-lookup"><span data-stu-id="d0499-128">Select **+ Create a resource** .</span></span> <span data-ttu-id="d0499-129">然后，从“Analytics”类别中选择“HDInsight”   。</span><span class="sxs-lookup"><span data-stu-id="d0499-129">Then, select **HDInsight** from the **Analytics** category.</span></span>

    ![从 Azure 门户创建 HDInsight 资源](./media/hdinsight-deployment/create-hdinsight-resource.png)

3. <span data-ttu-id="d0499-131">在“基本”下，提供以下值  ：</span><span class="sxs-lookup"><span data-stu-id="d0499-131">Under **Basics** , provide the following values:</span></span>

    |<span data-ttu-id="d0499-132">Property</span><span class="sxs-lookup"><span data-stu-id="d0499-132">Property</span></span>  |<span data-ttu-id="d0499-133">描述</span><span class="sxs-lookup"><span data-stu-id="d0499-133">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="d0499-134">订阅</span><span class="sxs-lookup"><span data-stu-id="d0499-134">Subscription</span></span>  | <span data-ttu-id="d0499-135">从下拉列表中选择一个可用 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="d0499-135">From the drop-down, choose one of your active Azure subscriptions.</span></span> |
    |<span data-ttu-id="d0499-136">资源组</span><span class="sxs-lookup"><span data-stu-id="d0499-136">Resource group</span></span> | <span data-ttu-id="d0499-137">指定是要创建新的资源组还是使用现有的资源组。</span><span class="sxs-lookup"><span data-stu-id="d0499-137">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="d0499-138">资源组是用于保存 Azure 解决方案相关资源的容器。</span><span class="sxs-lookup"><span data-stu-id="d0499-138">A resource group is a container that holds related resources for an Azure solution.</span></span> |
    |<span data-ttu-id="d0499-139">群集名称</span><span class="sxs-lookup"><span data-stu-id="d0499-139">Cluster name</span></span> | <span data-ttu-id="d0499-140">为 HDInsight Spark 群集命名。</span><span class="sxs-lookup"><span data-stu-id="d0499-140">Give a name to your HDInsight Spark cluster.</span></span>|
    |<span data-ttu-id="d0499-141">位置</span><span class="sxs-lookup"><span data-stu-id="d0499-141">Location</span></span>   | <span data-ttu-id="d0499-142">选择资源组的位置。</span><span class="sxs-lookup"><span data-stu-id="d0499-142">Select a location for the resource group.</span></span> <span data-ttu-id="d0499-143">模板将此位置用于创建群集，以及用于默认群集存储。</span><span class="sxs-lookup"><span data-stu-id="d0499-143">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span> |
    |<span data-ttu-id="d0499-144">群集类型</span><span class="sxs-lookup"><span data-stu-id="d0499-144">Cluster type</span></span>| <span data-ttu-id="d0499-145">选择“Spark”作为群集类型。 </span><span class="sxs-lookup"><span data-stu-id="d0499-145">Select **Spark** as the cluster type.</span></span>|
    |<span data-ttu-id="d0499-146">群集版本</span><span class="sxs-lookup"><span data-stu-id="d0499-146">Cluster version</span></span>|<span data-ttu-id="d0499-147">选择群集类型后，此字段中将自动填充默认版本。</span><span class="sxs-lookup"><span data-stu-id="d0499-147">This field will autopopulate with the default version once the cluster type has been selected.</span></span> <span data-ttu-id="d0499-148">选择 2.3 或 2.4 版本的 Spark。</span><span class="sxs-lookup"><span data-stu-id="d0499-148">Select a 2.3 or 2.4 version of Spark.</span></span>|
    |<span data-ttu-id="d0499-149">群集登录用户名</span><span class="sxs-lookup"><span data-stu-id="d0499-149">Cluster login username</span></span>| <span data-ttu-id="d0499-150">输入群集登录用户名。</span><span class="sxs-lookup"><span data-stu-id="d0499-150">Enter the cluster login username.</span></span>  <span data-ttu-id="d0499-151">默认名称为 *admin* 。</span><span class="sxs-lookup"><span data-stu-id="d0499-151">The default name is *admin* .</span></span> |
    |<span data-ttu-id="d0499-152">群集登录密码</span><span class="sxs-lookup"><span data-stu-id="d0499-152">Cluster login password</span></span>| <span data-ttu-id="d0499-153">输入任何登录密码。</span><span class="sxs-lookup"><span data-stu-id="d0499-153">Enter any login password.</span></span> |
    |<span data-ttu-id="d0499-154">安全外壳 (SSH) 用户名</span><span class="sxs-lookup"><span data-stu-id="d0499-154">Secure Shell (SSH) username</span></span>| <span data-ttu-id="d0499-155">输入 SSH 用户名。</span><span class="sxs-lookup"><span data-stu-id="d0499-155">Enter the SSH username.</span></span> <span data-ttu-id="d0499-156">默认情况下，此帐户的密码与群集登录用户名帐户的密码相同  。</span><span class="sxs-lookup"><span data-stu-id="d0499-156">By default, this account shares the same password as the *Cluster Login username* account.</span></span> |

4. <span data-ttu-id="d0499-157">在完成时选择“下一步:  存储 >>”转到“存储”页  。</span><span class="sxs-lookup"><span data-stu-id="d0499-157">Select **Next: Storage >>** to continue to the **Storage** page.</span></span> <span data-ttu-id="d0499-158">在“存储”下，提供以下值  ：</span><span class="sxs-lookup"><span data-stu-id="d0499-158">Under **Storage** , provide the following values:</span></span>

    |<span data-ttu-id="d0499-159">Property</span><span class="sxs-lookup"><span data-stu-id="d0499-159">Property</span></span>  |<span data-ttu-id="d0499-160">描述</span><span class="sxs-lookup"><span data-stu-id="d0499-160">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="d0499-161">主存储类型</span><span class="sxs-lookup"><span data-stu-id="d0499-161">Primary storage type</span></span>|<span data-ttu-id="d0499-162">使用默认值“Azure 存储”。 </span><span class="sxs-lookup"><span data-stu-id="d0499-162">Use the default value **Azure Storage** .</span></span>|
    |<span data-ttu-id="d0499-163">选择方法</span><span class="sxs-lookup"><span data-stu-id="d0499-163">Selection method</span></span>|<span data-ttu-id="d0499-164">使用默认值“从列表中选择”。 </span><span class="sxs-lookup"><span data-stu-id="d0499-164">Use the default value **Select from list** .</span></span>|
    |<span data-ttu-id="d0499-165">主存储帐户</span><span class="sxs-lookup"><span data-stu-id="d0499-165">Primary storage account</span></span>|<span data-ttu-id="d0499-166">选择订阅以及该订阅中的可用存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d0499-166">Choose your subscription and one of your active storage accounts within that subscription.</span></span>|
    |<span data-ttu-id="d0499-167">容器</span><span class="sxs-lookup"><span data-stu-id="d0499-167">Container</span></span>|<span data-ttu-id="d0499-168">此容器是存储帐户中特定的 blob 容器，群集在该容器中查找文件以在云中运行应用。</span><span class="sxs-lookup"><span data-stu-id="d0499-168">This container is the specific blob container in your storage account where your cluster looks for files to run your app in the cloud.</span></span> <span data-ttu-id="d0499-169">可使用任何可用名称为其命名。</span><span class="sxs-lookup"><span data-stu-id="d0499-169">You can give it any available name.</span></span>|

5. <span data-ttu-id="d0499-170">在“查看 + 创建”下，选择“创建”。  </span><span class="sxs-lookup"><span data-stu-id="d0499-170">Under **Review + create** , select **Create** .</span></span> <span data-ttu-id="d0499-171">创建群集大约需要 20 分钟时间。</span><span class="sxs-lookup"><span data-stu-id="d0499-171">It takes about 20 minutes to create the cluster.</span></span> <span data-ttu-id="d0499-172">必须先创建群集，才能继续执行下一步。</span><span class="sxs-lookup"><span data-stu-id="d0499-172">The cluster must be created before you can continue to the next step.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="d0499-173">发布你的应用</span><span class="sxs-lookup"><span data-stu-id="d0499-173">Publish your app</span></span>

<span data-ttu-id="d0499-174">接下来，发布在 [.NET for Apache Spark - 10 分钟入门](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro)教程中创建的 mySparkApp，以便 Spark 群集可以访问运行应用所需的所有文件  。</span><span class="sxs-lookup"><span data-stu-id="d0499-174">Next, you publish the *mySparkApp* created in the [.NET for Apache Spark - Get Started in 10-Minutes](https://dotnet.microsoft.com/learn/data/spark-tutorial/intro) tutorial, which gives your Spark cluster access to all the files it needs to run your app.</span></span>

1. <span data-ttu-id="d0499-175">运行以下命令以发布 mySparkApp  ：</span><span class="sxs-lookup"><span data-stu-id="d0499-175">Run the following commands to publish the *mySparkApp* :</span></span>

   <span data-ttu-id="d0499-176">在 Windows 上： </span><span class="sxs-lookup"><span data-stu-id="d0499-176">**On Windows:**</span></span>

   ```dotnetcli
   cd mySparkApp
   dotnet publish -c Release -f netcoreapp3.0 -r ubuntu.16.04-x64
   ```

   <span data-ttu-id="d0499-177">**在 Linux 上：**</span><span class="sxs-lookup"><span data-stu-id="d0499-177">**On Linux:**</span></span>

   ```bash
   cd mySparkApp
   foo@bar:~/path/to/app$ dotnet publish -c Release -f netcoreapp3.0 -r ubuntu.16.04-x64
   ```

2. <span data-ttu-id="d0499-178">执行以下任务以压缩已发布的应用文件，以便你可以轻松地将其上传到 HDInsight 群集。</span><span class="sxs-lookup"><span data-stu-id="d0499-178">Do the following tasks to zip your published app files so that you can easily upload them to your HDInsight cluster.</span></span> <span data-ttu-id="d0499-179">压缩发布文件夹（如 publish.zip）的内容，该文件夹是在步骤 1 中创建的。</span><span class="sxs-lookup"><span data-stu-id="d0499-179">Zip the contents of the publish folder, *publish.zip* for example, that was created as a result of Step 1.</span></span> <span data-ttu-id="d0499-180">所有程序集都应位于 ZIP 文件的第一层，并且不应有中间文件夹层。</span><span class="sxs-lookup"><span data-stu-id="d0499-180">All the assemblies should be in the first layer of the ZIP file and there should be no intermediate folder layer.</span></span> <span data-ttu-id="d0499-181">这意味着，当你解压缩 publish.zip 时，所有程序集都将被提取到当前工作目录中。</span><span class="sxs-lookup"><span data-stu-id="d0499-181">This means when you unzip *publish.zip* , all assemblies are extracted into your current working directory.</span></span>

   <span data-ttu-id="d0499-182">在 Windows 上：</span><span class="sxs-lookup"><span data-stu-id="d0499-182">**On Windows:**</span></span>

   <span data-ttu-id="d0499-183">使用提取程序（如 7-Zip 或 WinZip）将文件与所有已发布的二进制文件一起解压缩到 bin 目录中。</span><span class="sxs-lookup"><span data-stu-id="d0499-183">Use an extraction program, like 7-Zip or WinZip, to extract the file into the bin directory with all the published binaries.</span></span>

   <span data-ttu-id="d0499-184">**在 Linux 上，运行以下命令：**</span><span class="sxs-lookup"><span data-stu-id="d0499-184">**On Linux, run the following command:**</span></span>

   ```bash
   zip -r publish.zip
   ```

## <a name="upload-files-to-azure"></a><span data-ttu-id="d0499-185">将文件上传到 Azure</span><span class="sxs-lookup"><span data-stu-id="d0499-185">Upload files to Azure</span></span>

<span data-ttu-id="d0499-186">接下来，使用 Azure 存储资源管理器将以下五个文件上传到为群集存储选择的 blob 容器中：</span><span class="sxs-lookup"><span data-stu-id="d0499-186">Next, you use the Azure Storage Explorer to upload the following five files to the blob container you chose for your cluster's storage:</span></span>

* <span data-ttu-id="d0499-187">Microsoft.Spark.Worker</span><span class="sxs-lookup"><span data-stu-id="d0499-187">Microsoft.Spark.Worker</span></span>
* <span data-ttu-id="d0499-188">install-worker.sh</span><span class="sxs-lookup"><span data-stu-id="d0499-188">install-worker.sh</span></span>
* <span data-ttu-id="d0499-189">publish.zip</span><span class="sxs-lookup"><span data-stu-id="d0499-189">publish.zip</span></span>
* <span data-ttu-id="d0499-190">microsoft-spark-2.3.x-0.3.0.jar</span><span class="sxs-lookup"><span data-stu-id="d0499-190">microsoft-spark-2.3.x-0.3.0.jar</span></span>
* <span data-ttu-id="d0499-191">input.txt。</span><span class="sxs-lookup"><span data-stu-id="d0499-191">input.txt.</span></span>

1. <span data-ttu-id="d0499-192">打开 Azure 存储资源管理器，然后从左侧菜单导航到存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d0499-192">Open Azure Storage Explorer and navigate to your storage account from the left menu.</span></span> <span data-ttu-id="d0499-193">在存储帐户中的“Blob 容器”下，向下钻取到群集的 blob 容器  。</span><span class="sxs-lookup"><span data-stu-id="d0499-193">Drill down to the blob container for your cluster under **Blob Containers** in your storage account.</span></span>

2. <span data-ttu-id="d0499-194">Microsoft.Spark.Worker 可帮助 Apache Spark 执行你的应用，例如你可能已编写的任何用户定义函数 (UDF)。</span><span class="sxs-lookup"><span data-stu-id="d0499-194">*Microsoft.Spark.Worker* helps Apache Spark execute your app, such as any user-defined functions (UDFs) you may have written.</span></span> <span data-ttu-id="d0499-195">下载 [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases/download/v0.3.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.3.0.tar.gz)。</span><span class="sxs-lookup"><span data-stu-id="d0499-195">Download [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases/download/v0.3.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.3.0.tar.gz).</span></span> <span data-ttu-id="d0499-196">然后，在 Azure 存储资源管理器中选择“上传”以上传辅助角色  。</span><span class="sxs-lookup"><span data-stu-id="d0499-196">Then, select **Upload** in Azure Storage Explorer to upload the worker.</span></span>

   ![将文件上传到 Azure 存储资源管理器](./media/hdinsight-deployment/upload-files-to-storage.png)

3. <span data-ttu-id="d0499-198">install-worker.sh 是一个脚本，可使用该脚本将 .NET for Apache Spark 依赖项文件复制到群集的节点中。</span><span class="sxs-lookup"><span data-stu-id="d0499-198">The *install-worker.sh* is a script that lets you copy .NET for Apache Spark dependent files into the nodes of your cluster.</span></span>

   <span data-ttu-id="d0499-199">在本地计算机上创建一个名为 install-worker.sh 的新文件，并粘贴位于 GitHub 上的  。</span><span class="sxs-lookup"><span data-stu-id="d0499-199">Create a new file named **install-worker.sh** your local computer, and paste the [install-worker.sh contents](https://raw.githubusercontent.com/dotnet/spark/master/deployment/install-worker.sh) located on GitHub.</span></span> <span data-ttu-id="d0499-200">然后，将 install-worker.sh 上传到 blob 容器中  。</span><span class="sxs-lookup"><span data-stu-id="d0499-200">Then, upload *install-worker.sh* to your blob container.</span></span>

4. <span data-ttu-id="d0499-201">群集需要 publish.zip 文件，后者包含应用的已发布文件。</span><span class="sxs-lookup"><span data-stu-id="d0499-201">Your cluster needs the publish.zip file that contains your app's published files.</span></span> <span data-ttu-id="d0499-202">导航到已发布文件夹“mySparkApp/bin/Release/netcoreapp3.0/ubuntu.16.04-x64”，并找到“publish.zip”  。</span><span class="sxs-lookup"><span data-stu-id="d0499-202">Navigate to your published folder, **mySparkApp/bin/Release/netcoreapp3.0/ubuntu.16.04-x64** , and locate **publish.zip** .</span></span> <span data-ttu-id="d0499-203">然后，将 publish.zip 上传到 blob 容器  。</span><span class="sxs-lookup"><span data-stu-id="d0499-203">Then upload *publish.zip* to your blob container.</span></span>

5. <span data-ttu-id="d0499-204">群集需要已打包到 jar 文件中的应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="d0499-204">Your cluster needs the application code that was packaged into a jar file.</span></span> <span data-ttu-id="d0499-205">导航到已发布文件夹“mySparkApp/bin/Release/netcoreapp3.0/ubuntu.16.04-x64”，并找到“microsoft-spark-2.3.x-0.3.0.jar”  。</span><span class="sxs-lookup"><span data-stu-id="d0499-205">Navigate to your published folder, **mySparkApp/bin/Release/netcoreapp3.0/ubuntu.16.04-x64** , and locate **microsoft-spark-2.3.x-0.3.0.jar** .</span></span> <span data-ttu-id="d0499-206">然后，将 jar 文件上传到 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="d0499-206">Then, upload the jar file to your blob container.</span></span>

   <span data-ttu-id="d0499-207">对于 2.3.x 和 2.4.x 版的 Spark，可能存在多个 .jar 文件。</span><span class="sxs-lookup"><span data-stu-id="d0499-207">There may be multiple .jar files (for versions 2.3.x and 2.4.x of Spark).</span></span> <span data-ttu-id="d0499-208">你需要选择与在群集创建期间选择的 Spark 版本相匹配的 .jar 文件。</span><span class="sxs-lookup"><span data-stu-id="d0499-208">You need to choose the .jar file that matches the version of Spark you chose during cluster creation.</span></span> <span data-ttu-id="d0499-209">例如，如果在群集创建期间选择了 Spark 2.3.2，请选择 microsoft-spark-2.3.x-0.3.0.jar  。</span><span class="sxs-lookup"><span data-stu-id="d0499-209">For example, choose *microsoft-spark-2.3.x-0.3.0.jar* if you chose Spark 2.3.2 during cluster creation.</span></span>

6. <span data-ttu-id="d0499-210">群集需要应用的输入。</span><span class="sxs-lookup"><span data-stu-id="d0499-210">Your cluster needs the input to your app.</span></span> <span data-ttu-id="d0499-211">导航到 mySparkApp 目录，并找到“input.txt”  。</span><span class="sxs-lookup"><span data-stu-id="d0499-211">Navigate to your **mySparkApp** directory and locate **input.txt** .</span></span> <span data-ttu-id="d0499-212">将输入文件上传到 blob 容器中的 user/sshuser 目录  。</span><span class="sxs-lookup"><span data-stu-id="d0499-212">Upload your input file to the **user/sshuser** directory in your blob container.</span></span> <span data-ttu-id="d0499-213">你将通过 ssh 连接到群集，群集将在此文件夹中查找其输入。</span><span class="sxs-lookup"><span data-stu-id="d0499-213">You will be connecting to your cluster through ssh, and this folder is where your cluster looks for its input.</span></span> <span data-ttu-id="d0499-214">input.txt 文件是上传到特定目录的唯一文件  。</span><span class="sxs-lookup"><span data-stu-id="d0499-214">The *input.txt* file is the only file uploaded to a specific directory.</span></span>

## <a name="run-the-hdinsight-script-action"></a><span data-ttu-id="d0499-215">运行 HDInsight 脚本操作</span><span class="sxs-lookup"><span data-stu-id="d0499-215">Run the HDInsight script action</span></span>

<span data-ttu-id="d0499-216">群集运行并将文件上传到 Azure 后，可在群集上运行 install-worker.sh 脚本  。</span><span class="sxs-lookup"><span data-stu-id="d0499-216">Once your cluster is running and you've uploaded your files to Azure, you run the **install-worker.sh** script on the cluster.</span></span>

1. <span data-ttu-id="d0499-217">导航到 Azure 门户中的 HDInsight Spark 群集，然后选择“脚本操作”  。</span><span class="sxs-lookup"><span data-stu-id="d0499-217">Navigate to your HDInsight Spark cluster in Azure portal, and then select **Script actions** .</span></span>

2. <span data-ttu-id="d0499-218">选择“+ 提交新脚本”并提供以下值  ：</span><span class="sxs-lookup"><span data-stu-id="d0499-218">Select **+ Submit new** and provide the following values:</span></span>

   |<span data-ttu-id="d0499-219">属性</span><span class="sxs-lookup"><span data-stu-id="d0499-219">Property</span></span>  |<span data-ttu-id="d0499-220">描述</span><span class="sxs-lookup"><span data-stu-id="d0499-220">Description</span></span>  |
   |---------|---------|
   | <span data-ttu-id="d0499-221">脚本类型</span><span class="sxs-lookup"><span data-stu-id="d0499-221">Script type</span></span> |<span data-ttu-id="d0499-222">自定义</span><span class="sxs-lookup"><span data-stu-id="d0499-222">Custom</span></span>|
   | <span data-ttu-id="d0499-223">“属性”</span><span class="sxs-lookup"><span data-stu-id="d0499-223">Name</span></span> | <span data-ttu-id="d0499-224">安装辅助角色</span><span class="sxs-lookup"><span data-stu-id="d0499-224">Install Worker</span></span>|
   | <span data-ttu-id="d0499-225">Bash 脚本 URI</span><span class="sxs-lookup"><span data-stu-id="d0499-225">Bash script URI</span></span> |`https://mystorageaccount.blob.core.windows.net/mycontainer/install-worker.sh` </br> <span data-ttu-id="d0499-226">要确认此 URI，请在 Azure 存储资源管理器中右键单击“install-worker.sh”，然后选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="d0499-226">To confirm this URI, right-click on install-worker.sh in Azure Storage Explorer and select Properties.</span></span> |
   | <span data-ttu-id="d0499-227">节点类型</span><span class="sxs-lookup"><span data-stu-id="d0499-227">Node type(s)</span></span>| <span data-ttu-id="d0499-228">辅助角色</span><span class="sxs-lookup"><span data-stu-id="d0499-228">Worker</span></span>|
   | <span data-ttu-id="d0499-229">参数</span><span class="sxs-lookup"><span data-stu-id="d0499-229">Parameters</span></span> | <span data-ttu-id="d0499-230">azure</span><span class="sxs-lookup"><span data-stu-id="d0499-230">azure</span></span> </br> wasbs://mycontainer@myStorageAccount.blob.core.windows.net/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.6.0.tar.gz </br> <span data-ttu-id="d0499-231">/usr/local/bin</span><span class="sxs-lookup"><span data-stu-id="d0499-231">/usr/local/bin</span></span>

3. <span data-ttu-id="d0499-232">选择“创建”，提交脚本  。</span><span class="sxs-lookup"><span data-stu-id="d0499-232">Select **Create** to submit your script.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="d0499-233">运行应用</span><span class="sxs-lookup"><span data-stu-id="d0499-233">Run your app</span></span>

1. <span data-ttu-id="d0499-234">导航到 Azure 门户中的 HDInsight Spark 群集，然后选择“SSH + 群集登录名”  。</span><span class="sxs-lookup"><span data-stu-id="d0499-234">Navigate to your HDInsight Spark cluster in Azure portal, and then select **SSH + Cluster login** .</span></span>

2. <span data-ttu-id="d0499-235">复制 ssh 登录信息，并将登录名粘贴到终端。</span><span class="sxs-lookup"><span data-stu-id="d0499-235">Copy the ssh login information and paste the login into a terminal.</span></span> <span data-ttu-id="d0499-236">使用在群集创建期间设置的密码登录到群集。</span><span class="sxs-lookup"><span data-stu-id="d0499-236">Sign in to your cluster using the password you set during cluster creation.</span></span> <span data-ttu-id="d0499-237">应会看到“欢迎使用 Ubuntu 和 Spark”的消息。</span><span class="sxs-lookup"><span data-stu-id="d0499-237">You should see messages welcoming you to Ubuntu and Spark.</span></span>

3. <span data-ttu-id="d0499-238">使用 spark-submit 命令在 HDInsight 群集上运行应用  。</span><span class="sxs-lookup"><span data-stu-id="d0499-238">Use the **spark-submit** command to run your app on your HDInsight cluster.</span></span> <span data-ttu-id="d0499-239">请记得将示例脚本中的 mycontainer 和 mystorageaccount 替换为 blob 容器和存储帐户的实际名称  。</span><span class="sxs-lookup"><span data-stu-id="d0499-239">Remember to replace **mycontainer** and **mystorageaccount** in the example script with the actual names of your blob container and storage account.</span></span>

   ```bash
   $SPARK_HOME/bin/spark-submit \
   --master yarn \
   --class org.apache.spark.deploy.dotnet.DotnetRunner \
   wasbs://mycontainer@mystorageaccount.blob.core.windows.net/microsoft-spark-2.3.x-0.6.0.jar \
   wasbs://mycontainer@mystorageaccount.blob.core.windows.net/publish.zip mySparkApp
   ```

   <span data-ttu-id="d0499-240">应用运行时，你将在写入控制台的“本地运行入门”中看到相同的字数表。</span><span class="sxs-lookup"><span data-stu-id="d0499-240">When your app runs, you see the same word count table from the getting started local run written to the console.</span></span> <span data-ttu-id="d0499-241">恭喜，你已在云中运行了第一个 .NET for Apache Spark 应用程序！</span><span class="sxs-lookup"><span data-stu-id="d0499-241">Congratulations, you've run your first .NET for Apache Spark application in the cloud!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d0499-242">清理资源</span><span class="sxs-lookup"><span data-stu-id="d0499-242">Clean up resources</span></span>

<span data-ttu-id="d0499-243">HDInsight 将数据保存在 Azure 存储中，因此可以在群集不用时安全地删除群集。</span><span class="sxs-lookup"><span data-stu-id="d0499-243">HDInsight saves your data in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="d0499-244">此外，还需要支付 HDInsight 群集费用，即使未使用。</span><span class="sxs-lookup"><span data-stu-id="d0499-244">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="d0499-245">由于群集费用高于存储空间费用数倍，因此在不使用群集时将其删除可以节省费用。</span><span class="sxs-lookup"><span data-stu-id="d0499-245">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="d0499-246">还可以选择资源组名称来打开“资源组”页，然后选择“删除资源组”。</span><span class="sxs-lookup"><span data-stu-id="d0499-246">You can also select the resource group name to open the resource group page, and then select **Delete resource group** .</span></span> <span data-ttu-id="d0499-247">通过删除资源组，可以删除 HDInsight Spark 群集和默认存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d0499-247">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0499-248">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d0499-248">Next steps</span></span>

<span data-ttu-id="d0499-249">在本教程中，你已将 .NET for Apache Spark 应用程序部署到 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="d0499-249">In this tutorial, you deployed your .NET for Apache Spark application to Azure HDInsight.</span></span> <span data-ttu-id="d0499-250">要了解有关 HDInsight 的详细信息，请继续阅读 Azure HDInsight 文档。</span><span class="sxs-lookup"><span data-stu-id="d0499-250">To learn more about HDInsight, continue to the Azure HDInsight Documentation.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0499-251">Azure HDInsight 文档</span><span class="sxs-lookup"><span data-stu-id="d0499-251">Azure HDInsight Documentation</span></span>](/azure/hdinsight/)
