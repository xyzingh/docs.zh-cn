---
title: 从本地计算机连接到远程存储
description: 使用 .NET for Apache Spark 从本地计算机连接到 Azure 存储帐户。
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 09e92b0cae848f9c98b691a11842f131f613396b
ms.sourcegitcommit: eb7e87496f42361b1da98562dd75b516c9d58bbc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91877981"
---
# <a name="connect-to-azure-data-lake-storage-gen-2-or-wasb-account"></a><span data-ttu-id="41ec1-103">连接到 Azure Data Lake Storage Gen 2 或 WASB 帐户</span><span class="sxs-lookup"><span data-stu-id="41ec1-103">Connect to Azure Data Lake Storage Gen 2 or WASB account</span></span>

<span data-ttu-id="41ec1-104">本文介绍如何通过 Windows 计算机上本地运行的 [.NET for Apache Spark](https://github.com/dotnet/spark) 实例连接到 Azure Data Lake Storage (ADLS) Gen 2 或 Windows Azure Storage Blob (WASB) 帐户。</span><span class="sxs-lookup"><span data-stu-id="41ec1-104">In this article, you learn how to connect to an Azure Data Lake Storage (ADLS) Gen 2 or Windows Azure Storage Blob (WASB) account through an instance of [.NET for Apache Spark](https://github.com/dotnet/spark) running locally on your Windows machine.</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="41ec1-105">设置环境</span><span class="sxs-lookup"><span data-stu-id="41ec1-105">Set up the environment</span></span>

1. <span data-ttu-id="41ec1-106">请从[官方网站](https://archive.apache.org/dist/spark/)下载无 Hadoop 的 Apache Spark 分发版（选择一个 [.NET for Apache Spark](https://github.com/dotnet/spark#supported-apache-spark) 支持的版本），并将其解压缩到某个目录中。</span><span class="sxs-lookup"><span data-stu-id="41ec1-106">Download the Apache Spark distribution built without Hadoop from [official website](https://archive.apache.org/dist/spark/) (choose a version [supported by .NET for Apache Spark](https://github.com/dotnet/spark#supported-apache-spark)), and extract it to a directory.</span></span> <span data-ttu-id="41ec1-107">将 `SPARK_HOME` 环境变量设置为此目录。</span><span class="sxs-lookup"><span data-stu-id="41ec1-107">Set the environment variable `SPARK_HOME` to this directory.</span></span>
2. <span data-ttu-id="41ec1-108">从[此处](http://hadoop.apache.org/releases.html)下载 Apache Hadoop 二进制文件并将其解压缩到一个文件夹中，然后将 `HADOOP_HOME` 环境变量设置为此文件夹。</span><span class="sxs-lookup"><span data-stu-id="41ec1-108">Download the Apache Hadoop binary from [here](http://hadoop.apache.org/releases.html) and extract to a folder, and set your `HADOOP_HOME` environment variable to this folder.</span></span>
3. <span data-ttu-id="41ec1-109">从[此位置](https://github.com/cdarlint/winutils)下载 `winutils.exe` 和 `hadoop.dll` 文件（具体取决于上一步中安装的 Hadoop 版本），并将它们放在 Hadoop 的 bin 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="41ec1-109">Download the `winutils.exe` and `hadoop.dll` files from [this location](https://github.com/cdarlint/winutils) (depending on the version of Hadoop installed in the previous step) and put them in the bin folder of your Hadoop.</span></span> <span data-ttu-id="41ec1-110">Windows 上需要这些二进制文件才能正确设置所有内容（[此处的 Apache Wiki](https://cwiki.apache.org/confluence/display/HADOOP2/WindowsProblems) 对其进行了详细介绍）。</span><span class="sxs-lookup"><span data-stu-id="41ec1-110">These binaries are needed on Windows in order to get everything setup correctly (this is explained in detail in the [Apache wiki here](https://cwiki.apache.org/confluence/display/HADOOP2/WindowsProblems)).</span></span>
4. <span data-ttu-id="41ec1-111">对 `%HADOOP_HOME%\etc\hadoop\hadoop-env.cmd` 文件进行以下更改，以配置 Hadoop 安装：</span><span class="sxs-lookup"><span data-stu-id="41ec1-111">Configure your Hadoop installation by making the following changes to your `%HADOOP_HOME%\etc\hadoop\hadoop-env.cmd` file:</span></span>
    1. <span data-ttu-id="41ec1-112">使用 DOS 路径设置 `JAVA_HOME` 属性（因为 Hadoop 不太支持在 `JAVA_HOME` 中使用空格）。</span><span class="sxs-lookup"><span data-stu-id="41ec1-112">Set the `JAVA_HOME` property using the DOS path (since Hadoop doesn't like spaces in `JAVA_HOME`).</span></span> <span data-ttu-id="41ec1-113">具体类似如下：`C:\Progra~1\Java\jdk1.8.0_241`（指向本地计算机上安装的任何 Java 版本）。</span><span class="sxs-lookup"><span data-stu-id="41ec1-113">This should look something like this: `C:\Progra~1\Java\jdk1.8.0_241` (Pointing to whatever version of Java you have installed on your local machine).</span></span>
    2. <span data-ttu-id="41ec1-114">将 `%HADOOP_HOME%\share\hadoop\tools\lib\*` 追加到 `HADOOP_CLASSPATH`。</span><span class="sxs-lookup"><span data-stu-id="41ec1-114">Append `%HADOOP_HOME%\share\hadoop\tools\lib\*` to `HADOOP_CLASSPATH`.</span></span>
    <span data-ttu-id="41ec1-115">最终的 `hadoop-env.cmd` 文件应如下所示：</span><span class="sxs-lookup"><span data-stu-id="41ec1-115">Your final `hadoop-env.cmd` file should look something like this:</span></span>

    ![最终的 hadoop-env.cmd 文件](./media/connect-external-sources/hadoop-env.png)

## <a name="configure-your-storage-account-in-hadoop"></a><span data-ttu-id="41ec1-117">在 Hadoop 中配置存储帐户</span><span class="sxs-lookup"><span data-stu-id="41ec1-117">Configure your storage account in Hadoop</span></span>

1. <span data-ttu-id="41ec1-118">打开要通过 [Azure门户](https://portal.azure.com)连接的 ADLS Gen 2 或 WASB 存储帐户，然后打开“设置”边栏选项卡下的“访问密钥”面板，复制 key1 下的密钥值  。</span><span class="sxs-lookup"><span data-stu-id="41ec1-118">Open the ADLS Gen 2 or WASB storage account you want to connect to through the [Azure portal](https://portal.azure.com) and open the **Access keys** panel under the **Settings** blade and copy the value of **Key** from under key1.</span></span>
2. <span data-ttu-id="41ec1-119">现在，为了配置 Hadoop 以访问 ADLS Gen2 帐户，请务必编辑 `core-site.xml`（位于 `%HADOOP_HOME%\etc\hadoop\`）文件，其中包含群集范围的配置。</span><span class="sxs-lookup"><span data-stu-id="41ec1-119">Now in order to configure Hadoop to access your ADLS Gen2 account you would have to edit your `core-site.xml` (located in `%HADOOP_HOME%\etc\hadoop\` ) file which contains cluster-wide configuration.</span></span> <span data-ttu-id="41ec1-120">将以下属性添加到此文件中的 `<configuration>` 标记内：</span><span class="sxs-lookup"><span data-stu-id="41ec1-120">Add the following properties inside the `<configuration>` tags in this file:</span></span>

    ```xml
    <configuration>
      <property>
        <name>fs.azure.account.auth.type.YOUR_ACCOUNT_NAME.dfs.core.windows.net</name>
        <value>SharedKey</value>
        <description></description>
      </property>
      <property>
        <name>fs.azure.account.key.YOUR_ACCOUNT_NAME.dfs.core.windows.net</name>
        <value>YOUR ACCESS KEY (copied from Step 1)</value>
        <description>The secret password. Never share these.</description>
      </property>
    </configuration>
    ```

    <span data-ttu-id="41ec1-121">如果尝试连接到 WASB 帐户，请将属性名称中的 `dfs` 替换为 `blob`。</span><span class="sxs-lookup"><span data-stu-id="41ec1-121">If you are trying to connect to a WASB account, replace `dfs` with `blob` in the property names.</span></span> <span data-ttu-id="41ec1-122">例如，`fs.azure.account.auth.type.YOUR_ACCOUNT_NAME.blob.core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="41ec1-122">For example, `fs.azure.account.auth.type.YOUR_ACCOUNT_NAME.blob.core.windows.net`.</span></span>
3. <span data-ttu-id="41ec1-123">你可以在 `%HADOOP_HOME%` 目录中运行以下命令，通过 Hadoop 测试是否连接到存储帐户：</span><span class="sxs-lookup"><span data-stu-id="41ec1-123">You can test the connectivity to your Storage Account from Hadoop by running the following command from your `%HADOOP_HOME%` directory:</span></span>

    ```bash
    bin\hdfs dfs -ls <URI to your account>
    ```

<span data-ttu-id="41ec1-124">这会显示 URI 提供的路径中的所有文件/文件夹列表。</span><span class="sxs-lookup"><span data-stu-id="41ec1-124">This should display a list of all files/folders in the path provided by your URI.</span></span>

> [!NOTE]
> <span data-ttu-id="41ec1-125">为存储帐户派生 URI 的格式如下：</span><span class="sxs-lookup"><span data-stu-id="41ec1-125">The format to derive the URI to your Storage account is as follows:</span></span>
>
> ```
> For ADLS: abfs[s]://<file_system>@<account_name>.dfs.core.windows.net/<path>/<file_name>
> For WASB: wasb[s]://<file_system>@<account_name>.blob.core.windows.net/<path>/<file_name>
> ```

## <a name="connect-to-your-storage-account"></a><span data-ttu-id="41ec1-126">连接到你的存储帐户</span><span class="sxs-lookup"><span data-stu-id="41ec1-126">Connect to your storage account</span></span>

1. <span data-ttu-id="41ec1-127">如果以上命令正常运行，现可继续通过 Spark 访问此存储帐户。</span><span class="sxs-lookup"><span data-stu-id="41ec1-127">If the above command worked, you can now move on to accessing this storage account through Spark.</span></span> <span data-ttu-id="41ec1-128">首先从 `%HADOOP_HOME%` 中的命令行运行命令 `hadoop classpath`，然后复制输出。</span><span class="sxs-lookup"><span data-stu-id="41ec1-128">First run the command `hadoop classpath` from the commandline inside `%HADOOP_HOME%` and copy the output.</span></span>
2. <span data-ttu-id="41ec1-129">将步骤 1 中运行的命令的输出设置为环境变量 `SPARK_DIST_CLASSPATH` 的值。</span><span class="sxs-lookup"><span data-stu-id="41ec1-129">Set the output of the command run in Step 1 to the value of environment variable `SPARK_DIST_CLASSPATH`.</span></span>
3. <span data-ttu-id="41ec1-130">现在，你应该能够使用 abfs URI 通过 Spark .NET 访问 ADLS 或 WASB 存储帐户，如下面的简单示例所示。</span><span class="sxs-lookup"><span data-stu-id="41ec1-130">Now you should be able to access your ADLS or WASB storage account through Spark .NET using the abfs URI as shown in the simple example below.</span></span> <span data-ttu-id="41ec1-131">（在本例中，我们将使用每个 Apache Spark 安装中提供的标准 [`people.json`](https://github.com/apache/spark/blob/master/examples/src/main/resources/people.json) 示例文件）：</span><span class="sxs-lookup"><span data-stu-id="41ec1-131">(For this example we use the standard [`people.json`](https://github.com/apache/spark/blob/master/examples/src/main/resources/people.json) example file provided with every Apache Spark installation.):</span></span>

    ```csharp
    SparkSession spark = SparkSession
       .Builder()
       .AppName("Connect to Azure Storage locally")
       .GetOrCreate();
    DataFrame df = spark.Read().Json("wasbs://file_system@account_name.blob.core.windows.net/path/people.json");
    //DataFrame df = spark.Read().Json("abfss://file_system@account_name.dfs.core.windows.net/path/file.json");
    df.Show();
    ```

    <span data-ttu-id="41ec1-132">显示的结果为 DataFrame (`df`)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="41ec1-132">The result as displayed is the DataFrame (`df`) as shown below:</span></span>

    ```text
    +----+-------+
    | age|   name|
    +----+-------+
    |null|Michael|
    |  30|   Andy|
    |  19| Justin|
    +----+-------+
    ```
