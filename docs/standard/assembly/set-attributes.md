---
title: 设置程序集属性
description: 可以设置 .NET 程序集的程序集属性，包括程序集标识、信息性、程序集清单和强名称属性。
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET], attributes
- assembly binding, attributes
- assembly manifest, attributes
ms.assetid: 36a98a81-b5b5-4c19-912a-11f91eff7f4e
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 32318d647dee8f3f397e3497e7c2da640bd492d0
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687685"
---
# <a name="set-assembly-attributes"></a><span data-ttu-id="4a0d4-103">设置程序集属性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-103">Set assembly attributes</span></span>

<span data-ttu-id="4a0d4-104">程序集特性是提供程序集相关信息的值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-104">Assembly attributes are values that provide information about an assembly.</span></span> <span data-ttu-id="4a0d4-105">特性分为以下几组信息：</span><span class="sxs-lookup"><span data-stu-id="4a0d4-105">The attributes are divided into the following sets of information:</span></span>

- <span data-ttu-id="4a0d4-106">程序集标识特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-106">Assembly identity attributes</span></span>

- <span data-ttu-id="4a0d4-107">信息性特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-107">Informational attributes</span></span>

- <span data-ttu-id="4a0d4-108">程序集清单特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-108">Assembly manifest attributes</span></span>

- <span data-ttu-id="4a0d4-109">强名称特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-109">Strong name attributes</span></span>

## <a name="assembly-identity-attributes"></a><span data-ttu-id="4a0d4-110">程序集标识特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-110">Assembly identity attributes</span></span>

<span data-ttu-id="4a0d4-111">三个特性与强名称（如果适用）组合起来可以确定程序集的标识：名称、版本和区域性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-111">Three attributes, together with a strong name (if applicable), determine the identity of an assembly: name, version, and culture.</span></span> <span data-ttu-id="4a0d4-112">这些特性构成程序集的完整名称，在代码中引用程序集时必需使用。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-112">These attributes form the full name of the assembly and are required when referencing the assembly in code.</span></span> <span data-ttu-id="4a0d4-113">特性可用于设置程序集的版本和区域性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-113">You can use attributes to set an assembly's version and culture.</span></span> <span data-ttu-id="4a0d4-114">编译器或 [程序集链接器 (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) 依据包含程序集清单的文件在创建该程序集时设置名称值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-114">The compiler or the [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) sets the name value when the assembly is created, based on the file containing the assembly manifest.</span></span>

<span data-ttu-id="4a0d4-115">下表介绍了版本和区域性特性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-115">The following table describes the version and culture attributes.</span></span>

|<span data-ttu-id="4a0d4-116">程序集标识特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-116">Assembly identity attribute</span></span>|<span data-ttu-id="4a0d4-117">描述</span><span class="sxs-lookup"><span data-stu-id="4a0d4-117">Description</span></span>|
|---------------------------------|-----------------|
|<xref:System.Reflection.AssemblyCultureAttribute>|<span data-ttu-id="4a0d4-118">表示程序集所支持的区域性的枚举字段。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-118">Enumerated field indicating the culture that the assembly supports.</span></span> <span data-ttu-id="4a0d4-119">程序集还可以指定区域性独立性，表示它包含默认区域性的资源。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-119">An assembly can also specify culture independence, indicating that it contains the resources for the default culture.</span></span> <span data-ttu-id="4a0d4-120">**注意：** 运行时将任何没有将区域性属性设置为 null 的程序集视为附属程序集。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-120">**Note:**  The runtime treats any assembly that does not have the culture attribute set to null as a satellite assembly.</span></span> <span data-ttu-id="4a0d4-121">此类程序集需遵循附属程序集绑定规则。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-121">Such assemblies are subject to satellite assembly binding rules.</span></span> <span data-ttu-id="4a0d4-122">有关详细信息，请参阅[运行时如何定位程序集](../../framework/deployment/how-the-runtime-locates-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-122">For more information, see [How the runtime locates assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).</span></span>|
|<xref:System.Reflection.AssemblyFlagsAttribute>|<span data-ttu-id="4a0d4-123">设置程序集特性（例如是否可以并行运行程序集）的值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-123">Value that sets assembly attributes, such as whether the assembly can be run side by side.</span></span>|
|<xref:System.Reflection.AssemblyVersionAttribute>|<span data-ttu-id="4a0d4-124">以 *主版本* . *次版本* . *内部版本* . *修订版本* 为格式的数值（例如 2.4.0.0）。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-124">Numeric value in the format *major* . *minor* . *build* . *revision* (for example, 2.4.0.0).</span></span> <span data-ttu-id="4a0d4-125">公共语言运行时使用此值在强名称程序集中执行绑定操作。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-125">The common language runtime uses this value to perform binding operations in strong-named assemblies.</span></span> <span data-ttu-id="4a0d4-126">**注意：** 如果 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 特性不适用于程序集，则 <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType>、<xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> 属性使用由 <xref:System.Reflection.AssemblyVersionAttribute> 特性指定的版本号。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-126">**Note:**  If the <xref:System.Reflection.AssemblyInformationalVersionAttribute> attribute is not applied to an assembly, the version number specified by the <xref:System.Reflection.AssemblyVersionAttribute> attribute is used by the <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType>, <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType>, and <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> properties.</span></span>|

<span data-ttu-id="4a0d4-127">下面的示例演示了如何将版本和区域性特性应用到程序集中。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-127">The following code example shows how to apply the version and culture attributes to an assembly.</span></span>

```cpp
// Set version number for the assembly.
[assembly:AssemblyVersionAttribute("4.3.2.1")];
// Set culture as German.
[assembly:AssemblyCultureAttribute("de")];
```

```csharp
// Set version number for the assembly.
[assembly:AssemblyVersionAttribute("4.3.2.1")]
// Set culture as German.
[assembly:AssemblyCultureAttribute("de")]
```

```vb
' Set version number for the assembly.
<Assembly:AssemblyVersionAttribute("4.3.2.1")>
' Set culture as German.
<Assembly:AssemblyCultureAttribute("de")>
```

## <a name="informational-attributes"></a><span data-ttu-id="4a0d4-128">信息性特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-128">Informational attributes</span></span>

<span data-ttu-id="4a0d4-129">信息性特性可用于提供程序集的其他公司或产品信息。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-129">You can use informational attributes to provide additional company or product information for an assembly.</span></span> <span data-ttu-id="4a0d4-130">下表介绍了可应用于程序集的信息性特性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-130">The following table describes the informational attributes you can apply to an assembly.</span></span>

|<span data-ttu-id="4a0d4-131">信息性特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-131">Informational attribute</span></span>|<span data-ttu-id="4a0d4-132">描述</span><span class="sxs-lookup"><span data-stu-id="4a0d4-132">Description</span></span>|
|-----------------------------|-----------------|
|<xref:System.Reflection.AssemblyCompanyAttribute>|<span data-ttu-id="4a0d4-133">指定公司名称的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-133">String value specifying a company name.</span></span>|
|<xref:System.Reflection.AssemblyCopyrightAttribute>|<span data-ttu-id="4a0d4-134">指定版权信息的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-134">String value specifying copyright information.</span></span>|
|<xref:System.Reflection.AssemblyFileVersionAttribute>|<span data-ttu-id="4a0d4-135">指定 Win32 文件版本号的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-135">String value specifying the Win32 file version number.</span></span> <span data-ttu-id="4a0d4-136">通常默认为程序集版本。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-136">This normally defaults to the assembly version.</span></span>|
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|<span data-ttu-id="4a0d4-137">指定公共语言运行时未使用的版本信息（例如完整的产品版本号）的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-137">String value specifying version information that is not used by the common language runtime, such as a full product version number.</span></span> <span data-ttu-id="4a0d4-138">**注意：** 如果将此属性应用于程序集，可以在运行时使用 <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType> 属性获取它指定的字符串。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-138">**Note:**  If this attribute is applied to an assembly, the string it specifies can be obtained at run time by using the <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="4a0d4-139">此字符串还用于 <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> 属性所提供的路径和注册表项。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-139">The string is also used in the path and registry key provided by the <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> and <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> properties.</span></span>|
|<xref:System.Reflection.AssemblyProductAttribute>|<span data-ttu-id="4a0d4-140">指定产品信息的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-140">String value specifying product information.</span></span>|
|<xref:System.Reflection.AssemblyTrademarkAttribute>|<span data-ttu-id="4a0d4-141">指定商标信息的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-141">String value specifying trademark information.</span></span>|

<span data-ttu-id="4a0d4-142">这些特性可以出现在程序集的 Windows 属性页上，或使用 **/win32res** 编译器选项重写，以指定自己的 Win32 资源文件。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-142">These attributes can appear on the Windows Properties page of the assembly, or they can be overridden using the **/win32res** compiler option to specify your own Win32 resource file.</span></span>

## <a name="assembly-manifest-attributes"></a><span data-ttu-id="4a0d4-143">程序集清单特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-143">Assembly manifest attributes</span></span>

<span data-ttu-id="4a0d4-144">程序集清单特性可用于在程序集清单中提供标题、说明、默认别名和配置等信息。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-144">You can use assembly manifest attributes to provide information in the assembly manifest, including title, description, the default alias, and configuration.</span></span> <span data-ttu-id="4a0d4-145">下表介绍了程序集清单特性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-145">The following table describes the assembly manifest attributes.</span></span>

|<span data-ttu-id="4a0d4-146">程序集清单特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-146">Assembly manifest attribute</span></span>|<span data-ttu-id="4a0d4-147">描述</span><span class="sxs-lookup"><span data-stu-id="4a0d4-147">Description</span></span>|
|---------------------------------|-----------------|
|<xref:System.Reflection.AssemblyConfigurationAttribute>|<span data-ttu-id="4a0d4-148">表示程序集配置（如零售或调试）的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-148">String value indicating the configuration of the assembly, such as Retail or Debug.</span></span> <span data-ttu-id="4a0d4-149">运行时不使用此规则。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-149">The runtime does not use this value.</span></span>|
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|<span data-ttu-id="4a0d4-150">指定引用程序集所用的默认别名的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-150">String value specifying a default alias to be used by referencing assemblies.</span></span> <span data-ttu-id="4a0d4-151">此值会在程序集本身的名称不友好（例如 GUID 值）的情况下提供一个友好名称。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-151">This value provides a friendly name when the name of the assembly itself is not friendly (such as a GUID value).</span></span> <span data-ttu-id="4a0d4-152">此值还可用于完整程序集名称的缩写。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-152">This value can also be used as a short form of the full assembly name.</span></span>|
|<xref:System.Reflection.AssemblyDescriptionAttribute>|<span data-ttu-id="4a0d4-153">指定描述程序集性质和用途简短说明的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-153">String value specifying a short description that summarizes the nature and purpose of the assembly.</span></span>|
|<xref:System.Reflection.AssemblyTitleAttribute>|<span data-ttu-id="4a0d4-154">指定程序集的友好名称的字符串值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-154">String value specifying a friendly name for the assembly.</span></span> <span data-ttu-id="4a0d4-155">例如，名为 comdlg 的程序集的标题可能是“Microsoft 通用对话框控件”。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-155">For example, an assembly named *comdlg* might have the title Microsoft Common Dialog Control.</span></span>|

## <a name="strong-name-attributes"></a><span data-ttu-id="4a0d4-156">强名称特性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-156">Strong name attributes</span></span>

<span data-ttu-id="4a0d4-157">强名称特性可用于设置程序集的强名称。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-157">You can use strong name attributes to set a strong name for an assembly.</span></span> <span data-ttu-id="4a0d4-158">下表介绍了强名称特性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-158">The following table describes the strong name attributes.</span></span>

|<span data-ttu-id="4a0d4-159">强名称属性</span><span class="sxs-lookup"><span data-stu-id="4a0d4-159">Strong name attribute</span></span>|<span data-ttu-id="4a0d4-160">描述</span><span class="sxs-lookup"><span data-stu-id="4a0d4-160">Description</span></span>|
|----------------------------|-----------------|
|<xref:System.Reflection.AssemblyDelaySignAttribute>|<span data-ttu-id="4a0d4-161">表示正在使用延迟签名的布尔值。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-161">Boolean value indicating that delay signing is being used.</span></span>|
|<xref:System.Reflection.AssemblyKeyFileAttribute>|<span data-ttu-id="4a0d4-162">表示文件名称的字符串值，该文件包含公钥（如果使用延迟签名）或同时包含作为参数传递给此特性的构造函数的公钥和私钥。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-162">String value indicating the name of the file that contains either the public key (if using delay signing) or both the public and private keys passed as a parameter to the constructor of this attribute.</span></span> <span data-ttu-id="4a0d4-163">请注意，文件名与输出文件路径（.exe 或.dll）有关，与源文件路径无关 。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-163">Note that the file name is relative to the output file path (the *.exe* or *.dll* ), not the source file path.</span></span>|
|<xref:System.Reflection.AssemblyKeyNameAttribute>|<span data-ttu-id="4a0d4-164">表示包含作为参数传递给此特性的构造函数的密钥对的密钥容器。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-164">Indicates the key container that contains the key pair passed as a parameter to the constructor of this attribute.</span></span>|

<span data-ttu-id="4a0d4-165">以下代码示例显示了使用延迟签名创建具有名为 myKey.snk 的公钥文件的强名称程序集时要应用的属性。</span><span class="sxs-lookup"><span data-stu-id="4a0d4-165">The following code example shows the attributes to apply when using delay signing to create a strong-named assembly with a public key file called *myKey.snk* .</span></span>

```cpp
[assembly:AssemblyKeyFileAttribute("myKey.snk")];
[assembly:AssemblyDelaySignAttribute(true)];
```

```csharp
[assembly:AssemblyKeyFileAttribute("myKey.snk")]
[assembly:AssemblyDelaySignAttribute(true)]
```

```vb
<Assembly:AssemblyKeyFileAttribute("myKey.snk")>
<Assembly:AssemblyDelaySignAttribute(True)>
```

## <a name="see-also"></a><span data-ttu-id="4a0d4-166">请参阅</span><span class="sxs-lookup"><span data-stu-id="4a0d4-166">See also</span></span>

- [<span data-ttu-id="4a0d4-167">创建程序集</span><span class="sxs-lookup"><span data-stu-id="4a0d4-167">Create assemblies</span></span>](create.md)
