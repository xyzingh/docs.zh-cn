---
title: 序列化准则
description: 本文提供了在设计要序列化的 API 时应考虑的准则，并简要介绍了 .NET 提供的三个主要序列化技术。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serialization, guidelines
- binary serialization, guidelines
ms.assetid: ebbeddff-179d-443f-bf08-9c373199a73a
ms.openlocfilehash: 32d71aba5d8a650293a4d8653fb2a2e383b8a800
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282375"
---
# <a name="serialization-guidelines"></a><span data-ttu-id="f2488-103">序列化准则</span><span class="sxs-lookup"><span data-stu-id="f2488-103">Serialization guidelines</span></span>

<span data-ttu-id="f2488-104">本文列出了在设计要序列化的 API 时要考虑的准则。</span><span class="sxs-lookup"><span data-stu-id="f2488-104">This article lists the guidelines to consider when designing an API to be serialized.</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

 <span data-ttu-id="f2488-105">.NET 提供了针对各种序列化方案进行优化的三种主要序列化技术。</span><span class="sxs-lookup"><span data-stu-id="f2488-105">.NET offers three main serialization technologies that are optimized for various serialization scenarios.</span></span> <span data-ttu-id="f2488-106">下表列出了这些技术以及与这些技术相关的主要 .NET 类型。</span><span class="sxs-lookup"><span data-stu-id="f2488-106">The following table lists these technologies and the main .NET types related to these technologies.</span></span>

|<span data-ttu-id="f2488-107">技术</span><span class="sxs-lookup"><span data-stu-id="f2488-107">Technology</span></span>|<span data-ttu-id="f2488-108">相关的类</span><span class="sxs-lookup"><span data-stu-id="f2488-108">Relevant Classes</span></span>|<span data-ttu-id="f2488-109">说明</span><span class="sxs-lookup"><span data-stu-id="f2488-109">Notes</span></span>|
|----------------|----------------------|-----------|
|<span data-ttu-id="f2488-110">数据协定序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-110">Data Contract Serialization</span></span>|<xref:System.Runtime.Serialization.DataContractAttribute><br /><br /> <xref:System.Runtime.Serialization.DataMemberAttribute><br /><br /> <xref:System.Runtime.Serialization.DataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.NetDataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer><br /><br /> <xref:System.Runtime.Serialization.ISerializable>|<span data-ttu-id="f2488-111">常规持久性</span><span class="sxs-lookup"><span data-stu-id="f2488-111">General persistence</span></span><br /><br /> <span data-ttu-id="f2488-112">Web 服务</span><span class="sxs-lookup"><span data-stu-id="f2488-112">Web Services</span></span><br /><br /> <span data-ttu-id="f2488-113">JSON</span><span class="sxs-lookup"><span data-stu-id="f2488-113">JSON</span></span>|
|<span data-ttu-id="f2488-114">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-114">XML Serialization</span></span>|<xref:System.Xml.Serialization.XmlSerializer>|<span data-ttu-id="f2488-115">具有完全控制的</span><span class="sxs-lookup"><span data-stu-id="f2488-115">XML format</span></span> <br /><span data-ttu-id="f2488-116">XML 格式</span><span class="sxs-lookup"><span data-stu-id="f2488-116">with full control</span></span>|
|<span data-ttu-id="f2488-117">运行时 -序列化（二进制和 SOAP）</span><span class="sxs-lookup"><span data-stu-id="f2488-117">Runtime -Serialization (Binary and SOAP)</span></span>|<xref:System.SerializableAttribute><br /><br /> <xref:System.Runtime.Serialization.ISerializable><br /><br /> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>|<span data-ttu-id="f2488-118">.NET 远程处理</span><span class="sxs-lookup"><span data-stu-id="f2488-118">.NET Remoting</span></span>|

 <span data-ttu-id="f2488-119">设计新的类型时，应决定这些类型需要支持哪种技术（如果有的话）。</span><span class="sxs-lookup"><span data-stu-id="f2488-119">When you design new types, you should decide which, if any, of these technologies those types need to support.</span></span> <span data-ttu-id="f2488-120">以下准则介绍了如何做出此决定以及如何提供这类支持。</span><span class="sxs-lookup"><span data-stu-id="f2488-120">The following guidelines describe how to make that choice and how to provide such support.</span></span> <span data-ttu-id="f2488-121">这些准则并不表示帮助您选择在实现应用程序或库时应使用哪种序列化技术。</span><span class="sxs-lookup"><span data-stu-id="f2488-121">These guidelines are not meant to help you choose which serialization technology you should use in the implementation of your application or library.</span></span> <span data-ttu-id="f2488-122">这些准则与 API 设计不是直接相关的，因此它们不在本主题的讨论范围内。</span><span class="sxs-lookup"><span data-stu-id="f2488-122">Such guidelines are not directly related to API design and thus are not within the scope of this topic.</span></span>

## <a name="guidelines"></a><span data-ttu-id="f2488-123">准则</span><span class="sxs-lookup"><span data-stu-id="f2488-123">Guidelines</span></span>

- <span data-ttu-id="f2488-124">设计新类型时请务必考虑序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-124">DO think about serialization when you design new types.</span></span>

  <span data-ttu-id="f2488-125">对于任何类型来说，序列化都是一个重要的设计考虑事项，因为程序可能需要持久保持或传输类型的实例。</span><span class="sxs-lookup"><span data-stu-id="f2488-125">Serialization is an important design consideration for any type, because programs might need to persist or transmit instances of the type.</span></span>

### <a name="choosing-the-right-serialization-technology-to-support"></a><span data-ttu-id="f2488-126">选择要支持的合适的序列化技术</span><span class="sxs-lookup"><span data-stu-id="f2488-126">Choosing the right serialization technology to support</span></span>
 <span data-ttu-id="f2488-127">任何给定类型均可支持一种或多种序列化技术，或者不支持任何序列化技术。</span><span class="sxs-lookup"><span data-stu-id="f2488-127">Any given type can support none, one, or more of the serialization technologies.</span></span>

- <span data-ttu-id="f2488-128">如果可能需要在 Web 服务中持久保持或使用类型的实例，则应考虑支持数据协定序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-128">CONSIDER supporting *data contract serialization* if instances of your type might need to be persisted or used in Web Services.</span></span>

- <span data-ttu-id="f2488-129">如果需要对序列化类型时生成的 XML 格式具有更多控制，则应考虑改为支持 XML 序列化，或者在支持数据协定序列化之外还支持 XML 序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-129">CONSIDER supporting the *XML serialization* instead of or in addition to data contract serialization if you need more control over the XML format that is produced when the type is serialized.</span></span>

     <span data-ttu-id="f2488-130">这对于某些需要使用数据协定序列化所不支持的 XML 构造（例如，用于生成 XML 特性）的互操作性方案可能是必需的。</span><span class="sxs-lookup"><span data-stu-id="f2488-130">This may be necessary in some interoperability scenarios where you need to use an XML construct that is not supported by data contract serialization, for example, to produce XML attributes.</span></span>

- <span data-ttu-id="f2488-131">如果类型实例需要越过 .NET 远程处理边界传递，则应考虑支持运行时序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-131">CONSIDER supporting *runtime serialization* if instances of your type need to travel across .NET Remoting boundaries.</span></span>

- <span data-ttu-id="f2488-132">应避免仅仅因为常规持久性原因而支持运行时序列化或 XML 序列化，</span><span class="sxs-lookup"><span data-stu-id="f2488-132">AVOID supporting runtime serialization or XML serialization just for general persistence reasons.</span></span> <span data-ttu-id="f2488-133">而应首选数据协定序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-133">Prefer data contract serialization instead</span></span>

#### <a name="data-contract-serialization"></a><span data-ttu-id="f2488-134">数据协定序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-134">Data contract serialization</span></span>
 <span data-ttu-id="f2488-135">通过将 <xref:System.Runtime.Serialization.DataContractAttribute> 应用到类型，并将 <xref:System.Runtime.Serialization.DataMemberAttribute> 应用到类型的成员（字段和属性），类型可支持数据协定序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-135">Types can support data contract serialization by applying the <xref:System.Runtime.Serialization.DataContractAttribute> to the type and the <xref:System.Runtime.Serialization.DataMemberAttribute> to the members (fields and properties) of the type.</span></span>

 [!code-csharp[SerializationGuidelines#1](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#1)]
 [!code-vb[SerializationGuidelines#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#1)]

1. <span data-ttu-id="f2488-136">如果可以在部分信任模式下使用类型，则考虑将类型的数据成员标记为公共的。</span><span class="sxs-lookup"><span data-stu-id="f2488-136">CONSIDER marking data members of your type public if the type can be used in partial trust.</span></span> <span data-ttu-id="f2488-137">在完全信任模式下，数据协定序列化程序可对非公共类型和成员进行序列化和反序列化，但在部分信任模式下，仅可对公共成员进行序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-137">In full trust, data contract serializers can serialize and deserialize nonpublic types and members, but only public members can be serialized and deserialized in partial trust.</span></span>

2. <span data-ttu-id="f2488-138">请务必在包含 Data-MemberAttribute 的所有属性上实现 getter 和 setter。</span><span class="sxs-lookup"><span data-stu-id="f2488-138">DO implement a getter and setter on all properties that have Data-MemberAttribute.</span></span> <span data-ttu-id="f2488-139">对于考虑可进行序列化的类型，数据协定序列化程序要求同时具备 getter 和 setter。</span><span class="sxs-lookup"><span data-stu-id="f2488-139">Data contract serializers require both the getter and the setter for the type to be considered serializable.</span></span> <span data-ttu-id="f2488-140">如果不会在部分信任模式下使用类型，则这两个属性访问器中的一个或两个都可以是非公共的。</span><span class="sxs-lookup"><span data-stu-id="f2488-140">If the type won't be used in partial trust, one or both of the property accessors can be nonpublic.</span></span>

     [!code-csharp[SerializationGuidelines#2](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#2)]
     [!code-vb[SerializationGuidelines#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#2)]

3. <span data-ttu-id="f2488-141">对于反序列化实例的初始化，应考虑使用序列化回调。</span><span class="sxs-lookup"><span data-stu-id="f2488-141">CONSIDER using the serialization callbacks for initialization of deserialized instances.</span></span>

     <span data-ttu-id="f2488-142">反序列化对象时，不调用任何构造函数。</span><span class="sxs-lookup"><span data-stu-id="f2488-142">Constructors are not called when objects are deserialized.</span></span> <span data-ttu-id="f2488-143">因此，在正常构造期间执行的任何逻辑都需要作为一个序列化回调实现。</span><span class="sxs-lookup"><span data-stu-id="f2488-143">Therefore, any logic that executes during normal construction needs to be implemented as one of the *serialization callbacks*.</span></span>

     [!code-csharp[SerializationGuidelines#3](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#3)]
     [!code-vb[SerializationGuidelines#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#3)]

     <span data-ttu-id="f2488-144"><xref:System.Runtime.Serialization.OnDeserializedAttribute> 属性是最常用的回调属性。</span><span class="sxs-lookup"><span data-stu-id="f2488-144">The <xref:System.Runtime.Serialization.OnDeserializedAttribute> attribute is the most commonly used callback attribute.</span></span> <span data-ttu-id="f2488-145">此系列中的其他属性还包括 <xref:System.Runtime.Serialization.OnDeserializingAttribute>、<xref:System.Runtime.Serialization.OnSerializingAttribute> 和 <xref:System.Runtime.Serialization.OnSerializedAttribute>。</span><span class="sxs-lookup"><span data-stu-id="f2488-145">The other attributes in the family are <xref:System.Runtime.Serialization.OnDeserializingAttribute>, <xref:System.Runtime.Serialization.OnSerializingAttribute>, and <xref:System.Runtime.Serialization.OnSerializedAttribute>.</span></span> <span data-ttu-id="f2488-146">这些属性可分别用来标记在反序列化之前、序列化之前以及序列化之后执行的回调。</span><span class="sxs-lookup"><span data-stu-id="f2488-146">They can be used to mark callbacks that get executed before deserialization, before serialization, and finally, after serialization, respectively.</span></span>

4. <span data-ttu-id="f2488-147">请考虑使用 <xref:System.Runtime.Serialization.KnownTypeAttribute> 指示在反序列化复杂对象关系图时应使用的具体类型。</span><span class="sxs-lookup"><span data-stu-id="f2488-147">CONSIDER using the <xref:System.Runtime.Serialization.KnownTypeAttribute> to indicate concrete types that should be used when deserializing a complex object graph.</span></span>

     <span data-ttu-id="f2488-148">例如，如果使用一个抽象类表示反序列化数据成员的类型，则序列化程序将需要已知类型信息，以便决定要实例化并分配给成员的具体类型。</span><span class="sxs-lookup"><span data-stu-id="f2488-148">For example, if a type of a deserialized data member is represented by an abstract class, the serializer will need the *known type* information to decide what concrete type to instantiate and assign to the member.</span></span> <span data-ttu-id="f2488-149">如果未使用相关属性指定已知类型，则需要将已知类型显式传递给序列化程序（可通过将已知类型传递给序列化程序构造函数来执行此操作），或者需要在配置文件中指定已知类型。</span><span class="sxs-lookup"><span data-stu-id="f2488-149">If the known type is not specified using the attribute, it will need to be passed to the serializer explicitly (you can do it by passing known types to the serializer constructor) or it will need to be specified in the configuration file.</span></span>

     [!code-csharp[SerializationGuidelines#4](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#4)]
     [!code-vb[SerializationGuidelines#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#4)]

     <span data-ttu-id="f2488-150">在无法通过静态方式了解已知类型列表的情况下（当编译 Person 类时），KnownTypeAttribute 还可指向一个在运行时返回已知类型列表的方法 。</span><span class="sxs-lookup"><span data-stu-id="f2488-150">In cases where the list of known types is not known statically (when the **Person** class is compiled), the **KnownTypeAttribute** can also point to a method that returns a list of known types at run time.</span></span>

5. <span data-ttu-id="f2488-151">创建或更改可序列化的类型时，请务必考虑向后兼容性和向前兼容性。</span><span class="sxs-lookup"><span data-stu-id="f2488-151">DO consider backward and forward compatibility when creating or changing serializable types.</span></span>

     <span data-ttu-id="f2488-152">请记住，类型的未来版本的序列化流可反序列化到类型的当前版本，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="f2488-152">Keep in mind that serialized streams of future versions of your type can be deserialized into the current version of the type, and vice versa.</span></span> <span data-ttu-id="f2488-153">您一定要清楚，数据成员（甚至对于私有成员和内部成员）不能更改其名称和类型，甚至不能更改其在类型的未来版本中的顺序，除非特别留意将使用显式参数的协定保存到数据协定属性。在对可序列化的类型进行更改时，测试序列化的兼容性。</span><span class="sxs-lookup"><span data-stu-id="f2488-153">Make sure you understand that data members, even private and internal, cannot change their names, types, or even their order in future versions of the type unless special care is taken to preserve the contract using explicit parameters to the data contract attributes.Test compatibility of serialization when making changes to serializable types.</span></span> <span data-ttu-id="f2488-154">尝试将新版本反序列化为旧版本，以及将旧版本反序列化为新版本。</span><span class="sxs-lookup"><span data-stu-id="f2488-154">Try deserializing the new version into an old version, and vice versa.</span></span>

6. <span data-ttu-id="f2488-155">考虑实现 <xref:System.Runtime.Serialization.IExtensibleDataObject> 接口以允许在类型的两个不同版本之间进行往返。</span><span class="sxs-lookup"><span data-stu-id="f2488-155">CONSIDER implementing <xref:System.Runtime.Serialization.IExtensibleDataObject> interface to allow round-tripping between different versions of the type.</span></span>

     <span data-ttu-id="f2488-156">序列化程序可通过此接口确保在往返期间不丢失任何数据。</span><span class="sxs-lookup"><span data-stu-id="f2488-156">The interface allows the serializer to ensure that no data is lost during round-tripping.</span></span> <span data-ttu-id="f2488-157"><xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 属性可存储类型的未来版本中不为当前版本所知的任何数据。</span><span class="sxs-lookup"><span data-stu-id="f2488-157">The <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> property stores any data from the future version of the type that is unknown to the current version.</span></span> <span data-ttu-id="f2488-158">在随后序列化当前版本并将其反序列化为未来版本时，可通过 ExtensionData 属性值在序列化流中使用附加数据。</span><span class="sxs-lookup"><span data-stu-id="f2488-158">When the current version is subsequently serialized and deserialized into a future version, the additional data will be available in the serialized stream through the **ExtensionData** property value.</span></span>

     [!code-csharp[SerializationGuidelines#5](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#5)]
     [!code-vb[SerializationGuidelines#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#5)]

     <span data-ttu-id="f2488-159">有关详细信息，请参阅[向前兼容的数据协定](../../framework/wcf/feature-details/forward-compatible-data-contracts.md)。</span><span class="sxs-lookup"><span data-stu-id="f2488-159">For more information, see [Forward-Compatible Data Contracts](../../framework/wcf/feature-details/forward-compatible-data-contracts.md).</span></span>

#### <a name="xml-serialization"></a><span data-ttu-id="f2488-160">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-160">XML serialization</span></span>
 <span data-ttu-id="f2488-161">数据协定序列化是 .NET Framework 中的主要（默认）序列化技术，但也存在数据协定序列化不支持的序列化情况。</span><span class="sxs-lookup"><span data-stu-id="f2488-161">Data contract serialization is the main (default) serialization technology in .NET Framework, but there are serialization scenarios that data contract serialization does not support.</span></span> <span data-ttu-id="f2488-162">例如，数据协定序列化无法让您完全控制序列化程序生成或使用的 XML 的形状。</span><span class="sxs-lookup"><span data-stu-id="f2488-162">For example, it does not give you full control over the shape of XML produced or consumed by the serializer.</span></span> <span data-ttu-id="f2488-163">如果要求此类精细控制，则必须使用 XML 序列化，而且需要设计类型以支持此序列化技术。</span><span class="sxs-lookup"><span data-stu-id="f2488-163">If such fine control is required, *XML serialization* has to be used, and you need to design your types to support this serialization technology.</span></span>

1. <span data-ttu-id="f2488-164">应避免专门针对 XML 序列化设计类型，除非您有很充分的理由要控制所生成的 XML 的形状。</span><span class="sxs-lookup"><span data-stu-id="f2488-164">AVOID designing your types specifically for XML Serialization, unless you have a very strong reason to control the shape of the XML produced.</span></span> <span data-ttu-id="f2488-165">此序列化技术已由上一节讨论的数据协定序列化所取代。</span><span class="sxs-lookup"><span data-stu-id="f2488-165">This serialization technology has been superseded by the Data Contract Serialization discussed in the previous section.</span></span>

     <span data-ttu-id="f2488-166">换句话说，不要将 <xref:System.Xml.Serialization> 命名空间中的属性应用到新类型，除非你清楚该类型将会用于 XML 序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-166">In other words, don't apply attributes from the <xref:System.Xml.Serialization> namespace to new types, unless you know that the type will be used with XML Serialization.</span></span> <span data-ttu-id="f2488-167">以下示例展示如何使用 System.Xml.Serialization 来控制生成的 XML 的形状。</span><span class="sxs-lookup"><span data-stu-id="f2488-167">The following example shows how **System.Xml.Serialization** can be used to control the shape of the XML -produced.</span></span>

     [!code-csharp[SerializationGuidelines#6](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#6)]
     [!code-vb[SerializationGuidelines#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#6)]

2. <span data-ttu-id="f2488-168">如果通过应用 XML 序列化属性所提供的对于序列化 XML 的形状的控制还无法满足你的需要，则可考虑实现 <xref:System.Xml.Serialization.IXmlSerializable> 接口。</span><span class="sxs-lookup"><span data-stu-id="f2488-168">CONSIDER implementing the <xref:System.Xml.Serialization.IXmlSerializable> interface if you want even more control over the shape of the serialized XML than what's offered by applying the XML Serialization attributes.</span></span> <span data-ttu-id="f2488-169">利用此接口的两种方法（<xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 和 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>），你可以完全控制序列化的 XML 流。</span><span class="sxs-lookup"><span data-stu-id="f2488-169">Two methods of the interface, <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> and <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>, allow you to fully control the serialized XML stream.</span></span> <span data-ttu-id="f2488-170">还可以通过应用 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 属性来控制为类型生成的 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="f2488-170">You can also control the XML schema that gets generated for the type by applying the <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> attribute.</span></span>

#### <a name="runtime-serialization"></a><span data-ttu-id="f2488-171">运行时序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-171">Runtime serialization</span></span>
 <span data-ttu-id="f2488-172">运行时序列化是 .NET 远程处理所使用的一项技术。</span><span class="sxs-lookup"><span data-stu-id="f2488-172">*Runtime serialization* is a technology used by .NET Remoting.</span></span> <span data-ttu-id="f2488-173">如果你认为将会使用 .NET 远程处理传输类型，则确保类型支持运行时序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-173">If you think your types will be transported using .NET Remoting, make sure they support runtime serialization.</span></span>

 <span data-ttu-id="f2488-174">可通过应用 <xref:System.SerializableAttribute> 属性提供对运行时序列化的基本支持，更高级的方案涉及实现一个简单的运行时可序列化模式（实现 -<xref:System.Runtime.Serialization.ISerializable> 并提供一个序列化构造函数） 。</span><span class="sxs-lookup"><span data-stu-id="f2488-174">The basic support for *runtime serialization* can be provided by applying the <xref:System.SerializableAttribute> attribute, and more advanced scenarios involve implementing a simple *runtime serializable pattern* (implement -<xref:System.Runtime.Serialization.ISerializable> and provide a serialization constructor).</span></span>

1. <span data-ttu-id="f2488-175">如果您的类型将要用于 .NET 远程处理，则应考虑支持运行时序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-175">CONSIDER supporting runtime serialization if your types will be used with .NET Remoting.</span></span> <span data-ttu-id="f2488-176">例如，<xref:System.AddIn> 命名空间使用 .NET 远程处理，因此在 System.AddIn 加载项之间交换的所有类型都需要支持运行时序列化。</span><span class="sxs-lookup"><span data-stu-id="f2488-176">For example, the <xref:System.AddIn> namespace uses .NET Remoting, and so all types exchanged between **System.AddIn** add-ins need to support runtime serialization.</span></span>

     [!code-csharp[SerializationGuidelines#7](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#7)]
     [!code-vb[SerializationGuidelines#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#7)]

2. <span data-ttu-id="f2488-177">如果需要完全控制序列化过程，则应考虑实现运行时可序列化模式。</span><span class="sxs-lookup"><span data-stu-id="f2488-177">CONSIDER implementing the *runtime serializable pattern* if you want complete control over the serialization process.</span></span> <span data-ttu-id="f2488-178">例如，如果您需要在对数据进行序列化或反序列化时转换数据。</span><span class="sxs-lookup"><span data-stu-id="f2488-178">For example, if you want to transform data as it gets serialized or deserialized.</span></span>

     <span data-ttu-id="f2488-179">此模式非常简单。</span><span class="sxs-lookup"><span data-stu-id="f2488-179">The pattern is very simple.</span></span> <span data-ttu-id="f2488-180">您需要执行的全部操作就是实现 <xref:System.Runtime.Serialization.ISerializable> 接口，并提供在反序列化对象时使用的特殊构造函数。</span><span class="sxs-lookup"><span data-stu-id="f2488-180">All you need to do is implement the <xref:System.Runtime.Serialization.ISerializable> interface and provide a special constructor that is used when the object is deserialized.</span></span>

     [!code-csharp[SerializationGuidelines#8](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#8)]
     [!code-vb[SerializationGuidelines#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#8)]

3. <span data-ttu-id="f2488-181">请务必保护序列化构造函数，并提供完全按照此处示例中的显示类型化和命名的两个参数。</span><span class="sxs-lookup"><span data-stu-id="f2488-181">DO make the serialization constructor protected and provide two parameters typed and named exactly as shown in the sample here.</span></span>

     [!code-csharp[SerializationGuidelines#9](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#9)]
     [!code-vb[SerializationGuidelines#9](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#9)]

4. <span data-ttu-id="f2488-182">请务必显式实现 ISerializable 成员。</span><span class="sxs-lookup"><span data-stu-id="f2488-182">DO implement the ISerializable members explicitly.</span></span>

     [!code-csharp[SerializationGuidelines#10](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#10)]
     [!code-vb[SerializationGuidelines#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#10)]

5. <span data-ttu-id="f2488-183">请务必向 **ISerializable.GetObjectData** 实现应用链接要求。</span><span class="sxs-lookup"><span data-stu-id="f2488-183">DO apply a link demand to **ISerializable.GetObjectData** implementation.</span></span> <span data-ttu-id="f2488-184">这将确保只有完全受信任的核心和运行时序列化程序才有权访问成员。</span><span class="sxs-lookup"><span data-stu-id="f2488-184">This ensures that only fully trusted core and the runtime serializer have access to the member.</span></span>

     [!code-csharp[SerializationGuidelines#11](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#11)]
     [!code-vb[SerializationGuidelines#11](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#11)]

## <a name="see-also"></a><span data-ttu-id="f2488-185">请参阅</span><span class="sxs-lookup"><span data-stu-id="f2488-185">See also</span></span>

- [<span data-ttu-id="f2488-186">使用数据协定</span><span class="sxs-lookup"><span data-stu-id="f2488-186">Using Data Contracts</span></span>](../../framework/wcf/feature-details/using-data-contracts.md)
- [<span data-ttu-id="f2488-187">数据协定序列化程序</span><span class="sxs-lookup"><span data-stu-id="f2488-187">Data Contract Serializer</span></span>](../../framework/wcf/feature-details/data-contract-serializer.md)
- [<span data-ttu-id="f2488-188">数据协定序列化程序支持的类型</span><span class="sxs-lookup"><span data-stu-id="f2488-188">Types Supported by the Data Contract Serializer</span></span>](../../framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
- [<span data-ttu-id="f2488-189">二进制序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-189">Binary Serialization</span></span>](binary-serialization.md)
- <span data-ttu-id="f2488-190">[.NET 远程处理](/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="f2488-190">[.NET Remoting](/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))</span></span>
- [<span data-ttu-id="f2488-191">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-191">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
- [<span data-ttu-id="f2488-192">安全性和序列化</span><span class="sxs-lookup"><span data-stu-id="f2488-192">Security and Serialization</span></span>](../../framework/misc/security-and-serialization.md)
