---
title: 自定义序列化
description: 自定义序列化控制着类型的序列化和反序列化。 控制序列化可确保序列化兼容性。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binary serialization, custom serialization
- custom serialization
- binary serialization, controlling
- OptionalFieldAttribute class, custom serialization
- ISerializable interface, custom serialization
- OnDeserializingAttribute class, custom serialization
- OnSerializedAttribute class, custom serialization
- serialization, custom serialization
- serialization, controlling
- OnDeserializedAttribute class, custom serialization
- OnSerializingAttribute class, custom serialization
ms.assetid: 12ed422d-5280-49b8-9b71-a2ed129c0384
ms.openlocfilehash: 8e8d8d38ab8170a9bf9fae098e267be1a38f27d0
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93281796"
---
# <a name="custom-serialization"></a><span data-ttu-id="7108d-104">自定义序列化</span><span class="sxs-lookup"><span data-stu-id="7108d-104">Custom serialization</span></span>

<span data-ttu-id="7108d-105">自定义序列化是控制类型的序列化和反序列化的过程。</span><span class="sxs-lookup"><span data-stu-id="7108d-105">Custom serialization is the process of controlling the serialization and deserialization of a type.</span></span> <span data-ttu-id="7108d-106">通过控制序列化，可以确保序列化兼容性。换而言之，在不中断类型核心功能的情况下，可在类型的不同版本之间序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="7108d-106">By controlling serialization, it's possible to ensure serialization compatibility, which is the ability to serialize and deserialize between versions of a type without breaking the core functionality of the type.</span></span> <span data-ttu-id="7108d-107">例如，在类型的第一个版本中，可能只有两个字段。</span><span class="sxs-lookup"><span data-stu-id="7108d-107">For example, in the first version of a type, there may be only two fields.</span></span> <span data-ttu-id="7108d-108">在类型的下一个版本中，添加了其他几个字段。</span><span class="sxs-lookup"><span data-stu-id="7108d-108">In the next version of a type, several more fields are added.</span></span> <span data-ttu-id="7108d-109">但是，第二个版本的应用程序必须可对这两种类型进行序列化和反序列化。</span><span class="sxs-lookup"><span data-stu-id="7108d-109">Yet the second version of an application must be able to serialize and deserialize both types.</span></span> <span data-ttu-id="7108d-110">以下各节说明如何控制序列化。</span><span class="sxs-lookup"><span data-stu-id="7108d-110">The following sections describe how to control serialization.</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
> [!IMPORTANT]
> <span data-ttu-id="7108d-111">在早于 .NET Framework 4.0 的版本中，部分受信任的程序集中自定义用户数据的序列化是使用 `GetObjectData` 完成的。</span><span class="sxs-lookup"><span data-stu-id="7108d-111">In versions previous to .NET Framework 4.0, serialization of custom user data in a partially trusted assembly was accomplished using `GetObjectData`.</span></span> <span data-ttu-id="7108d-112">从版本 4.0 开始，该方法将标记有 <xref:System.Security.SecurityCriticalAttribute> 特性，该特性阻止在部分受信任的程序集中执行。</span><span class="sxs-lookup"><span data-stu-id="7108d-112">Starting with version 4.0, that method is marked with the <xref:System.Security.SecurityCriticalAttribute> attribute, which prevents execution in partially trusted assemblies.</span></span> <span data-ttu-id="7108d-113">若要解决此情况，请实现 <xref:System.Runtime.Serialization.ISafeSerializationData> 接口。</span><span class="sxs-lookup"><span data-stu-id="7108d-113">To work around this condition, implement the <xref:System.Runtime.Serialization.ISafeSerializationData> interface.</span></span>  
  
## <a name="running-custom-methods-during-and-after-serialization"></a><span data-ttu-id="7108d-114">在序列化期间和序列化之后运行自定义方法</span><span class="sxs-lookup"><span data-stu-id="7108d-114">Running custom methods during and after serialization</span></span>

<span data-ttu-id="7108d-115">序列化期间和序列化之后运行自定义方法的建议方法，是在序列化期间和序列化之后，将下列属性应用于更正数据所用的方法：</span><span class="sxs-lookup"><span data-stu-id="7108d-115">The recommended way to run custom methods during and after serialization is to apply the following attributes to methods that are used to correct data during and after serialization:</span></span>  
  
- <xref:System.Runtime.Serialization.OnDeserializedAttribute>  
  
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>  
  
- <xref:System.Runtime.Serialization.OnSerializedAttribute>  
  
- <xref:System.Runtime.Serialization.OnSerializingAttribute>  
  
 <span data-ttu-id="7108d-116">这些属性允许类型参与序列化和反序列化过程中的任何一个阶段或所有四个阶段。</span><span class="sxs-lookup"><span data-stu-id="7108d-116">These attributes allow the type to participate in any one of, or all four of the phases, of the serialization and deserialization processes.</span></span> <span data-ttu-id="7108d-117">这些特性为类型指定了应该在每个阶段调用的方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-117">The attributes specify the methods of the type that should be invoked during each phase.</span></span> <span data-ttu-id="7108d-118">这些方法不会访问序列化流，但是反而允许您在序列化或反序列化前后更改对象。</span><span class="sxs-lookup"><span data-stu-id="7108d-118">The methods do not access the serialization stream but instead allow you to alter the object before and after serialization, or before and after deserialization.</span></span> <span data-ttu-id="7108d-119">可以在类型继承层次结构中的所有级别上应用这些特性，而每种方法在该层次结构中是按从基类型到派生程度最大的类型的顺序调用的。</span><span class="sxs-lookup"><span data-stu-id="7108d-119">The attributes can be applied at all levels of the type inheritance hierarchy, and each method is called in the hierarchy from the base to the most derived.</span></span> <span data-ttu-id="7108d-120">这种机制使得序列化和反序列化可以负责到派生程度最大的实现，从而可以避免实现 <xref:System.Runtime.Serialization.ISerializable> 接口时的复杂性和任何导致的问题。</span><span class="sxs-lookup"><span data-stu-id="7108d-120">This mechanism avoids the complexity and any resulting issues of implementing the <xref:System.Runtime.Serialization.ISerializable> interface by giving the responsibility for serialization and deserialization to the most derived implementation.</span></span> <span data-ttu-id="7108d-121">此外，这种机制允许格式化程序忽略字段的填充以及从序列化流中检索。</span><span class="sxs-lookup"><span data-stu-id="7108d-121">Additionally, this mechanism allows the formatters to ignore the population of fields and retrieval from the serialization stream.</span></span> <span data-ttu-id="7108d-122">有关控制序列化和反序列化的详细信息和示例，请单击以上任一链接。</span><span class="sxs-lookup"><span data-stu-id="7108d-122">For details and examples of controlling serialization and deserialization, click any of the previous links.</span></span>  
  
 <span data-ttu-id="7108d-123">另外，向现有的可序列化类型中添加新字段时，可将 <xref:System.Runtime.Serialization.OptionalFieldAttribute> 特性应用于该字段。</span><span class="sxs-lookup"><span data-stu-id="7108d-123">In addition, when adding a new field to an existing serializable type, apply the <xref:System.Runtime.Serialization.OptionalFieldAttribute> attribute to the field.</span></span> <span data-ttu-id="7108d-124">处理缺少新字段的流时，<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 和 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 可以忽略不存在该字段的情况。</span><span class="sxs-lookup"><span data-stu-id="7108d-124">The <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> and the <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> ignores the absence of the field when a stream that is missing the new field is processed.</span></span>  
  
## <a name="implementing-the-iserializable-interface"></a><span data-ttu-id="7108d-125">实现 ISerializable 接口</span><span class="sxs-lookup"><span data-stu-id="7108d-125">Implementing the ISerializable interface</span></span>  
 <span data-ttu-id="7108d-126">控制序列化的另一种方法是对某个对象实现 <xref:System.Runtime.Serialization.ISerializable> 接口。</span><span class="sxs-lookup"><span data-stu-id="7108d-126">The other way to control serialization is achieved by implementing the <xref:System.Runtime.Serialization.ISerializable> interface on an object.</span></span> <span data-ttu-id="7108d-127">但请注意，上一节采用的方法会取代这种方法对序列化进行控制。</span><span class="sxs-lookup"><span data-stu-id="7108d-127">Note, however, that the method in the previous section supersedes this method to control serialization.</span></span>  
  
 <span data-ttu-id="7108d-128">除此之外，如果使用 [Serializable](xref:System.SerializableAttribute) 属性对某个类进行标记，且该类在类级别或对其构造函数具有声明性或命令性安全，则不应对该类执行默认的序列化。</span><span class="sxs-lookup"><span data-stu-id="7108d-128">In addition, you should not use default serialization on a class that is marked with the [Serializable](xref:System.SerializableAttribute) attribute and has declarative or imperative security at the class level or on its constructors.</span></span> <span data-ttu-id="7108d-129">相反，这样的类应该始终实现 <xref:System.Runtime.Serialization.ISerializable> 接口。</span><span class="sxs-lookup"><span data-stu-id="7108d-129">Instead, these classes should always implement the <xref:System.Runtime.Serialization.ISerializable> interface.</span></span>  
  
 <span data-ttu-id="7108d-130">实现 <xref:System.Runtime.Serialization.ISerializable> 涉及到实现 `GetObjectData` 方法以及反序列化对象时所用的特殊构造函数。</span><span class="sxs-lookup"><span data-stu-id="7108d-130">Implementing <xref:System.Runtime.Serialization.ISerializable> involves implementing the `GetObjectData` method and a special constructor that is used when the object is deserialized.</span></span> <span data-ttu-id="7108d-131">下面的示例代码演示如何对上一节中的 <xref:System.Runtime.Serialization.ISerializable> 类实现 `MyObject`。</span><span class="sxs-lookup"><span data-stu-id="7108d-131">The following sample code shows how to implement <xref:System.Runtime.Serialization.ISerializable> on the `MyObject` class from a previous section.</span></span>  
  
```csharp
[Serializable]
public class MyObject : ISerializable
{
    public int n1;
    public int n2;
    public String str;

    public MyObject()
    {
    }

    protected MyObject(SerializationInfo info, StreamingContext context)
    {
      n1 = info.GetInt32("i");
      n2 = info.GetInt32("j");
      str = info.GetString("k");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public virtual void GetObjectData(SerializationInfo info, StreamingContext context)
    {
        info.AddValue("i", n1);
        info.AddValue("j", n2);
        info.AddValue("k", str);
    }
}
```

```vb
<Serializable()>  _
Public Class MyObject
    Implements ISerializable
    Public n1 As Integer
    Public n2 As Integer
    Public str As String

    Public Sub New()
    End Sub

    Protected Sub New(ByVal info As SerializationInfo, ByVal context As StreamingContext)
        n1 = info.GetInt32("i")
        n2 = info.GetInt32("j")
        str = info.GetString("k")
    End Sub 'New

    <SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)> _
    Public Overridable Sub GetObjectData(ByVal info As SerializationInfo, ByVal context As StreamingContext)
        info.AddValue("i", n1)
        info.AddValue("j", n2)
        info.AddValue("k", str)
    End Sub
End Class
```  
  
 <span data-ttu-id="7108d-132">序列化期间调用 GetObjectData 时，由用户负责填充随方法调用一起提供的 <xref:System.Runtime.Serialization.SerializationInfo>。</span><span class="sxs-lookup"><span data-stu-id="7108d-132">When **GetObjectData** is called during serialization, you are responsible for populating the <xref:System.Runtime.Serialization.SerializationInfo> provided with the method call.</span></span> <span data-ttu-id="7108d-133">将待序列化变量以名称和值对的形式添加。</span><span class="sxs-lookup"><span data-stu-id="7108d-133">Add the variables to be serialized as name and value pairs.</span></span> <span data-ttu-id="7108d-134">任何文本都能用作名称。</span><span class="sxs-lookup"><span data-stu-id="7108d-134">Any text can be used as the name.</span></span> <span data-ttu-id="7108d-135">如果对足够多的数据进行序列化，以在反序列化期间还原对象，您便可随意决定将哪些成员变量添加到 <xref:System.Runtime.Serialization.SerializationInfo>。</span><span class="sxs-lookup"><span data-stu-id="7108d-135">You have the freedom to decide which member variables are added to the <xref:System.Runtime.Serialization.SerializationInfo>, provided that sufficient data is serialized to restore the object during deserialization.</span></span> <span data-ttu-id="7108d-136">如果基对象实现 <xref:System.Runtime.Serialization.ISerializable>，则派生类应该对该基对象调用 GetObjectData 方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-136">Derived classes should call the **GetObjectData** method on the base object if the latter implements <xref:System.Runtime.Serialization.ISerializable>.</span></span>  
  
 <span data-ttu-id="7108d-137">请注意，序列化可以允许其他代码查看或修改用其他方式无法访问的对象实例数据。</span><span class="sxs-lookup"><span data-stu-id="7108d-137">Note that serialization can allow other code to see or modify object instance data that is otherwise inaccessible.</span></span> <span data-ttu-id="7108d-138">因此，执行序列化的代码需使用指定了 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 标志的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)。</span><span class="sxs-lookup"><span data-stu-id="7108d-138">Therefore, code that performs serialization requires the [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> flag specified.</span></span> <span data-ttu-id="7108d-139">在默认策略下，通过 Internet 下载的代码或 Intranet 代码不会授予该权限；只有本地计算机上的代码才被授予该权限。</span><span class="sxs-lookup"><span data-stu-id="7108d-139">Under default policy, this permission is not given to Internet-downloaded or intranet code; only code on the local computer is granted this permission.</span></span> <span data-ttu-id="7108d-140">必须采用下列方式显式保护 GetObjectData 方法：要求使用使用指定了 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 标志的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)，或者要求具备专门用于帮助保护私有数据的其他权限。</span><span class="sxs-lookup"><span data-stu-id="7108d-140">The **GetObjectData** method must be explicitly protected either by demanding the [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> flag specified or by demanding other permissions that specifically help protect private data.</span></span>  
  
 <span data-ttu-id="7108d-141">若私有字段存储的是敏感信息，应该要求对 GetObjectData 具备相应权限，以便保护该数据。</span><span class="sxs-lookup"><span data-stu-id="7108d-141">If a private field stores sensitive information, you should demand the appropriate permissions on **GetObjectData** to protect the data.</span></span> <span data-ttu-id="7108d-142">请记住，如果已向代码授予指定了 SerializationFormatter 标志的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)，则该代码可查看和修改私有字段中存储的数据。</span><span class="sxs-lookup"><span data-stu-id="7108d-142">Remember that code that has been granted [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the **SerializationFormatter** flag specified can view and modify the data stored in private fields.</span></span> <span data-ttu-id="7108d-143">被授予此 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) 的恶意调用方可以查看相关数据（如隐藏的目录位置或授予的权限），还可以通过这些数据利用计算机中的安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="7108d-143">A malicious caller granted this [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) can view data such as hidden directory locations or granted permissions and use the data to exploit a security vulnerability on the computer.</span></span> <span data-ttu-id="7108d-144">有关可以指定的安全权限标志的完整列表，请参阅 [SecurityPermissionFlag 枚举](xref:System.Security.Permissions.SecurityPermissionFlag)。</span><span class="sxs-lookup"><span data-stu-id="7108d-144">For a complete list of the security permission flags you can specify, see the [SecurityPermissionFlag Enumeration](xref:System.Security.Permissions.SecurityPermissionFlag).</span></span>  
  
 <span data-ttu-id="7108d-145">强调何时将 <xref:System.Runtime.Serialization.ISerializable> 添加到必须同时实现 **GetObjectData** 和特殊构造函数的某个类，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="7108d-145">It's important to stress that when <xref:System.Runtime.Serialization.ISerializable> is added to a class you must implement both **GetObjectData** and the special constructor.</span></span> <span data-ttu-id="7108d-146">如果缺少 GetObjectData，编译器会发出警告。</span><span class="sxs-lookup"><span data-stu-id="7108d-146">The compiler warns you if **GetObjectData** is missing.</span></span> <span data-ttu-id="7108d-147">但是，鉴于无法强制实现构造函数，如果不存在该构造函数，则不会发出任何警告，但此时如果尝试对某个类进行反序列化，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="7108d-147">However, because it is impossible to enforce the implementation of a constructor, no warning is provided if the constructor is absent, and an exception is thrown when an attempt is made to deserialize a class without the constructor.</span></span>  
  
 <span data-ttu-id="7108d-148">若要解决潜在的安全和版本化问题，当前的设计应该优先于 <xref:System.Runtime.Serialization.ISerializationSurrogate.SetObjectData%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-148">The current design was favored above a <xref:System.Runtime.Serialization.ISerializationSurrogate.SetObjectData%2A> method to get around potential security and versioning problems.</span></span> <span data-ttu-id="7108d-149">例如，如果将 `SetObjectData` 方法定义为接口的组成部分，则该方法必须是公共方法。因此，用户必须编写代码，以防多次调用 SetObjectData 方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-149">For example, a `SetObjectData` method must be public if it is defined as part of an interface; thus users must write code to defend against having the **SetObjectData** method called multiple times.</span></span> <span data-ttu-id="7108d-150">否则，在执行某项操作的过程中，对某个对象调用 SetObjectData 方法的恶意应用程序可能会导致潜在的问题。</span><span class="sxs-lookup"><span data-stu-id="7108d-150">Otherwise, a malicious application that calls the **SetObjectData** method on an object in the process of executing an operation can cause potential problems.</span></span>  
  
 <span data-ttu-id="7108d-151">在反序列化期间，使用为这个目的提供的构造函数将 <xref:System.Runtime.Serialization.SerializationInfo> 传递到类。</span><span class="sxs-lookup"><span data-stu-id="7108d-151">During deserialization, <xref:System.Runtime.Serialization.SerializationInfo> is passed to the class using the constructor provided for this purpose.</span></span> <span data-ttu-id="7108d-152">反序列化该对象时，将会忽略对该构造函数施加的任何可见性限制。因此，可将该类标记为公共类、受保护的类、内部类或私有类。</span><span class="sxs-lookup"><span data-stu-id="7108d-152">Any visibility constraints placed on the constructor are ignored when the object is deserialized; so you can mark the class as public, protected, internal, or private.</span></span> <span data-ttu-id="7108d-153">但是，除非密封了该类，否则最好将构造函数设为受保护的函数；如果密封了该类，应将构造函数标记为私有函数。</span><span class="sxs-lookup"><span data-stu-id="7108d-153">However, it is a best practice to make the constructor protected unless the class is sealed, in which case the constructor should be marked private.</span></span> <span data-ttu-id="7108d-154">构造函数还应该执行彻底的输入验证。</span><span class="sxs-lookup"><span data-stu-id="7108d-154">The constructor should also perform thorough input validation.</span></span> <span data-ttu-id="7108d-155">为避免被恶意代码误用，构造函数应该强制实施安全性检查和权限，而这些安全性检查和权限也是使用其他任何构造函数获取该类的实例所必需的。</span><span class="sxs-lookup"><span data-stu-id="7108d-155">To avoid misuse by malicious code, the constructor should enforce the same security checks and permissions required to obtain an instance of the class using any other constructor.</span></span> <span data-ttu-id="7108d-156">如果不采纳上述建议，恶意代码会跳过使用公共构造函数在标准实例构造期间应用的所有安全性，预序列化对象，获取对使用指定了 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 标志的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) 的控制，并反序列化客户端计算机上的对象。</span><span class="sxs-lookup"><span data-stu-id="7108d-156">If you do not follow this recommendation, malicious code can preserialize an object, obtain control with the [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> flag specified and deserialize the object on a client computer bypassing any security that would have been applied during standard instance construction using a public constructor.</span></span>  
  
 <span data-ttu-id="7108d-157">若要还原对象的状态，只需使用序列化期间采用的名称从 <xref:System.Runtime.Serialization.SerializationInfo> 中检索变量值即可。</span><span class="sxs-lookup"><span data-stu-id="7108d-157">To restore the state of the object, simply retrieve the values of the variables from <xref:System.Runtime.Serialization.SerializationInfo> using the names used during serialization.</span></span> <span data-ttu-id="7108d-158">如果基类实现 <xref:System.Runtime.Serialization.ISerializable>，则应调用基构造函数，以使基对象可以还原其变量。</span><span class="sxs-lookup"><span data-stu-id="7108d-158">If the base class implements <xref:System.Runtime.Serialization.ISerializable>, the base constructor should be called to allow the base object to restore its variables.</span></span>  
  
 <span data-ttu-id="7108d-159">从实现 <xref:System.Runtime.Serialization.ISerializable> 的类派生新类时，如果派生类的变量需要进行序列化，则该派生类必须同时实现构造函数和 GetObjectData 方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-159">When you derive a new class from one that implements <xref:System.Runtime.Serialization.ISerializable>, the derived class must implement both the constructor as well as the **GetObjectData** method if it has variables that need to be serialized.</span></span> <span data-ttu-id="7108d-160">下面的代码示例演示如何使用前面说明的 `MyObject` 类完成此项操作。</span><span class="sxs-lookup"><span data-stu-id="7108d-160">The following code example shows how this is done using the `MyObject` class shown previously.</span></span>  
  
```csharp
[Serializable]
public class ObjectTwo : MyObject
{
    public int num;

    public ObjectTwo()
      : base()
    {
    }

    protected ObjectTwo(SerializationInfo si, StreamingContext context)
      : base(si, context)
    {
        num = si.GetInt32("num");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public override void GetObjectData(SerializationInfo si, StreamingContext context)
    {
        base.GetObjectData(si,context);
        si.AddValue("num", num);
    }
}
```

```vb
<Serializable()>  _
Public Class ObjectTwo
    Inherits MyObject
    Public num As Integer

    Public Sub New()

    End Sub

    Protected Sub New(ByVal si As SerializationInfo, _
    ByVal context As StreamingContext)
        MyBase.New(si, context)
        num = si.GetInt32("num")
    End Sub

    <SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)> _
    Public Overrides Sub GetObjectData(ByVal si As SerializationInfo, ByVal context As StreamingContext)
        MyBase.GetObjectData(si, context)
        si.AddValue("num", num)
    End Sub
End Class
```  
  
 <span data-ttu-id="7108d-161">不要忘记在反序列化构造函数中调用基类。</span><span class="sxs-lookup"><span data-stu-id="7108d-161">Don't forget to call the base class in the deserialization constructor.</span></span> <span data-ttu-id="7108d-162">如果没有完成此操作，决不会调用基类上的构造函数，也不会在反序列化之后完全构造该对象。</span><span class="sxs-lookup"><span data-stu-id="7108d-162">If this isn't done, the constructor on the base class is never called, and the object is not fully constructed after deserialization.</span></span>  
  
 <span data-ttu-id="7108d-163">对象是从内到外重新构造的；在反序列化期间调用方法时，可能会产生非预期的副作用，原因是调用的方法引用的可能是执行调用时尚未反序列化的对象引用。</span><span class="sxs-lookup"><span data-stu-id="7108d-163">Objects are reconstructed from the inside out; and calling methods during deserialization can have undesirable side effects, because the methods called might refer to object references that have not been deserialized by the time the call is made.</span></span> <span data-ttu-id="7108d-164">如果正在被反序列化的类实现 <xref:System.Runtime.Serialization.IDeserializationCallback>，则反序列化整个对象图后，将会自动调用 <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-164">If the class being deserialized implements the <xref:System.Runtime.Serialization.IDeserializationCallback>, the <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%2A> method is automatically called when the entire object graph has been deserialized.</span></span> <span data-ttu-id="7108d-165">此时，便已完全还原引用的所有子对象。</span><span class="sxs-lookup"><span data-stu-id="7108d-165">At this point, all the child objects referenced have been fully restored.</span></span> <span data-ttu-id="7108d-166">哈希表是类的典型示例，在不使用事件侦听器的情况下，很难对哈希表进行反序列化。</span><span class="sxs-lookup"><span data-stu-id="7108d-166">A hash table is a typical example of a class that is difficult to deserialize without using the event listener.</span></span> <span data-ttu-id="7108d-167">虽然在反序列化期间易于检索键和值对，但是，将这些对象重新添加到哈希表时，可能会引起问题，原因是不能保证派生自哈希表的类已被反序列化。</span><span class="sxs-lookup"><span data-stu-id="7108d-167">It is easy to retrieve the key and value pairs during deserialization, but adding these objects back to the hash table can cause problems, because there is no guarantee that classes that derived from the hash table have been deserialized.</span></span> <span data-ttu-id="7108d-168">因此，不建议在这个阶段对哈希表调用方法。</span><span class="sxs-lookup"><span data-stu-id="7108d-168">Calling methods on a hash table at this stage is therefore not advisable.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7108d-169">请参阅</span><span class="sxs-lookup"><span data-stu-id="7108d-169">See also</span></span>

- [<span data-ttu-id="7108d-170">二进制序列化</span><span class="sxs-lookup"><span data-stu-id="7108d-170">Binary Serialization</span></span>](binary-serialization.md)
- [<span data-ttu-id="7108d-171">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="7108d-171">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
- [<span data-ttu-id="7108d-172">安全性和序列化</span><span class="sxs-lookup"><span data-stu-id="7108d-172">Security and Serialization</span></span>](../../framework/misc/security-and-serialization.md)
