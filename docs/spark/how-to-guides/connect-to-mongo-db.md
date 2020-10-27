---
title: 将 .NET for Apache Spark 连接到 MongoDB
description: 了解如何从 .NET for Apache Spark 应用程序连接到 MongoDB 实例。
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 928cc8e3559e13af66268f3d1b3766cf2df9041f
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223981"
---
# <a name="connect-net-for-apache-spark-to-mongodb"></a><span data-ttu-id="c731a-103">将 .NET for Apache Spark 连接到 MongoDB</span><span class="sxs-lookup"><span data-stu-id="c731a-103">Connect .NET for Apache Spark to MongoDB</span></span>

<span data-ttu-id="c731a-104">本文介绍如何从 .NET for Apache Spark 应用程序连接到 MongoDB 实例。</span><span class="sxs-lookup"><span data-stu-id="c731a-104">In this article, you learn how to connect to a MongoDB instance from your .NET for Apache Spark application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c731a-105">先决条件</span><span class="sxs-lookup"><span data-stu-id="c731a-105">Prerequisites</span></span>

1. <span data-ttu-id="c731a-106">启动并运行 MongoDB 服务器，向其添加一个[数据库和一些集合](https://docs.mongodb.com/manual/core/databases-and-collections/)（对于本地服务器，请下载[此社区服务器](https://www.mongodb.com/try/download/community)，或者对于 MongoDB 云服务，可以尝试 [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)。）</span><span class="sxs-lookup"><span data-stu-id="c731a-106">Have a MongoDB server up and running with a [database and some collection](https://docs.mongodb.com/manual/core/databases-and-collections/) added to it (Download [this community server](https://www.mongodb.com/try/download/community) for a local server or you can try [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) for a cloud MongoDB service.)</span></span>

## <a name="set-up-your-mongodb-instance"></a><span data-ttu-id="c731a-107">设置 MongoDB 实例</span><span class="sxs-lookup"><span data-stu-id="c731a-107">Set up your MongoDB instance</span></span>

<span data-ttu-id="c731a-108">若要让 .NET for Apache Spark 与 MongoDB 实例进行通信，你需要执行以下操作，确保它已正确设置：</span><span class="sxs-lookup"><span data-stu-id="c731a-108">In order to get .NET for Apache Spark to talk to your MongoDB instance you need to make sure it is set up correctly by doing the following:</span></span>

1. <span data-ttu-id="c731a-109">为应用程序创建一个用户名和密码以进行连接，并通过 mongo shell 使用以下命令为用户提供必要的权限/角色：</span><span class="sxs-lookup"><span data-stu-id="c731a-109">Create a username and password for your application to connect through, and give the user the necessary permissions/roles using the following command through mongo shell:</span></span>

    ```bash
    use database
    db.createUser(
      {
        user: "mySparkUser",
        pwd: "<password>",
        roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
      }
    )
    ```

2. <span data-ttu-id="c731a-110">请确保运行 .NET for Apache Spark 应用程序的计算机的 IP 地址已列入允许清单，以便 MongoDB 服务器能够连接。</span><span class="sxs-lookup"><span data-stu-id="c731a-110">Make sure the IP address of the machine your .NET for Apache Spark application is running on is whitelisted for the MongoDB server to be able to connect to.</span></span> <span data-ttu-id="c731a-111">你可以参考[本指南](https://docs.atlas.mongodb.com/security/add-ip-address-to-list/)了解如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c731a-111">You can refer to [this guide](https://docs.atlas.mongodb.com/security/add-ip-address-to-list/) to learn how to do that.</span></span>

## <a name="configure-your-net-for-apache-spark-application"></a><span data-ttu-id="c731a-112">配置 .NET for Apache Spark 应用程序</span><span class="sxs-lookup"><span data-stu-id="c731a-112">Configure your .NET for Apache Spark application</span></span>

1. <span data-ttu-id="c731a-113">设置以下变量，将应用程序配置为与 MongoDB 实例通信并从集合中读取。</span><span class="sxs-lookup"><span data-stu-id="c731a-113">Have the following variables set to configure your application to talk to the MongoDB instance and read from a collection.</span></span>
    1. <span data-ttu-id="c731a-114">**authURI** ："授权应用程序连接到所需 MongoDB 实例的连接字符串"。</span><span class="sxs-lookup"><span data-stu-id="c731a-114">**authURI** : "Connection string authorizing your application to connect to the required MongoDB instance".</span></span> <span data-ttu-id="c731a-115">其格式如下：</span><span class="sxs-lookup"><span data-stu-id="c731a-115">The format for that is as follows:</span></span>

        ```
        "mongodb+srv://<username>:<password>@<cluster_address>/<database>.<collection>"
        ```

    2. <span data-ttu-id="c731a-116">**username** ：在上一部分的步骤 1 中创建的帐户用户名</span><span class="sxs-lookup"><span data-stu-id="c731a-116">**username** : Username of the account you created in Step 1 of the previous section</span></span>
    3. <span data-ttu-id="c731a-117">**password** ：创建的用户帐户的密码</span><span class="sxs-lookup"><span data-stu-id="c731a-117">**password** : Password of the user account created</span></span>
    4. <span data-ttu-id="c731a-118">**cluster_address** ：MongoDB 群集的主机名/地址</span><span class="sxs-lookup"><span data-stu-id="c731a-118">**cluster_address** : hostname/address of your MongoDB cluster</span></span>
    5. <span data-ttu-id="c731a-119">**database** ：要连接到的 MongoDB 数据库</span><span class="sxs-lookup"><span data-stu-id="c731a-119">**database** : The MongoDB database you want to connect to</span></span>
    6. <span data-ttu-id="c731a-120">**collection** ：要读取的 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="c731a-120">**collection** : The MongoDB collection you want to read.</span></span> <span data-ttu-id="c731a-121">（在本例中，我们将使用每个 Apache Spark 安装中提供的标准 [`people.json`](https://github.com/apache/spark/blob/master/examples/src/main/resources/people.json) 示例文件。）</span><span class="sxs-lookup"><span data-stu-id="c731a-121">(For this example we use the standard [`people.json`](https://github.com/apache/spark/blob/master/examples/src/main/resources/people.json) example file provided with every Apache Spark installation.)</span></span>

2. <span data-ttu-id="c731a-122">使用的 `com.mongodb.spark.sql.DefaultSource` 格式为 `spark.Read()`，如下面简单的代码片段中所示：</span><span class="sxs-lookup"><span data-stu-id="c731a-122">Use the `com.mongodb.spark.sql.DefaultSource` format is `spark.Read()` as shown below in a simple code snippet:</span></span>

    ```csharp
    class Program
    {
        static void Main()
        {
            var authURI = "mongodb+srv://<username>:<password>@<cluster_address>/<database>.<collection>?retryWrites=true&w=majority";
            SparkSession spark = SparkSession
                .Builder()
                .AppName("Connect to Mongo DB example")
                .Config("spark.mongodb.input.uri", authURI)
                .GetOrCreate();

            DataFrame df = spark.Read().Format("com.mongodb.spark.sql.DefaultSource").Load();
            df.PrintSchema();
            df.Show();
            spark.Stop();
        }
    }
    ```

## <a name="run-your-application"></a><span data-ttu-id="c731a-123">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="c731a-123">Run your application</span></span>

<span data-ttu-id="c731a-124">为了运行 .NET for Apache Spark 应用程序，应在 Spark 项目中将 `mongo-spark-connector` 模块定义为生成定义的一部分，对于 sbt 项目，请使用 `build.sbt` 中的 `libraryDependency`。</span><span class="sxs-lookup"><span data-stu-id="c731a-124">In order to run your .NET for Apache Spark application, you should define the `mongo-spark-connector` module as part of the build definition in your Spark project, using `libraryDependency` in `build.sbt` for sbt projects.</span></span> <span data-ttu-id="c731a-125">对于 Spark 环境（如 `spark-submit` 或 `spark-shell`），请使用 `--packages` 命令行选项，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c731a-125">For Spark environments such as `spark-submit` (or `spark-shell`) you should use the `--packages` command-line option like so:</span></span>

```bash
spark-submit --master local --packages org.mongodb.spark:mongo-spark-connector_2.12:3.0.0 --class org.apache.spark.deploy.dotnet.DotnetRunner microsoft-spark-<version>.jar yourApp.exe
```

> [!NOTE]
> <span data-ttu-id="c731a-126">请确保包含与正在运行的 Spark 版本相符的包版本。</span><span class="sxs-lookup"><span data-stu-id="c731a-126">Make sure to include the package version in accordance with the version of Spark being run.</span></span>

<span data-ttu-id="c731a-127">显示的结果为 DataFrame (`df`)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c731a-127">The result as displayed is the DataFrame (`df`) as shown below:</span></span>

```text
+--------------------+----+-------+
|                 _id| age|   name|
+--------------------+----+-------+
|[5f7c28438029a134...|null|Michael|
|[5f7c287f8029a134...|  30|   Andy|
|[5f7c289a8029a134...|  19| Justin|
+--------------------+----+-------+
```
