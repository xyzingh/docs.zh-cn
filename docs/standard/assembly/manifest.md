---
title: 程序集清单
description: .NET 程序集清单指定其版本要求、安全标识和程序集的范围以及要解析引用的信息。
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest
- dynamic assemblies, assembly manifest
- metadata, assembly manifest
- culture, assembly manifest
- assemblies [.NET], metadata
ms.assetid: 8e40fab9-549d-4731-aec2-ffa47a382de0
ms.openlocfilehash: 4b3bf6f7f6b8cf459a13dd0aca45069f82d01130
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687587"
---
# <a name="assembly-manifest"></a><span data-ttu-id="32e08-103">程序集清单</span><span class="sxs-lookup"><span data-stu-id="32e08-103">Assembly manifest</span></span>

<span data-ttu-id="32e08-104">每一程序集，无论是静态的还是动态的，均包含描述该程序集中各元素彼此如何关联的数据集合。</span><span class="sxs-lookup"><span data-stu-id="32e08-104">Every assembly, whether static or dynamic, contains a collection of data that describes how the elements in the assembly relate to each other.</span></span> <span data-ttu-id="32e08-105">程序集清单就包含这些程序集元数据。</span><span class="sxs-lookup"><span data-stu-id="32e08-105">The assembly manifest contains this assembly metadata.</span></span> <span data-ttu-id="32e08-106">程序集清单包含指定该程序集的版本要求和安全标识所需的所有元数据，以及定义该程序集的范围和解析对资源和类的引用所需的全部元数据。</span><span class="sxs-lookup"><span data-stu-id="32e08-106">An assembly manifest contains all the metadata needed to specify the assembly's version requirements and security identity, and all metadata needed to define the scope of the assembly and resolve references to resources and classes.</span></span> <span data-ttu-id="32e08-107">程序集清单可以存储在具有 Microsoft 中间语言 (MSIL) 代码的 PE 文件（.exe 或 .dll）中，也可存储在只包含程序集清单信息的独立 PE 文件中 。</span><span class="sxs-lookup"><span data-stu-id="32e08-107">The assembly manifest can be stored in either a PE file (an *.exe* or *.dll* ) with Microsoft intermediate language (MSIL) code or in a standalone PE file that contains only assembly manifest information.</span></span>  
  
 <span data-ttu-id="32e08-108">以下插图显示了清单的不同存储方法。</span><span class="sxs-lookup"><span data-stu-id="32e08-108">The following illustration shows the different ways the manifest can be stored.</span></span>  
  
 ![显示单文件程序集和多文件程序集配置中的清单的图表。](./media/manifest/assembly-types-diagram.gif)  
  
 <span data-ttu-id="32e08-110">对于有一个关联文件的程序集，该清单将被合并到 PE 文件中以构成单文件程序集。</span><span class="sxs-lookup"><span data-stu-id="32e08-110">For an assembly with one associated file, the manifest is incorporated into the PE file to form a single-file assembly.</span></span> <span data-ttu-id="32e08-111">您可以创建有独立的清单文件，或清单被合并到同一多文件程序集中某一 PE 文件的多文件程序集。</span><span class="sxs-lookup"><span data-stu-id="32e08-111">You can create a multifile assembly with a standalone manifest file or with the manifest incorporated into one of the PE files in the assembly.</span></span>  
  
 <span data-ttu-id="32e08-112">每一程序集的清单均执行以下功能：</span><span class="sxs-lookup"><span data-stu-id="32e08-112">Each assembly's manifest performs the following functions:</span></span>  
  
- <span data-ttu-id="32e08-113">枚举构成该程序集的文件。</span><span class="sxs-lookup"><span data-stu-id="32e08-113">Enumerates the files that make up the assembly.</span></span>  
  
- <span data-ttu-id="32e08-114">控制对该程序集的类型和资源的引用如何映射到包含其声明和实现的文件。</span><span class="sxs-lookup"><span data-stu-id="32e08-114">Governs how references to the assembly's types and resources map to the files that contain their declarations and implementations.</span></span>  
  
- <span data-ttu-id="32e08-115">枚举该程序集所依赖的其他程序集。</span><span class="sxs-lookup"><span data-stu-id="32e08-115">Enumerates other assemblies on which the assembly depends.</span></span>  
  
- <span data-ttu-id="32e08-116">在程序集的使用者和程序集的实现详细信息的使用者之间提供一定程度的间接性。</span><span class="sxs-lookup"><span data-stu-id="32e08-116">Provides a level of indirection between consumers of the assembly and the assembly's implementation details.</span></span>  
  
- <span data-ttu-id="32e08-117">呈现程序集自述。</span><span class="sxs-lookup"><span data-stu-id="32e08-117">Renders the assembly self-describing.</span></span>  
  
## <a name="assembly-manifest-contents"></a><span data-ttu-id="32e08-118">程序集清单内容</span><span class="sxs-lookup"><span data-stu-id="32e08-118">Assembly manifest contents</span></span>  
 <span data-ttu-id="32e08-119">下表显示了在程序集清单中包含的信息。</span><span class="sxs-lookup"><span data-stu-id="32e08-119">The following table shows the information contained in the assembly manifest.</span></span> <span data-ttu-id="32e08-120">前四项：程序集名称、版本号、区域性和强名称信息共同构成了程序集的标识。</span><span class="sxs-lookup"><span data-stu-id="32e08-120">The first four items: assembly name, version number, culture, and strong name information make up the assembly's identity.</span></span>  
  
|<span data-ttu-id="32e08-121">信息</span><span class="sxs-lookup"><span data-stu-id="32e08-121">Information</span></span>|<span data-ttu-id="32e08-122">描述</span><span class="sxs-lookup"><span data-stu-id="32e08-122">Description</span></span>|  
|-----------------|-----------------|  
|<span data-ttu-id="32e08-123">程序集名称</span><span class="sxs-lookup"><span data-stu-id="32e08-123">Assembly name</span></span>|<span data-ttu-id="32e08-124">指定程序集名称的文本字符串。</span><span class="sxs-lookup"><span data-stu-id="32e08-124">A text string specifying the assembly's name.</span></span>|  
|<span data-ttu-id="32e08-125">版本号</span><span class="sxs-lookup"><span data-stu-id="32e08-125">Version number</span></span>|<span data-ttu-id="32e08-126">主版本号和次版本号，以及修订号和生成号。</span><span class="sxs-lookup"><span data-stu-id="32e08-126">A major and minor version number, and a revision and build number.</span></span> <span data-ttu-id="32e08-127">公共语言运行时使用这些编号来强制实施版本策略。</span><span class="sxs-lookup"><span data-stu-id="32e08-127">The common language runtime uses these numbers to enforce version policy.</span></span>|  
|<span data-ttu-id="32e08-128">culture</span><span class="sxs-lookup"><span data-stu-id="32e08-128">Culture</span></span>|<span data-ttu-id="32e08-129">有关该程序集支持的区域性或语言的信息。</span><span class="sxs-lookup"><span data-stu-id="32e08-129">Information on the culture or language the assembly supports.</span></span> <span data-ttu-id="32e08-130">此信息只应用于将一个程序集指定为包含特定区域性或特定语言信息的附属程序集。</span><span class="sxs-lookup"><span data-stu-id="32e08-130">This information should be used only to designate an assembly as a satellite assembly containing culture- or language-specific information.</span></span> <span data-ttu-id="32e08-131">（具有区域性信息的程序集被自动假定为附属程序集。）</span><span class="sxs-lookup"><span data-stu-id="32e08-131">(An assembly with culture information is automatically assumed to be a satellite assembly.)</span></span>|  
|<span data-ttu-id="32e08-132">强名称信息</span><span class="sxs-lookup"><span data-stu-id="32e08-132">Strong name information</span></span>|<span data-ttu-id="32e08-133">如果已经为程序集提供了一个强名称，则为来自发行者的公钥。</span><span class="sxs-lookup"><span data-stu-id="32e08-133">The public key from the publisher if the assembly has been given a strong name.</span></span>|  
|<span data-ttu-id="32e08-134">程序集中所有文件的列表</span><span class="sxs-lookup"><span data-stu-id="32e08-134">List of all files in the assembly</span></span>|<span data-ttu-id="32e08-135">在程序集中包含的每一文件的散列及文件名。</span><span class="sxs-lookup"><span data-stu-id="32e08-135">A hash of each file contained in the assembly and a file name.</span></span> <span data-ttu-id="32e08-136">请注意，构成程序集的所有文件所在的目录必须是包含该程序集清单的文件所在的目录。</span><span class="sxs-lookup"><span data-stu-id="32e08-136">Note that all files that make up the assembly must be in the same directory as the file containing the assembly manifest.</span></span>|  
|<span data-ttu-id="32e08-137">类型引用信息</span><span class="sxs-lookup"><span data-stu-id="32e08-137">Type reference information</span></span>|<span data-ttu-id="32e08-138">运行时用来将类型引用映射到包含其声明和实现的文件的信息。</span><span class="sxs-lookup"><span data-stu-id="32e08-138">Information used by the runtime to map a type reference to the file that contains its declaration and implementation.</span></span> <span data-ttu-id="32e08-139">该信息用于从程序集导出的类型。</span><span class="sxs-lookup"><span data-stu-id="32e08-139">This is used for types that are exported from the assembly.</span></span>|  
|<span data-ttu-id="32e08-140">有关被引用程序集的信息</span><span class="sxs-lookup"><span data-stu-id="32e08-140">Information on referenced assemblies</span></span>|<span data-ttu-id="32e08-141">该程序集静态引用的其他程序集的列表。</span><span class="sxs-lookup"><span data-stu-id="32e08-141">A list of other assemblies that are statically referenced by the assembly.</span></span> <span data-ttu-id="32e08-142">如果依赖的程序集具有强名称，则每一引用均包括该依赖程序集的名称、程序集元数据（版本、区域性、操作系统等）和公钥。</span><span class="sxs-lookup"><span data-stu-id="32e08-142">Each reference includes the dependent assembly's name, assembly metadata (version, culture, operating system, and so on), and public key, if the assembly is strong named.</span></span>|  
  
 <span data-ttu-id="32e08-143">通过在代码中使用程序集特性，您可以添加或更改程序集清单中的一些信息。</span><span class="sxs-lookup"><span data-stu-id="32e08-143">You can add or change some information in the assembly manifest by using assembly attributes in your code.</span></span> <span data-ttu-id="32e08-144">您可以更改版本信息和信息性特性，包括商标、版权、产品、公司和信息性版本。</span><span class="sxs-lookup"><span data-stu-id="32e08-144">You can change version information and informational attributes, including Trademark, Copyright, Product, Company, and Informational Version.</span></span> <span data-ttu-id="32e08-145">有关程序集特性的完整列表，请参阅[设置程序集属性](set-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="32e08-145">For a complete list of assembly attributes, see [Set assembly attributes](set-attributes.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="32e08-146">请参阅</span><span class="sxs-lookup"><span data-stu-id="32e08-146">See also</span></span>

- [<span data-ttu-id="32e08-147">程序集内容</span><span class="sxs-lookup"><span data-stu-id="32e08-147">Assembly contents</span></span>](contents.md)
- [<span data-ttu-id="32e08-148">程序集版本控制</span><span class="sxs-lookup"><span data-stu-id="32e08-148">Assembly versioning</span></span>](versioning.md)
- [<span data-ttu-id="32e08-149">创建附属程序集</span><span class="sxs-lookup"><span data-stu-id="32e08-149">Create satellite assemblies</span></span>](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
- [<span data-ttu-id="32e08-150">具有强名称的程序集</span><span class="sxs-lookup"><span data-stu-id="32e08-150">Strong-named assemblies</span></span>](strong-named.md)
