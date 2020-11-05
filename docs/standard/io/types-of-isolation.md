---
title: 隔离的类型
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- storing data using isolated storage, accessing isolated storage
- storing data using isolated storage, isolation types
- authentication [.NET], isolated storage
- assemblies [.NET], identity
- isolated storage, accessing
- data storage using isolated storage, isolation types
- data storage using isolated storage, accessing isolated storage
- domain identity
- isolated storage, types
- user authentication, isolated storage
ms.assetid: 14812988-473f-44ae-b75f-fd5c2f21fb7b
ms.openlocfilehash: a1d64f0dfe8a457ae551792a852bd816941f2777
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189027"
---
# <a name="types-of-isolation"></a><span data-ttu-id="5ff38-102">隔离的类型</span><span class="sxs-lookup"><span data-stu-id="5ff38-102">Types of isolation</span></span>

<span data-ttu-id="5ff38-103">独立存储始终仅限创建它的用户访问。</span><span class="sxs-lookup"><span data-stu-id="5ff38-103">Access to isolated storage is always restricted to the user who created it.</span></span> <span data-ttu-id="5ff38-104">为了实现这种隔离，公共语言运行时使用操作系统识别的相同用户标识，即与存储打开时的代码运行进程相关联的标识。</span><span class="sxs-lookup"><span data-stu-id="5ff38-104">To implement this type of isolation, the common language runtime uses the same notion of user identity that the operating system recognizes, which is the identity associated with the process in which the code is running when the store is opened.</span></span> <span data-ttu-id="5ff38-105">虽然此标识是已验证用户标识，但模拟可能会导致当前用户的标识发生动态变化。</span><span class="sxs-lookup"><span data-stu-id="5ff38-105">This identity is an authenticated user identity, but impersonation can cause the identity of the current user to change dynamically.</span></span>  
  
 <span data-ttu-id="5ff38-106">独立存储访问的限制条件还包括，与应用的域和程序集相关联的标识或仅与程序集相关联的标识。</span><span class="sxs-lookup"><span data-stu-id="5ff38-106">Access to isolated storage is also restricted according to the identity associated with the application's domain and assembly, or with the assembly alone.</span></span> <span data-ttu-id="5ff38-107">运行时通过以下方式获取这些标识：</span><span class="sxs-lookup"><span data-stu-id="5ff38-107">The runtime obtains these identities in the following ways:</span></span>  
  
- <span data-ttu-id="5ff38-108">域标识表示证明应用的证据，对于 Web 应用，这可能就是完整 URL。</span><span class="sxs-lookup"><span data-stu-id="5ff38-108">Domain identity represents the evidence of the application, which in the case of a web application might be the full URL.</span></span> <span data-ttu-id="5ff38-109">对于 shell 托管代码，域标识可能基于应用目录路径。</span><span class="sxs-lookup"><span data-stu-id="5ff38-109">For shell-hosted code, the domain identity might be based on the application directory path.</span></span> <span data-ttu-id="5ff38-110">例如，如果通过路径 C:\Office\MyApp.exe 运行可执行文件，域标识为 C:\Office\MyApp.exe。</span><span class="sxs-lookup"><span data-stu-id="5ff38-110">For example, if the executable runs from the path C:\Office\MyApp.exe, the domain identity would be C:\Office\MyApp.exe.</span></span>  
  
- <span data-ttu-id="5ff38-111">程序集标识是证明程序集的证据。</span><span class="sxs-lookup"><span data-stu-id="5ff38-111">Assembly identity is the evidence of the assembly.</span></span> <span data-ttu-id="5ff38-112">这可能来自加密数字签名，可以是程序集的[强名称](../assembly/strong-named.md)、程序集的软件发行者或程序集的 URL 标识。</span><span class="sxs-lookup"><span data-stu-id="5ff38-112">This might come from a cryptographic digital signature, which can be the assembly's [strong name](../assembly/strong-named.md), the software publisher of the assembly, or its URL identity.</span></span> <span data-ttu-id="5ff38-113">如果程序集同时包含强名称和软件发行者标识，使用的是软件发行者标识。</span><span class="sxs-lookup"><span data-stu-id="5ff38-113">If an assembly has both a strong name and a software publisher identity, then the software publisher identity is used.</span></span> <span data-ttu-id="5ff38-114">如果程序集来自 Internet 且未签名，使用的是 URL 标识。</span><span class="sxs-lookup"><span data-stu-id="5ff38-114">If the assembly comes from the Internet and is unsigned, the URL identity is used.</span></span> <span data-ttu-id="5ff38-115">若要详细了解程序集和强名称，请参阅[使用程序集编程](../assembly/index.md)。</span><span class="sxs-lookup"><span data-stu-id="5ff38-115">For more information about assemblies and strong names, see [Programming with Assemblies](../assembly/index.md).</span></span>  
  
- <span data-ttu-id="5ff38-116">漫游存储与有漫游用户策略文件的用户一起移动。</span><span class="sxs-lookup"><span data-stu-id="5ff38-116">Roaming stores move with a user that has a roaming user profile.</span></span> <span data-ttu-id="5ff38-117">文件被写入网络目录，并下载到用户登录的所有计算机中。</span><span class="sxs-lookup"><span data-stu-id="5ff38-117">Files are written to a network directory and are downloaded to any computer the user logs into.</span></span> <span data-ttu-id="5ff38-118">若要详细了解漫游用户策略文件，请参阅 <xref:System.IO.IsolatedStorage.IsolatedStorageScope.Roaming?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="5ff38-118">For more information about roaming user profiles, see <xref:System.IO.IsolatedStorage.IsolatedStorageScope.Roaming?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="5ff38-119">通过将用户、域和程序集标识这些概念相结合，独立存储可以通过下列方式隔离数据，每种方式都有自己的使用方案：</span><span class="sxs-lookup"><span data-stu-id="5ff38-119">By combining the concepts of user, domain, and assembly identity, isolated storage can isolate data in the following ways, each of which has its own usage scenarios:</span></span>  
  
- [<span data-ttu-id="5ff38-120">按用户和程序集隔离</span><span class="sxs-lookup"><span data-stu-id="5ff38-120">Isolation by user and assembly</span></span>](#UserAssembly)  
  
- [<span data-ttu-id="5ff38-121">按用户、域和程序集隔离</span><span class="sxs-lookup"><span data-stu-id="5ff38-121">Isolation by user, domain, and assembly</span></span>](#UserDomainAssembly)  
  
 <span data-ttu-id="5ff38-122">这两种隔离都可以与漫游用户策略文件结合使用。</span><span class="sxs-lookup"><span data-stu-id="5ff38-122">Either of these isolations can be combined with a roaming user profile.</span></span> <span data-ttu-id="5ff38-123">有关详细信息，请参阅[独立存储和漫游](#Roaming)部分。</span><span class="sxs-lookup"><span data-stu-id="5ff38-123">For more information, see the section [Isolated Storage and Roaming](#Roaming).</span></span>  
  
 <span data-ttu-id="5ff38-124">下图展示了存储在不同范围的隔离情况：</span><span class="sxs-lookup"><span data-stu-id="5ff38-124">The following illustration demonstrates how stores are isolated in different scopes:</span></span>  
  
 ![显示按用户和程序集隔离的图表。](./media/types-of-isolation/isolated-storage-types.gif)  
  
 <span data-ttu-id="5ff38-126">除漫游存储外，独立存储始终按计算机隐式隔离，因为它使用指定计算机的本地存储设备。</span><span class="sxs-lookup"><span data-stu-id="5ff38-126">Except for roaming stores, isolated storage is always implicitly isolated by computer because it uses the storage facilities that are local to a given computer.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="5ff38-127">独立存储不适用于 Windows 8.x 应用商店应用。</span><span class="sxs-lookup"><span data-stu-id="5ff38-127">Isolated storage is not available for Windows 8.x Store apps.</span></span> <span data-ttu-id="5ff38-128">请改用 Windows 运行时 API 包含的 `Windows.Storage` 命名空间中的应用程序数据类来存储本地数据和文件。</span><span class="sxs-lookup"><span data-stu-id="5ff38-128">Instead, use the application data classes in the `Windows.Storage` namespaces included in the Windows Runtime API to store local data and files.</span></span> <span data-ttu-id="5ff38-129">有关详细信息，请参阅 Windows 开发人员中心的 [应用程序数据](/previous-versions/windows/apps/hh464917(v=win.10)) 。</span><span class="sxs-lookup"><span data-stu-id="5ff38-129">For more information, see [Application data](/previous-versions/windows/apps/hh464917(v=win.10)) in the Windows Dev Center.</span></span>  
  
<a name="UserAssembly"></a>
## <a name="isolation-by-user-and-assembly"></a><span data-ttu-id="5ff38-130">按用户和程序集隔离</span><span class="sxs-lookup"><span data-stu-id="5ff38-130">Isolation by User and Assembly</span></span>  
 <span data-ttu-id="5ff38-131">如果需要从任何应用的域都可以访问程序集使用的数据存储，按用户和程序集隔离更为合适。</span><span class="sxs-lookup"><span data-stu-id="5ff38-131">When the assembly that uses the data store needs to be accessible from any application's domain, isolation by user and assembly is appropriate.</span></span> <span data-ttu-id="5ff38-132">在这种情况下，独立存储通常用于存储跨多个应用的数据，而不是与任何特定应用绑定的数据，如用户名或许可证信息。</span><span class="sxs-lookup"><span data-stu-id="5ff38-132">Typically, in this situation, isolated storage is used to store data that applies across multiple applications and is not tied to any particular application, such as the user's name or license information.</span></span> <span data-ttu-id="5ff38-133">若要访问按用户和程序集隔离的存储，必须信任代码在应用之间传输信息。</span><span class="sxs-lookup"><span data-stu-id="5ff38-133">To access storage isolated by user and assembly, code must be trusted to transfer information between applications.</span></span> <span data-ttu-id="5ff38-134">通常情况下，按用户和程序集隔离可用于 Intranet，但不可用于 Internet。</span><span class="sxs-lookup"><span data-stu-id="5ff38-134">Typically, isolation by user and assembly is allowed on intranets but not on the Internet.</span></span> <span data-ttu-id="5ff38-135">调用静态 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A?displayProperty=nameWithType> 方法并传入用户和程序集 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>，即可返回采用这种隔离的存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-135">Calling the static <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A?displayProperty=nameWithType> method and passing in a user and an assembly <xref:System.IO.IsolatedStorage.IsolatedStorageScope> returns storage with this kind of isolation.</span></span>  
  
 <span data-ttu-id="5ff38-136">下面的代码示例检索按用户和程序集隔离的存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-136">The following code example retrieves a store that is isolated by user and assembly.</span></span> <span data-ttu-id="5ff38-137">可通过 `isoFile` 对象访问此存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-137">The store can be accessed through the `isoFile` object.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source11.cpp#17)]
 [!code-csharp[Conceptual.IsolatedStorage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source11.cs#17)]
 [!code-vb[Conceptual.IsolatedStorage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source11.vb#17)]  
  
 <span data-ttu-id="5ff38-138">有关使用证据参数的示例，请参阅 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%28System.IO.IsolatedStorage.IsolatedStorageScope%2CSystem.Security.Policy.Evidence%2CSystem.Type%2CSystem.Security.Policy.Evidence%2CSystem.Type%29>。</span><span class="sxs-lookup"><span data-stu-id="5ff38-138">For an example that uses the evidence parameters, see <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%28System.IO.IsolatedStorage.IsolatedStorageScope%2CSystem.Security.Policy.Evidence%2CSystem.Type%2CSystem.Security.Policy.Evidence%2CSystem.Type%29>.</span></span>  
  
 <span data-ttu-id="5ff38-139"><xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A> 方法可用作快捷方式，如下面的代码示例所示。</span><span class="sxs-lookup"><span data-stu-id="5ff38-139">The <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A> method is available as a shortcut, as shown in the following code example.</span></span> <span data-ttu-id="5ff38-140">此快捷方式不能用于打开漫游存储；在这种情况下，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>。</span><span class="sxs-lookup"><span data-stu-id="5ff38-140">This shortcut cannot be used to open stores that are capable of roaming; use <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> in such cases.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source11.cpp#18)]
 [!code-csharp[Conceptual.IsolatedStorage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source11.cs#18)]
 [!code-vb[Conceptual.IsolatedStorage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source11.vb#18)]  
  
<a name="UserDomainAssembly"></a>
## <a name="isolation-by-user-domain-and-assembly"></a><span data-ttu-id="5ff38-141">按用户、域和程序集隔离</span><span class="sxs-lookup"><span data-stu-id="5ff38-141">Isolation by User, Domain, and Assembly</span></span>  
 <span data-ttu-id="5ff38-142">如果应用使用需要专用数据存储的第三方程序集，可以使用独立存储来存储专用数据。</span><span class="sxs-lookup"><span data-stu-id="5ff38-142">If your application uses a third-party assembly that requires a private data store, you can use isolated storage to store the private data.</span></span> <span data-ttu-id="5ff38-143">按用户、域和程序集隔离可确保，仅当使用程序集的应用在程序集创建存储时正在运行时，且仅当为其创建存储的用户运行应用时，只有给定程序集中的代码才能访问数据。</span><span class="sxs-lookup"><span data-stu-id="5ff38-143">Isolation by user, domain, and assembly ensures that only code in a given assembly can access the data, and only when the assembly is used by the application that was running when the assembly created the store, and only when the user for whom the store was created runs the application.</span></span> <span data-ttu-id="5ff38-144">按用户、域和程序集隔离可防止第三方程序集将数据泄漏给其他应用。</span><span class="sxs-lookup"><span data-stu-id="5ff38-144">Isolation by user, domain, and assembly keeps the third-party assembly from leaking data to other applications.</span></span> <span data-ttu-id="5ff38-145">如果确定要使用独立存储，但不确定要使用哪种类型的隔离，此隔离类型应为默认选择。</span><span class="sxs-lookup"><span data-stu-id="5ff38-145">This isolation type should be your default choice if you know that you want to use isolated storage but are not sure which type of isolation to use.</span></span> <span data-ttu-id="5ff38-146">调用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 的静态 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 方法并传入用户、域和程序集 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>，即可返回采用这种隔离的存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-146">Calling the static <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> method of <xref:System.IO.IsolatedStorage.IsolatedStorageFile> and passing in a user, domain, and assembly <xref:System.IO.IsolatedStorage.IsolatedStorageScope> returns storage with this kind of isolation.</span></span>  
  
 <span data-ttu-id="5ff38-147">下面的代码示例检索按用户、域和程序集隔离的存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-147">The following code example retrieves a store isolated by user, domain, and assembly.</span></span> <span data-ttu-id="5ff38-148">可通过 `isoFile` 对象访问此存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-148">The store can be accessed through the `isoFile` object.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source10.cpp#14)]
 [!code-csharp[Conceptual.IsolatedStorage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source10.cs#14)]
 [!code-vb[Conceptual.IsolatedStorage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source10.vb#14)]  
  
 <span data-ttu-id="5ff38-149">另一个方法可用作快捷方式，如下面的代码示例所示。</span><span class="sxs-lookup"><span data-stu-id="5ff38-149">Another method is available as a shortcut, as shown in the following code example.</span></span> <span data-ttu-id="5ff38-150">此快捷方式不能用于打开漫游存储；在这种情况下，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>。</span><span class="sxs-lookup"><span data-stu-id="5ff38-150">This shortcut cannot be used to open stores that are capable of roaming; use <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> in such cases.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source10.cpp#15)]
 [!code-csharp[Conceptual.IsolatedStorage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source10.cs#15)]
 [!code-vb[Conceptual.IsolatedStorage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source10.vb#15)]  
  
<a name="Roaming"></a>
## <a name="isolated-storage-and-roaming"></a><span data-ttu-id="5ff38-151">独立存储和漫游</span><span class="sxs-lookup"><span data-stu-id="5ff38-151">Isolated Storage and Roaming</span></span>  
 <span data-ttu-id="5ff38-152">漫游用户策略文件是一项 Windows 功能，可便于用户在网络上设置标识，并使用此标识登录任何网络计算机，同时应用所有个性化设置。</span><span class="sxs-lookup"><span data-stu-id="5ff38-152">Roaming user profiles are a Windows feature that enables a user to set up an identity on a network and use that identity to log into any network computer, carrying over all personalized settings.</span></span> <span data-ttu-id="5ff38-153">使用独立存储的程序集可以指定，用户的独立存储应随漫游用户策略文件一起移动。</span><span class="sxs-lookup"><span data-stu-id="5ff38-153">An assembly that uses isolated storage can specify that the user's isolated storage should move with the roaming user profile.</span></span> <span data-ttu-id="5ff38-154">漫游可以与按用户和程序集隔离或按用户、域和程序集隔离结合使用。</span><span class="sxs-lookup"><span data-stu-id="5ff38-154">Roaming can be used in conjunction with isolation by user and assembly or with isolation by user, domain, and assembly.</span></span> <span data-ttu-id="5ff38-155">如果未使用漫游范围，即使使用漫游用户策略文件，存储也不会漫游。</span><span class="sxs-lookup"><span data-stu-id="5ff38-155">If a roaming scope is not used, stores will not roam even if a roaming user profile is used.</span></span>  
  
 <span data-ttu-id="5ff38-156">下面的代码示例检索按用户和程序集隔离的漫游存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-156">The following code example retrieves a roaming store isolated by user and assembly.</span></span> <span data-ttu-id="5ff38-157">可通过 `isoFile` 对象访问此存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-157">The store can be accessed through the `isoFile` object.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source9.cpp#11)]
 [!code-csharp[Conceptual.IsolatedStorage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source9.cs#11)]
 [!code-vb[Conceptual.IsolatedStorage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source9.vb#11)]  
  
 <span data-ttu-id="5ff38-158">可以添加域范围，以创建按用户、域和应用隔离的漫游存储。</span><span class="sxs-lookup"><span data-stu-id="5ff38-158">A domain scope can be added to create a roaming store isolated by user, domain, and application.</span></span> <span data-ttu-id="5ff38-159">下面的代码示例展示了此操作。</span><span class="sxs-lookup"><span data-stu-id="5ff38-159">The following code example demonstrates this.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source9.cpp#12)]
 [!code-csharp[Conceptual.IsolatedStorage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source9.cs#12)]
 [!code-vb[Conceptual.IsolatedStorage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source9.vb#12)]  
  
## <a name="see-also"></a><span data-ttu-id="5ff38-160">请参阅</span><span class="sxs-lookup"><span data-stu-id="5ff38-160">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageScope>
- [<span data-ttu-id="5ff38-161">独立存储</span><span class="sxs-lookup"><span data-stu-id="5ff38-161">Isolated Storage</span></span>](isolated-storage.md)
