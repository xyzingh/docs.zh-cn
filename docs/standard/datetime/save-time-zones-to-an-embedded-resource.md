---
title: 如何：将时区保存到嵌入的资源中
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET], saving
- time zone objects [.NET], serializing
- time zone objects [.NET], saving
ms.assetid: 3c96d83a-a057-4496-abb0-8f4b12712558
ms.openlocfilehash: 3d355003b3e6309644fa1ccaf779b2e63b0523d2
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063399"
---
# <a name="how-to-save-time-zones-to-an-embedded-resource"></a><span data-ttu-id="f2b5d-102">如何：将时区保存到嵌入的资源中</span><span class="sxs-lookup"><span data-stu-id="f2b5d-102">How to: Save time zones to an embedded resource</span></span>

<span data-ttu-id="f2b5d-103">时区感知应用程序通常要求存在特定时区。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-103">A time zone-aware application often requires the presence of a particular time zone.</span></span> <span data-ttu-id="f2b5d-104">但是，由于单个对象的可用性 <xref:System.TimeZoneInfo> 取决于存储在本地系统的注册表中的信息，因此可能不存在通常可用的时区。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-104">However, because the availability of individual <xref:System.TimeZoneInfo> objects depends on information stored in the local system's registry, even customarily available time zones may be absent.</span></span> <span data-ttu-id="f2b5d-105">此外，通过使用方法实例化的自定义时区的相关信息 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 不会与注册表中的其他时区信息一起存储。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-105">In addition, information about custom time zones instantiated by using the <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> method is not stored with other time zone information in the registry.</span></span> <span data-ttu-id="f2b5d-106">若要确保这些时区在需要时可用，可以通过序列化它们来保存，然后通过反序列化它们来还原它们。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-106">To ensure that these time zones are available when they are needed, you can save them by serializing them, and later restore them by deserializing them.</span></span>

<span data-ttu-id="f2b5d-107">通常，序列化 <xref:System.TimeZoneInfo> 对象的过程与时区感知应用程序分离。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-107">Typically, serializing a <xref:System.TimeZoneInfo> object occurs apart from the time zone-aware application.</span></span> <span data-ttu-id="f2b5d-108">根据用于保存序列化对象的数据存储区 <xref:System.TimeZoneInfo> ，时区数据可以作为安装或安装例程的一部分进行序列化 (例如，将数据存储在注册表) 的应用程序密钥中，或作为在编译最终应用程序之前运行的实用工具例程的一部分 (例如，当将序列化数据存储在 .NET XML 资源 ( .resx) 文件) 时。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-108">Depending on the data store used to hold serialized <xref:System.TimeZoneInfo> objects, time zone data may be serialized as part of a setup or installation routine (for example, when the data is stored in an application key of the registry), or as part of a utility routine that runs before the final application is compiled (for example, when the serialized data is stored in a .NET XML resource (.resx) file).</span></span>

<span data-ttu-id="f2b5d-109">除了使用应用程序编译的资源文件外，还可以使用多个其他数据存储区来存储时区信息。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-109">In addition to a resource file that is compiled with the application, several other data stores can be used for time zone information.</span></span> <span data-ttu-id="f2b5d-110">这些功能包括以下这些：</span><span class="sxs-lookup"><span data-stu-id="f2b5d-110">These include the following:</span></span>

- <span data-ttu-id="f2b5d-111">注册表。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-111">The registry.</span></span> <span data-ttu-id="f2b5d-112">请注意，应用程序应使用其自己的应用程序密钥的子项来存储自定义时区数据，而不是使用 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones 的子项。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-112">Note that an application should use the subkeys of its own application key to store custom time zone data rather than using the subkeys of HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones.</span></span>

- <span data-ttu-id="f2b5d-113">配置文件。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-113">Configuration files.</span></span>

- <span data-ttu-id="f2b5d-114">其他系统文件。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-114">Other system files.</span></span>

### <a name="to-save-a-time-zone-by-serializing-it-to-a-resx-file"></a><span data-ttu-id="f2b5d-115">通过将时区序列化到 .resx 文件来保存时区</span><span class="sxs-lookup"><span data-stu-id="f2b5d-115">To save a time zone by serializing it to a .resx file</span></span>

1. <span data-ttu-id="f2b5d-116">检索现有时区或创建新时区。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-116">Retrieve an existing time zone or create a new time zone.</span></span>

   <span data-ttu-id="f2b5d-117">若要检索现有时区，请参阅 [如何：访问预定义的 UTC 和本地时区对象](access-utc-and-local.md) 和 [如何：实例化 TimeZoneInfo 对象](instantiate-time-zone-info.md)。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-117">To retrieve an existing time zone, see [How to: Access the predefined UTC and local time zone objects](access-utc-and-local.md) and [How to: Instantiate a TimeZoneInfo object](instantiate-time-zone-info.md).</span></span>

   <span data-ttu-id="f2b5d-118">若要创建新的时区，请调用方法的重载之一 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-118">To create a new time zone, call one of the overloads of the <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> method.</span></span> <span data-ttu-id="f2b5d-119">有关详细信息，请参阅 [如何：创建不带调整规则的时区](create-time-zones-without-adjustment-rules.md) 和 [如何：创建带有调整规则的](create-time-zones-with-adjustment-rules.md)时区。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-119">For more information, see [How to: Create time zones without adjustment rules](create-time-zones-without-adjustment-rules.md) and [How to: Create time zones with adjustment rules](create-time-zones-with-adjustment-rules.md).</span></span>

2. <span data-ttu-id="f2b5d-120">调用 <xref:System.TimeZoneInfo.ToSerializedString%2A> 方法以创建包含时区数据的字符串。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-120">Call the <xref:System.TimeZoneInfo.ToSerializedString%2A> method to create a string that contains the time zone's data.</span></span>

3. <span data-ttu-id="f2b5d-121"><xref:System.IO.StreamWriter>通过向 <xref:System.IO.StreamWriter> 类构造函数提供 .resx 文件的名称和（可选）路径来实例化对象。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-121">Instantiate a <xref:System.IO.StreamWriter> object by providing the name and optionally the path of the .resx file to the <xref:System.IO.StreamWriter> class constructor.</span></span>

4. <span data-ttu-id="f2b5d-122"><xref:System.Resources.ResXResourceWriter>通过 <xref:System.IO.StreamWriter> 将对象传递给类构造函数来实例化对象 <xref:System.Resources.ResXResourceWriter> 。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-122">Instantiate a <xref:System.Resources.ResXResourceWriter> object by passing the <xref:System.IO.StreamWriter> object to the <xref:System.Resources.ResXResourceWriter> class constructor.</span></span>

5. <span data-ttu-id="f2b5d-123">将时区的序列化字符串传递给 <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-123">Pass the time zone's serialized string to the <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType> method.</span></span>

6. <span data-ttu-id="f2b5d-124">调用 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-124">Call the <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> method.</span></span>

7. <span data-ttu-id="f2b5d-125">调用 <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-125">Call the <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> method.</span></span>

8. <span data-ttu-id="f2b5d-126"><xref:System.IO.StreamWriter>通过调用其方法关闭对象 <xref:System.IO.StreamWriter.Close%2A> 。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-126">Close the <xref:System.IO.StreamWriter> object by calling its <xref:System.IO.StreamWriter.Close%2A> method.</span></span>

9. <span data-ttu-id="f2b5d-127">将生成的 .resx 文件添加到应用程序的 Visual Studio 项目中。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-127">Add the generated .resx file to the application's Visual Studio project.</span></span>

10. <span data-ttu-id="f2b5d-128">使用 Visual Studio 中的 " **属性** " 窗口，确保将 .resx 文件的 " **生成操作** " 属性设置为 " **嵌入的资源** "。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-128">Using the **Properties** window in Visual Studio, make sure that the .resx file's **Build Action** property is set to **Embedded Resource** .</span></span>

## <a name="example"></a><span data-ttu-id="f2b5d-129">示例</span><span class="sxs-lookup"><span data-stu-id="f2b5d-129">Example</span></span>

<span data-ttu-id="f2b5d-130">下面的示例序列化一个 <xref:System.TimeZoneInfo> 表示中部标准时间的对象，以及一个对象，该对象表示 <xref:System.TimeZoneInfo> Palmer 站，南极洲 Time 为一个名为 SerializedTimeZones 的 .net XML 资源文件。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-130">The following example serializes a <xref:System.TimeZoneInfo> object that represents Central Standard Time and a <xref:System.TimeZoneInfo> object that represents the Palmer Station, Antarctica time to a .NET XML resource file that is named SerializedTimeZones.resx.</span></span> <span data-ttu-id="f2b5d-131">中央标准时间通常在注册表中定义;Palmer 工作站，南极洲是自定义时区。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-131">Central Standard Time is typically defined in the registry; Palmer Station, Antarctica is a custom time zone.</span></span>

[!code-csharp[TimeZone2.Serialization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#1)]
[!code-vb[TimeZone2.Serialization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#1)]

<span data-ttu-id="f2b5d-132">此示例 <xref:System.TimeZoneInfo> 对对象进行序列化，以便在编译时在资源文件中提供这些对象。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-132">This example serializes <xref:System.TimeZoneInfo> objects so that they are available in a resource file at compile time.</span></span>

<span data-ttu-id="f2b5d-133">由于 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> 方法会将完整的标头信息添加到 .NET XML 资源文件中，因此不能将其用于将资源添加到现有文件中。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-133">Because the <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> method adds complete header information to a .NET XML resource file, it cannot be used to add resources to an existing file.</span></span> <span data-ttu-id="f2b5d-134">该示例通过检查 SerializedTimeZones 文件来处理这种情况，如果该文件存在，则将其除两个序列化时区之外的所有资源存储到一个泛型 <xref:System.Collections.Generic.Dictionary%602> 对象。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-134">The example handles this by checking for the SerializedTimeZones.resx file and, if it exists, storing all of its resources other than the two serialized time zones to a generic <xref:System.Collections.Generic.Dictionary%602> object.</span></span> <span data-ttu-id="f2b5d-135">然后删除现有的文件，并将现有资源添加到新的 SerializedTimeZones 文件。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-135">The existing file is then deleted and the existing resources are added to a new SerializedTimeZones.resx file.</span></span> <span data-ttu-id="f2b5d-136">序列化的时区数据也将添加到此文件中。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-136">The serialized time zone data is also added to this file.</span></span>

<span data-ttu-id="f2b5d-137">资源的键 (或 **名称** ) 字段不应包含嵌入的空格。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-137">The key (or **Name** ) fields of resources should not contain embedded spaces.</span></span> <span data-ttu-id="f2b5d-138"><xref:System.String.Replace%28System.String%2CSystem.String%29>调用方法以删除时区标识符中的所有嵌入空格，然后将其分配给资源文件。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-138">The <xref:System.String.Replace%28System.String%2CSystem.String%29> method is called to remove all embedded spaces in the time zone identifiers before they are assigned to the resource file.</span></span>

## <a name="compiling-the-code"></a><span data-ttu-id="f2b5d-139">编译代码</span><span class="sxs-lookup"><span data-stu-id="f2b5d-139">Compiling the code</span></span>

<span data-ttu-id="f2b5d-140">此示例需要：</span><span class="sxs-lookup"><span data-stu-id="f2b5d-140">This example requires:</span></span>

- <span data-ttu-id="f2b5d-141">对 System.Windows.Forms.dll 和 System.Core.dll 的引用将添加到项目。</span><span class="sxs-lookup"><span data-stu-id="f2b5d-141">That a reference to System.Windows.Forms.dll and System.Core.dll be added to the project.</span></span>

- <span data-ttu-id="f2b5d-142">导入以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="f2b5d-142">That the following namespaces be imported:</span></span>

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a><span data-ttu-id="f2b5d-143">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f2b5d-143">See also</span></span>

- [<span data-ttu-id="f2b5d-144">日期、时间和时区</span><span class="sxs-lookup"><span data-stu-id="f2b5d-144">Dates, times, and time zones</span></span>](index.md)
- [<span data-ttu-id="f2b5d-145">时区概述</span><span class="sxs-lookup"><span data-stu-id="f2b5d-145">Time zone overview</span></span>](time-zone-overview.md)
- [<span data-ttu-id="f2b5d-146">如何：从嵌入的资源还原时区</span><span class="sxs-lookup"><span data-stu-id="f2b5d-146">How to: Restore time zones from an embedded resource</span></span>](restore-time-zones-from-an-embedded-resource.md)
