---
title: <schemaImporterExtensions> 的 <add> 元素
description: <add> 元素可添加 XmlSchemaImporter 在将 XSD 类型映射到 .NET 类型时所用的类型。
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- <add> element for <schemaImporterExtensions> element
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
ms.openlocfilehash: 38d8ebd6e973632b23865ad60e007d9aa21e7da6
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282006"
---
# <a name="add-element-for-schemaimporterextensions"></a><span data-ttu-id="6d3f6-103">\<schemaImporterExtensions> 的 \<add> 元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-103">\<add> Element for \<schemaImporterExtensions></span></span>

<span data-ttu-id="6d3f6-104">添加将 XSD 类型映射到 .NET 类型时 <xref:System.Xml.Serialization.XmlSchemaImporter> 所用的类型。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-104">Adds types used by the <xref:System.Xml.Serialization.XmlSchemaImporter> for mapping XSD types to .NET types.</span></span> <span data-ttu-id="6d3f6-105">有关配置文件的详细信息，请参阅[配置文件架构](../../framework/configure-apps/file-schema/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-105">For more information about configuration files, see [Configuration File Schema](../../framework/configure-apps/file-schema/index.md).</span></span>  
  
\<configuration>  
\<system.xml.serialization>  
\<schemaImporterExtensions>  
\<add>  
  
## <a name="syntax"></a><span data-ttu-id="6d3f6-106">语法</span><span class="sxs-lookup"><span data-stu-id="6d3f6-106">Syntax</span></span>  
  
```xml  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="6d3f6-107">特性和元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-107">Attributes and Elements</span></span>  
 <span data-ttu-id="6d3f6-108">下列各节描述了特性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-108">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="6d3f6-109">特性</span><span class="sxs-lookup"><span data-stu-id="6d3f6-109">Attributes</span></span>  
  
|<span data-ttu-id="6d3f6-110">特性</span><span class="sxs-lookup"><span data-stu-id="6d3f6-110">Attribute</span></span>|<span data-ttu-id="6d3f6-111">描述</span><span class="sxs-lookup"><span data-stu-id="6d3f6-111">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="6d3f6-112">**name**</span><span class="sxs-lookup"><span data-stu-id="6d3f6-112">**name**</span></span>|<span data-ttu-id="6d3f6-113">用于查找实例的简单名称。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-113">A simple name that is used to find the instance.</span></span>|  
|<span data-ttu-id="6d3f6-114">**type**</span><span class="sxs-lookup"><span data-stu-id="6d3f6-114">**type**</span></span>|<span data-ttu-id="6d3f6-115">必需。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-115">Required.</span></span> <span data-ttu-id="6d3f6-116">指定要添加的架构扩展类。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-116">Specifies the schema  extension class to add.</span></span> <span data-ttu-id="6d3f6-117">type 特性值必须位于一行上，并且包含完全限定的类型名称。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-117">The **type** attribute value must be on one line, and include the fully qualified type name.</span></span> <span data-ttu-id="6d3f6-118">当程序集放置在全局程序集缓存 (GAC) 中时，该特性值还必须包括已签名程序集的版本、区域性和公钥标记。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-118">When the assembly is placed in the Global Assembly Cache (GAC), it must also include the version, culture, and public key token of the signed assembly.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="6d3f6-119">子元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-119">Child Elements</span></span>  
 <span data-ttu-id="6d3f6-120">无。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-120">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="6d3f6-121">父元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-121">Parent Elements</span></span>  
  
|<span data-ttu-id="6d3f6-122">元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-122">Element</span></span>|<span data-ttu-id="6d3f6-123">描述</span><span class="sxs-lookup"><span data-stu-id="6d3f6-123">Description</span></span>|  
|-------------|-----------------|  
|\<schemaImporterExtensions>|<span data-ttu-id="6d3f6-124">包含 <xref:System.Xml.Serialization.XmlSchemaImporter> 所使用的类型。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-124">Contains the types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter>.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="6d3f6-125">示例</span><span class="sxs-lookup"><span data-stu-id="6d3f6-125">Example</span></span>  
 <span data-ttu-id="6d3f6-126">下面的代码示例添加 XmlSchemaImporter 可以在映射类型时使用的扩展类型。</span><span class="sxs-lookup"><span data-stu-id="6d3f6-126">The following code example adds an extension type that the XmlSchemaImporter can use when mapping types.</span></span>  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <schemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,
       PublicKeyToken=b03f5f7f11d50a3a" />
    </schemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="6d3f6-127">请参阅</span><span class="sxs-lookup"><span data-stu-id="6d3f6-127">See also</span></span>

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- [<span data-ttu-id="6d3f6-128">\<system.xml.serialization> 元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-128">\<system.xml.serialization> Element</span></span>](system-xml-serialization-element.md)
- [<span data-ttu-id="6d3f6-129">\<schemaImporterExtensions> 元素</span><span class="sxs-lookup"><span data-stu-id="6d3f6-129">\<schemaImporterExtensions> Element</span></span>](schemaimporterextensions-element.md)
