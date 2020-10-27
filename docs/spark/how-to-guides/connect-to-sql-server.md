---
title: 将 .NET for Apache Spark 连接到 SQL Server
description: 了解如何从 .NET for Apache Spark 应用程序连接到 SQL Server 实例。
ms.author: nidutta
author: Niharikadutta
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: b20710000d8717b5df238aa9a782371fbe586037
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224030"
---
# <a name="connect-net-for-apache-spark-to-sql-server"></a><span data-ttu-id="24e38-103">将 .NET for Apache Spark 连接到 SQL Server</span><span class="sxs-lookup"><span data-stu-id="24e38-103">Connect .NET for Apache Spark to SQL Server</span></span>

<span data-ttu-id="24e38-104">本文介绍如何从 [.NET for Apache Spark](https://github.com/dotnet/spark) 应用程序连接到 SQL Server 实例。</span><span class="sxs-lookup"><span data-stu-id="24e38-104">In this article, you learn how to connect to an SQL server instance from your [.NET for Apache Spark](https://github.com/dotnet/spark) application.</span></span>

## <a name="configure-sql-server-to-grant-your-application-access"></a><span data-ttu-id="24e38-105">配置 SQL Server 以授予应用程序访问权限</span><span class="sxs-lookup"><span data-stu-id="24e38-105">Configure SQL Server to grant your application access</span></span>

1. <span data-ttu-id="24e38-106">将登录用户和密码添加到 SQL Server 实例的 SQL Server 身份验证。</span><span class="sxs-lookup"><span data-stu-id="24e38-106">Add a login user and password choosing SQL Server authentication to your SQL Server instance.</span></span>
2. <span data-ttu-id="24e38-107">在相应的数据库级别向该登录用户授予所需的权限，如下所示：</span><span class="sxs-lookup"><span data-stu-id="24e38-107">Give that login user necessary permissions at the relevant database level as shown below:</span></span>

    ![SQL Server 权限](./media/connect-external-sources/SqlServerAuth.png)

3. <span data-ttu-id="24e38-109">请确保允许 SQL Server 的默认端口 `1433` 通过防火墙。</span><span class="sxs-lookup"><span data-stu-id="24e38-109">Make sure the default port for SQL Server `1433` is allowed through the firewall.</span></span>
4. <span data-ttu-id="24e38-110">打开 SQL 配置管理器，通过网络配置启用 TCP/IP，如下所示：</span><span class="sxs-lookup"><span data-stu-id="24e38-110">Open SQL configure manager to enable TCP/IP through the network configuration as shown below:</span></span>

    ![启用 SQL Server TCP/IP](./media/connect-external-sources/SqlServerTCPIP.png)

    <span data-ttu-id="24e38-112">另请注意上图“协议”下的选项卡中“全部侦听”的值 。</span><span class="sxs-lookup"><span data-stu-id="24e38-112">Also note the value of **Listen All** in above tab under **Protocol** .</span></span>

5. <span data-ttu-id="24e38-113">如果 `Listen All` 设置为 `No`，则针对所有必需的 IP 地址，将 TCP/IP 端口配置为 1433。</span><span class="sxs-lookup"><span data-stu-id="24e38-113">Configure the TCP/IP port to 1433 for all required IP addresses if the `Listen All` is set to `No`.</span></span> <span data-ttu-id="24e38-114">否则，请在 IPAll 中设置 TCP 端口。</span><span class="sxs-lookup"><span data-stu-id="24e38-114">Otherwise, set the TCP Port in IPAll.</span></span>

    ![SQL Server TCP/IP 端口](./media/connect-external-sources/SQLServerTCPIIPPort.png)

## <a name="connect-to-sql-server-from-your-application"></a><span data-ttu-id="24e38-116">从应用程序连接到 SQL Server</span><span class="sxs-lookup"><span data-stu-id="24e38-116">Connect to SQL Server from your application</span></span>

1. <span data-ttu-id="24e38-117">使用 Microsoft JDBC Driver for SQL Server 通过你的应用程序提供数据库连接（从[此官方网站](https://docs.microsoft.com/sql/connect/jdbc/download-microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15)下载）。</span><span class="sxs-lookup"><span data-stu-id="24e38-117">Use the Microsoft JDBC Driver for SQL Server to provide database connectivity through your application (download from [this official website](https://docs.microsoft.com/sql/connect/jdbc/download-microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15)).</span></span>
2. <span data-ttu-id="24e38-118">设置以下配置，以从应用程序连接到 SQL server 实例和数据库：</span><span class="sxs-lookup"><span data-stu-id="24e38-118">Set the following configurations to connect to the SQL server instance and database from your application:</span></span>
    1. <span data-ttu-id="24e38-119">**connection_url** ：这是用于连接到 SQL Server 实例/数据库的 URL，格式如下：</span><span class="sxs-lookup"><span data-stu-id="24e38-119">**connection_url** : This is the URL used to connect to the SQL server instance/database and has the following format:</span></span>

        ```
        jdbc:sqlserver://<SQL_server_IP_address>:1433;instanceName=<instance_name>;databaseName=<database_name>;
        ```

    2. <span data-ttu-id="24e38-120">**dbtable** ：要访问的表的名称。</span><span class="sxs-lookup"><span data-stu-id="24e38-120">**dbtable** : Name of table being accessed.</span></span>
    3. <span data-ttu-id="24e38-121">**user** ：在配置 SQL Server 的步骤 1 中设置的登录用户。</span><span class="sxs-lookup"><span data-stu-id="24e38-121">**user** : Login user set up in Step 1 of configuring the SQL server.</span></span>
    4. <span data-ttu-id="24e38-122">**password** ：在配置 SQL Server 的步骤 1 中设置的用户密码。</span><span class="sxs-lookup"><span data-stu-id="24e38-122">**password** : Password of user set up in Step 1 of configuring the SQL server.</span></span>
3. <span data-ttu-id="24e38-123">在应用程序代码中使用上述配置来读取表中的数据，如下所示：</span><span class="sxs-lookup"><span data-stu-id="24e38-123">Use the above configuration in your application code to read the data from a table as shown below:</span></span>

    ```csharp
    static void Main()
    {
        SparkSession spark = SparkSession
            .Builder()
            .AppName("Connect to SQL Server")
            .GetOrCreate();

        string connection_url = "<URL to connect to SQL server instance>";
        string dbtable = "<database table to access>";
        string user = "<Login user name>";
        string password = "<Login user password>";

        DataFrame jdbcDF = spark.Read()
            .Format("jdbc")
            .Option("driver", "com.microsoft.sqlserver.jdbc.SQLServerDriver")
            .Option("url", connection_url)
            .Option("dbtable", dbtable)
            .Option("user", user)
            .Option("password", password).Load();
        jdbcDF.Show(); // Displays the content of the SQL table as a DataFrame
    }
    ```
