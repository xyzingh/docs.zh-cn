---
title: 程序集安全注意事项
description: 在生成 .NET 程序集时，可指定该程序集运行所需的权限。 本文讨论强名称程序集和签名工具。
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET], security
- signcodes
- names [.NET], assemblies
- strong-named assemblies, security considerations
- signing assemblies
- assemblies [.NET], signing
- granting permissions, assemblies
- assemblies [.NET], strong-named
- names [.NET], strong names
- permissions [.NET], assemblies
- security [.NET], assemblies
- integrity with assemblies
ms.assetid: 1b5439c1-f3d5-4529-bd69-01814703d067
ms.openlocfilehash: 91ea206abf80da275651854b9f13aa0116b7a1c5
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687261"
---
# <a name="assembly-security-considerations"></a><span data-ttu-id="dc0ca-104">程序集安全注意事项</span><span class="sxs-lookup"><span data-stu-id="dc0ca-104">Assembly security considerations</span></span>

<span data-ttu-id="dc0ca-105">在生成程序集时，可指定该程序集运行所需的一组权限。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-105">When you build an assembly, you can specify a set of permissions that the assembly requires to run.</span></span> <span data-ttu-id="dc0ca-106">是否将特定的权限授予程序集是基于证据的。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-106">Whether certain permissions are granted or not granted to an assembly is based on evidence.</span></span>  
  
 <span data-ttu-id="dc0ca-107">使用证据有两种截然不同的方式：</span><span class="sxs-lookup"><span data-stu-id="dc0ca-107">There are two distinct ways evidence is used:</span></span>  
  
- <span data-ttu-id="dc0ca-108">将输入证据与加载程序所收集的证据合并，以创建用于策略决策的最终证据集。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-108">The input evidence is merged with the evidence gathered by the loader to create a final set of evidence used for policy resolution.</span></span> <span data-ttu-id="dc0ca-109">使用这种语义的方法包括 **Assembly.Load** 、 **Assembly.LoadFrom** 和 **Activator.CreateInstance** 。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-109">The methods that use this semantic include **Assembly.Load** , **Assembly.LoadFrom** , and **Activator.CreateInstance** .</span></span>  
  
- <span data-ttu-id="dc0ca-110">原封不动地使用输入证据作为用于策略决策的最终证据集。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-110">The input evidence is used unaltered as the final set of evidence used for policy resolution.</span></span> <span data-ttu-id="dc0ca-111">使用这种语义的方法包括 **Assembly.Load(byte[])** 和 **AppDomain.DefineDynamicAssembly()** 。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-111">The methods that use this semantic include **Assembly.Load(byte[])** and **AppDomain.DefineDynamicAssembly()** .</span></span>  
  
  <span data-ttu-id="dc0ca-112">通过在将运行程序集的计算机上设置[安全策略](../../framework/misc/code-access-security-basics.md)，可以授予一些可选的权限。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-112">Optional permissions can be granted by the [security policy](../../framework/misc/code-access-security-basics.md) set on the computer where the assembly will run.</span></span> <span data-ttu-id="dc0ca-113">如果你希望代码可以处理所有潜在的安全异常，可以执行以下操作之一：</span><span class="sxs-lookup"><span data-stu-id="dc0ca-113">If you want your code to handle all potential security exceptions, you can do one of the following:</span></span>  
  
- <span data-ttu-id="dc0ca-114">为您的代码必须具有的所有权限插入权限请求，并预先处理在未授予权限时发生的加载时错误。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-114">Insert a permission request for all the permissions your code must have, and handle up front the load-time failure that occurs if the permissions are not granted.</span></span>  
  
- <span data-ttu-id="dc0ca-115">不要使用权限请求来获取您的代码可能需要的权限，但一定要准备处理在未授予权限时发生的安全异常。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-115">Do not use a permission request to obtain permissions your code might need, but be prepared to handle security exceptions if permissions are not granted.</span></span>  
  
  > [!NOTE]
  > <span data-ttu-id="dc0ca-116">安全性是一个较为复杂的领域，您将要作出很多选择。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-116">Security is a complex area, and you have many options to choose from.</span></span> <span data-ttu-id="dc0ca-117">有关详细信息，请参阅[安全性的基础概念](../security/key-security-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-117">For more information, see [Key Security Concepts](../security/key-security-concepts.md).</span></span>  
  
 <span data-ttu-id="dc0ca-118">在加载时，程序集的证据用作安全策略的输入。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-118">At load time, the assembly's evidence is used as input to security policy.</span></span> <span data-ttu-id="dc0ca-119">安全策略是由企业和计算机的管理员以及用户策略设置建立的，它在执行时确定向所有托管代码授予的权限组。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-119">Security policy is established by the enterprise and the computer's administrator as well as by user policy settings, and determines the set of permissions that is granted to all managed code when executed.</span></span> <span data-ttu-id="dc0ca-120">可以为该程序集（如果该程序集具有签名工具生成的签名）的发行者建立安全策略，或者为该程序集的下载网站和区域（就 Internet Explorer 而言）建立安全策略，也可以为该程序集的强名称建立该策略。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-120">Security policy can be established for the publisher of the assembly (if it has a signing tool generated signature), for the Web site and zone (in Internet Explorer terms) the assembly was downloaded from, or for the assembly's strong name.</span></span> <span data-ttu-id="dc0ca-121">例如，一台计算机的管理员可以建立这样一种安全策略：它允许从某一网站下载由指定软件公司签发用以访问计算机上的数据库的所有代码，但不授予对该计算机磁盘的写访问权。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-121">For example, a computer's administrator can establish security policy that allows all code downloaded from a Web site and signed by a given software company to access a database on a computer, but does not grant access to write to the computer's disk.</span></span>  
  
## <a name="strong-named-assemblies-and-signing-tools"></a><span data-ttu-id="dc0ca-122">强名称程序集和签名工具</span><span class="sxs-lookup"><span data-stu-id="dc0ca-122">Strong-named assemblies and signing tools</span></span>  

 > [!WARNING]
 > <span data-ttu-id="dc0ca-123">不要依赖于通过强名称实现安全性。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-123">Do not rely on strong names for security.</span></span> <span data-ttu-id="dc0ca-124">它们仅提供唯一的标识。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-124">They provide a unique identity only.</span></span>

 <span data-ttu-id="dc0ca-125">可采用两种不同但相互补充的方式对程序集进行签名：使用强名称或使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-125">You can sign an assembly in two different but complementary ways: with a strong name or by using  [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md).</span></span> <span data-ttu-id="dc0ca-126">使用强名称对程序集进行签名将向包含程序集清单的文件添加公钥加密。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-126">Signing an assembly with a strong name adds public key encryption to the file containing the assembly manifest.</span></span> <span data-ttu-id="dc0ca-127">强名称签名帮助验证名称的唯一性，避免名称欺骗，并在解析引用时向调用方提供某标识。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-127">Strong name signing helps to verify name uniqueness, prevent name spoofing, and provide callers with some identity when a reference is resolved.</span></span>  
  
 <span data-ttu-id="dc0ca-128">任何信任级别都不会与一个强名称关联，这就使 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)变得十分重要。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-128">No level of trust is associated with a strong name, which makes [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) important.</span></span> <span data-ttu-id="dc0ca-129">这两个签名工具要求发行者向第三方证书颁发机构证实其标识并获取证书。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-129">The two signing tools require a publisher to prove its identity to a third-party authority and obtain a certificate.</span></span> <span data-ttu-id="dc0ca-130">然后此证书将嵌入到你的文件中，并且管理员能够使用该证书来决定是否相信这些代码的真实性。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-130">This certificate is then embedded in your file and can be used by an administrator to decide whether to trust the code's authenticity.</span></span>  
  
 <span data-ttu-id="dc0ca-131">可将强名称和使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)创建的数字签名一起提供给程序集，或者可以单独使用其中之一。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-131">You can give both a strong name and a digital signature created using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) to an assembly, or you can use either alone.</span></span> <span data-ttu-id="dc0ca-132">这两个签名工具一次只能对一个文件进行签名，对于多文件程序集，您可以对包含程序集清单的文件进行签名。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-132">The two signing tools can sign only one file at a time; for a multifile assembly, you sign the file that contains the assembly manifest.</span></span> <span data-ttu-id="dc0ca-133">强名称存储在包含程序集清单的文件中，但使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)创建的签名存储在该程序集清单所在的可迁移可执行 (PE) 文件中保留的槽中。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-133">A strong name is stored in the file containing the assembly manifest, but a signature created using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) is stored in a reserved slot in the portable executable (PE) file containing the assembly manifest.</span></span> <span data-ttu-id="dc0ca-134">在已具有依赖于 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)生成的签名的信任层次结构时，或者当策略只使用密钥部分并且不检查信任链时，就可以使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)对程序集进行的签名（带或不带强名称）。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-134">Signing of an assembly using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) can be used (with or without a strong name) when you already have a trust hierarchy that relies on [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) generated signatures, or when your policy uses only the key portion and does not check a chain of trust.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="dc0ca-135">在一个程序集上同时使用强名称和签名工具签名时，必须首先分配强名称。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-135">When using both a strong name and a signing tool signature on an assembly, the strong name must be assigned first.</span></span>  
  
 <span data-ttu-id="dc0ca-136">公共语言运行时还将执行哈希验证；程序集清单包含构成该程序集的所有文件的列表，包括当生成清单时存在的每一文件的散列。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-136">The common language runtime also performs a hash verification; the assembly manifest contains a list of all files that make up the assembly, including a hash of each file as it existed when the manifest was built.</span></span> <span data-ttu-id="dc0ca-137">在加载每个文件时，将对文件的内容进行哈希处理，并将该内容与存储在清单中的哈希值进行比较。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-137">As each file is loaded, its contents are hashed and compared with the hash value stored in the manifest.</span></span> <span data-ttu-id="dc0ca-138">如果两个哈希值不匹配，则将无法加载该程序集。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-138">If the two hashes do not match, the assembly fails to load.</span></span>  
  
 <span data-ttu-id="dc0ca-139">因为强命名和使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)进行签名确保了完整性，因此可将代码访问安全策略建立在这两种形式的程序集证据的基础上。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-139">Because strong naming and signing using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) guarantee integrity, you can base code access security policy on these two forms of assembly evidence.</span></span> <span data-ttu-id="dc0ca-140">强命名和使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md)进行签名通过数字签名和证书来确保完整性。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-140">Strong naming and signing using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) guarantee integrity through digital signatures and certificates.</span></span> <span data-ttu-id="dc0ca-141">上面提到的所有技术（哈希验证、强命名和使用 [SignTool.exe（签名工具）](../../framework/tools/signtool-exe.md) 进行签名）可协同工作，确保程序集没有做过任何方式的改动。</span><span class="sxs-lookup"><span data-stu-id="dc0ca-141">All the technologies mentioned—hash verification, strong naming, and signing using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md)—work together to ensure that the assembly has not been altered in any way.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dc0ca-142">请参阅</span><span class="sxs-lookup"><span data-stu-id="dc0ca-142">See also</span></span>

- [<span data-ttu-id="dc0ca-143">具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="dc0ca-143">Strong-named assemblies</span></span>](strong-named.md)
- [<span data-ttu-id="dc0ca-144">.NET 中的程序集</span><span class="sxs-lookup"><span data-stu-id="dc0ca-144">Assemblies in .NET</span></span>](index.md)
- [<span data-ttu-id="dc0ca-145">SignTool.exe（签名工具）</span><span class="sxs-lookup"><span data-stu-id="dc0ca-145">SignTool.exe (Sign Tool)</span></span>](../../framework/tools/signtool-exe.md)
