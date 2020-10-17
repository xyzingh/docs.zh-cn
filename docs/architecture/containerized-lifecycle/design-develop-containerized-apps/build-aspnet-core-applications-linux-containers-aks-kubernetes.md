---
title: 构建作为 Linux 容器部署到 AKS/Kubernetes 群集中的 ASP.NET Core 应用程序
description: 使用 Microsoft 平台和工具的容器化 Docker 应用程序的生命周期
ms.date: 08/06/2020
ms.openlocfilehash: 8b3141d79eeb252ec3721d57293bed0e335b41d3
ms.sourcegitcommit: a6bd4cad438fe479cbd112eae10f2cd449f06e40
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2020
ms.locfileid: "91844558"
---
# <a name="build-aspnet-core-applications-deployed-as-linux-containers-into-an-akskubernetes-orchestrator"></a><span data-ttu-id="8eacb-103">构建作为 Linux 容器部署到 AKS/Kubernetes 业务流程协调程序中的 ASP.NET Core 应用程序</span><span class="sxs-lookup"><span data-stu-id="8eacb-103">Build ASP.NET Core applications deployed as Linux containers into an AKS/Kubernetes orchestrator</span></span>

<span data-ttu-id="8eacb-104">Azure Kubernetes 服务 (AKS) 是 Azure 的托管 Kubernetes 业务流程服务，可简化容器部署和管理。</span><span class="sxs-lookup"><span data-stu-id="8eacb-104">Azure Kubernetes Services (AKS) is Azure's managed Kubernetes orchestrations services that simplify container deployment and management.</span></span>

<span data-ttu-id="8eacb-105">AKS 主要功能如下：</span><span class="sxs-lookup"><span data-stu-id="8eacb-105">AKS main features are:</span></span>

- <span data-ttu-id="8eacb-106">Azure 托管的控制面板</span><span class="sxs-lookup"><span data-stu-id="8eacb-106">An Azure-hosted control plane</span></span>
- <span data-ttu-id="8eacb-107">自动升级</span><span class="sxs-lookup"><span data-stu-id="8eacb-107">Automated upgrades</span></span>
- <span data-ttu-id="8eacb-108">自我修复</span><span class="sxs-lookup"><span data-stu-id="8eacb-108">Self-healing</span></span>
- <span data-ttu-id="8eacb-109">用户可配置的缩放</span><span class="sxs-lookup"><span data-stu-id="8eacb-109">User-configurable scaling</span></span>
- <span data-ttu-id="8eacb-110">针对开发人员和群集操作员提供的更简单的用户体验。</span><span class="sxs-lookup"><span data-stu-id="8eacb-110">Simpler user experience for both developers and cluster operators.</span></span>

<span data-ttu-id="8eacb-111">以下示例探讨了如何创建在 Linux 上运行并部署到 Azure 中的 AKS 群集的 ASP.NET Core 3.1 应用程序，同时使用 Visual Studio 2019 完成开发。</span><span class="sxs-lookup"><span data-stu-id="8eacb-111">The following examples explore the creation of an ASP.NET Core 3.1 application that runs on Linux and deploys to an AKS Cluster in Azure, while development is done using Visual Studio 2019.</span></span>

## <a name="creating-the-aspnet-core-project-using-visual-studio-2019"></a><span data-ttu-id="8eacb-112">使用 Visual Studio 2019 创建 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="8eacb-112">Creating the ASP.NET Core Project using Visual Studio 2019</span></span>

<span data-ttu-id="8eacb-113">ASP.NET Core 是一个通用开发平台，由 Microsoft 和 GitHub 上的 .NET 社区共同维护。</span><span class="sxs-lookup"><span data-stu-id="8eacb-113">ASP.NET Core is a general-purpose development platform maintained by Microsoft and the .NET community on GitHub.</span></span> <span data-ttu-id="8eacb-114">它跨平台支持 Windows、macOS 和 Linux，并且可用于设备、云和嵌入式/IoT 方案。</span><span class="sxs-lookup"><span data-stu-id="8eacb-114">It's cross-platform, supporting Windows, macOS and Linux, and can be used in device, cloud, and embedded/IoT scenarios.</span></span>

<span data-ttu-id="8eacb-115">此示例使用几个基于 Visual Studio Web API 模板的简单项目，因此你无需太多其他知识即可创建示例。</span><span class="sxs-lookup"><span data-stu-id="8eacb-115">This example uses a couple of simple projects based on Visual Studio templates, so you don't need much additional knowledge to create the sample.</span></span> <span data-ttu-id="8eacb-116">只需使用标准模板创建项目，该模板包含使用 ASP.NET Core 3.1 技术运行带有 REST API 和带有 Razor Pages 的 Web 应用的小项目的所有元素。</span><span class="sxs-lookup"><span data-stu-id="8eacb-116">You only have to create the project using a standard template that includes all the elements to run a small project with a REST API and a Web App with Razor pages, using ASP.NET Core 3.1 technology.</span></span>

![Visual Studio 中的“添加新项目”窗口，已选择 ASP.NET Core Web 应用。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/create-aspnet-core-application.png)

<span data-ttu-id="8eacb-118">**图 4-35**。</span><span class="sxs-lookup"><span data-stu-id="8eacb-118">**Figure 4-35**.</span></span> <span data-ttu-id="8eacb-119">在 Visual Studio 2019 中创建 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8eacb-119">Creating an ASP.NET Core Web Application in Visual Studio 2019.</span></span>

<span data-ttu-id="8eacb-120">要在 Visual Studio 中创建示例项目，请选择“文件” > “新建” > “项目”，选择“Web”项目类型，然后选择“ASP.NET Core Web 应用程序”模板    。</span><span class="sxs-lookup"><span data-stu-id="8eacb-120">To create the sample project in Visual Studio, select **File** > **New** > **Project**, select the **Web** project type and then the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="8eacb-121">你还可以根据需要搜索模板。</span><span class="sxs-lookup"><span data-stu-id="8eacb-121">You can also search for the template if you need it.</span></span>

<span data-ttu-id="8eacb-122">然后输入应用程序名称和位置，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="8eacb-122">Then enter the application name and location as shown in the next image.</span></span>

![输入项目名称和位置。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/enter-project-name-and-location.png)

<span data-ttu-id="8eacb-124">图 4-36  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-124">**Figure 4-36**.</span></span> <span data-ttu-id="8eacb-125">在 Visual Studio 2019 中输入项目名称和位置。</span><span class="sxs-lookup"><span data-stu-id="8eacb-125">Enter the project name and location in Visual Studio 2019.</span></span>

<span data-ttu-id="8eacb-126">验证是否已选择 ASP.NET Core 3.1 作为框架。</span><span class="sxs-lookup"><span data-stu-id="8eacb-126">Verify that you've selected ASP.NET Core 3.1 as the framework.</span></span> <span data-ttu-id="8eacb-127">.NET Core 3.1 包含在 Visual Studio 2019 的最新版本中，并在安装 Visual Studio 时自动安装和配置。</span><span class="sxs-lookup"><span data-stu-id="8eacb-127">.NET Core 3.1 is included in the latest release of Visual Studio 2019 and is automatically installed and configured for you when you install Visual Studio.</span></span>

![用于选择 ASP.NET Core Web 应用类型的 Visual Studio 对话框，已选择 API 选项。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/create-web-api-application.png)

<span data-ttu-id="8eacb-129">图 4-37  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-129">**Figure 4-37**.</span></span> <span data-ttu-id="8eacb-130">选择 ASP.NET CORE 3.1 和 Web API 项目类型</span><span class="sxs-lookup"><span data-stu-id="8eacb-130">Selecting ASP.NET CORE 3.1 and Web API project type</span></span>

<span data-ttu-id="8eacb-131">注意，现在尚未启用 Docker 支持，只是为了表明它可以在项目创建后完成。</span><span class="sxs-lookup"><span data-stu-id="8eacb-131">Notice Docker support is not enabled now, just to show it can be done after project creation.</span></span>

<span data-ttu-id="8eacb-132">如果有任何以前版本的 .NET Core，则可以从 <https://dotnet.microsoft.com/download> 下载并安装 3.1 版本。</span><span class="sxs-lookup"><span data-stu-id="8eacb-132">If you have any previous version of .NET Core, you can download and install the 3.1 version from <https://dotnet.microsoft.com/download>.</span></span>

<span data-ttu-id="8eacb-133">若要显示你可以随时“Docker 化”项目，请立即添加 Docker 支持。</span><span class="sxs-lookup"><span data-stu-id="8eacb-133">To show you can "Dockerize" your project at any time, you'll add Docker support now.</span></span> <span data-ttu-id="8eacb-134">在解决方案资源管理器中右键单击项目节点，然后在上下文菜单中选择“添加” > “Docker 支持” 。</span><span class="sxs-lookup"><span data-stu-id="8eacb-134">So right-click on the project node in Solution Explorer and select **Add** > **Docker support** on the context menu.</span></span>

![用于向现有项目添加 Docker 支持的上下文菜单选项：右键单击（在项目上）>“添加”>“Docker 支持”。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/add-docker-support-to-project.png)

<span data-ttu-id="8eacb-136">图 4-38  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-136">**Figure 4-38**.</span></span> <span data-ttu-id="8eacb-137">向现有项目添加 Docker 支持</span><span class="sxs-lookup"><span data-stu-id="8eacb-137">Adding Docker support to an existing project</span></span>

<span data-ttu-id="8eacb-138">若要完成添加 Docker 支持，可以选择 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="8eacb-138">To complete adding Docker support, you can choose Windows or Linux.</span></span> <span data-ttu-id="8eacb-139">在本例中，选择“Linux”。</span><span class="sxs-lookup"><span data-stu-id="8eacb-139">In this case, select **Linux**.</span></span>

![为 Dockerfile 选择目标操作系统的选项对话框。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/select-linux-docker-support.png)

<span data-ttu-id="8eacb-141">图 4-39  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-141">**Figure 4-39**.</span></span> <span data-ttu-id="8eacb-142">选择 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="8eacb-142">Selecting Linux containers.</span></span>

<span data-ttu-id="8eacb-143">通过这些简单的步骤，你就可以在 Linux 容器上运行 ASP.NET Core 3.1 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8eacb-143">With these simple steps, you have your ASP.NET Core 3.1 application running on a Linux container.</span></span>

<span data-ttu-id="8eacb-144">同样，你还可以添加一个非常简单的 WebApp 项目（图 4-40）来使用 Web API 终结点，但此处不进行详细介绍。</span><span class="sxs-lookup"><span data-stu-id="8eacb-144">In a similar way, you can also add a very simple **WebApp** project (Figure 4-40) to consume the web API endpoint, although the details are not discussed here.</span></span>

<span data-ttu-id="8eacb-145">然后，为 WebApi 项目添加业务流程协调程序支持，如下图 4-40 所示。</span><span class="sxs-lookup"><span data-stu-id="8eacb-145">After that, you add orchestrator support for your **WebApi** project as shown next, in image 4-40.</span></span>

![正在向 WebApi 项目添加业务流程协调程序支持](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/add-orchestrator-support.png)

<span data-ttu-id="8eacb-147">图 4-40  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-147">**Figure 4-40**.</span></span> <span data-ttu-id="8eacb-148">正在向 WebApi 项目添加业务流程协调程序支持。</span><span class="sxs-lookup"><span data-stu-id="8eacb-148">Adding orchestrator support to *WebApi* project.</span></span>

<span data-ttu-id="8eacb-149">当你选择适用于本地开发的 `Docker Compose` 选项时，Visual Studio 会添加包含 docker-compose 文件的 docker-compose 项目，如图 4-41 中所示。</span><span class="sxs-lookup"><span data-stu-id="8eacb-149">When you choose the `Docker Compose` option, which is fine for local development, Visual Studio adds the docker-compose project, with the docker-compose files as shown in image 4-41.</span></span>

![Docker-compose 已添加到解决方案中](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/docker-compose-project-in-visual-studio.png)

<span data-ttu-id="8eacb-151">图 4-41  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-151">**Figure 4-41**.</span></span> <span data-ttu-id="8eacb-152">正在向 WebApi 项目添加业务流程协调程序支持。</span><span class="sxs-lookup"><span data-stu-id="8eacb-152">Adding orchestrator support to *WebApi* project.</span></span>

<span data-ttu-id="8eacb-153">添加的初始文件与以下文件类似：</span><span class="sxs-lookup"><span data-stu-id="8eacb-153">The initial files added are similar to these ones:</span></span>

`docker-compose.yml`

```yml
version: "3.4"

services:
  webapi:
    image: ${DOCKER_REGISTRY-}webapi
    build:
      context: .
      dockerfile: WebApi/Dockerfile

  webapp:
    image: ${DOCKER_REGISTRY-}webapp
    build:
      context: .
      dockerfile: WebApp/Dockerfile
```

`docker-compose.override.yml`

```yml
version: "3.4"

services:
  webapi:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=https://+:443;http://+:80
    ports:
      - "80"
      - "443"
    volumes:
      - ${APPDATA}/Microsoft/UserSecrets:/root/.microsoft/usersecrets:ro
      - ${APPDATA}/ASP.NET/Https:/root/.aspnet/https:ro
  webapp:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=https://+:443;http://+:80
    ports:
      - "80"
      - "443"
    volumes:
      - ${APPDATA}/Microsoft/UserSecrets:/root/.microsoft/usersecrets:ro
      - ${APPDATA}/ASP.NET/Https:/root/.aspnet/https:ro
```

<span data-ttu-id="8eacb-154">若要使用 Docker Compose 运行应用，你只需对 `docker-compose.override.yml` 进行一些调整即可</span><span class="sxs-lookup"><span data-stu-id="8eacb-154">To have you app running with Docker Compose you just have to make a few tweaks to `docker-compose.override.yml`</span></span>

```yml
services:
  webapi:
    #...
    ports:
      - "51080:80"
      - "51443:443"
    #...
  webapp:
    environment:
      #...
      - WebApiBaseAddress=http://webapi
    ports:
      - "50080:80"
      - "50443:443"
    #...
```

<span data-ttu-id="8eacb-155">现在，你可以通过以下三种方式运行应用程序：按 F5 键、使用“播放”按钮或按 Ctrl+F5 键，从而选择 docker-compose 项目，如图 4-42 所示  。</span><span class="sxs-lookup"><span data-stu-id="8eacb-155">Now you can run your application with the **F5** key, or by using the **Play** button, or the **Ctrl+F5** key, selecting the docker-compose project, as shown in image 4-42.</span></span>

![使用 Visual Studio 运行 docker-compose 项目](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/running-docker-compose-with-visual-studio.png)

<span data-ttu-id="8eacb-157">图 4-42  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-157">**Figure 4-42**.</span></span> <span data-ttu-id="8eacb-158">正在向 WebApi 项目添加业务流程协调程序支持。</span><span class="sxs-lookup"><span data-stu-id="8eacb-158">Adding orchestrator support to *WebApi* project.</span></span>

<span data-ttu-id="8eacb-159">按照说明运行 docker-compose 应用程序时，你将获得：</span><span class="sxs-lookup"><span data-stu-id="8eacb-159">When running the docker-compose application as explained, you get:</span></span>

1. <span data-ttu-id="8eacb-160">根据 docker-compose 文件构建的映像和创建的容器。</span><span class="sxs-lookup"><span data-stu-id="8eacb-160">The images built and containers created as per the docker-compose file.</span></span>
2. <span data-ttu-id="8eacb-161">浏览器将在 `docker-compose` 项目的“属性”对话框中配置的地址中打开。</span><span class="sxs-lookup"><span data-stu-id="8eacb-161">The browser open in the address configured in the "Properties" dialog for the `docker-compose` project.</span></span>
3. <span data-ttu-id="8eacb-162">“容器”窗口打开（在 Visual Studio 2019 版本 16.4 及更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="8eacb-162">The **Container** window open (in Visual Studio 2019 version 16.4 and later).</span></span>
4. <span data-ttu-id="8eacb-163">调试器支持解决方案中的所有项目，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="8eacb-163">Debugger support for all projects in the solution, as shown in the following images.</span></span>

<span data-ttu-id="8eacb-164">浏览器已打开：</span><span class="sxs-lookup"><span data-stu-id="8eacb-164">Browser opened:</span></span>

![正在运行 Web 应用的浏览器视图](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/browser-opened.png)

<span data-ttu-id="8eacb-166">图 4-43  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-166">**Figure 4-43**.</span></span> <span data-ttu-id="8eacb-167">具有在多个容器上运行的应用程序的浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="8eacb-167">Browser window with an application running on multiple containers.</span></span>

<span data-ttu-id="8eacb-168">容器窗口：</span><span class="sxs-lookup"><span data-stu-id="8eacb-168">Containers window:</span></span>

![Visual Studio“容器”窗口](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/visual-studio-containers-window.png)

<span data-ttu-id="8eacb-170">图 4-44  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-170">**Figure 4-44**.</span></span> <span data-ttu-id="8eacb-171">Visual Studio“容器”窗口</span><span class="sxs-lookup"><span data-stu-id="8eacb-171">Visual Studio "Containers" window</span></span>

<span data-ttu-id="8eacb-172">通过“容器”窗口，你可以查看正在运行的容器、浏览可用的映像、查看环境变量、日志和端口映射、检查文件系统、附加调试器，或者在容器环境中打开终端窗口。</span><span class="sxs-lookup"><span data-stu-id="8eacb-172">The **Containers** window lets you view running containers, browse available images, view environment variables, logs, and port mappings, inspect the filesystem, attach a debugger, or open a terminal window inside the container environment.</span></span>

<span data-ttu-id="8eacb-173">如你所见，Visual Studio 2019 与 Docker 之间的集成完全面向开发人员的工作效率。</span><span class="sxs-lookup"><span data-stu-id="8eacb-173">As you can see, the integration between Visual Studio 2019 and Docker is completely oriented to the developer's productivity.</span></span>

<span data-ttu-id="8eacb-174">当然，你也可以使用 `docker images` 命令列出图像。</span><span class="sxs-lookup"><span data-stu-id="8eacb-174">Of course, you can also list the images using the `docker images` command.</span></span> <span data-ttu-id="8eacb-175">你应看到使用 Visual Studio 2019 自动部署项目时创建的带有 `dev` 标记的 `webapi` 和 `webapp` 映像。</span><span class="sxs-lookup"><span data-stu-id="8eacb-175">You should see the `webapi` and `webapp` images with the `dev` tags created by the automatic deployment of our project with Visual Studio 2019.</span></span>

```console
docker images
```

![来自 Docker 映像命令的控制台输出，显示了一个包含以下内容的列表：存储库、标记、映像 ID、创建（日期）和大小。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/docker-images-command.png)

<span data-ttu-id="8eacb-177">图 4-45  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-177">**Figure 4-45**.</span></span> <span data-ttu-id="8eacb-178">Docker 映像视图</span><span class="sxs-lookup"><span data-stu-id="8eacb-178">View of Docker images</span></span>

## <a name="register-the-solution-in-an-azure-container-registry-acr"></a><span data-ttu-id="8eacb-179">在 Azure 容器注册表 (ACR) 中注册解决方案</span><span class="sxs-lookup"><span data-stu-id="8eacb-179">Register the Solution in an Azure Container Registry (ACR)</span></span>

<span data-ttu-id="8eacb-180">你可以将映像上传到 [Azure 容器注册表 (ACR)](https://azure.microsoft.com/services/container-registry/)，但你也可以使用 Docker Hub 或任何其他注册表，因此可以将映像从该注册表部署到 AKS 群集。</span><span class="sxs-lookup"><span data-stu-id="8eacb-180">You can upload the images to the [Azure Container Registry (ACR)](https://azure.microsoft.com/services/container-registry/), but you could also use Docker Hub or any other registry, so the images can be deployed to the AKS cluster from that registry.</span></span>

### <a name="create-an-acr-instance"></a><span data-ttu-id="8eacb-181">创建 ACR 实例</span><span class="sxs-lookup"><span data-stu-id="8eacb-181">Create an ACR instance</span></span>

<span data-ttu-id="8eacb-182">从 az cli 运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8eacb-182">Run the following command from the **az cli**:</span></span>

```powershell
az acr create --name exploredocker --resource-group explore-docker-aks-rg --sku basic --admin-enabled
```

> [!NOTE]
> <span data-ttu-id="8eacb-183">容器注册表名称（例如 `exploredocker`）在 Azure 中必须唯一，并且必须包含 5-50 个字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="8eacb-183">The container registry name (e.g `exploredocker`) must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="8eacb-184">如需了解详情，请参阅[创建容器注册表](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-azure-cli#create-a-container-registry)</span><span class="sxs-lookup"><span data-stu-id="8eacb-184">For more details, refer [Create a container registry](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-azure-cli#create-a-container-registry)</span></span>

### <a name="create-the-image-in-release-mode"></a><span data-ttu-id="8eacb-185">在发布模式下创建映像</span><span class="sxs-lookup"><span data-stu-id="8eacb-185">Create the image in Release mode</span></span>

<span data-ttu-id="8eacb-186">现在，你将通过更改为“发布”，在“发布”模式（准备生产）中创建映像，如图 4-46 所示，并像以前一样运行应用程序 。</span><span class="sxs-lookup"><span data-stu-id="8eacb-186">You'll now create the image in **Release** mode (ready for production) by changing to **Release**, as shown in Figure 4-46, and running the application as you did before.</span></span>

![VS 中的工具栏选项，用于在发布模式下生成。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/select-release-mode.png)

<span data-ttu-id="8eacb-188">图 4-46  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-188">**Figure 4-46**.</span></span> <span data-ttu-id="8eacb-189">选择发布模式</span><span class="sxs-lookup"><span data-stu-id="8eacb-189">Selecting Release Mode</span></span>

<span data-ttu-id="8eacb-190">如果执行 `docker images` 命令，则你将看到创建的两个映像：一个用于 `debug` (dev) 模式，另一个用于 `release` (latest) 模式 。</span><span class="sxs-lookup"><span data-stu-id="8eacb-190">If you execute the `docker images` command, you'll see both images created, one for `debug` (**dev**) and the other for `release` (**latest**) mode.</span></span>

### <a name="create-a-new-tag-for-the-image"></a><span data-ttu-id="8eacb-191">为映像创建新标记</span><span class="sxs-lookup"><span data-stu-id="8eacb-191">Create a new Tag for the Image</span></span>

<span data-ttu-id="8eacb-192">需要使用注册表的 `loginServer` 名称标记每个容器映像。</span><span class="sxs-lookup"><span data-stu-id="8eacb-192">Each container image needs to be tagged with the `loginServer` name of the registry.</span></span> <span data-ttu-id="8eacb-193">在将容器映像推送到映像注册表时，使用此标记进行路由。</span><span class="sxs-lookup"><span data-stu-id="8eacb-193">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="8eacb-194">可以从 Azure 门户中查看 `loginServer` 名称，从 Azure 容器注册表中获取信息</span><span class="sxs-lookup"><span data-stu-id="8eacb-194">You can view the `loginServer` name from the Azure portal, taking the information from the Azure Container Registry</span></span>

![位于右上角的 Azure 容器注册表名称的浏览器视图。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/loginServer-name.png)

<span data-ttu-id="8eacb-196">图 4-47  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-196">**Figure 4-47**.</span></span> <span data-ttu-id="8eacb-197">注册表名称的视图</span><span class="sxs-lookup"><span data-stu-id="8eacb-197">View of the name of the Registry</span></span>

<span data-ttu-id="8eacb-198">或者通过运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8eacb-198">Or by running the following command:</span></span>

```console
az acr list --resource-group <resource-group-name> --query "[].{acrLoginServer:loginServer}" --output table
```

![来自上述命令的控制台输出。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/az-cli-loginServer-name.png)

<span data-ttu-id="8eacb-200">图 4-48  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-200">**Figure 4-48**.</span></span> <span data-ttu-id="8eacb-201">使用 az cli 获取注册表的名称</span><span class="sxs-lookup"><span data-stu-id="8eacb-201">Get the name of the registry using **az cli**</span></span>

<span data-ttu-id="8eacb-202">这两种情况都可获得名称。</span><span class="sxs-lookup"><span data-stu-id="8eacb-202">In both cases, you'll obtain the name.</span></span> <span data-ttu-id="8eacb-203">在本示例中，为 `exploredocker.azurecr.io`。</span><span class="sxs-lookup"><span data-stu-id="8eacb-203">In our example, `exploredocker.azurecr.io`.</span></span>

<span data-ttu-id="8eacb-204">现在，可以使用以下命令标记映像，获取最新映像（发布映像）：</span><span class="sxs-lookup"><span data-stu-id="8eacb-204">Now you can tag the image, taking the latest image (the Release image), with the command:</span></span>

```console
docker tag <image-name>:latest <login-server-name>/<image-name>:v1
```

<span data-ttu-id="8eacb-205">运行 `docker tag` 命令后，使用 `docker images` 命令列出映像，你应看到带有新标记的映像。</span><span class="sxs-lookup"><span data-stu-id="8eacb-205">After running the `docker tag` command, list the images with the `docker images` command, and you should see the image with the new tag.</span></span>

![来自 Docker 映像命令的控制台输出。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/tagged-docker-images-list.png)

<span data-ttu-id="8eacb-207">图 4-49  .</span><span class="sxs-lookup"><span data-stu-id="8eacb-207">**Figure 4-49**.</span></span> <span data-ttu-id="8eacb-208">带标记的映像视图</span><span class="sxs-lookup"><span data-stu-id="8eacb-208">View of tagged images</span></span>

### <a name="push-the-image-into-the-azure-acr"></a><span data-ttu-id="8eacb-209">将映像推送到 Azure ACR</span><span class="sxs-lookup"><span data-stu-id="8eacb-209">Push the image into the Azure ACR</span></span>

<span data-ttu-id="8eacb-210">登录到 Azure 容器注册表</span><span class="sxs-lookup"><span data-stu-id="8eacb-210">Log in to the Azure Container Registry</span></span>

```console
az acr login --name exploredocker
```

<span data-ttu-id="8eacb-211">使用以下命令将映像推送到 Azure ACR：</span><span class="sxs-lookup"><span data-stu-id="8eacb-211">Push the image into the Azure ACR, using the following command:</span></span>

```console
docker push <login-server-name>/<image-name>:v1
```

<span data-ttu-id="8eacb-212">此命令需要一段时间上传映像，但会在此过程中为你提供反馈。</span><span class="sxs-lookup"><span data-stu-id="8eacb-212">This command takes a while uploading the images but gives you feedback in the process.</span></span> <span data-ttu-id="8eacb-213">在下图中，你可以看到一个映像已完成输出，而另一个映像正在输出。</span><span class="sxs-lookup"><span data-stu-id="8eacb-213">In the following image, you can see the output from one image completed and another in progress.</span></span>

![来自 Docker 推送命令的控制台输出。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/uploading-docker-images-complete.png)

<span data-ttu-id="8eacb-215">图 4-50。</span><span class="sxs-lookup"><span data-stu-id="8eacb-215">**Figure 4-50**.</span></span> <span data-ttu-id="8eacb-216">来自推送命令的控制台输出。</span><span class="sxs-lookup"><span data-stu-id="8eacb-216">Console output from the push command.</span></span>

<span data-ttu-id="8eacb-217">若要将多容器应用部署到 AKS 群集中，你需要一些清单 `.yaml` 文件，这些文件的大部分属性都是从 `docker-compose.yml` 和 `docker-compose.override.yml` 文件中获取的。</span><span class="sxs-lookup"><span data-stu-id="8eacb-217">To deploy your multi-container app into your AKS cluster you need some manifest `.yaml` files that have, most of the properties taken from the `docker-compose.yml` and `docker-compose.override.yml` files.</span></span>

#### `deploy-webapi.yml`

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapi
  labels:
    app: weather-forecast
spec:
  replicas: 1
  selector:
    matchLabels:
      service: webapi
  template:
    metadata:
      labels:
        app: weather-forecast
        service: webapi
    spec:
      containers:
        - name: webapi
          image: exploredocker.azurecr.io/webapi:v1
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
              protocol: TCP
          env:
            - name: ASPNETCORE_URLS
              value: http://+:80
---
apiVersion: v1
kind: Service
metadata:
  name: webapi
  labels:
    app: weather-forecast
    service: webapi
spec:
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
  selector:
    service: webapi
```

#### `deploy-webapp.yml`

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
  labels:
    app: weather-forecast
spec:
  replicas: 1
  selector:
    matchLabels:
      service: webapp
  template:
    metadata:
      labels:
        app: weather-forecast
        service: webapp
    spec:
      containers:
        - name: webapp
          image: exploredocker.azurecr.io/webapp:v1
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 80
              protocol: TCP
          env:
            - name: ASPNETCORE_URLS
              value: http://+:80
            - name: WebApiBaseAddress
              value: http://webapi
---
apiVersion: v1
kind: Service
metadata:
  name: webapp
  labels:
    app: weather-forecast
    service: webapp
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
  selector:
    service: webapp
```

> [!NOTE]
> <span data-ttu-id="8eacb-218">以前的 `.yml` 文件仅使用 `ASPNETCORE_URLS` 参数启用 `HTTP` 端口，以避免示例应用中出现证书缺失的问题。</span><span class="sxs-lookup"><span data-stu-id="8eacb-218">The previous `.yml` files only enable the `HTTP` ports, using the `ASPNETCORE_URLS` parameter, to avoid issues with the missing certificate in the sample app.</span></span>

> [!TIP]
> <span data-ttu-id="8eacb-219">可在本指南的[部署到 Azure Kubernetes 服务 (AKS)](deploy-azure-kubernetes-service.md) 部分中了解如何为此示例创建 AKS 群集  。</span><span class="sxs-lookup"><span data-stu-id="8eacb-219">You can see how to create the AKS Cluster for this sample in section [**Deploy to Azure Kubernetes Service (AKS)**](deploy-azure-kubernetes-service.md) on this guide.</span></span>

<span data-ttu-id="8eacb-220">现已准备好使用 kubectl 进行部署，但首先必须使用以下命令获取 AKS 群集中的凭据：</span><span class="sxs-lookup"><span data-stu-id="8eacb-220">Now you're almost ready to deploy using **kubectl**, but first you must get the credentials from the AKS Cluster with this command:</span></span>

```console
az aks get-credentials --resource-group explore-docker-aks-rg --name explore-docker-aks
```

![来自上述命令的控制台输出：将“explore-docker-aks”合并为 C:\Users\Miguel.kube\config 中的当前上下文](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/getting-aks-credentials.png)

<span data-ttu-id="8eacb-222">图 4-51。</span><span class="sxs-lookup"><span data-stu-id="8eacb-222">**Figure 4-51**.</span></span> <span data-ttu-id="8eacb-223">从 AKS 获取凭证到 kubectl 环境。</span><span class="sxs-lookup"><span data-stu-id="8eacb-223">Getting credentials from AKS into the kubectl environment.</span></span>

<span data-ttu-id="8eacb-224">还必须允许 AKS 群集使用以下命令从 ACR 中拉取映像：</span><span class="sxs-lookup"><span data-stu-id="8eacb-224">You also have to allow the AKS cluster to pull images from the ACR, using this command:</span></span>

```console
az aks update --name explore-docker-aks --resource-group explore-docker-aks-rg --attach-acr exploredocker
```

<span data-ttu-id="8eacb-225">上一个命令可能需要几分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="8eacb-225">The previous command might take a couple of minutes to complete.</span></span> <span data-ttu-id="8eacb-226">然后，使用 `kubectl apply` 命令启动部署，然后使用 `kubectl get all` 列出集群对象。</span><span class="sxs-lookup"><span data-stu-id="8eacb-226">Then, use the `kubectl apply` command to launch the deployments, and then `kubectl get all` get list the cluster objects.</span></span>

```console
kubectl apply -f deploy-webapi.yml
kubectl apply -f deploy-webapp.yml

kubectl get all
```

![上述命令的控制台输出：已应用部署。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/kubectl-apply-command.png)

<span data-ttu-id="8eacb-229">图 4-52。</span><span class="sxs-lookup"><span data-stu-id="8eacb-229">**Figure 4-52**.</span></span> <span data-ttu-id="8eacb-230">部署到 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8eacb-230">Deployment to Kubernetes</span></span>

<span data-ttu-id="8eacb-231">需要等待一段时间，直到负载均衡器获取外部 IP，并使用 `kubectl get services` 进行检查，然后该应用程序应该在该地址可用，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="8eacb-231">You'll have to wait a while until the load balancer gets the external IP, checking with `kubectl get services`, and then the application should be available at that address, as shown in the next image:</span></span>

![部署到 AKS 的应用程序的浏览器视图](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/aks-deployed-application.png)

<span data-ttu-id="8eacb-233">图 4-53。</span><span class="sxs-lookup"><span data-stu-id="8eacb-233">**Figure 4-53**.</span></span> <span data-ttu-id="8eacb-234">部署到 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8eacb-234">Deployment to Kubernetes</span></span>

<span data-ttu-id="8eacb-235">部署完成后，你可以通过 ssh 隧道使用本地代理访问 [Kubernetes Web UI](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)。</span><span class="sxs-lookup"><span data-stu-id="8eacb-235">When the deployment completes, you can access the [Kubernetes Web UI](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) with a local proxy, using an ssh tunnel.</span></span>

<span data-ttu-id="8eacb-236">首先，你必须使用以下命令创建 ClusterRoleBinding：</span><span class="sxs-lookup"><span data-stu-id="8eacb-236">First you must create a ClusterRoleBinding with the following command:</span></span>

```console
kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

<span data-ttu-id="8eacb-237">然后使用以下命令启动代理：</span><span class="sxs-lookup"><span data-stu-id="8eacb-237">And then this command to start the proxy:</span></span>

```console
az aks browse --resource-group exploredocker-aks-rg --name explore-docker-aks
```

<span data-ttu-id="8eacb-238">浏览器窗口应在 `http://127.0.0.1:8001` 处打开，其视图与下图类似：</span><span class="sxs-lookup"><span data-stu-id="8eacb-238">A browser window should open at `http://127.0.0.1:8001` with a view similar to this one:</span></span>

![Kubernetes 仪表板的浏览器视图，显示了部署、Pod、副本集和服务。](media/build-aspnet-core-applications-linux-containers-aks-kubernetes/kubernetes-cluster-information.png)

<span data-ttu-id="8eacb-240">图 4-54。</span><span class="sxs-lookup"><span data-stu-id="8eacb-240">**Figure 4-54**.</span></span> <span data-ttu-id="8eacb-241">查看 Kubernetes 群集信息</span><span class="sxs-lookup"><span data-stu-id="8eacb-241">View Kubernetes cluster information</span></span>

<span data-ttu-id="8eacb-242">现在，你已在 Linux 容器中运行 ASP.NET Core 应用程序，并将其部署到了 Azure 上的 AKS 群集。</span><span class="sxs-lookup"><span data-stu-id="8eacb-242">Now you have your ASP.NET Core application, running in Linux containers, and deployed to an AKS cluster on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="8eacb-243">有关使用 Kubernetes 进行部署的更多信息，请参阅：<https://kubernetes.io/docs/reference/kubectl/cheatsheet/></span><span class="sxs-lookup"><span data-stu-id="8eacb-243">For more information on deployment with Kubernetes see: <https://kubernetes.io/docs/reference/kubectl/cheatsheet/></span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8eacb-244">[上一页](set-up-windows-containers-with-powershell.md)
> [下一页](../docker-devops-workflow/index.md)</span><span class="sxs-lookup"><span data-stu-id="8eacb-244">[Previous](set-up-windows-containers-with-powershell.md)
[Next](../docker-devops-workflow/index.md)</span></span>
