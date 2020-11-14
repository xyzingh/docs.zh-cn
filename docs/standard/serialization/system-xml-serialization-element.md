---
title: <system.xml.serialization> 元素
description: 本文介绍 <system.xml.serialization> 元素，该元素是用于控制 XML 序列化的顶级元素。
ms.date: 03/30/2017
helpviewer_keywords:
- system.xml.serialization element
- XML serialization, configuration
- <system.xml.serialization> element
ms.assetid: 3ce45919-388a-418c-8968-6df0372c73ec
ms.openlocfilehash: 6291799aadc429e943996f2256d773ac36dd370f
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282389"
---
# <a name="systemxmlserialization-element"></a><span data-ttu-id="0d232-103">\<system.xml.serialization> 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-103">\<system.xml.serialization> Element</span></span>

<span data-ttu-id="0d232-104">用于控制 XML 序列化的顶级元素。</span><span class="sxs-lookup"><span data-stu-id="0d232-104">The top-level element for controlling XML serialization.</span></span> <span data-ttu-id="0d232-105">有关配置文件的详细信息，请参阅[配置文件架构](../../framework/configure-apps/file-schema/index.md)。</span><span class="sxs-lookup"><span data-stu-id="0d232-105">For more information about configuration files, see [Configuration File Schema](../../framework/configure-apps/file-schema/index.md).</span></span>

\<configuration>\
\<system.xml.serialization>

## <a name="syntax"></a><span data-ttu-id="0d232-106">语法</span><span class="sxs-lookup"><span data-stu-id="0d232-106">Syntax</span></span>

```xml
<system.xml.serialization>
</system.xml.serialization>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0d232-107">特性和元素</span><span class="sxs-lookup"><span data-stu-id="0d232-107">Attributes and Elements</span></span>

<span data-ttu-id="0d232-108">下列各节描述了特性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="0d232-108">The following sections describe attributes, child elements, and parent elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="0d232-109">特性</span><span class="sxs-lookup"><span data-stu-id="0d232-109">Attributes</span></span>

<span data-ttu-id="0d232-110">无。</span><span class="sxs-lookup"><span data-stu-id="0d232-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0d232-111">子元素</span><span class="sxs-lookup"><span data-stu-id="0d232-111">Child Elements</span></span>

|<span data-ttu-id="0d232-112">元素</span><span class="sxs-lookup"><span data-stu-id="0d232-112">Element</span></span>|<span data-ttu-id="0d232-113">描述</span><span class="sxs-lookup"><span data-stu-id="0d232-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0d232-114">\<dateTimeSerialization> 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-114">\<dateTimeSerialization> Element</span></span>](datetimeserialization-element.md)|<span data-ttu-id="0d232-115">确定 <xref:System.DateTime> 对象的序列化模式。</span><span class="sxs-lookup"><span data-stu-id="0d232-115">Determines the serialization mode of <xref:System.DateTime> objects.</span></span>|
|[<span data-ttu-id="0d232-116">\<schemaImporterExtensions> 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-116">\<schemaImporterExtensions> Element</span></span>](schemaimporterextensions-element.md)|<span data-ttu-id="0d232-117">包含将 XSD 类型映射到 .NET 类型时 <xref:System.Xml.Serialization.XmlSchemaImporter> 所用的类型。</span><span class="sxs-lookup"><span data-stu-id="0d232-117">Contains types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> for mapping of XSD types to .NET types.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0d232-118">父元素</span><span class="sxs-lookup"><span data-stu-id="0d232-118">Parent Elements</span></span>

|<span data-ttu-id="0d232-119">元素</span><span class="sxs-lookup"><span data-stu-id="0d232-119">Element</span></span>|<span data-ttu-id="0d232-120">描述</span><span class="sxs-lookup"><span data-stu-id="0d232-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0d232-121">\<configuration> 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-121">\<configuration> Element</span></span>](../../framework/configure-apps/file-schema/configuration-element.md)|<span data-ttu-id="0d232-122">公共语言运行库和 .NET Framework 应用程序所使用的每个配置文件中的根元素。</span><span class="sxs-lookup"><span data-stu-id="0d232-122">The root element in every configuration file that is used by the common language runtime and .NET Framework applications.</span></span>|

## <a name="example"></a><span data-ttu-id="0d232-123">示例</span><span class="sxs-lookup"><span data-stu-id="0d232-123">Example</span></span>

<span data-ttu-id="0d232-124">下面的代码示例演示如何指定 <xref:System.DateTime> 对象的序列化模式，以及将 XSD 类型映射到 .NET 类型时 <xref:System.Xml.Serialization.XmlSchemaImporter> 所用的其他类型。</span><span class="sxs-lookup"><span data-stu-id="0d232-124">The following code example illustrates how to specify the serialization mode of a <xref:System.DateTime> object, and the addition of types used by the <xref:System.Xml.Serialization.XmlSchemaImporter> when mapping XSD types to .NET types.</span></span>

```xml
<system.xml.serialization>
    <xmlSerializer checkDeserializeAdvances="false" />
    <dateTimeSerialization mode = "Local" />
    <schemaImporterExtensions>
        <add
        name = "MobileCapabilities"
        type = "System.Web.Mobile.MobileCapabilities,
        System.Web.Mobile, Version=2.0.0.0, Culture=neutral,
        PublicKeyToken=b03f5f6f11d40a3a" />
    </schemaImporterExtensions>
</system.xml.serialization>
```

## <a name="see-also"></a><span data-ttu-id="0d232-125">请参阅</span><span class="sxs-lookup"><span data-stu-id="0d232-125">See also</span></span>

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [<span data-ttu-id="0d232-126">配置文件架构</span><span class="sxs-lookup"><span data-stu-id="0d232-126">Configuration File Schema</span></span>](../../framework/configure-apps/file-schema/index.md)
- [<span data-ttu-id="0d232-127">\<dateTimeSerialization> 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-127">\<dateTimeSerialization> Element</span></span>](datetimeserialization-element.md)
- [<span data-ttu-id="0d232-128">\<schemaImporterExtensions> 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-128">\<schemaImporterExtensions> Element</span></span>](schemaimporterextensions-element.md)
- <span data-ttu-id="0d232-129">[\<add> 的 \<schemaImporterExtensions>](add-element-for-schemaimporterextensions.md) 元素</span><span class="sxs-lookup"><span data-stu-id="0d232-129">[\<add> Element for \<schemaImporterExtensions>](add-element-for-schemaimporterextensions.md)</span></span>
