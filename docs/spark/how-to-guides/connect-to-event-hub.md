---
title: 将 .NET for Apache Spark 连接到 Azure 事件中心
description: 了解如何从本地 .NET for Apache Spark 实例连接到 Azure 事件中心。
ms.date: 10/09/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 4de4836ba2b63429e29ae819afac09c7a3998480
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91954966"
---
# <a name="connect-net-for-apache-spark-to-azure-event-hubs"></a><span data-ttu-id="33019-103">将 .NET for Apache Spark 连接到 Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="33019-103">Connect .NET for Apache Spark to Azure Event Hubs</span></span>

<span data-ttu-id="33019-104">本文介绍如何将 [.NET for Apache Spark](https://github.com/dotnet/spark) 应用程序连接到 Azure 事件中心，以读取和写入 Apache Kafka 流。</span><span class="sxs-lookup"><span data-stu-id="33019-104">In this article, you will learn how to connect your [.NET for Apache Spark](https://github.com/dotnet/spark) application with Azure Event Hubs to read and write Apache Kafka streams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33019-105">先决条件</span><span class="sxs-lookup"><span data-stu-id="33019-105">Prerequisites</span></span>

<span data-ttu-id="33019-106">使用事件中心准备好事件中心命名空间。</span><span class="sxs-lookup"><span data-stu-id="33019-106">Have an Event Hubs Namespace ready with an event hub.</span></span> <span data-ttu-id="33019-107">有关查看分步指南，请参阅 [快速入门：使用 Azure 门户创建事件中心](/azure/event-hubs/event-hubs-create)。</span><span class="sxs-lookup"><span data-stu-id="33019-107">For a step-by-step guide, refer to [Quickstart: Create an event hub using Azure portal](/azure/event-hubs/event-hubs-create).</span></span> <span data-ttu-id="33019-108">创建事件中心命名空间时，请确保选择标准定价层。</span><span class="sxs-lookup"><span data-stu-id="33019-108">Make sure to select the Standard Pricing tier while creating the Event Hub Namespace.</span></span>

## <a name="what-is-azure-event-hubs"></a><span data-ttu-id="33019-109">什么是 Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="33019-109">What is Azure Event Hubs</span></span>

<span data-ttu-id="33019-110">[Azure 事件中心](/azure/event-hubs/event-hubs-about)是大数据流式处理平台和事件引入服务。</span><span class="sxs-lookup"><span data-stu-id="33019-110">[Azure Event Hubs](/azure/event-hubs/event-hubs-about) is a big-data streaming platform and event-ingestion service.</span></span> <span data-ttu-id="33019-111">它是一种完全托管的平台即服务 (PaaS)，可以轻松地与 [Apache Kafka](https://kafka.apache.org/) 集成，为你提供无需管理、配置或运行自己的群集的 PaaS Kafka 体验。</span><span class="sxs-lookup"><span data-stu-id="33019-111">It is a fully managed Platform-as-a-Service (PaaS) that can easily integrate with [Apache Kafka](https://kafka.apache.org/) to give you the PaaS Kafka experience without having to manage, configure, or run your own clusters.</span></span>

## <a name="connect-your-application-to-azure-event-hubs"></a><span data-ttu-id="33019-112">将应用程序连接到 Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="33019-112">Connect your application to Azure Event Hubs</span></span>

1. <span data-ttu-id="33019-113">获取事件中心连接字符串和完全限定域名 (FQDN) 供以后使用。</span><span class="sxs-lookup"><span data-stu-id="33019-113">Get the Event Hubs connection string and fully qualified domain name (FQDN) for later use.</span></span> <span data-ttu-id="33019-114">有关说明，请参阅[获取事件中心连接字符串](/azure/event-hubs/event-hubs-get-connection-string)。</span><span class="sxs-lookup"><span data-stu-id="33019-114">For instructions, see [Get an Event Hubs connection string](/azure/event-hubs/event-hubs-get-connection-string).</span></span>
2. <span data-ttu-id="33019-115">在代码中使用命名空间中的详细信息设置以下配置，开始从适用于 Kafka 的事件中心读取：</span><span class="sxs-lookup"><span data-stu-id="33019-115">Set the following configurations with details from your namespace in your code to start reading from Event Hubs for Kafka:</span></span>
    1. <span data-ttu-id="33019-116">在应用程序中更新 BOOTSTRAP_SERVERS 和 EH_SASL ：</span><span class="sxs-lookup"><span data-stu-id="33019-116">Update **BOOTSTRAP_SERVERS** and **EH_SASL** in your application like so:</span></span>

    ```csharp
    string BOOTSTRAP_SERVERS = "hostname:9093"; // 9093 is the port used to communicate with Event Hubs, see [troubleshooting guide](https://docs.microsoft.com/azure/event-hubs/troubleshooting-guide)
    string EH_SASL = "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"$ConnectionString\" password=\"<CONNECTION_STRING>\";"; // Connection string obtained from Step 1
    ```

## <a name="read-from-azure-event-hub-stream"></a><span data-ttu-id="33019-117">从 Azure 事件中心流读取</span><span class="sxs-lookup"><span data-stu-id="33019-117">Read from Azure Event Hub stream</span></span>

<span data-ttu-id="33019-118">你现在可以使用事件中心进行流式处理，就像使用 Kafka 一样。</span><span class="sxs-lookup"><span data-stu-id="33019-118">You can now start streaming with Event Hubs as you would with Kafka.</span></span> <span data-ttu-id="33019-119">示例代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="33019-119">Sample code as shown below:</span></span>

```csharp
SparkSession spark = SparkSession
    .Builder()
    .AppName("Connect Event Hub")
    .GetOrCreate();

DataFrame df = spark
    .ReadStream()
    .Format("kafka")
    .Option("kafka.bootstrap.servers", BOOTSTRAP_SERVERS)
    .Option("subscribe", "spark-test")
    .Option("kafka.sasl.mechanism", "PLAIN")
    .Option("kafka.security.protocol", "SASL_SSL")
    .Option("kafka.sasl.jaas.config", EH_SASL)
    .Option("kafka.request.timeout.ms", "60000")
    .Option("kafka.session.timeout.ms", "60000")
    .Option("failOnDataLoss", "false")
    .Load();

DataFrame dfWrite = df
    .WriteStream()
    .OutputMode("append")
    .Format("console")
    .Start();
```

## <a name="write-to-azure-event-hub-stream"></a><span data-ttu-id="33019-120">写入 Azure 事件中心流</span><span class="sxs-lookup"><span data-stu-id="33019-120">Write to Azure Event Hub stream</span></span>

<span data-ttu-id="33019-121">你也可以使用相同方式写入事件中心，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33019-121">You can also write to Event Hubs in the same way, as shown below:</span></span>

```csharp
// df is the DataFrame to write

df.WriteStream()
    .Format("kafka")
    .Option("topic", topics)
    .Option("kafka.bootstrap.servers", BOOTSTRAP_SERVERS)
    .Option("kafka.sasl.mechanism", "PLAIN")
    .Option("kafka.security.protocol", "SASL_SSL")
    .Option("kafka.sasl.jaas.config", EH_SASL)
    .Option("checkpointLocation", "./checkpoint")
    .Start();
```

## <a name="run-your-application"></a><span data-ttu-id="33019-122">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="33019-122">Run your application</span></span>

<span data-ttu-id="33019-123">为了运行 .NET for Apache Spark 应用程序，请在 Spark 项目中将 `spark-sql-kafka-0-10` 模块定义为生成定义的一部分，对于 sbt 项目，应使用 `build.sbt` 中的 `libraryDependency`。</span><span class="sxs-lookup"><span data-stu-id="33019-123">In order to run your .NET for Apache Spark application, define the `spark-sql-kafka-0-10` module as part of the build definition in your Spark project, using `libraryDependency` in `build.sbt` for sbt projects.</span></span> <span data-ttu-id="33019-124">对于 Spark 环境（如 `spark-submit` 或 `spark-shell`），请使用 `--packages` 命令行选项，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33019-124">For Spark environments such as `spark-submit` (or `spark-shell`), use the `--packages` command-line option like so:</span></span>

```bash
spark-shell --packages org.apache.spark:spark-sql-kafka-0-10_2.12:2.4.5
```

> [!NOTE]
> <span data-ttu-id="33019-125">请确保包含与正在运行的 Spark 版本相符的包版本。</span><span class="sxs-lookup"><span data-stu-id="33019-125">Make sure to include the package version in accordance with the version of Spark being run.</span></span>
