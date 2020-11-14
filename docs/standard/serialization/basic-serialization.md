---
title: 基本序列化
description: 本文说明如何使用 SerializableAttribute 使类可序列化，并包括序列化和反序列化的示例。
ms.date: 03/30/2017
helpviewer_keywords:
- binary serialization, basic serialization
- serialization, basic serialization
ms.assetid: d899d43c-335a-433e-a589-cd187192984f
dev_langs:
- CSharp
ms.openlocfilehash: 2b75ba6875b2a4430b6776c27dead72476884fff
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282074"
---
# <a name="basic-serialization"></a><span data-ttu-id="90f8a-103">基本序列化</span><span class="sxs-lookup"><span data-stu-id="90f8a-103">Basic serialization</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

<span data-ttu-id="90f8a-104">使类可序列化最简单的方法是按以下方式使用 <xref:System.SerializableAttribute> 对其进行标记。</span><span class="sxs-lookup"><span data-stu-id="90f8a-104">The easiest way to make a class serializable is to mark it with the <xref:System.SerializableAttribute> as follows.</span></span>  
  
```csharp  
[Serializable]  
public class MyObject {  
  public int n1 = 0;  
  public int n2 = 0;  
  public String str = null;  
}  
```  
  
<span data-ttu-id="90f8a-105">下面的代码示例演示如何将此类的实例序列化为文件。</span><span class="sxs-lookup"><span data-stu-id="90f8a-105">The following code example shows how an instance of this class can be serialized to a file.</span></span>  
  
```csharp  
MyObject obj = new MyObject();  
obj.n1 = 1;  
obj.n2 = 24;  
obj.str = "Some String";  
IFormatter formatter = new BinaryFormatter();  
Stream stream = new FileStream("MyFile.bin", FileMode.Create, FileAccess.Write, FileShare.None);  
formatter.Serialize(stream, obj);  
stream.Close();  
```  
  
<span data-ttu-id="90f8a-106">此示例使用二进制格式化程序执行序列化。</span><span class="sxs-lookup"><span data-stu-id="90f8a-106">This example uses a binary formatter to do the serialization.</span></span> <span data-ttu-id="90f8a-107">只需创建该流的实例及要使用的格式化程序，然后在该格式化程序上调用 Serialize 方法。</span><span class="sxs-lookup"><span data-stu-id="90f8a-107">All you need to do is create an instance of the stream and the formatter you intend to use, and then call the **Serialize** method on the formatter.</span></span> <span data-ttu-id="90f8a-108">要序列化的流和对象将作为参数提供给此调用。</span><span class="sxs-lookup"><span data-stu-id="90f8a-108">The stream and the object to serialize are provided as parameters to this call.</span></span> <span data-ttu-id="90f8a-109">尽管未在此示例中明确演示，但类的所有成员变量都将被序列化，即使将变量标记为私有也是如此。</span><span class="sxs-lookup"><span data-stu-id="90f8a-109">Although it is not explicitly demonstrated in this example, all member variables of a class will be serialized—even variables marked as private.</span></span> <span data-ttu-id="90f8a-110">在这一方面，二进制序列化与 <xref:System.Xml.Serialization.XmlSerializer> 类不同，后者只序列化公共字段。</span><span class="sxs-lookup"><span data-stu-id="90f8a-110">In this aspect, binary serialization differs from the <xref:System.Xml.Serialization.XmlSerializer> class, which only serializes public fields.</span></span> <span data-ttu-id="90f8a-111">有关从二进制序列化排除成员变量的信息，请参阅[选择性的序列化](selective-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="90f8a-111">For information on excluding member variables from binary serialization, see [Selective Serialization](selective-serialization.md).</span></span>  
  
<span data-ttu-id="90f8a-112">将对象还原回以前的状态同样很容易。</span><span class="sxs-lookup"><span data-stu-id="90f8a-112">Restoring the object back to its former state is just as easy.</span></span> <span data-ttu-id="90f8a-113">首先，创建用于读取的流和 <xref:System.Runtime.Serialization.Formatter>，然后指导格式化程序对该对象进行反序列化。</span><span class="sxs-lookup"><span data-stu-id="90f8a-113">First, create a stream for reading and a <xref:System.Runtime.Serialization.Formatter>, and then instruct the formatter to deserialize the object.</span></span> <span data-ttu-id="90f8a-114">下面的代码示例演示如何完成以上过程。</span><span class="sxs-lookup"><span data-stu-id="90f8a-114">The code example below shows how this is done.</span></span>  
  
```csharp  
IFormatter formatter = new BinaryFormatter();  
Stream stream = new FileStream("MyFile.bin", FileMode.Open, FileAccess.Read, FileShare.Read);  
MyObject obj = (MyObject) formatter.Deserialize(stream);  
stream.Close();  
  
// Here's the proof.  
Console.WriteLine("n1: {0}", obj.n1);  
Console.WriteLine("n2: {0}", obj.n2);  
Console.WriteLine("str: {0}", obj.str);  
```  
  
<span data-ttu-id="90f8a-115">上面使用的 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 非常有效，还可生成压缩字节流。</span><span class="sxs-lookup"><span data-stu-id="90f8a-115">The <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> used above is very efficient and produces a compact byte stream.</span></span> <span data-ttu-id="90f8a-116">使用此格式化程序序列化的所有对象也可使用它进行反序列化，这使得它成为对将在 .NET 上反序列化的对象进行序列化的理想工具。</span><span class="sxs-lookup"><span data-stu-id="90f8a-116">All objects serialized with this formatter can also be deserialized with it, which makes it an ideal tool for serializing objects that will be deserialized on .NET.</span></span> <span data-ttu-id="90f8a-117">需要特别注意的是，反序列化对象时不调用构造函数。</span><span class="sxs-lookup"><span data-stu-id="90f8a-117">It is important to note that constructors are not called when an object is deserialized.</span></span> <span data-ttu-id="90f8a-118">这是出于性能原因而对反序列化进行的约束。</span><span class="sxs-lookup"><span data-stu-id="90f8a-118">This constraint is placed on deserialization for performance reasons.</span></span> <span data-ttu-id="90f8a-119">然而，这违反了运行库对对象编写器制定的某些常用协定，并且将对象标记为可序列化时开发人员应确保了解其后果。</span><span class="sxs-lookup"><span data-stu-id="90f8a-119">However, this violates some of the usual contracts the runtime makes with the object writer, and developers should ensure that they understand the ramifications when marking an object as serializable.</span></span>  
  
<span data-ttu-id="90f8a-120">如果要求可迁移性，请改用 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>。</span><span class="sxs-lookup"><span data-stu-id="90f8a-120">If portability is a requirement, use the <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> instead.</span></span> <span data-ttu-id="90f8a-121">只需将以上代码中的 BinaryFormatter 替换为 SoapFormatter，然后同前面一样调用 Serialize 和 Deserialize   。</span><span class="sxs-lookup"><span data-stu-id="90f8a-121">Simply replace the **BinaryFormatter** in the code above with **SoapFormatter,** and call **Serialize** and **Deserialize** as before.</span></span> <span data-ttu-id="90f8a-122">此格式化程序针对以上使用的示例产生下面的输出：</span><span class="sxs-lookup"><span data-stu-id="90f8a-122">This formatter produces the following output for the example used above.</span></span>  
  
```xml  
<SOAP-ENV:Envelope  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns:SOAP-ENC="http://schemas.xmlsoap.org/soap/encoding/"  
  xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
  SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"  
  xmlns:a1="http://schemas.microsoft.com/clr/assem/ToFile">  
  
  <SOAP-ENV:Body>  
    <a1:MyObject id="ref-1">  
      <n1>1</n1>  
      <n2>24</n2>  
      <str id="ref-3">Some String</str>  
    </a1:MyObject>  
  </SOAP-ENV:Body>  
</SOAP-ENV:Envelope>  
```  
  
<span data-ttu-id="90f8a-123">请注意，无法继承 [Serializable](xref:System.SerializableAttribute) 属性。</span><span class="sxs-lookup"><span data-stu-id="90f8a-123">It's important to note that the [Serializable](xref:System.SerializableAttribute) attribute cannot be inherited.</span></span> <span data-ttu-id="90f8a-124">如果从 `MyObject` 派生新类，新类也必须标记为以上特性，否则将无法序列化。</span><span class="sxs-lookup"><span data-stu-id="90f8a-124">If you derive a new class from `MyObject`, the new class must be marked with the attribute as well, or it cannot be serialized.</span></span> <span data-ttu-id="90f8a-125">例如，尝试序列化以下类的实例时，将收到 <xref:System.Runtime.Serialization.SerializationException> 信息，提示 `MyStuff` 类型未标记为可序列化。</span><span class="sxs-lookup"><span data-stu-id="90f8a-125">For example, when you attempt to serialize an instance of the class below, you'll get a <xref:System.Runtime.Serialization.SerializationException> informing you that the `MyStuff` type is not marked as serializable.</span></span>  
  
```csharp  
public class MyStuff : MyObject
{  
  public int n3;  
}  
```  
  
 <span data-ttu-id="90f8a-126">使用 [Serializable](xref:System.SerializableAttribute) 属性非常方便，但有以上所述的限制。</span><span class="sxs-lookup"><span data-stu-id="90f8a-126">Using the [Serializable](xref:System.SerializableAttribute) attribute is convenient, but it has limitations as previously demonstrated.</span></span> <span data-ttu-id="90f8a-127">有关何时应标记类以进行序列化的信息，请参阅[序列化准则](serialization-guidelines.md)。</span><span class="sxs-lookup"><span data-stu-id="90f8a-127">Refer to the [Serialization Guidelines](serialization-guidelines.md) for information about when you should mark a class for serialization.</span></span> <span data-ttu-id="90f8a-128">若类已编译，则无法对其进行序列化。</span><span class="sxs-lookup"><span data-stu-id="90f8a-128">Serialization cannot be added to a class after it has been compiled.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="90f8a-129">请参阅</span><span class="sxs-lookup"><span data-stu-id="90f8a-129">See also</span></span>

- [<span data-ttu-id="90f8a-130">二进制序列化</span><span class="sxs-lookup"><span data-stu-id="90f8a-130">Binary Serialization</span></span>](binary-serialization.md)
- [<span data-ttu-id="90f8a-131">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="90f8a-131">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
