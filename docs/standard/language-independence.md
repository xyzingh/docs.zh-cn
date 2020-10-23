---
title: 语言独立性和与语言无关的组件
description: 了解如何使用 .NET 中支持的众多语言之一（如 C#、C++/CLI、F#、IronPython、VB、Visual COBOL 和 PowerShell）进行开发。
ms.date: 07/22/2016
dev_langs:
- csharp
- vb
ms.technology: dotnet-standard
ms.assetid: 2dbed1bc-86f5-43cd-9a57-adbb1c5efba4
ms.openlocfilehash: 524f8dc9838d7c438e8155da683c4fa5b01f36a3
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162981"
---
# <a name="language-independence-and-language-independent-components"></a><span data-ttu-id="8fc7a-103">语言独立性和与语言无关的组件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-103">Language independence and language-independent components</span></span>

<span data-ttu-id="8fc7a-104">.NET 是独立的语言。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-104">.NET is language independent.</span></span> <span data-ttu-id="8fc7a-105">这意味着，开发人员可使用面向 .NET 实现的多种语言之一（例如 C#、F# 和 Visual Basic）进行开发。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-105">This means that, as a developer, you can develop in one of the many languages that target .NET implementations, such as C#, F#, and Visual Basic.</span></span> <span data-ttu-id="8fc7a-106">可访问针对 .NET 实现开发的类库的类型和成员，而不必了解它们的初始编写语言，也不必遵循任何原始语言的约定。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-106">You can access the types and members of class libraries developed for .NET implementations without having to know the language in which they were originally written and without having to follow any of the original language's conventions.</span></span> <span data-ttu-id="8fc7a-107">如果你是组件开发人员，无论组件采用哪种语言，均可由任何 .NET 应用访问。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-107">If you're a component developer, your component can be accessed by any .NET app, regardless of its language.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc7a-108">本文的第一部分讨论如何创建独立于语言的组件（即以任何语言编写的应用均可以使用的组件）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-108">This first part of this article discusses creating language-independent components, that is, components that can be consumed by apps that are written in any language.</span></span> <span data-ttu-id="8fc7a-109">还可以从用多种语言编写的源代码创建单个组件或应用；请参阅本文第二部分的[跨语言互操作性](#cross-language-interoperability)。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-109">You can also create a single component or app from source code written in multiple languages; see [Cross-Language Interoperability](#cross-language-interoperability) in the second part of this article.</span></span>

<span data-ttu-id="8fc7a-110">若要与使用任何语言编写的其他对象完全交互，对象必须只向调用方公开那些所有语言共有的功能。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-110">To fully interact with other objects written in any language, objects must expose to callers only those features that are common to all languages.</span></span> <span data-ttu-id="8fc7a-111">此组通用功能由公共语言规范 (CLS) 定义，后者是一组适用于生成的程序集的规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-111">This common set of features is defined by the Common Language Specification (CLS), which is a set of rules that apply to generated assemblies.</span></span> <span data-ttu-id="8fc7a-112">公共语言规范在 [ECMA-335 标准：公共语言基础结构](https://www.ecma-international.org/publications/standards/Ecma-335.htm)的第 I 部分的第 7 条至第 11 条中进行了定义。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-112">The Common Language Specification is defined in Partition I, Clauses 7 through 11 of the [ECMA-335 Standard: Common Language Infrastructure](https://www.ecma-international.org/publications/standards/Ecma-335.htm).</span></span>

<span data-ttu-id="8fc7a-113">如果你的组件符合公共语言规范，则保证其符合 CLS 并可通过支持 CLS 的任何编程语言编写的程序集中的代码对其进行访问。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-113">If your component conforms to the Common Language Specification, it is guaranteed to be CLS-compliant and can be accessed from code in assemblies written in any programming language that supports the CLS.</span></span> <span data-ttu-id="8fc7a-114">可以通过将 [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) 特性应用于源代码来确定自己的组件在编译时是否符合公共语言规范。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-114">You can determine whether your component conforms to the Common Language Specification at compile time by applying the [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) attribute to your source code.</span></span> <span data-ttu-id="8fc7a-115">有关详细信息，请参阅 [CLSCompliantAttribute 特性](#the-clscompliantattribute-attribute)。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-115">For more information, see [The CLSCompliantAttribute attribute](#the-clscompliantattribute-attribute).</span></span>

## <a name="cls-compliance-rules"></a><span data-ttu-id="8fc7a-116">CLS 遵从性规则</span><span class="sxs-lookup"><span data-stu-id="8fc7a-116">CLS compliance rules</span></span>

<span data-ttu-id="8fc7a-117">本节讨论用于创建符合 CLS 的组件的规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-117">This section discusses the rules for creating a CLS-compliant component.</span></span> <span data-ttu-id="8fc7a-118">有关规则的完整列表，请参阅 [ECMA-335 标准：公共语言基础结构](https://www.ecma-international.org/publications/standards/Ecma-335.htm)的第 I 部分的第 7 条至第 11 条中进行了定义。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-118">For a complete list of rules, see Partition I, Clause 11 of the [ECMA-335 Standard: Common Language Infrastructure](https://www.ecma-international.org/publications/standards/Ecma-335.htm).</span></span>

> [!NOTE]
> <span data-ttu-id="8fc7a-119">公共语言规范讨论 CLS 遵从性的每个规则，因为它应用于使用者（以编程方式访问符合 CLS 的组件的开发人员）、框架（使用语言编译器创建符合 CLS 的库的开发人员）和扩展人员（创建可创建符合 CLS 的组件的语言编译器或代码分析器等工具的开发人员）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-119">The Common Language Specification discusses each rule for CLS compliance as it applies to consumers (developers who are programmatically accessing a component that is CLS-compliant), frameworks (developers who are using a language compiler to create CLS-compliant libraries), and extenders (developers who are creating a tool such as a language compiler or a code parser that creates CLS-compliant components).</span></span> <span data-ttu-id="8fc7a-120">本文重点介绍适用于框架的规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-120">This article focuses on the rules as they apply to frameworks.</span></span> <span data-ttu-id="8fc7a-121">但请注意，一些适用于扩展程序的规则也适用于使用 [Reflection.Emit](xref:System.Reflection.Emit) 创建的程序集。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-121">Note, though, that some of the rules that apply to extenders may also apply to assemblies that are created using [Reflection.Emit](xref:System.Reflection.Emit).</span></span>

<span data-ttu-id="8fc7a-122">若要设计独立于语言的组件，您只需将 CLS 遵从性的规则应用于组件的公共接口即可。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-122">To design a component that is language independent, you only need to apply the rules for CLS compliance to your component's public interface.</span></span> <span data-ttu-id="8fc7a-123">您的私有实现不必符合规范。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-123">Your private implementation does not have to conform to the specification.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fc7a-124">CLS 遵从性的规则仅适用于组件的公共接口，而非其私有实现。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-124">The rules for CLS compliance apply only to a component's public interface, not to its private implementation.</span></span>

<span data-ttu-id="8fc7a-125">例如，[Byte](xref:System.Byte) 之外的无符号整数不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-125">For example, unsigned integers other than [Byte](xref:System.Byte) are not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-126">由于以下示例中的 `Person` 类公开了 [UInt16](xref:System.UInt16) 类型的 `Age` 属性，因此下面的代码显示编译器警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-126">Because the `Person` class in the following example exposes an `Age` property of type [UInt16](xref:System.UInt16), the following code displays a compiler warning.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Person
{
   private UInt16 personAge = 0;

   public UInt16 Age
   { get { return personAge; } }
}
// The attempt to compile the example displays the following compiler warning:
//    Public1.cs(10,18): warning CS3003: Type of 'Person.Age' is not CLS-compliant
```

```vb
<Assembly: CLSCompliant(True)>

Public Class Person
   Private personAge As UInt16

   Public ReadOnly Property Age As UInt16
      Get
         Return personAge
      End Get
   End Property
End Class
' The attempt to compile the example displays the following compiler warning:
'    Public1.vb(9) : warning BC40027: Return type of function 'Age' is not CLS-compliant.
'
'       Public ReadOnly Property Age As UInt16
'                                ~~~
```

<span data-ttu-id="8fc7a-127">可以通过将 `Age` 属性的类型从 `UInt16` 更改为 [Int16](xref:System.Int16) 来将 Person 类设置为符合 CLS，即一个符合 CLS 的 16 位带符号整数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-127">You can make the Person class CLS-compliant by changing the type of `Age` property from `UInt16` to [Int16](xref:System.Int16), which is a CLS-compliant, 16-bit signed integer.</span></span> <span data-ttu-id="8fc7a-128">您无需更改私有 `personAge` 字段的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-128">You do not have to change the type of the private `personAge` field.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Person
{
   private Int16 personAge = 0;

   public Int16 Age
   { get { return personAge; } }
}
```

```vb
<Assembly: CLSCompliant(True)>

Public Class Person
   Private personAge As UInt16

   Public ReadOnly Property Age As Int16
      Get
         Return CType(personAge, Int16)
      End Get
   End Property
End Class
```

<span data-ttu-id="8fc7a-129">库的公共接口包括：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-129">A library's public interface consists of the following:</span></span>

* <span data-ttu-id="8fc7a-130">公共类的定义。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-130">Definitions of public classes.</span></span>

* <span data-ttu-id="8fc7a-131">公共类中公共成员的定义，以及派生类可以访问的成员（即受保护的成员）的定义。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-131">Definitions of the public members of public classes, and definitions of members accessible to derived classes (that is, protected members).</span></span>

* <span data-ttu-id="8fc7a-132">公共类中公共方法的参数和返回类型，以及派生类可以访问的方法的参数和返回类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-132">Parameters and return types of public methods of public classes, and parameters and return types of methods accessible to derived classes.</span></span>

<span data-ttu-id="8fc7a-133">下表中将列出 CLS 遵从性规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-133">The rules for CLS compliance are listed in the following table.</span></span> <span data-ttu-id="8fc7a-134">规则的文本摘自 [ECMA-335 标准：公共语言基础结构](https://www.ecma-international.org/publications/standards/Ecma-335.htm)（版权所有 2012，Ecma International）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-134">The text of the rules is taken verbatim from the [ECMA-335 Standard: Common Language Infrastructure](https://www.ecma-international.org/publications/standards/Ecma-335.htm), which is Copyright 2012 by Ecma International.</span></span> <span data-ttu-id="8fc7a-135">有关这些规则的详细信息，请参阅以下各节。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-135">More detailed information about these rules is found in the following sections.</span></span>

<span data-ttu-id="8fc7a-136">类别</span><span class="sxs-lookup"><span data-stu-id="8fc7a-136">Category</span></span> | <span data-ttu-id="8fc7a-137">查看</span><span class="sxs-lookup"><span data-stu-id="8fc7a-137">See</span></span> | <span data-ttu-id="8fc7a-138">规则</span><span class="sxs-lookup"><span data-stu-id="8fc7a-138">Rule</span></span> | <span data-ttu-id="8fc7a-139">规则编号</span><span class="sxs-lookup"><span data-stu-id="8fc7a-139">Rule Number</span></span>
-------- | --- | ---- | -----------
<span data-ttu-id="8fc7a-140">可访问性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-140">Accessibility</span></span> | [<span data-ttu-id="8fc7a-141">成员可访问性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-141">Member accessibility</span></span>](#member-accessibility) | <span data-ttu-id="8fc7a-142">重写继承的方法时，可访问性应不会更改（重写一个继承自其他具有可访问性 `family-or-assembly` 的程序集的方法除外）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-142">Accessibility shall not be changed when overriding inherited methods, except when overriding a method inherited from a different assembly with accessibility `family-or-assembly`.</span></span> <span data-ttu-id="8fc7a-143">在此情况下，重写应具有可访问性 `family`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-143">In this case, the override shall have accessibility `family`.</span></span> | <span data-ttu-id="8fc7a-144">10</span><span class="sxs-lookup"><span data-stu-id="8fc7a-144">10</span></span>
<span data-ttu-id="8fc7a-145">可访问性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-145">Accessibility</span></span> | [<span data-ttu-id="8fc7a-146">成员可访问性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-146">Member accessibility</span></span>](#member-accessibility) | <span data-ttu-id="8fc7a-147">类型和成员的可见性和可访问性应是这样的：只要任何成员是可见的且可访问的，则该成员签名中的类型应是可见且可访问的。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-147">The visibility and accessibility of types and members shall be such that types in the signature of any member shall be visible and accessible whenever the member itself is visible and accessible.</span></span> <span data-ttu-id="8fc7a-148">例如，在其程序集外部可见的公共方法不应具有其类型仅在程序集内可见的参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-148">For example, a public method that is visible outside its assembly shall not have an argument whose type is visible only within the assembly.</span></span> <span data-ttu-id="8fc7a-149">只要任何成员是可见且可访问的，则构成该成员签名中使用的实例化泛型类型的类型应是可见且可访问的。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-149">The visibility and accessibility of types composing an instantiated generic type used in the signature of any member shall be visible and accessible whenever the member itself is visible and accessible.</span></span> <span data-ttu-id="8fc7a-150">例如，一个在其程序集外部可见的成员签名中出现的实例化泛型类型不应具有其类型仅在程序集内可见的泛型实参。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-150">For example, an instantiated generic type present in the signature of a member that is visible outside its assembly shall not have a generic argument whose type is visible only within the assembly.</span></span> | <span data-ttu-id="8fc7a-151">12</span><span class="sxs-lookup"><span data-stu-id="8fc7a-151">12</span></span>
<span data-ttu-id="8fc7a-152">数组</span><span class="sxs-lookup"><span data-stu-id="8fc7a-152">Arrays</span></span> | [<span data-ttu-id="8fc7a-153">数组</span><span class="sxs-lookup"><span data-stu-id="8fc7a-153">Arrays</span></span>](#arrays) | <span data-ttu-id="8fc7a-154">数组应具有符合 CLS 的类型的元素，且数组的所有维度的下限应为零。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-154">Arrays shall have elements with a CLS-compliant type, and all dimensions of the array shall have lower bounds of zero.</span></span> <span data-ttu-id="8fc7a-155">各重载间只需区别：项是数组还是数组的元素类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-155">Only the fact that an item is an array and the element type of the array shall be required to distinguish between overloads.</span></span> <span data-ttu-id="8fc7a-156">当重载基于两个或更多数组类型时，元素类型应为命名类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-156">When overloading is based on two or more array types, the element types shall be named types.</span></span> | <span data-ttu-id="8fc7a-157">16</span><span class="sxs-lookup"><span data-stu-id="8fc7a-157">16</span></span>
<span data-ttu-id="8fc7a-158">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-158">Attributes</span></span> | [<span data-ttu-id="8fc7a-159">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-159">Attributes</span></span>](#attributes) | <span data-ttu-id="8fc7a-160">特性应为 [System.Attribute](xref:System.Attribute) 类型或继承自该类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-160">Attributes shall be of type [System.Attribute](xref:System.Attribute), or a type inheriting from it.</span></span> | <span data-ttu-id="8fc7a-161">41</span><span class="sxs-lookup"><span data-stu-id="8fc7a-161">41</span></span>
<span data-ttu-id="8fc7a-162">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-162">Attributes</span></span> | [<span data-ttu-id="8fc7a-163">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-163">Attributes</span></span>](#attributes) | <span data-ttu-id="8fc7a-164">CLS 只允许自定义特性编码的子集。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-164">The CLS only allows a subset of the encodings of custom attributes.</span></span> <span data-ttu-id="8fc7a-165">应在这些编码中出现的唯一类型是（请参阅第 IV 部分）：[System.Type](xref:System.Type)、[System.String](xref:System.String)、[System.Char](xref:System.Char)、[System.Boolean](xref:System.Boolean)、[System.Byte](xref:System.Byte)、[System.Int16](xref:System.Int16)、[System.Int32](xref:System.Int32)、[System.Int64](xref:System.Int64)、[System.Single](xref:System.Single)、[System.Double](xref:System.Double)，以及基于符合 CLS 的基整数类型的任何枚举类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-165">The only types that shall appear in these encodings are (see Partition IV): [System.Type](xref:System.Type), [System.String](xref:System.String), [System.Char](xref:System.Char), [System.Boolean](xref:System.Boolean), [System.Byte](xref:System.Byte), [System.Int16](xref:System.Int16), [System.Int32](xref:System.Int32), [System.Int64](xref:System.Int64), [System.Single](xref:System.Single), [System.Double](xref:System.Double), and any enumeration type based on a CLS-compliant base integer type.</span></span> | <span data-ttu-id="8fc7a-166">34</span><span class="sxs-lookup"><span data-stu-id="8fc7a-166">34</span></span>
<span data-ttu-id="8fc7a-167">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-167">Attributes</span></span> | [<span data-ttu-id="8fc7a-168">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-168">Attributes</span></span>](#attributes) | <span data-ttu-id="8fc7a-169">CLS 不允许公开可见的所需修饰符（`modreq`，请参阅第 II 部分)，但允许其不了解的可选修饰符（`modopt`，请参阅第 II 部分）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-169">The CLS does not allow publicly visible required modifiers (`modreq`, see Partition II), but does allow optional modifiers (`modopt`, see Partition II) it does not understand.</span></span> | <span data-ttu-id="8fc7a-170">35</span><span class="sxs-lookup"><span data-stu-id="8fc7a-170">35</span></span>
<span data-ttu-id="8fc7a-171">构造函数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-171">Constructors</span></span> | [<span data-ttu-id="8fc7a-172">构造函数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-172">Constructors</span></span>](#constructors) | <span data-ttu-id="8fc7a-173">在访问继承的实例数据之前，对象构造函数应调用其基类的某个实例构造函数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-173">An object constructor shall call some instance constructor of its base class before any access occurs to inherited instance data.</span></span> <span data-ttu-id="8fc7a-174">（这不适用于不需要构造函数的值类型。)</span><span class="sxs-lookup"><span data-stu-id="8fc7a-174">(This does not apply to value types, which need not have constructors.)</span></span>  | <span data-ttu-id="8fc7a-175">21</span><span class="sxs-lookup"><span data-stu-id="8fc7a-175">21</span></span>
<span data-ttu-id="8fc7a-176">构造函数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-176">Constructors</span></span> | [<span data-ttu-id="8fc7a-177">构造函数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-177">Constructors</span></span>](#constructors) | <span data-ttu-id="8fc7a-178">对象构造函数只能在创建对象的过程中调用，并且不应将对象初始化两次。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-178">An object constructor shall not be called except as part of the creation of an object, and an object shall not be initialized twice.</span></span> | <span data-ttu-id="8fc7a-179">22</span><span class="sxs-lookup"><span data-stu-id="8fc7a-179">22</span></span>
<span data-ttu-id="8fc7a-180">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-180">Enumerations</span></span> | [<span data-ttu-id="8fc7a-181">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-181">Enumerations</span></span>](#enumerations) | <span data-ttu-id="8fc7a-182">枚举的基础类型应是内置的 CLS 整数类型，字段的名称应为“value__”，并且应将该字段标记为 `RTSpecialName`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-182">The underlying type of an enum shall be a built-in CLS integer type, the name of the field shall be "value__", and that field shall be marked `RTSpecialName`.</span></span> |  <span data-ttu-id="8fc7a-183">7</span><span class="sxs-lookup"><span data-stu-id="8fc7a-183">7</span></span>
<span data-ttu-id="8fc7a-184">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-184">Enumerations</span></span> | [<span data-ttu-id="8fc7a-185">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-185">Enumerations</span></span>](#enumerations) | <span data-ttu-id="8fc7a-186">有两种不同的枚举，二者由是否存在 [System.FlagsAttribute](xref:System.FlagsAttribute)（请参阅第 IV 部分库）自定义特性指示。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-186">There are two distinct kinds of enums, indicated by the presence or absence of the [System.FlagsAttribute](xref:System.FlagsAttribute) (see Partition IV Library) custom attribute.</span></span> <span data-ttu-id="8fc7a-187">一个表示命名的整数值；另一个表示命名的位标记（可合并以生成一个未命名的值）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-187">One represents named integer values; the other represents named bit flags that can be combined to generate an unnamed value.</span></span> <span data-ttu-id="8fc7a-188">`enum` 的值不仅限于指定的值。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-188">The value of an `enum` is not limited to the specified values.</span></span> |  <span data-ttu-id="8fc7a-189">8</span><span class="sxs-lookup"><span data-stu-id="8fc7a-189">8</span></span>
<span data-ttu-id="8fc7a-190">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-190">Enumerations</span></span> | [<span data-ttu-id="8fc7a-191">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-191">Enumerations</span></span>](#enumerations) | <span data-ttu-id="8fc7a-192">枚举的文本静态字段需具有枚举本身的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-192">Literal static fields of an enum shall have the type of the enum itself.</span></span> |  <span data-ttu-id="8fc7a-193">9</span><span class="sxs-lookup"><span data-stu-id="8fc7a-193">9</span></span>
<span data-ttu-id="8fc7a-194">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-194">Events</span></span> | [<span data-ttu-id="8fc7a-195">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-195">Events</span></span>](#events) | <span data-ttu-id="8fc7a-196">实现事件的方法将在元数据中标记为 `SpecialName`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-196">The methods that implement an event shall be marked `SpecialName` in the metadata.</span></span> |<span data-ttu-id="8fc7a-197">29</span><span class="sxs-lookup"><span data-stu-id="8fc7a-197">29</span></span>
<span data-ttu-id="8fc7a-198">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-198">Events</span></span> | [<span data-ttu-id="8fc7a-199">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-199">Events</span></span>](#events) | <span data-ttu-id="8fc7a-200">事件及其访问器的可访问性应相同。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-200">The accessibility of an event and of its accessors shall be identical.</span></span> |<span data-ttu-id="8fc7a-201">30</span><span class="sxs-lookup"><span data-stu-id="8fc7a-201">30</span></span>
<span data-ttu-id="8fc7a-202">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-202">Events</span></span> | [<span data-ttu-id="8fc7a-203">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-203">Events</span></span>](#events) | <span data-ttu-id="8fc7a-204">事件的 `add` 和 `remove` 方法应同时存在或不存在。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-204">The `add` and `remove` methods for an event shall both either be present or absent.</span></span> |<span data-ttu-id="8fc7a-205">31</span><span class="sxs-lookup"><span data-stu-id="8fc7a-205">31</span></span>
<span data-ttu-id="8fc7a-206">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-206">Events</span></span> | [<span data-ttu-id="8fc7a-207">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-207">Events</span></span>](#events) | <span data-ttu-id="8fc7a-208">事件的 `add` 和 `remove` 方法均应采用一个参数，该参数的类型定义了事件的类型，且应派生自 [System.Delegate](xref:System.Delegate)。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-208">The `add` and `remove` methods for an event shall each take one parameter whose type defines the type of the event and that shall be derived from [System.Delegate](xref:System.Delegate).</span></span> |<span data-ttu-id="8fc7a-209">32</span><span class="sxs-lookup"><span data-stu-id="8fc7a-209">32</span></span>
<span data-ttu-id="8fc7a-210">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-210">Events</span></span> | [<span data-ttu-id="8fc7a-211">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-211">Events</span></span>](#events) | <span data-ttu-id="8fc7a-212">事件应遵循特定的命名模式。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-212">Events shall adhere to a specific naming pattern.</span></span> <span data-ttu-id="8fc7a-213">CLS 规则 29 中引用的 SpecialName 特性将在适当名称比较中被忽略，且应遵循标识符规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-213">The SpecialName attribute referred to in CLS rule 29 shall be ignored in appropriate name comparisons and shall adhere to identifier rules.</span></span>  |<span data-ttu-id="8fc7a-214">33</span><span class="sxs-lookup"><span data-stu-id="8fc7a-214">33</span></span>
<span data-ttu-id="8fc7a-215">异常</span><span class="sxs-lookup"><span data-stu-id="8fc7a-215">Exceptions</span></span> | [<span data-ttu-id="8fc7a-216">异常</span><span class="sxs-lookup"><span data-stu-id="8fc7a-216">Exceptions</span></span>](#exceptions) | <span data-ttu-id="8fc7a-217">引发的对象应为 [System.Exception](xref:System.Exception) 类型或从该类型继承的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-217">Objects that are thrown shall be of type [System.Exception](xref:System.Exception) or a type inheriting from it.</span></span> <span data-ttu-id="8fc7a-218">但是，阻止其他类型的异常的传播无需符合 CLS 的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-218">Nonetheless, CLS-compliant methods are not required to block the propagation of other types of exceptions.</span></span> | <span data-ttu-id="8fc7a-219">40</span><span class="sxs-lookup"><span data-stu-id="8fc7a-219">40</span></span>
<span data-ttu-id="8fc7a-220">常规</span><span class="sxs-lookup"><span data-stu-id="8fc7a-220">General</span></span> | [<span data-ttu-id="8fc7a-221">CLS 遵从性规则</span><span class="sxs-lookup"><span data-stu-id="8fc7a-221">CLS compliance rules</span></span>](#cls-compliance-rules) | <span data-ttu-id="8fc7a-222">CLS 规则仅适用于类型中在定义程序集之外可访问或可显示的部分。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-222">CLS rules apply only to those parts of a type that are accessible or visible outside of the defining assembly.</span></span> | <span data-ttu-id="8fc7a-223">1</span><span class="sxs-lookup"><span data-stu-id="8fc7a-223">1</span></span>
<span data-ttu-id="8fc7a-224">常规</span><span class="sxs-lookup"><span data-stu-id="8fc7a-224">General</span></span> | [<span data-ttu-id="8fc7a-225">CLS 遵从性规则</span><span class="sxs-lookup"><span data-stu-id="8fc7a-225">CLS compliance rules</span></span>](#cls-compliance-rules) | <span data-ttu-id="8fc7a-226">不应将不符合 CLS 的类型的成员标记为符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-226">Members of non-CLS compliant types shall not be marked CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-227">2</span><span class="sxs-lookup"><span data-stu-id="8fc7a-227">2</span></span>
<span data-ttu-id="8fc7a-228">泛型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-228">Generics</span></span> | [<span data-ttu-id="8fc7a-229">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-229">Generic types and members</span></span>](#generic-types-and-members) | <span data-ttu-id="8fc7a-230">嵌套类型拥有的泛型形参的数目至少应与封闭类型的一样多。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-230">Nested types shall have at least as many generic parameters as the enclosing type.</span></span> <span data-ttu-id="8fc7a-231">嵌套类型中的泛型参数在位置上与其封闭类型中的泛型参数对应。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-231">Generic parameters in a nested type correspond by position to the generic parameters in its enclosing type.</span></span>  | <span data-ttu-id="8fc7a-232">42</span><span class="sxs-lookup"><span data-stu-id="8fc7a-232">42</span></span>
<span data-ttu-id="8fc7a-233">泛型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-233">Generics</span></span> | [<span data-ttu-id="8fc7a-234">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-234">Generic types and members</span></span>](#generic-types-and-members) | <span data-ttu-id="8fc7a-235">根据上面定义的规则，泛型类型的名称将对非嵌套类型上声明的或新引入到类型（如果嵌套）中的类型参数的数量进行编码。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-235">The name of a generic type shall encode the number of type parameters declared on the non-nested type, or newly introduced to the type if nested, according to the rules defined above.</span></span> | <span data-ttu-id="8fc7a-236">43</span><span class="sxs-lookup"><span data-stu-id="8fc7a-236">43</span></span>
<span data-ttu-id="8fc7a-237">泛型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-237">Generics</span></span> | [<span data-ttu-id="8fc7a-238">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-238">Generic types and members</span></span>](#generic-types-and-members) | <span data-ttu-id="8fc7a-239">泛型类型应该重新声明足够多的约束，以确保对基类型或接口的任何约束能够满足泛型类型约束的需要。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-239">A generic type shall redeclare sufficient constraints to guarantee that any constraints on the base type, or interfaces would be satisfied by the generic type constraints.</span></span> | <span data-ttu-id="8fc7a-240">44</span><span class="sxs-lookup"><span data-stu-id="8fc7a-240">44</span></span>
<span data-ttu-id="8fc7a-241">泛型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-241">Generics</span></span> | [<span data-ttu-id="8fc7a-242">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-242">Generic types and members</span></span>](#generic-types-and-members) | <span data-ttu-id="8fc7a-243">用作对泛型参数的约束的类型本身应符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-243">Types used as constraints on generic parameters shall themselves be CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-244">45</span><span class="sxs-lookup"><span data-stu-id="8fc7a-244">45</span></span>
<span data-ttu-id="8fc7a-245">泛型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-245">Generics</span></span> | [<span data-ttu-id="8fc7a-246">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-246">Generic types and members</span></span>](#generic-types-and-members) | <span data-ttu-id="8fc7a-247">实例化泛型类型中的成员（包括嵌套类型）的可见性和可访问性应被认为限制在特定的实例化中，而不是限制在整个泛型类型声明中。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-247">The visibility and accessibility of members (including nested types) in an instantiated generic type shall be considered to be scoped to the specific instantiation rather than the generic type declaration as a whole.</span></span> <span data-ttu-id="8fc7a-248">作出以下假定：CLS 规则 12 的可见性和可访问性仍适用。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-248">Assuming this, the visibility and accessibility rules of CLS rule 12 still apply.</span></span> | <span data-ttu-id="8fc7a-249">46</span><span class="sxs-lookup"><span data-stu-id="8fc7a-249">46</span></span>
<span data-ttu-id="8fc7a-250">泛型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-250">Generics</span></span> | [<span data-ttu-id="8fc7a-251">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-251">Generic types and members</span></span>](#generic-types-and-members) | <span data-ttu-id="8fc7a-252">对于每个抽象或虚拟泛型方法，应该有默认的具体（非抽象）实现</span><span class="sxs-lookup"><span data-stu-id="8fc7a-252">For each abstract or virtual generic method, there shall be a default concrete (nonabstract) implementation</span></span> | <span data-ttu-id="8fc7a-253">47</span><span class="sxs-lookup"><span data-stu-id="8fc7a-253">47</span></span>
<span data-ttu-id="8fc7a-254">接口</span><span class="sxs-lookup"><span data-stu-id="8fc7a-254">Interfaces</span></span> | [<span data-ttu-id="8fc7a-255">接口</span><span class="sxs-lookup"><span data-stu-id="8fc7a-255">Interfaces</span></span>](#interfaces) | <span data-ttu-id="8fc7a-256">符合 CLS 的接口不需要不符合 CLS 的方法的定义即可实现这些方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-256">CLS-compliant interfaces shall not require the definition of non-CLS compliant methods in order to implement them.</span></span> | <span data-ttu-id="8fc7a-257">18</span><span class="sxs-lookup"><span data-stu-id="8fc7a-257">18</span></span>
<span data-ttu-id="8fc7a-258">接口</span><span class="sxs-lookup"><span data-stu-id="8fc7a-258">Interfaces</span></span> | [<span data-ttu-id="8fc7a-259">接口</span><span class="sxs-lookup"><span data-stu-id="8fc7a-259">Interfaces</span></span>](#interfaces) | <span data-ttu-id="8fc7a-260">符合 CLS 的接口不应定义静态方法，也不应定义字段。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-260">CLS-compliant interfaces shall not define static methods, nor shall they define fields.</span></span> | <span data-ttu-id="8fc7a-261">19</span><span class="sxs-lookup"><span data-stu-id="8fc7a-261">19</span></span>
<span data-ttu-id="8fc7a-262">成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-262">Members</span></span> | [<span data-ttu-id="8fc7a-263">类型成员概述</span><span class="sxs-lookup"><span data-stu-id="8fc7a-263">Type members in general</span></span>](#type-members-in-general) | <span data-ttu-id="8fc7a-264">全局静态字段和方法不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-264">Global static fields and methods are not CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-265">36</span><span class="sxs-lookup"><span data-stu-id="8fc7a-265">36</span></span>
<span data-ttu-id="8fc7a-266">成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-266">Members</span></span> | -- | <span data-ttu-id="8fc7a-267">通过使用字段初始化元数据指定文本静态值。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-267">The value of a literal static is specified through the use of field initialization metadata.</span></span> <span data-ttu-id="8fc7a-268">符合 CLS 的文本必须在类型与文本（或基本类型，如果文本为 `enum`）完全相同的字段初始化元数据中指定值。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-268">A CLS-compliant literal must have a value specified in field initialization metadata that is of exactly the same type as the literal (or of the underlying type, if that literal is an `enum`).</span></span> | <span data-ttu-id="8fc7a-269">13</span><span class="sxs-lookup"><span data-stu-id="8fc7a-269">13</span></span>
<span data-ttu-id="8fc7a-270">成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-270">Members</span></span> | [<span data-ttu-id="8fc7a-271">类型成员概述</span><span class="sxs-lookup"><span data-stu-id="8fc7a-271">Type members in general</span></span>](#type-members-in-general) | <span data-ttu-id="8fc7a-272">vararg 约束不属于 CLS，并且 CLS 支持的唯一调用约定是标准托管调用约定。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-272">The vararg constraint is not part of the CLS, and the only calling convention supported by the CLS is the standard managed calling convention.</span></span> | <span data-ttu-id="8fc7a-273">15</span><span class="sxs-lookup"><span data-stu-id="8fc7a-273">15</span></span>
<span data-ttu-id="8fc7a-274">命名约定</span><span class="sxs-lookup"><span data-stu-id="8fc7a-274">Naming conventions</span></span> | [<span data-ttu-id="8fc7a-275">命名约定</span><span class="sxs-lookup"><span data-stu-id="8fc7a-275">Naming conventions</span></span>](#naming-conventions) | <span data-ttu-id="8fc7a-276">程序集应遵守用于管理允许启用且包含在标识符中的字符集的 Unicode 标准 3.0 的技术报告 15 的附件 7（可通过 [Unicode 范式](https://unicode.org/reports/tr15/)在线获得）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-276">Assemblies shall follow Annex 7 of Technical Report 15 of the Unicode Standard3.0 governing the set of characters permitted to start and be included in identifiers, available online at [Unicode Normalization Forms](https://unicode.org/reports/tr15/).</span></span> <span data-ttu-id="8fc7a-277">标识符应是由 Unicode 范式 C 定义的规范格式。对于 CLS，如果两个标识符的小写映射（由不区分区域设置的 Unicode、一对一小写映射指定）相同，则它们也相同。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-277">Identifiers shall be in the canonical format defined by Unicode Normalization Form C. For CLS purposes, two identifiers are the same if their lowercase mappings (as specified by the Unicode locale-insensitive, one-to-one lowercase mappings) are the same.</span></span> <span data-ttu-id="8fc7a-278">也就是说，对于要在 CLS 下视为不同的两个标识符，它们应以大小写之外的差别进行区分。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-278">That is, for two identifiers to be considered different under the CLS they shall differ in more than simply their case.</span></span> <span data-ttu-id="8fc7a-279">但是，若要重写继承的定义，CLI 需要对使用的原始声明进行准确编码。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-279">However, in order to override an inherited definition the CLI requires the precise encoding of the original declaration be used.</span></span> | <span data-ttu-id="8fc7a-280">4</span><span class="sxs-lookup"><span data-stu-id="8fc7a-280">4</span></span>
<span data-ttu-id="8fc7a-281">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-281">Overloading</span></span> | [<span data-ttu-id="8fc7a-282">命名约定</span><span class="sxs-lookup"><span data-stu-id="8fc7a-282">Naming conventions</span></span>](#naming-conventions) | <span data-ttu-id="8fc7a-283">在符合 CLS 的范围中引入的所有名称都应是明显独立的类型，除非名称完全相同且通过重载解析。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-283">All names introduced in a CLS-compliant scope shall be distinct independent of kind, except where the names are identical and resolved via overloading.</span></span> <span data-ttu-id="8fc7a-284">也就是说，CTS 允许单个类型对方法和字段使用相同的名称，但 CLS 不允许。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-284">That is, while the CTS allows a single type to use the same name for a method and a field, the CLS does not.</span></span> | <span data-ttu-id="8fc7a-285">5</span><span class="sxs-lookup"><span data-stu-id="8fc7a-285">5</span></span>
<span data-ttu-id="8fc7a-286">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-286">Overloading</span></span> | [<span data-ttu-id="8fc7a-287">命名约定</span><span class="sxs-lookup"><span data-stu-id="8fc7a-287">Naming conventions</span></span>](#naming-conventions) | <span data-ttu-id="8fc7a-288">即使 CTS 允许区分不同的签名，但字段和嵌套类型只能由标识符比较区分。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-288">Fields and nested types shall be distinct by identifier comparison alone, even though the CTS allows distinct signatures to be distinguished.</span></span> <span data-ttu-id="8fc7a-289">（标识符比较后）具有相同名称的方法、属性和事件应在除返回类型不同之外还具有其他差异，CLS 规则 39 中指定的差异除外</span><span class="sxs-lookup"><span data-stu-id="8fc7a-289">Methods, properties, and events that have the same name (by identifier comparison) shall differ by more than just the return type, except as specified in CLS Rule 39</span></span> | <span data-ttu-id="8fc7a-290">6</span><span class="sxs-lookup"><span data-stu-id="8fc7a-290">6</span></span>
<span data-ttu-id="8fc7a-291">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-291">Overloading</span></span> | [<span data-ttu-id="8fc7a-292">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-292">Overloads</span></span>](#overloads) | <span data-ttu-id="8fc7a-293">只可重载属性和方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-293">Only properties and methods can be overloaded.</span></span> | <span data-ttu-id="8fc7a-294">37</span><span class="sxs-lookup"><span data-stu-id="8fc7a-294">37</span></span>
<span data-ttu-id="8fc7a-295">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-295">Overloading</span></span> | [<span data-ttu-id="8fc7a-296">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-296">Overloads</span></span>](#overloads) |<span data-ttu-id="8fc7a-297">属性和方法仅可基于其参数的数目和类型进行重载，名为 `op_Implicit` 和 `op_Explicit` 的转换运算符除外，这两种转换运算符也可基于其返回类型进行重载。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-297">Properties and methods can be overloaded based only on the number and types of their parameters, except the conversion operators named `op_Implicit` and `op_Explicit`, which can also be overloaded based on their return type.</span></span> | <span data-ttu-id="8fc7a-298">38</span><span class="sxs-lookup"><span data-stu-id="8fc7a-298">38</span></span>
<span data-ttu-id="8fc7a-299">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-299">Overloading</span></span> | -- | <span data-ttu-id="8fc7a-300">如果类型中声明的两种或更多符合 CLS 的方法都具有相同的名称，并且对于特定的类型实例化集而言，它们具有相同的参数和返回类型，则所有这些方法在这些类型实例化时都应在语义上保持等效。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-300">If two or more CLS-compliant methods declared in a type have the same name and, for a specific set of type instantiations, they have the same parameter and return types, then all these methods shall be semantically equivalent at those type instantiations.</span></span> | <span data-ttu-id="8fc7a-301">48</span><span class="sxs-lookup"><span data-stu-id="8fc7a-301">48</span></span>
<span data-ttu-id="8fc7a-302">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-302">Properties</span></span> | [<span data-ttu-id="8fc7a-303">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-303">Properties</span></span>](#properties) | <span data-ttu-id="8fc7a-304">实现属性的 getter 和 setter 方法的方法应在元数据中标记为 `SpecialName`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-304">The methods that implement the getter and setter methods of a property shall be marked `SpecialName` in the metadata.</span></span> | <span data-ttu-id="8fc7a-305">24</span><span class="sxs-lookup"><span data-stu-id="8fc7a-305">24</span></span>
<span data-ttu-id="8fc7a-306">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-306">Properties</span></span> | [<span data-ttu-id="8fc7a-307">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-307">Properties</span></span>](#properties) | <span data-ttu-id="8fc7a-308">属性的访问器必须同为静态、同为虚拟或同为实例。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-308">A property's accessors shall all be static, all be virtual, or all be instance.</span></span> | <span data-ttu-id="8fc7a-309">26</span><span class="sxs-lookup"><span data-stu-id="8fc7a-309">26</span></span>
<span data-ttu-id="8fc7a-310">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-310">Properties</span></span> | [<span data-ttu-id="8fc7a-311">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-311">Properties</span></span>](#properties) | <span data-ttu-id="8fc7a-312">属性的类型应该是 getter 的返回类型和 setter 的最后一个自变量的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-312">The type of a property shall be the return type of the getter and the type of the last argument of the setter.</span></span> <span data-ttu-id="8fc7a-313">属性参数的类型应是对应于 getter 的参数的类型和 setter 的除最后一个参数之外所有参数的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-313">The types of the parameters of the property shall be the types of the parameters to the getter and the types of all but the final parameter of the setter.</span></span> <span data-ttu-id="8fc7a-314">所有这些类型都应该符合 CLS，并且不应是托管指针（也就是说，不应该被引用传递）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-314">All of these types shall be CLS-compliant, and shall not be managed pointers (that is, shall not be passed by reference).</span></span> | <span data-ttu-id="8fc7a-315">27</span><span class="sxs-lookup"><span data-stu-id="8fc7a-315">27</span></span>
<span data-ttu-id="8fc7a-316">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-316">Properties</span></span> | [<span data-ttu-id="8fc7a-317">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-317">Properties</span></span>](#properties) | <span data-ttu-id="8fc7a-318">属性应遵循特定的命名模式。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-318">Properties shall adhere to a specific naming pattern.</span></span> <span data-ttu-id="8fc7a-319">CLS 规则 24 中引用的 `SpecialName` 特性将在适当名称比较中被忽略，且应遵循标识符规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-319">The `SpecialName` attribute referred to in CLS rule 24 shall be ignored in appropriate name comparisons and shall adhere to identifier rules.</span></span> <span data-ttu-id="8fc7a-320">属性应具有 getter 和/或 setter 方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-320">A property shall have a getter method, a setter method, or both.</span></span> | <span data-ttu-id="8fc7a-321">28</span><span class="sxs-lookup"><span data-stu-id="8fc7a-321">28</span></span>
<span data-ttu-id="8fc7a-322">类型转换</span><span class="sxs-lookup"><span data-stu-id="8fc7a-322">Type conversion</span></span> | [<span data-ttu-id="8fc7a-323">类型转换</span><span class="sxs-lookup"><span data-stu-id="8fc7a-323">Type conversion</span></span>](#type-conversion) | <span data-ttu-id="8fc7a-324">如果提供 op_Implicit 或 op_Explicit，则必须提供实现强制转换的替代方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-324">If either op_Implicit or op_Explicit is provided, an alternate means of providing the coercion shall be provided.</span></span> | <span data-ttu-id="8fc7a-325">39</span><span class="sxs-lookup"><span data-stu-id="8fc7a-325">39</span></span>
<span data-ttu-id="8fc7a-326">类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-326">Types</span></span> | [<span data-ttu-id="8fc7a-327">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-327">Types and type member signatures</span></span>](#types-and-type-member-signatures) | <span data-ttu-id="8fc7a-328">装箱的值类型不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-328">Boxed value types are not CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-329">3</span><span class="sxs-lookup"><span data-stu-id="8fc7a-329">3</span></span>
<span data-ttu-id="8fc7a-330">类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-330">Types</span></span> | [<span data-ttu-id="8fc7a-331">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-331">Types and type member signatures</span></span>](#types-and-type-member-signatures) | <span data-ttu-id="8fc7a-332">显示在签名中的所有类型应符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-332">All types appearing in a signature shall be CLS-compliant.</span></span> <span data-ttu-id="8fc7a-333">构成实例化泛型类型的所有类型应符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-333">All types composing an instantiated generic type shall be CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-334">11</span><span class="sxs-lookup"><span data-stu-id="8fc7a-334">11</span></span>
<span data-ttu-id="8fc7a-335">类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-335">Types</span></span> | [<span data-ttu-id="8fc7a-336">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-336">Types and type member signatures</span></span>](#types-and-type-member-signatures) | <span data-ttu-id="8fc7a-337">类型化的引用是不符合 CLS 的。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-337">Typed references are not CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-338">14</span><span class="sxs-lookup"><span data-stu-id="8fc7a-338">14</span></span>
<span data-ttu-id="8fc7a-339">类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-339">Types</span></span> | [<span data-ttu-id="8fc7a-340">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-340">Types and type member signatures</span></span>](#types-and-type-member-signatures) | <span data-ttu-id="8fc7a-341">非托管的指针类型不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-341">Unmanaged pointer types are not CLS-compliant.</span></span> | <span data-ttu-id="8fc7a-342">17</span><span class="sxs-lookup"><span data-stu-id="8fc7a-342">17</span></span>
<span data-ttu-id="8fc7a-343">类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-343">Types</span></span> | [<span data-ttu-id="8fc7a-344">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-344">Types and type member signatures</span></span>](#types-and-type-member-signatures) | <span data-ttu-id="8fc7a-345">符合 CLS 的类、值类型和接口不应要求实现不符合 CLS 的成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-345">CLS-compliant classes, value types, and interfaces shall not require the implementation of non-CLS-compliant members</span></span> | <span data-ttu-id="8fc7a-346">20</span><span class="sxs-lookup"><span data-stu-id="8fc7a-346">20</span></span>
<span data-ttu-id="8fc7a-347">类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-347">Types</span></span> | [<span data-ttu-id="8fc7a-348">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-348">Types and type member signatures</span></span>](#types-and-type-member-signatures) | <span data-ttu-id="8fc7a-349">[System.Object](xref:System.Object) 符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-349">[System.Object](xref:System.Object) is CLS-compliant.</span></span> <span data-ttu-id="8fc7a-350">任何其他符合 CLS 的类应从符合 CLS 的类继承。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-350">Any other CLS-compliant class shall inherit from a CLS-compliant class.</span></span> | <span data-ttu-id="8fc7a-351">23</span><span class="sxs-lookup"><span data-stu-id="8fc7a-351">23</span></span>

<span data-ttu-id="8fc7a-352">索引到各个子部分：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-352">Index to subsections:</span></span>

* [<span data-ttu-id="8fc7a-353">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-353">Types and type member signatures</span></span>](#types-and-type-member-signatures)
* [<span data-ttu-id="8fc7a-354">命名约定</span><span class="sxs-lookup"><span data-stu-id="8fc7a-354">Naming conventions</span></span>](#naming-conventions)
* [<span data-ttu-id="8fc7a-355">类型转换</span><span class="sxs-lookup"><span data-stu-id="8fc7a-355">Type conversion</span></span>](#type-conversion)
* [<span data-ttu-id="8fc7a-356">数组</span><span class="sxs-lookup"><span data-stu-id="8fc7a-356">Arrays</span></span>](#arrays)
* [<span data-ttu-id="8fc7a-357">接口</span><span class="sxs-lookup"><span data-stu-id="8fc7a-357">Interfaces</span></span>](#interfaces)
* [<span data-ttu-id="8fc7a-358">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-358">Enumerations</span></span>](#enumerations)
* [<span data-ttu-id="8fc7a-359">类型成员概述</span><span class="sxs-lookup"><span data-stu-id="8fc7a-359">Type members in general</span></span>](#type-members-in-general)
* [<span data-ttu-id="8fc7a-360">成员可访问性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-360">Member accessibility</span></span>](#member-accessibility)
* [<span data-ttu-id="8fc7a-361">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-361">Generic types and members</span></span>](#generic-types-and-members)
* [<span data-ttu-id="8fc7a-362">构造函数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-362">Constructors</span></span>](#constructors)
* [<span data-ttu-id="8fc7a-363">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-363">Properties</span></span>](#properties)
* [<span data-ttu-id="8fc7a-364">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-364">Events</span></span>](#events)
* [<span data-ttu-id="8fc7a-365">重载</span><span class="sxs-lookup"><span data-stu-id="8fc7a-365">Overloads</span></span>](#overloads)
* [<span data-ttu-id="8fc7a-366">异常</span><span class="sxs-lookup"><span data-stu-id="8fc7a-366">Exceptions</span></span>](#exceptions)
* [<span data-ttu-id="8fc7a-367">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-367">Attributes</span></span>](#attributes)

### <a name="types-and-type-member-signatures"></a><span data-ttu-id="8fc7a-368">类型和类型成员签名</span><span class="sxs-lookup"><span data-stu-id="8fc7a-368">Types and type member signatures</span></span>

<span data-ttu-id="8fc7a-369">[System.Object](xref:System.Object) 类型符合 CLS，是 .NET 类型系统中所有对象类型的基础类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-369">The [System.Object](xref:System.Object) type is CLS-compliant and is the base type of all object types in the .NET type system.</span></span> <span data-ttu-id="8fc7a-370">.NET 中的继承要么是隐式的（例如，[String](xref:System.String) 类从 `Object` 类隐式继承），要么是显式的（例如，[CultureNotFoundException](xref:System.Globalization.CultureNotFoundException) 类从 [ArgumentException](xref:System.ArgumentException) 类显式继承，后者又从 [Exception](xref:System.Exception) 类显式继承。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-370">Inheritance in .NET is either implicit (for example, the [String](xref:System.String) class implicitly inherits from the `Object` class) or explicit (for example, the [CultureNotFoundException](xref:System.Globalization.CultureNotFoundException) class explicitly inherits from the [ArgumentException](xref:System.ArgumentException) class, which explicitly inherits from the [Exception](xref:System.Exception) class.</span></span> <span data-ttu-id="8fc7a-371">对于要符合 CLS 的派生类型，其基本类型也必须符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-371">For a derived type to be CLS compliant, its base type must also be CLS-compliant.</span></span>

<span data-ttu-id="8fc7a-372">下面的示例显示基本类型不符合 CLS 的派生类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-372">The following example shows a derived type whose base type is not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-373">它定义使用无符号 32 位整数作为计数器的基本 `Counter` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-373">It defines a base `Counter` class that uses an unsigned 32-bit integer as a counter.</span></span> <span data-ttu-id="8fc7a-374">由于类通过对无符号整数进行换行来提供计数器功能，因此类标记为不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-374">Because the class provides counter functionality by wrapping an unsigned integer, the class is marked as non-CLS-compliant.</span></span> <span data-ttu-id="8fc7a-375">因此，派生类 `NonZeroCounter` 也不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-375">As a result, a derived class, `NonZeroCounter`, is also not CLS-compliant.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

[CLSCompliant(false)]
public class Counter
{
   UInt32 ctr;

   public Counter()
   {
      ctr = 0;
   }

   protected Counter(UInt32 ctr)
   {
      this.ctr = ctr;
   }

   public override string ToString()
   {
      return $"{ctr}). ";
   }

   public UInt32 Value
   {
      get { return ctr; }
   }

   public void Increment()
   {
      ctr += (uint) 1;
   }
}

public class NonZeroCounter : Counter
{
   public NonZeroCounter(int startIndex) : this((uint) startIndex)
   {
   }

   private NonZeroCounter(UInt32 startIndex) : base(startIndex)
   {
   }
}
// Compilation produces a compiler warning like the following:
//    Type3.cs(37,14): warning CS3009: 'NonZeroCounter': base type 'Counter' is not
//            CLS-compliant
//    Type3.cs(7,14): (Location of symbol related to previous warning)
```

```vb
<Assembly: CLSCompliant(True)>

<CLSCompliant(False)> _
Public Class Counter
   Dim ctr As UInt32

   Public Sub New
      ctr = 0
   End Sub

   Protected Sub New(ctr As UInt32)
      ctr = ctr
   End Sub

   Public Overrides Function ToString() As String
      Return $"{ctr}). "
   End Function

   Public ReadOnly Property Value As UInt32
      Get
         Return ctr
      End Get
   End Property

   Public Sub Increment()
      ctr += CType(1, UInt32)
   End Sub
End Class

Public Class NonZeroCounter : Inherits Counter
   Public Sub New(startIndex As Integer)
      MyClass.New(CType(startIndex, UInt32))
   End Sub

   Private Sub New(startIndex As UInt32)
      MyBase.New(CType(startIndex, UInt32))
   End Sub
End Class
' Compilation produces a compiler warning like the following:
'    Type3.vb(34) : warning BC40026: 'NonZeroCounter' is not CLS-compliant
'    because it derives from 'Counter', which is not CLS-compliant.
'
'    Public Class NonZeroCounter : Inherits Counter
'                 ~~~~~~~~~~~~~~
```

<span data-ttu-id="8fc7a-376">成员签名中出现的所有类型（包括方法的返回类型或属性类型）必须符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-376">All types that appear in member signatures, including a method's return type or a property type, must be CLS-compliant.</span></span> <span data-ttu-id="8fc7a-377">此外，对于泛型类型：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-377">In addition, for generic types:</span></span>

* <span data-ttu-id="8fc7a-378">构成实例化泛型类型的所有类型必须符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-378">All types that compose an instantiated generic type must be CLS-compliant.</span></span>

* <span data-ttu-id="8fc7a-379">所有用作针对泛型参数的约束的类型必须符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-379">All types used as constraints on generic parameters must be CLS-compliant.</span></span>

<span data-ttu-id="8fc7a-380">.NET [通用类型系统](common-type-system.md)包括大量直接受公共语言运行时支持且专以程序集的元数据编码的内置类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-380">The .NET [common type system](common-type-system.md) includes a number of built-in types that are supported directly by the common language runtime and are specially encoded in an assembly's metadata.</span></span> <span data-ttu-id="8fc7a-381">在这些内部类型中，下表中所列的类型都符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-381">Of these intrinsic types, the types listed in the following table are CLS-compliant.</span></span>

<span data-ttu-id="8fc7a-382">符合 CLS 的类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-382">CLS-compliant type</span></span> | <span data-ttu-id="8fc7a-383">描述</span><span class="sxs-lookup"><span data-stu-id="8fc7a-383">Description</span></span>
------------------ | -----------
[<span data-ttu-id="8fc7a-384">Byte</span><span class="sxs-lookup"><span data-stu-id="8fc7a-384">Byte</span></span>](xref:System.Byte) | <span data-ttu-id="8fc7a-385">8 位无符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-385">8-bit unsigned integer</span></span>
[<span data-ttu-id="8fc7a-386">Int16</span><span class="sxs-lookup"><span data-stu-id="8fc7a-386">Int16</span></span>](xref:System.Int16) | <span data-ttu-id="8fc7a-387">16 位带符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-387">16-bit signed integer</span></span>
[<span data-ttu-id="8fc7a-388">Int32</span><span class="sxs-lookup"><span data-stu-id="8fc7a-388">Int32</span></span>](xref:System.Int32) | <span data-ttu-id="8fc7a-389">32 位带符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-389">32-bit signed integer</span></span>
[<span data-ttu-id="8fc7a-390">Int64</span><span class="sxs-lookup"><span data-stu-id="8fc7a-390">Int64</span></span>](xref:System.Int64) | <span data-ttu-id="8fc7a-391">64 位带符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-391">64-bit signed integer</span></span>
[<span data-ttu-id="8fc7a-392">单精度</span><span class="sxs-lookup"><span data-stu-id="8fc7a-392">Single</span></span>](xref:System.Single) | <span data-ttu-id="8fc7a-393">单精度浮点值</span><span class="sxs-lookup"><span data-stu-id="8fc7a-393">Single-precision floating-point value</span></span>
[<span data-ttu-id="8fc7a-394">双精度</span><span class="sxs-lookup"><span data-stu-id="8fc7a-394">Double</span></span>](xref:System.Double) | <span data-ttu-id="8fc7a-395">双精度浮点值</span><span class="sxs-lookup"><span data-stu-id="8fc7a-395">Double-precision floating-point value</span></span>
[<span data-ttu-id="8fc7a-396">布尔值</span><span class="sxs-lookup"><span data-stu-id="8fc7a-396">Boolean</span></span>](xref:System.Boolean) | <span data-ttu-id="8fc7a-397">true 或 false 值类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-397">true or false value type</span></span>
[<span data-ttu-id="8fc7a-398">Char</span><span class="sxs-lookup"><span data-stu-id="8fc7a-398">Char</span></span>](xref:System.Char) | <span data-ttu-id="8fc7a-399">UTF 16 编码单元</span><span class="sxs-lookup"><span data-stu-id="8fc7a-399">UTF-16 encoded code unit</span></span>
[<span data-ttu-id="8fc7a-400">小数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-400">Decimal</span></span>](xref:System.Decimal) | <span data-ttu-id="8fc7a-401">非浮点十进制数字</span><span class="sxs-lookup"><span data-stu-id="8fc7a-401">Non-floating-point decimal number</span></span>
[<span data-ttu-id="8fc7a-402">IntPtr</span><span class="sxs-lookup"><span data-stu-id="8fc7a-402">IntPtr</span></span>](xref:System.IntPtr) | <span data-ttu-id="8fc7a-403">平台定义的大小的指针或句柄</span><span class="sxs-lookup"><span data-stu-id="8fc7a-403">Pointer or handle of a platform-defined size</span></span>
[<span data-ttu-id="8fc7a-404">字符串</span><span class="sxs-lookup"><span data-stu-id="8fc7a-404">String</span></span>](xref:System.String) | <span data-ttu-id="8fc7a-405">零个、一个或多个 Char 对象的集合</span><span class="sxs-lookup"><span data-stu-id="8fc7a-405">Collection of zero, one, or more Char objects</span></span>

<span data-ttu-id="8fc7a-406">下表中所列的内部类型不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-406">The intrinsic types listed in the following table are not CLS-Compliant.</span></span>

<span data-ttu-id="8fc7a-407">不符合类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-407">Non-compliant type</span></span> | <span data-ttu-id="8fc7a-408">描述</span><span class="sxs-lookup"><span data-stu-id="8fc7a-408">Description</span></span> | <span data-ttu-id="8fc7a-409">符合 CLS 的替代方法</span><span class="sxs-lookup"><span data-stu-id="8fc7a-409">CLS-compliant alternative</span></span>
------------------ | ----------- | -------------------------
[<span data-ttu-id="8fc7a-410">SByte</span><span class="sxs-lookup"><span data-stu-id="8fc7a-410">SByte</span></span>](xref:System.SByte) | <span data-ttu-id="8fc7a-411">8 位带符号整数数据类型</span><span class="sxs-lookup"><span data-stu-id="8fc7a-411">8-bit signed integer data type</span></span> | [<span data-ttu-id="8fc7a-412">Int16</span><span class="sxs-lookup"><span data-stu-id="8fc7a-412">Int16</span></span>](xref:System.Int16)
[<span data-ttu-id="8fc7a-413">UInt16</span><span class="sxs-lookup"><span data-stu-id="8fc7a-413">UInt16</span></span>](xref:System.UInt16) | <span data-ttu-id="8fc7a-414">16 位无符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-414">16-bit unsigned integer</span></span> | [<span data-ttu-id="8fc7a-415">Int32</span><span class="sxs-lookup"><span data-stu-id="8fc7a-415">Int32</span></span>](xref:System.Int32)
[<span data-ttu-id="8fc7a-416">UInt32</span><span class="sxs-lookup"><span data-stu-id="8fc7a-416">UInt32</span></span>](xref:System.UInt32) | <span data-ttu-id="8fc7a-417">32 位无符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-417">32-bit unsigned integer</span></span> | [<span data-ttu-id="8fc7a-418">Int64</span><span class="sxs-lookup"><span data-stu-id="8fc7a-418">Int64</span></span>](xref:System.Int64)
[<span data-ttu-id="8fc7a-419">UInt64</span><span class="sxs-lookup"><span data-stu-id="8fc7a-419">UInt64</span></span>](xref:System.UInt64) | <span data-ttu-id="8fc7a-420">64 位无符号整数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-420">64-bit unsigned integer</span></span> | <span data-ttu-id="8fc7a-421">[Int64](xref:System.Int64)（可能溢出）、[BigInteger](xref:System.Numerics.BigInteger) 或 [Double](xref:System.Double)</span><span class="sxs-lookup"><span data-stu-id="8fc7a-421">[Int64](xref:System.Int64) (may overflow), [BigInteger](xref:System.Numerics.BigInteger), or [Double](xref:System.Double)</span></span>
[<span data-ttu-id="8fc7a-422">UIntPtr</span><span class="sxs-lookup"><span data-stu-id="8fc7a-422">UIntPtr</span></span>](xref:System.UIntPtr) | <span data-ttu-id="8fc7a-423">未签名的指针或句柄</span><span class="sxs-lookup"><span data-stu-id="8fc7a-423">Unsigned pointer or handle</span></span> | [<span data-ttu-id="8fc7a-424">IntPtr</span><span class="sxs-lookup"><span data-stu-id="8fc7a-424">IntPtr</span></span>](xref:System.IntPtr)

<span data-ttu-id="8fc7a-425">.NET 类库或任何其他类库可能包含不符合 CLS 的其他类型；例如：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-425">The .NET Class Library or any other class library may include other types that aren't CLS-compliant; for example:</span></span>

* <span data-ttu-id="8fc7a-426">装箱的值类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-426">Boxed value types.</span></span> <span data-ttu-id="8fc7a-427">下面的 C# 示例创建一个具有名为 `int*` 的 `Value` 类型的公共属性的类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-427">The following C# example creates a class that has a public property of type `int*` named `Value`.</span></span> <span data-ttu-id="8fc7a-428">由于 `int*` 是一个装箱的值类型，因此编译器将其标记为不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-428">Because an `int*` is a boxed value type, the compiler flags it as non-CLS-compliant.</span></span>

```csharp
using System;

[assembly:CLSCompliant(true)]

public unsafe class TestClass
{
   private int* val;

   public TestClass(int number)
   {
      val = (int*) number;
   }

   public int* Value {
      get { return val; }
   }
}
// The compiler generates the following output when compiling this example:
//        warning CS3003: Type of 'TestClass.Value' is not CLS-compliant
```

* <span data-ttu-id="8fc7a-429">类型化的引用是一个特殊构造，它包含一个对对象的引用和一个对类型的引用。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-429">Typed references, which are special constructs that contain a reference to an object and a reference to a type.</span></span>

<span data-ttu-id="8fc7a-430">如果类型不符合 CLS，则需对其应用 *isCompliant* 值为 `false` 的 [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-430">If a type is not CLS-compliant, you should apply the [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) attribute with an *isCompliant* parameter with a value of `false` to it.</span></span> <span data-ttu-id="8fc7a-431">有关详细信息，请参阅 [CLSCompliantAttribute 特性](#the-clscompliantattribute-attribute)部分。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-431">For more information, see the [CLSCompliantAttribute attribute](#the-clscompliantattribute-attribute) section.</span></span>

<span data-ttu-id="8fc7a-432">下面的示例说明了方法签名和泛型类型实例化中 CLS 遵从性的问题。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-432">The following example illustrates the problem of CLS compliance in a method signature and in generic type instantiation.</span></span> <span data-ttu-id="8fc7a-433">它定义一个具有类型为 [UInt32](xref:System.UInt32) 的属性和类型为 [Nullable(Of UInt32)](xref:System.Nullable%601) 的属性的 `InvoiceItem` 类，以及一个具有类型为 `UInt32` 和 `Nullable(Of UInt32)` 的参数的构造函数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-433">It defines an `InvoiceItem` class with a property of type [UInt32](xref:System.UInt32), a property of type [Nullable(Of UInt32)](xref:System.Nullable%601), and a constructor with parameters of type `UInt32` and `Nullable(Of UInt32)`.</span></span> <span data-ttu-id="8fc7a-434">您尝试编译此示例时会收到四个编译器警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-434">You get four compiler warnings when you try to compile this example.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class InvoiceItem
{
   private uint invId = 0;
   private uint itemId = 0;
   private Nullable<uint> qty;

   public InvoiceItem(uint sku, Nullable<uint> quantity)
   {
      itemId = sku;
      qty = quantity;
   }

   public Nullable<uint> Quantity
   {
      get { return qty; }
      set { qty = value; }
   }

   public uint InvoiceId
   {
      get { return invId; }
      set { invId = value; }
   }
}
// The attempt to compile the example displays the following output:
//    Type1.cs(13,23): warning CS3001: Argument type 'uint' is not CLS-compliant
//    Type1.cs(13,33): warning CS3001: Argument type 'uint?' is not CLS-compliant
//    Type1.cs(19,26): warning CS3003: Type of 'InvoiceItem.Quantity' is not CLS-compliant
//    Type1.cs(25,16): warning CS3003: Type of 'InvoiceItem.InvoiceId' is not CLS-compliant
```

```vb
<Assembly: CLSCompliant(True)>

Public Class InvoiceItem

   Private invId As UInteger = 0
   Private itemId As UInteger = 0
   Private qty AS Nullable(Of UInteger)

   Public Sub New(sku As UInteger, quantity As Nullable(Of UInteger))
      itemId = sku
      qty = quantity
   End Sub

   Public Property Quantity As Nullable(Of UInteger)
      Get
         Return qty
      End Get
      Set
         qty = value
      End Set
   End Property

   Public Property InvoiceId As UInteger
      Get
         Return invId
      End Get
      Set
         invId = value
      End Set
   End Property
End Class
' The attempt to compile the example displays output similar to the following:
'    Type1.vb(13) : warning BC40028: Type of parameter 'sku' is not CLS-compliant.
'
'       Public Sub New(sku As UInteger, quantity As Nullable(Of UInteger))
'                      ~~~
'    Type1.vb(13) : warning BC40041: Type 'UInteger' is not CLS-compliant.
'
'       Public Sub New(sku As UInteger, quantity As Nullable(Of UInteger))
'                                                               ~~~~~~~~
'    Type1.vb(18) : warning BC40041: Type 'UInteger' is not CLS-compliant.
'
'       Public Property Quantity As Nullable(Of UInteger)
'                                               ~~~~~~~~
'    Type1.vb(27) : warning BC40027: Return type of function 'InvoiceId' is not CLS-compliant.
'
'       Public Property InvoiceId As UInteger
```

<span data-ttu-id="8fc7a-435">若要消除编译器警告，请将 `InvoiceItem` 公共接口中不符合 CLS 的类型替换为符合 CLS 的类型：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-435">To eliminate the compiler warnings, replace the non-CLS-compliant types in the `InvoiceItem` public interface with compliant types:</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class InvoiceItem
{
   private uint invId = 0;
   private uint itemId = 0;
   private Nullable<int> qty;

   public InvoiceItem(int sku, Nullable<int> quantity)
   {
      if (sku <= 0)
         throw new ArgumentOutOfRangeException("The item number is zero or negative.");
      itemId = (uint) sku;

      qty = quantity;
   }

   public Nullable<int> Quantity
   {
      get { return qty; }
      set { qty = value; }
   }

   public int InvoiceId
   {
      get { return (int) invId; }
      set {
         if (value <= 0)
            throw new ArgumentOutOfRangeException("The invoice number is zero or negative.");
         invId = (uint) value; }
   }
}
```

```vb
Assembly: CLSCompliant(True)>

Public Class InvoiceItem

   Private invId As UInteger = 0
   Private itemId As UInteger = 0
   Private qty AS Nullable(Of Integer)

   Public Sub New(sku As Integer, quantity As Nullable(Of Integer))
      If sku <= 0 Then
         Throw New ArgumentOutOfRangeException("The item number is zero or negative.")
      End If
      itemId = CUInt(sku)
      qty = quantity
   End Sub

   Public Property Quantity As Nullable(Of Integer)
      Get
         Return qty
      End Get
      Set
         qty = value
      End Set
   End Property

   Public Property InvoiceId As Integer
      Get
         Return CInt(invId)
      End Get
      Set
         invId = CUInt(value)
      End Set
   End Property
End Class
```

<span data-ttu-id="8fc7a-436">除了列出的特定类型之外，某些类型的类别也不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-436">In addition to the specific types listed, some categories of types are not CLS compliant.</span></span> <span data-ttu-id="8fc7a-437">其中包括非托管指针类型和函数指针类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-437">These include unmanaged pointer types and function pointer types.</span></span> <span data-ttu-id="8fc7a-438">下面的示例将生成一个编译器警告，因为它使用指向整数的指针来创建整数数组。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-438">The following example generates a compiler warning because it uses a pointer to an integer to create an array of integers.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ArrayHelper
{
   unsafe public static Array CreateInstance(Type type, int* ptr, int items)
   {
      Array arr = Array.CreateInstance(type, items);
      int* addr = ptr;
      for (int ctr = 0; ctr < items; ctr++) {
          int value = *addr;
          arr.SetValue(value, ctr);
          addr++;
      }
      return arr;
   }
}
// The attempt to compile this example displays the following output:
//    UnmanagedPtr1.cs(8,57): warning CS3001: Argument type 'int*' is not CLS-compliant
```

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ArrayHelper
{
   unsafe public static Array CreateInstance(Type type, int* ptr, int items)
   {
      Array arr = Array.CreateInstance(type, items);
      int* addr = ptr;
      for (int ctr = 0; ctr < items; ctr++) {
          int value = *addr;
          arr.SetValue(value, ctr);
          addr++;
      }
      return arr;
   }
}
// The attempt to compile this example displays the following output:
//    UnmanagedPtr1.cs(8,57): warning CS3001: Argument type 'int*' is not CLS-compliant
```

<span data-ttu-id="8fc7a-439">对于符合 CLS 的抽象类（即在 C# 中标记为 `abstract` 的类），该类的所有成员也必须符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-439">For CLS-compliant abstract classes (that is, classes marked as `abstract` in C#), all members of the class must also be CLS-compliant.</span></span>

### <a name="naming-conventions"></a><span data-ttu-id="8fc7a-440">命名约定</span><span class="sxs-lookup"><span data-stu-id="8fc7a-440">Naming conventions</span></span>

<span data-ttu-id="8fc7a-441">由于一些编程语言不区分大小写，因此标识符（例如，命名空间、类型和成员的名称）必须不仅限于大小写不同。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-441">Because some programming languages are case-insensitive, identifiers (such as the names of namespaces, types, and members) must differ by more than case.</span></span> <span data-ttu-id="8fc7a-442">如果两个标识符的小写映射是相同的，则这两个标识符被视为等效。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-442">Two identifiers are considered equivalent if their lowercase mappings are the same.</span></span> <span data-ttu-id="8fc7a-443">下面的 C# 示例定义两个公共类：`Person` 和 `person`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-443">The following C# example defines two public classes, `Person` and `person`.</span></span> <span data-ttu-id="8fc7a-444">由于它们只是大小写不同，因此 C# 编译器会将其标记为不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-444">Because they differ only by case, the C# compiler flags them as not CLS-compliant.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Person : person
{

}

public class person
{

}
// Compilation produces a compiler warning like the following:
//    Naming1.cs(11,14): warning CS3005: Identifier 'person' differing
//                       only in case is not CLS-compliant
//    Naming1.cs(6,14): (Location of symbol related to previous warning)
```

<span data-ttu-id="8fc7a-445">编程语言标识符（例如，命名空间、类型和成员的名称）必须遵照 [Unicode 标准](https://unicode.org/reports/tr15/)。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-445">Programming language identifiers, such as the names of namespaces, types, and members, must conform to the [Unicode Standard](https://unicode.org/reports/tr15/).</span></span> <span data-ttu-id="8fc7a-446">这表示：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-446">This means that:</span></span>

* <span data-ttu-id="8fc7a-447">标识符的第一个字符可以是任何 Unicode 大写字母、小写字母、标题大小写字母、修饰符字母、其他字母或字母数字。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-447">The first character of an identifier can be any Unicode uppercase letter, lowercase letter, title case letter, modifier letter, other letter, or letter number.</span></span> <span data-ttu-id="8fc7a-448">有关 Unicode 字符类别的信息，请参阅 [System.Globalization.UnicodeCategory](xref:System.Globalization.UnicodeCategory) 枚举。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-448">For information on Unicode character categories, see the [System.Globalization.UnicodeCategory](xref:System.Globalization.UnicodeCategory) enumeration.</span></span>

* <span data-ttu-id="8fc7a-449">后继字符可以是任何类别的第一个字符，还可以包含无间隔标记、间距组合标记、十进制数字、连接器标点符号以及格式设置代码。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-449">Subsequent characters can be from any of the categories as the first character, and can also include non-spacing marks, spacing combining marks, decimal numbers, connector punctuation, and formatting codes.</span></span>

<span data-ttu-id="8fc7a-450">在比较标识符之前，应筛选格式设置代码，并将标识符转换为 Unicode 范式 C，因为单个字符可由多个 UTF 16 编码的代码单位表示。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-450">Before you compare identifiers, you should filter out formatting codes and convert the identifiers to Unicode Normalization Form C, because a single character can be represented by multiple UTF-16-encoded code units.</span></span> <span data-ttu-id="8fc7a-451">在 Unicode 范式 C 中生成相同代码单位的字符序列不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-451">Character sequences that produce the same code units in Unicode Normalization Form C are not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-452">下列示例定义了一个名为 `Å` 的属性（包含字符 ANGSTROM SIGN (U+212B)）和另一个名为 `Å` 的属性（包含字符 LATIN CAPITAL LETTER A WITH RING ABOVE (U+00C5)）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-452">The following example defines a property named `Å`, which consists of the character ANGSTROM SIGN (U+212B), and a second property named `Å`, which consists of the character LATIN CAPITAL LETTER A WITH RING ABOVE (U+00C5).</span></span> <span data-ttu-id="8fc7a-453">C# 编译器将源代码标记为不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-453">The C# compiler flags the source code as non-CLS-compliant.</span></span>

```csharp
public class Size
{
   private double a1;
   private double a2;

   public double Å
   {
       get { return a1; }
       set { a1 = value; }
   }

   public double Å
   {
       get { return a2; }
       set { a2 = value; }
   }
}
// Compilation produces a compiler warning like the following:
//    Naming2a.cs(16,18): warning CS3005: Identifier 'Size.Å' differing only in case is not
//            CLS-compliant
//    Naming2a.cs(10,18): (Location of symbol related to previous warning)
//    Naming2a.cs(18,8): warning CS3005: Identifier 'Size.Å.get' differing only in case is not
//            CLS-compliant
//    Naming2a.cs(12,8): (Location of symbol related to previous warning)
//    Naming2a.cs(19,8): warning CS3005: Identifier 'Size.Å.set' differing only in case is not
//            CLS-compliant
//    Naming2a.cs(13,8): (Location of symbol related to previous warning)
```

```vb
<Assembly: CLSCompliant(True)>
Public Class Size
   Private a1 As Double
   Private a2 As Double

   Public Property Å As Double
       Get
          Return a1
       End Get
       Set
          a1 = value
       End Set
   End Property

   Public Property Å As Double
       Get
          Return a2
       End Get
       Set
          a2 = value
       End Set
   End Property
End Class
' Compilation produces a compiler warning like the following:
'    Naming1.vb(9) : error BC30269: 'Public Property Å As Double' has multiple definitions
'     with identical signatures.
'
'       Public Property Å As Double
'                       ~
```

<span data-ttu-id="8fc7a-454">特定范围内的成员名称（如程序集中的命名空间、命名空间中的类型或某类型中的成员）必须是唯一的，通过重载解析的名称除外。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-454">Member names within a particular scope (such as the namespaces within an assembly, the types within a namespace, or the members within a type) must be unique except for names that are resolved through overloading.</span></span> <span data-ttu-id="8fc7a-455">此要求比常规类型系统的要求更加严格，后者允许一个范围内的多个成员在作为不同类型的成员（例如，一个是方法，一个是字段时）时，可以具有相同的名称。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-455">This requirement is more stringent than that of the common type system, which allows multiple members within a scope to have identical names as long as they are different kinds of members (for example, one is a method and one is a field).</span></span> <span data-ttu-id="8fc7a-456">具体而言，对于类型成员：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-456">In particular, for type members:</span></span>

* <span data-ttu-id="8fc7a-457">字段和嵌套类型只能通过名称区分。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-457">Fields and nested types are distinguished by name alone.</span></span>

* <span data-ttu-id="8fc7a-458">具有相同名称的方法、属性和事件必须具有除返回类型不同之外的其他不同之处。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-458">Methods, properties, and events that have the same name must differ by more than just return type.</span></span>

<span data-ttu-id="8fc7a-459">下面的示例说明了成员名称在其范围内必须是唯一的要求。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-459">The following example illustrates the requirement that member names must be unique within their scope.</span></span> <span data-ttu-id="8fc7a-460">它定义了一个名为 `Converter` 的类，该类包括四个名为 `Conversion` 的成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-460">It defines a class named `Converter` that includes four members named `Conversion`.</span></span> <span data-ttu-id="8fc7a-461">其中三个是方法，一个是属性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-461">Three are methods, and one is a property.</span></span> <span data-ttu-id="8fc7a-462">包含 `Int64` 参数的方法具有唯一名称，但是，具有 `Int32` 参数的两个方法不是，因为返回值不被视为成员签名的一部分。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-462">The method that includes an `Int64` parameter is uniquely named, but the two methods with an `Int32` parameter are not, because return value is not considered a part of a member's signature.</span></span> <span data-ttu-id="8fc7a-463">由于属性不能具有与重载方法相同的名称，因此 `Conversion` 属性也违反了此要求。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-463">The `Conversion` property also violates this requirement, because properties cannot have the same name as overloaded methods.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Converter
{
   public double Conversion(int number)
   {
      return (double) number;
   }

   public float Conversion(int number)
   {
      return (float) number;
   }

   public double Conversion(long number)
   {
      return (double) number;
   }

   public bool Conversion
   {
      get { return true; }
   }
}
// Compilation produces a compiler error like the following:
//    Naming3.cs(13,17): error CS0111: Type 'Converter' already defines a member called
//            'Conversion' with the same parameter types
//    Naming3.cs(8,18): (Location of symbol related to previous error)
//    Naming3.cs(23,16): error CS0102: The type 'Converter' already contains a definition for
//            'Conversion'
//    Naming3.cs(8,18): (Location of symbol related to previous error)
```

```vb
<Assembly: CLSCompliant(True)>

Public Class Converter
   Public Function Conversion(number As Integer) As Double
      Return CDbl(number)
   End Function

   Public Function Conversion(number As Integer) As Single
      Return CSng(number)
   End Function

   Public Function Conversion(number As Long) As Double
      Return CDbl(number)
   End Function

   Public ReadOnly Property Conversion As Boolean
      Get
         Return True
      End Get
   End Property
End Class
' Compilation produces a compiler error like the following:
'    Naming3.vb(8) : error BC30301: 'Public Function Conversion(number As Integer) As Double'
'                    and 'Public Function Conversion(number As Integer) As Single' cannot
'                    overload each other because they differ only by return types.
'
'       Public Function Conversion(number As Integer) As Double
'                       ~~~~~~~~~~
'    Naming3.vb(20) : error BC30260: 'Conversion' is already declared as 'Public Function
'                     Conversion(number As Integer) As Single' in this class.
'
'       Public ReadOnly Property Conversion As Boolean
'                                ~~~~~~~~~~
```

<span data-ttu-id="8fc7a-464">各种语言都包含唯一关键字，因此面向公共语言运行时的语言还必须提供一些机制，以便引用与关键字相符的标识符（例如，类型名称）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-464">Individual languages include unique keywords, so languages that target the common language runtime must also provide some mechanism for referencing identifiers (such as type names) that coincide with keywords.</span></span> <span data-ttu-id="8fc7a-465">例如，`case` 是 C# 和 Visual Basic 两者中的关键字。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-465">For example, `case` is a keyword in both C# and Visual Basic.</span></span> <span data-ttu-id="8fc7a-466">但是，下面的 Visual Basic 示例可以通过使用左大括号和右大括号将名为 `case` 的类从 `case` 关键字中消除。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-466">However, the following Visual Basic example is able to disambiguate a class named `case` from the `case` keyword by using opening and closing braces.</span></span> <span data-ttu-id="8fc7a-467">否则，该示例将生成错误消息“关键字无法用作标识符”，并且编译将失败。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-467">Otherwise, the example would produce the error message, "Keyword is not valid as an identifier," and fail to compile.</span></span>

```vb
Public Class [case]
   Private _id As Guid
   Private name As String

   Public Sub New(name As String)
      _id = Guid.NewGuid()
      Me.name = name
   End Sub

   Public ReadOnly Property ClientName As String
      Get
         Return name
      End Get
   End Property
End Class
```

<span data-ttu-id="8fc7a-468">以下 C# 示例可以通过使用 @ 符号从语言关键字中消除标识符来实例化 `case` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-468">The following C# example is able to instantiate the `case` class by using the @ symbol to disambiguate the identifier from the language keyword.</span></span> <span data-ttu-id="8fc7a-469">如果没有该符号，C# 编译器会显示两条错误消息：“应为类型”和“无效表达式术语‘case’”。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-469">Without it, the C# compiler would display two error messages, "Type expected" and "Invalid expression term 'case'."</span></span>

```csharp
using System;

public class Example
{
   public static void Main()
   {
      @case c = new @case("John");
      Console.WriteLine(c.ClientName);
   }
}
```

### <a name="type-conversion"></a><span data-ttu-id="8fc7a-470">类型转换</span><span class="sxs-lookup"><span data-stu-id="8fc7a-470">Type conversion</span></span>

<span data-ttu-id="8fc7a-471">公共语言规范定义了两个转换运算符：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-471">The Common Language Specification defines two conversion operators:</span></span>

* <span data-ttu-id="8fc7a-472">`op_Implicit` 用于扩大转换，不会丢失数据或精度。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-472">`op_Implicit`, which is used for widening conversions that do not result in loss of data or precision.</span></span> <span data-ttu-id="8fc7a-473">例如，[Decimal](xref:System.Decimal) 结构包含一个已重载的 `op_Implicit` 运算符，将整数类型值和 [Char](xref:System.Char) 值转换为 `Decimal` 值。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-473">For example, the [Decimal](xref:System.Decimal) structure includes an overloaded `op_Implicit` operator to convert values of integral types and [Char](xref:System.Char) values to `Decimal` values.</span></span>

* <span data-ttu-id="8fc7a-474">`op_Explicit` 用于收缩可能导致丢失量级（将一个值转换为一个范围更小的值）或精度的转换。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-474">`op_Explicit`, which is used for narrowing conversions that can result in loss of magnitude (a value is converted to a value that has a smaller range) or precision.</span></span> <span data-ttu-id="8fc7a-475">例如，`Decimal` 结构包含一个已重载的 `op_Explicit` 运算符，将 [Double](xref:System.Double) 和 [Single](xref:System.Single) 值转换为 `Decimal`，将 `Decimal` 值转换为整数值：`Double`、`Single` 和 `Char`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-475">For example, the `Decimal` structure includes an overloaded `op_Explicit` operator to convert [Double](xref:System.Double) and [Single](xref:System.Single) values to `Decimal` and to convert `Decimal` values to integral values, `Double`, `Single`, and `Char`.</span></span>

<span data-ttu-id="8fc7a-476">但是，并非所有语言都支持运算符重载或定义自定义运算符。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-476">However, not all languages support operator overloading or the definition of custom operators.</span></span> <span data-ttu-id="8fc7a-477">如果选择实现这些转换运算符，您还应提供另一种执行转换的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-477">If you choose to implement these conversion operators, you should also provide an alternate way to perform the conversion.</span></span> <span data-ttu-id="8fc7a-478">我们建议提供 `From`Xxx 和 `To`Xxx 方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-478">We recommend that you provide `From`Xxx and `To`Xxx methods.</span></span>

<span data-ttu-id="8fc7a-479">下面的示例定义符合 CLS 的隐式和显式转换。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-479">The following example defines CLS-compliant implicit and explicit conversions.</span></span> <span data-ttu-id="8fc7a-480">它创建表示带符号的双精度浮点数字的 `UDouble` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-480">It creates a `UDouble` class that represents a signed double-precision, floating-point number.</span></span> <span data-ttu-id="8fc7a-481">它提供从 `UDouble` 到 `Double` 的隐式转换和从 `UDouble` 到 `Single`、从 `Double` 到 `UDouble` 以及从 `Single` 到 `UDouble` 的显式转换。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-481">It provides for implicit conversions from `UDouble` to `Double` and for explicit conversions from `UDouble` to `Single`, `Double` to `UDouble`, and `Single` to `UDouble`.</span></span> <span data-ttu-id="8fc7a-482">它还将 `ToDouble` 方法定义为隐式转换运算符的替代方法，并将 `ToSingle`、`FromDouble` 和 `FromSingle` 方法定义为显式转换运算符的替代方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-482">It also defines a `ToDouble` method as an alternative to the implicit conversion operator and the `ToSingle`, `FromDouble`, and `FromSingle` methods as alternatives to the explicit conversion operators.</span></span>

```csharp
using System;

public struct UDouble
{
   private double number;

   public UDouble(double value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      number = value;
   }

   public UDouble(float value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      number = value;
   }

   public static readonly UDouble MinValue = (UDouble) 0.0;
   public static readonly UDouble MaxValue = (UDouble) Double.MaxValue;

   public static explicit operator Double(UDouble value)
   {
      return value.number;
   }

   public static implicit operator Single(UDouble value)
   {
      if (value.number > (double) Single.MaxValue)
         throw new InvalidCastException("A UDouble value is out of range of the Single type.");

      return (float) value.number;
   }

   public static explicit operator UDouble(double value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      return new UDouble(value);
   }

   public static implicit operator UDouble(float value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      return new UDouble(value);
   }

   public static Double ToDouble(UDouble value)
   {
      return (Double) value;
   }

   public static float ToSingle(UDouble value)
   {
      return (float) value;
   }

   public static UDouble FromDouble(double value)
   {
      return new UDouble(value);
   }

   public static UDouble FromSingle(float value)
   {
      return new UDouble(value);
   }
}
```

```vb
Public Structure UDouble
   Private number As Double

   Public Sub New(value As Double)
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      number = value
   End Sub

   Public Sub New(value As Single)
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      number = value
   End Sub

   Public Shared ReadOnly MinValue As UDouble = CType(0.0, UDouble)
   Public Shared ReadOnly MaxValue As UDouble = Double.MaxValue

   Public Shared Widening Operator CType(value As UDouble) As Double
      Return value.number
   End Operator

   Public Shared Narrowing Operator CType(value As UDouble) As Single
      If value.number > CDbl(Single.MaxValue) Then
         Throw New InvalidCastException("A UDouble value is out of range of the Single type.")
      End If
      Return CSng(value.number)
   End Operator

   Public Shared Narrowing Operator CType(value As Double) As UDouble
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      Return New UDouble(value)
   End Operator

   Public Shared Narrowing Operator CType(value As Single) As UDouble
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      Return New UDouble(value)
   End Operator

   Public Shared Function ToDouble(value As UDouble) As Double
      Return CType(value, Double)
   End Function

   Public Shared Function ToSingle(value As UDouble) As Single
      Return CType(value, Single)
   End Function

   Public Shared Function FromDouble(value As Double) As UDouble
      Return New UDouble(value)
   End Function

   Public Shared Function FromSingle(value As Single) As UDouble
      Return New UDouble(value)
   End Function
End Structure
```

### <a name="arrays"></a><span data-ttu-id="8fc7a-483">数组</span><span class="sxs-lookup"><span data-stu-id="8fc7a-483">Arrays</span></span>

<span data-ttu-id="8fc7a-484">符合 CLS 的数组符合以下规则：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-484">CLS-compliant arrays conform to the following rules:</span></span>

* <span data-ttu-id="8fc7a-485">数组的所有维度必须具有零下限。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-485">All dimensions of an array must have a lower bound of zero.</span></span> <span data-ttu-id="8fc7a-486">下面的示例创建一个不符合 CLS 的数组，其下限为 1。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-486">The following example creates a non-CLS-compliant array with a lower bound of one.</span></span> <span data-ttu-id="8fc7a-487">请注意，无论是否存在 [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) 特性，编译器都不检测由 `Numbers.GetTenPrimes` 方法返回的数组是否符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-487">Despite the presence of the [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) attribute, the compiler does not detect that the array returned by the `Numbers.GetTenPrimes` method is not CLS-compliant.</span></span>

  ```csharp
  [assembly: CLSCompliant(true)]

  public class Numbers
  {
    public static Array GetTenPrimes()
    {
        Array arr = Array.CreateInstance(typeof(Int32), new int[] {10}, new int[] {1});
        arr.SetValue(1, 1);
        arr.SetValue(2, 2);
        arr.SetValue(3, 3);
        arr.SetValue(5, 4);
        arr.SetValue(7, 5);
        arr.SetValue(11, 6);
        arr.SetValue(13, 7);
        arr.SetValue(17, 8);
        arr.SetValue(19, 9);
        arr.SetValue(23, 10);

        return arr;
    }
  }
  ```

  ```vb
  <Assembly: CLSCompliant(True)>

  Public Class Numbers
     Public Shared Function GetTenPrimes() As Array
        Dim arr As Array = Array.CreateInstance(GetType(Int32), {10}, {1})
        arr.SetValue(1, 1)
        arr.SetValue(2, 2)
        arr.SetValue(3, 3)
        arr.SetValue(5, 4)
        arr.SetValue(7, 5)
        arr.SetValue(11, 6)
        arr.SetValue(13, 7)
        arr.SetValue(17, 8)
        arr.SetValue(19, 9)
        arr.SetValue(23, 10)
        Return arr
     End Function
  End Class
  ```

* <span data-ttu-id="8fc7a-488">所有数组元素必须包括符合 CLS 的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-488">All array elements must consist of CLS-compliant types.</span></span> <span data-ttu-id="8fc7a-489">下面的示例定义返回不符合 CLS 的数组的两种方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-489">The following example defines two methods that return non-CLS-compliant arrays.</span></span> <span data-ttu-id="8fc7a-490">第一个返回 [UInt32](xref:System.UInt32) 值的数组。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-490">The first returns an array of [UInt32](xref:System.UInt32) values.</span></span> <span data-ttu-id="8fc7a-491">第二个返回包括 [Int32](xref:System.Int32) 和 `UInt32` 值的 [Object](xref:System.Object) 数组。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-491">The second returns an [Object](xref:System.Object) array that includes [Int32](xref:System.Int32) and `UInt32` values.</span></span> <span data-ttu-id="8fc7a-492">虽然编译器因第一个数组是 `UInt32` 类型而将其标识为不合规，但无法识别第二个包含不符合 CLS 元素的数组。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-492">Although the compiler identifies the first array as non-compliant because of its `UInt32` type, it fails to recognize that the second array includes non-CLS-compliant elements.</span></span>

  ```csharp
  using System;

  [assembly: CLSCompliant(true)]

  public class Numbers
  {
    public static UInt32[] GetTenPrimes()
    {
        uint[] arr = { 1u, 2u, 3u, 5u, 7u, 11u, 13u, 17u, 19u };
        return arr;
    }

    public static Object[] GetFivePrimes()
    {
        Object[] arr = { 1, 2, 3, 5u, 7u };
        return arr;
    }
  }
  // Compilation produces a compiler warning like the following:
  //    Array2.cs(8,27): warning CS3002: Return type of 'Numbers.GetTenPrimes()' is not
  //            CLS-compliant
  ```

  ```vb
  <Assembly: CLSCompliant(True)>

  Public Class Numbers
     Public Shared Function GetTenPrimes() As UInt32()
        Return { 1ui, 2ui, 3ui, 5ui, 7ui, 11ui, 13ui, 17ui, 19ui }
     End Function
     Public Shared Function GetFivePrimes() As Object()
        Dim arr() As Object = { 1, 2, 3, 5ui, 7ui }
        Return arr
     End Function
  End Class
  ' Compilation produces a compiler warning like the following:
  '    warning BC40027: Return type of function 'GetTenPrimes' is not CLS-compliant.
  ```

* <span data-ttu-id="8fc7a-493">具有数组参数的方法的重载决策基于它们是否为数组及它们的元素类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-493">Overload resolution for methods that have array parameters is based on the fact that they are arrays and on their element type.</span></span> <span data-ttu-id="8fc7a-494">因此，以下对重载的 `GetSquares` 方法的定义符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-494">For this reason, the following definition of an overloaded `GetSquares` method is CLS-compliant.</span></span>

  ```csharp
  using System;
  using System.Numerics;

  [assembly: CLSCompliant(true)]

  public class Numbers
  {
    public static byte[] GetSquares(byte[] numbers)
    {
        byte[] numbersOut = new byte[numbers.Length];
        for (int ctr = 0; ctr < numbers.Length; ctr++) {
            int square = ((int) numbers[ctr]) * ((int) numbers[ctr]);
            if (square <= Byte.MaxValue)
                numbersOut[ctr] = (byte) square;
            // If there's an overflow, assign MaxValue to the corresponding
            // element.
            else
                numbersOut[ctr] = Byte.MaxValue;

        }
        return numbersOut;
    }

    public static BigInteger[] GetSquares(BigInteger[] numbers)
  {
        BigInteger[] numbersOut = new BigInteger[numbers.Length];
        for (int ctr = 0; ctr < numbers.Length; ctr++)
            numbersOut[ctr] = numbers[ctr] * numbers[ctr];

       return numbersOut;
    }
  }
  ```

  ```vb
  Imports System.Numerics

  <Assembly: CLSCompliant(True)>

  Public Module Numbers
     Public Function GetSquares(numbers As Byte()) As Byte()
        Dim numbersOut(numbers.Length - 1) As Byte
        For ctr As Integer = 0 To numbers.Length - 1
           Dim square As Integer = (CInt(numbers(ctr)) * CInt(numbers(ctr)))
           If square <= Byte.MaxValue Then
              numbersOut(ctr) = CByte(square)
           ' If there's an overflow, assign MaxValue to the corresponding
           ' element.
           Else
              numbersOut(ctr) = Byte.MaxValue
           End If
        Next
        Return numbersOut
     End Function

     Public Function GetSquares(numbers As BigInteger()) As BigInteger()
         Dim numbersOut(numbers.Length - 1) As BigInteger
         For ctr As Integer = 0 To numbers.Length - 1
            numbersOut(ctr) = numbers(ctr) * numbers(ctr)
         Next
         Return numbersOut
     End Function
  End Module
  ```

### <a name="interfaces"></a><span data-ttu-id="8fc7a-495">接口</span><span class="sxs-lookup"><span data-stu-id="8fc7a-495">Interfaces</span></span>

<span data-ttu-id="8fc7a-496">符合 CLS 的接口可以定义属性、事件和虚拟方法（没有实现的方法）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-496">CLS-compliant interfaces can define properties, events, and virtual methods (methods with no implementation).</span></span> <span data-ttu-id="8fc7a-497">符合 CLS 的接口不能有：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-497">A CLS-compliant interface cannot have any of the following:</span></span>

* <span data-ttu-id="8fc7a-498">静态方法或静态字段。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-498">Static methods or static fields.</span></span> <span data-ttu-id="8fc7a-499">如果在接口中定义静态成员，C# 编译器将生成编译器错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-499">The C# compiler generates compiler errors if you define a static member in an interface.</span></span>

* <span data-ttu-id="8fc7a-500">字段。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-500">Fields.</span></span> <span data-ttu-id="8fc7a-501">如果在接口中定义字段，C# 编译器将生成编译器错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-501">The C# a compiler generates compiler errors if you define a field in an interface.</span></span>

* <span data-ttu-id="8fc7a-502">不符合 CLS 的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-502">Methods that are not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-503">例如，下面的接口定义包括方法 `INumber.GetUnsigned`，该方法标记为不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-503">For example, the following interface definition includes a method, `INumber.GetUnsigned`, that is marked as non-CLS-compliant.</span></span> <span data-ttu-id="8fc7a-504">此示例生成编译器警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-504">This example generates a compiler warning.</span></span>

  ```csharp
  using System;

  [assembly:CLSCompliant(true)]

  public interface INumber
  {
      int Length();
      [CLSCompliant(false)] ulong GetUnsigned();
  }
  // Attempting to compile the example displays output like the following:
  //    Interface2.cs(8,32): warning CS3010: 'INumber.GetUnsigned()': CLS-compliant interfaces
  //            must have only CLS-compliant members
  ```

  ```vb
  <Assembly: CLSCompliant(True)>

  Public Interface INumber
    Function Length As Integer
      <CLSCompliant(False)> Function GetUnsigned As ULong
    End Interface
    ' Attempting to compile the example displays output like the following:
    '    Interface2.vb(9) : warning BC40033: Non CLS-compliant 'function' is not allowed in a
    '    CLS-compliant interface.
    '
    '       <CLSCompliant(False)> Function GetUnsigned As ULong
    '                                      ~~~~~~~~~~~
  ```

  <span data-ttu-id="8fc7a-505">由于存在此规则，因此符合 CLS 的类型不需要实现不符合 CLS 的成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-505">Because of this rule, CLS-compliant types are not required to implement non-CLS-compliant members.</span></span> <span data-ttu-id="8fc7a-506">如果一个符合 CLS 的框架公开实现不符合 CLS 接口的类，则其还应提供所有不符合 CLS 的成员的具体实现。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-506">If a CLS-compliant framework does expose a class that implements a non-CLS compliant interface, it should also provide concrete implementations of all non-CLS-compliant members.</span></span>

<span data-ttu-id="8fc7a-507">符合 CLS 的语言编译器还必须允许类提供在多个接口中具有相同名称和签名的成员的单独实现。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-507">CLS-compliant language compilers must also allow a class to provide separate implementations of members that have the same name and signature in multiple interfaces.</span></span> <span data-ttu-id="8fc7a-508">C# 支持使用显式接口实现来提供同名方法的不同实现。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-508">C# supports explicit interface implementations to provide different implementations of identically named methods.</span></span> <span data-ttu-id="8fc7a-509">下面的示例通过定义一个将 `Temperature` 和 `ICelsius` 接口作为显式接口实现的 `IFahrenheit` 类来说明此方案。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-509">The following example illustrates this scenario by defining a `Temperature` class that implements the `ICelsius` and `IFahrenheit` interfaces as explicit interface implementations.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public interface IFahrenheit
{
   decimal GetTemperature();
}

public interface ICelsius
{
   decimal GetTemperature();
}

public class Temperature : ICelsius, IFahrenheit
{
   private decimal _value;

   public Temperature(decimal value)
   {
      // We assume that this is the Celsius value.
      _value = value;
   }

   decimal IFahrenheit.GetTemperature()
   {
      return _value * 9 / 5 + 32;
   }

   decimal ICelsius.GetTemperature()
   {
      return _value;
   }
}
public class Example
{
   public static void Main()
   {
      Temperature temp = new Temperature(100.0m);
      ICelsius cTemp = temp;
      IFahrenheit fTemp = temp;
      Console.WriteLine("Temperature in Celsius: {0} degrees",
                        cTemp.GetTemperature());
      Console.WriteLine("Temperature in Fahrenheit: {0} degrees",
                        fTemp.GetTemperature());
   }
}
// The example displays the following output:
//       Temperature in Celsius: 100.0 degrees
//       Temperature in Fahrenheit: 212.0 degrees
```

```vb
Assembly: CLSCompliant(True)>

Public Interface IFahrenheit
   Function GetTemperature() As Decimal
End Interface

Public Interface ICelsius
   Function GetTemperature() As Decimal
End Interface

Public Class Temperature : Implements ICelsius, IFahrenheit
   Private _value As Decimal

   Public Sub New(value As Decimal)
      ' We assume that this is the Celsius value.
      _value = value
   End Sub

   Public Function GetFahrenheit() As Decimal _
          Implements IFahrenheit.GetTemperature
      Return _value * 9 / 5 + 32
   End Function

   Public Function GetCelsius() As Decimal _
          Implements ICelsius.GetTemperature
      Return _value
   End Function
End Class

Module Example
   Public Sub Main()
      Dim temp As New Temperature(100.0d)
      Console.WriteLine("Temperature in Celsius: {0} degrees",
                        temp.GetCelsius())
      Console.WriteLine("Temperature in Fahrenheit: {0} degrees",
                        temp.GetFahrenheit())
   End Sub
End Module
' The example displays the following output:
'       Temperature in Celsius: 100.0 degrees
'       Temperature in Fahrenheit: 212.0 degrees
```

### <a name="enumerations"></a><span data-ttu-id="8fc7a-510">枚举</span><span class="sxs-lookup"><span data-stu-id="8fc7a-510">Enumerations</span></span>

<span data-ttu-id="8fc7a-511">符合 CLS 的枚举必须遵循下列规则：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-511">CLS-compliant enumerations must follow these rules:</span></span>

* <span data-ttu-id="8fc7a-512">枚举的基础类型必须是符合 CLS 的内部整数（[Byte](xref:System.Byte)、[Int16](xref:System.Int16)、[Int32](xref:System.Int32) 或 [Int64](xref:System.Int64)）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-512">The underlying type of the enumeration must be an intrinsic CLS-compliant integer ([Byte](xref:System.Byte), [Int16](xref:System.Int16), [Int32](xref:System.Int32), or [Int64](xref:System.Int64)).</span></span> <span data-ttu-id="8fc7a-513">例如，下面的代码尝试定义基础类型为 [UInt32](xref:System.UInt32) 的枚举并生成编译器警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-513">For example, the following code tries to define an enumeration whose underlying type is [UInt32](xref:System.UInt32) and generates a compiler warning.</span></span>

    ```csharp
    using System;

    [assembly: CLSCompliant(true)]

    public enum Size : uint {
        Unspecified = 0,
        XSmall = 1,
        Small = 2,
        Medium = 3,
        Large = 4,
        XLarge = 5
    };

    public class Clothing
    {
        public string Name;
        public string Type;
        public string Size;
    }
    // The attempt to compile the example displays a compiler warning like the following:
    //    Enum3.cs(6,13): warning CS3009: 'Size': base type 'uint' is not CLS-compliant
    ```

    ```vb
    <Assembly: CLSCompliant(True)>

    Public Enum Size As UInt32
       Unspecified = 0
       XSmall = 1
       Small = 2
       Medium = 3
       Large = 4
       XLarge = 5
    End Enum

    Public Class Clothing
       Public Name As String
       Public Type As String
       Public Size As Size
    End Class
    ' The attempt to compile the example displays a compiler warning like the following:
    '    Enum3.vb(6) : warning BC40032: Underlying type 'UInt32' of Enum is not CLS-compliant.
    '
    '    Public Enum Size As UInt32
    '                ~~~~
    ```

* <span data-ttu-id="8fc7a-514">枚举类型必须具有名为 `Value__` 且标有 `FieldAttributes.RTSpecialName` 特性的单个实例字段。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-514">An enumeration type must have a single instance field named `Value__` that is marked with the `FieldAttributes.RTSpecialName` attribute.</span></span> <span data-ttu-id="8fc7a-515">这使得您可以隐式引用字段值。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-515">This enables you to reference the field value implicitly.</span></span>

* <span data-ttu-id="8fc7a-516">枚举包括文本静态字段，该字段的类型与枚举本身的类型匹配。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-516">An enumeration includes literal static fields whose types match the type of the enumeration itself.</span></span> <span data-ttu-id="8fc7a-517">例如，如果您用 `State` 和 `State.On` 的值定义 `State.Off` 枚举，则 `State.On` 和 `State.Off` 都是文本静态字段，其类型为 `State`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-517">For example, if you define a `State` enumeration with values of `State.On` and `State.Off`, `State.On` and `State.Off` are both literal static fields whose type is `State`.</span></span>

* <span data-ttu-id="8fc7a-518">有两种枚举：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-518">There are two kinds of enumerations:</span></span>

  * <span data-ttu-id="8fc7a-519">一种表示一组互斥的命名整数值的枚举。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-519">An enumeration that represents a set of mutually exclusive, named integer values.</span></span> <span data-ttu-id="8fc7a-520">这种类型的枚举由缺少 [System.FlagsAttribute](xref:System.FlagsAttribute) 自定义特性表示。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-520">This type of enumeration is indicated by the absence of the [System.FlagsAttribute](xref:System.FlagsAttribute) custom attribute.</span></span>

  * <span data-ttu-id="8fc7a-521">一种表示可结合用来生成未命名值的一组位标志的枚举。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-521">An enumeration that represents a set of bit flags that can combine to generate an unnamed value.</span></span> <span data-ttu-id="8fc7a-522">这种类型的枚举由存在 [System.FlagsAttribute](xref:System.FlagsAttribute) 自定义特性表示。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-522">This type of enumeration is indicated by the presence of the [System.FlagsAttribute](xref:System.FlagsAttribute) custom attribute.</span></span>

<span data-ttu-id="8fc7a-523">有关详细信息，请参阅 [Enum](xref:System.Enum) 结构的文档。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-523">For more information, see the documentation for the [Enum](xref:System.Enum) structure.</span></span>

* <span data-ttu-id="8fc7a-524">枚举的值不限于其指定值的范围。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-524">The value of an enumeration is not limited to the range of its specified values.</span></span> <span data-ttu-id="8fc7a-525">换言之，枚举中的值的范围是其基础值的范围。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-525">In other words, the range of values in an enumeration is the range of its underlying value.</span></span> <span data-ttu-id="8fc7a-526">您可以使用 `Enum.IsDefined` 方法来确定指定的值是否为枚举成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-526">You can use the `Enum.IsDefined` method to determine whether a specified value is a member of an enumeration.</span></span>

### <a name="type-members-in-general"></a><span data-ttu-id="8fc7a-527">类型成员概述</span><span class="sxs-lookup"><span data-stu-id="8fc7a-527">Type members in general</span></span>

<span data-ttu-id="8fc7a-528">公共语言规范要求将所有字段和方法作为特定类的成员进行访问。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-528">The Common Language Specification requires all fields and methods to be accessed as members of a particular class.</span></span> <span data-ttu-id="8fc7a-529">因此，全局静态字段和方法（即，除类型外定义的静态字段或方法）不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-529">Therefore, global static fields and methods (that is, static fields or methods that are defined apart from a type) are not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-530">如果尝试在源代码中包括全局字段或方法，C# 编译器将生成编译器错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-530">If you try to include a global field or method in your source code, the C# compiler generates a compiler error.</span></span>

<span data-ttu-id="8fc7a-531">公共语言规范仅支持标准托管调用约定。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-531">The Common Language Specification supports only the standard managed calling convention.</span></span> <span data-ttu-id="8fc7a-532">它不支持非托管调用约定和带使用 `varargs` 关键字标记的变量参数列表的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-532">It doesn't support unmanaged calling conventions and methods with variable argument lists marked with the `varargs` keyword.</span></span> <span data-ttu-id="8fc7a-533">对于符合标准托管调用约定的变量自变量列表，请使用 [ParamArrayAttribute](xref:System.ParamArrayAttribute) 特性或单个语言的实现，如 C# 中的 `params` 关键字和 Visual Basic 中的 `ParamArray` 关键字。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-533">For variable argument lists that are compatible with the standard managed calling convention, use the [ParamArrayAttribute](xref:System.ParamArrayAttribute) attribute or the individual language's implementation, such as the `params` keyword in C# and the `ParamArray` keyword in Visual Basic.</span></span>

### <a name="member-accessibility"></a><span data-ttu-id="8fc7a-534">成员可访问性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-534">Member accessibility</span></span>

<span data-ttu-id="8fc7a-535">重写继承成员不能更改该成员的可访问性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-535">Overriding an inherited member cannot change the accessibility of that member.</span></span> <span data-ttu-id="8fc7a-536">例如，无法在派生类中通过私有方法重写基类中的公共方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-536">For example, a public method in a base class cannot be overridden by a private method in a derived class.</span></span> <span data-ttu-id="8fc7a-537">有一个例外：由其他程序集中的类型重写的程序集中的 `protected internal`（在 C# 中）或 `Protected Friend`（在 Visual Basic 中）成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-537">There is one exception: a `protected internal` (in C#) or `Protected Friend` (in Visual Basic) member in one assembly that is overridden by a type in a different assembly.</span></span>  <span data-ttu-id="8fc7a-538">在该示例中，重写的可访问性是 `Protected`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-538">In that case, the accessibility of the override is `Protected`.</span></span>

<span data-ttu-id="8fc7a-539">下面的示例说明了当 [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) 特性设置为 `true`，并且 `Person`（它是派生自 `Animal` 的类）尝试将 `Species` 属性的可访问性从公开更改为私有时生成的错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-539">The following example illustrates the error that is generated when the [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) attribute is set to `true`, and `Person`, which is a class derived from `Animal`, tries to change the accessibility of the `Species` property from public to private.</span></span> <span data-ttu-id="8fc7a-540">如果该示例的可访问性更改为公共，则其编译成功。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-540">The example compiles successfully if its accessibility is changed to public.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Animal
{
   private string _species;

   public Animal(string species)
   {
      _species = species;
   }

   public virtual string Species
   {
      get { return _species; }
   }

   public override string ToString()
   {
      return _species;
   }
}

public class Human : Animal
{
   private string _name;

   public Human(string name) : base("Homo Sapiens")
   {
      _name = name;
   }

   public string Name
   {
      get { return _name; }
   }

   private override string Species
   {
      get { return base.Species; }
   }

   public override string ToString()
   {
      return _name;
   }
}

public class Example
{
   public static void Main()
   {
      Human p = new Human("John");
      Console.WriteLine(p.Species);
      Console.WriteLine(p.ToString());
   }
}
// The example displays the following output:
//    error CS0621: 'Human.Species': virtual or abstract members cannot be private
```

```vb
<Assembly: CLSCompliant(True)>

Public Class Animal
   Private _species As String

   Public Sub New(species As String)
      _species = species
   End Sub

   Public Overridable ReadOnly Property Species As String
      Get
         Return _species
      End Get
   End Property

   Public Overrides Function ToString() As String
      Return _species
   End Function
End Class

Public Class Human : Inherits Animal
   Private _name As String

   Public Sub New(name As String)
      MyBase.New("Homo Sapiens")
      _name = name
   End Sub

   Public ReadOnly Property Name As String
      Get
         Return _name
      End Get
   End Property

   Private Overrides ReadOnly Property Species As String
      Get
         Return MyBase.Species
      End Get
   End Property

   Public Overrides Function ToString() As String
      Return _name
   End Function
End Class

Public Module Example
   Public Sub Main()
      Dim p As New Human("John")
      Console.WriteLine(p.Species)
      Console.WriteLine(p.ToString())
   End Sub
End Module
' The example displays the following output:
'     'Private Overrides ReadOnly Property Species As String' cannot override
'     'Public Overridable ReadOnly Property Species As String' because
'      they have different access levels.
'
'         Private Overrides ReadOnly Property Species As String
```

<span data-ttu-id="8fc7a-541">如果某个成员是可访问的，则该成员签名中的类型必须是可访问的。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-541">Types in the signature of a member must be accessible whenever that member is accessible.</span></span> <span data-ttu-id="8fc7a-542">例如，这意味着公共成员不能包含类型是私有的、受保护的或内部的参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-542">For example, this means that a public member cannot include a parameter whose type is private, protected, or internal.</span></span> <span data-ttu-id="8fc7a-543">下面的示例说明了当 `StringWrapper` 类构造函数公开一个用于确定如何包装字符串值的内部 `StringOperationType` 枚举值时出现的编译器错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-543">The following example illustrates the compiler error that results when a `StringWrapper` class constructor exposes an internal `StringOperationType` enumeration value that determines how a string value should be wrapped.</span></span>

```csharp
using System;
using System.Text;

public class StringWrapper
{
   string internalString;
   StringBuilder internalSB = null;
   bool useSB = false;

   public StringWrapper(StringOperationType type)
   {
      if (type == StringOperationType.Normal) {
         useSB = false;
      }
      else {
         useSB = true;
         internalSB = new StringBuilder();
      }
   }

   // The remaining source code...
}

internal enum StringOperationType { Normal, Dynamic }
// The attempt to compile the example displays the following output:
//    error CS0051: Inconsistent accessibility: parameter type
//            'StringOperationType' is less accessible than method
//            'StringWrapper.StringWrapper(StringOperationType)'
```

```vb
Imports System.Text

<Assembly:CLSCompliant(True)>

Public Class StringWrapper

   Dim internalString As String
   Dim internalSB As StringBuilder = Nothing
   Dim useSB As Boolean = False

   Public Sub New(type As StringOperationType)
      If type = StringOperationType.Normal Then
         useSB = False
      Else
         internalSB = New StringBuilder()
         useSB = True
      End If
   End Sub

   ' The remaining source code...
End Class

Friend Enum StringOperationType As Integer
   Normal = 0
   Dynamic = 1
End Enum
' The attempt to compile the example displays the following output:
'    error BC30909: 'type' cannot expose type 'StringOperationType'
'     outside the project through class 'StringWrapper'.
'
'       Public Sub New(type As StringOperationType)
'                              ~~~~~~~~~~~~~~~~~~~
```

### <a name="generic-types-and-members"></a><span data-ttu-id="8fc7a-544">泛型类型和成员</span><span class="sxs-lookup"><span data-stu-id="8fc7a-544">Generic types and members</span></span>

<span data-ttu-id="8fc7a-545">嵌套类型拥有的泛型参数数目总是至少与封闭类型的一样多。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-545">Nested types always have at least as many generic parameters as their enclosing type.</span></span> <span data-ttu-id="8fc7a-546">它们按位置对应于封闭类型中的泛型参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-546">These correspond by position to the generic parameters in the enclosing type.</span></span> <span data-ttu-id="8fc7a-547">泛型类型还可以包括新的泛型参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-547">The generic type can also include new generic parameters.</span></span>

<span data-ttu-id="8fc7a-548">一个包含类型及其嵌套类型的泛型类型参数之间的关系可能由各种语言的语法隐藏。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-548">The relationship between the generic type parameters of a containing type and its nested types may be hidden by the syntax of individual languages.</span></span> <span data-ttu-id="8fc7a-549">在下面的示例中，泛型类型 `Outer<T>` 包含两个嵌套的类：`Inner1A` 和 `Inner1B<U>`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-549">In the following example, a generic type `Outer<T>` contains two nested classes, `Inner1A` and `Inner1B<U>`.</span></span> <span data-ttu-id="8fc7a-550">对于每个类从 `ToString` 继承的 `Object.ToString` 方法的调用，表示每个嵌套的类包括其包含的类的类型参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-550">The calls to the `ToString` method, which each class inherits from `Object.ToString`, show that each nested class includes the type parameters of its containing class.</span></span>

```csharp
using System;

[assembly:CLSCompliant(true)]

public class Outer<T>
{
   T value;

   public Outer(T value)
   {
      this.value = value;
   }

   public class Inner1A : Outer<T>
   {
      public Inner1A(T value) : base(value)
      {  }
   }

   public class Inner1B<U> : Outer<T>
   {
      U value2;

      public Inner1B(T value1, U value2) : base(value1)
      {
         this.value2 = value2;
      }
   }
}

public class Example
{
   public static void Main()
   {
      var inst1 = new Outer<String>("This");
      Console.WriteLine(inst1);

      var inst2 = new Outer<String>.Inner1A("Another");
      Console.WriteLine(inst2);

      var inst3 = new Outer<String>.Inner1B<int>("That", 2);
      Console.WriteLine(inst3);
   }
}
// The example displays the following output:
//       Outer`1[System.String]
//       Outer`1+Inner1A[System.String]
//       Outer`1+Inner1B`1[System.String,System.Int32]
```

```vb
<Assembly:CLSCompliant(True)>

Public Class Outer(Of T)
   Dim value As T

   Public Sub New(value As T)
      Me.value = value
   End Sub

   Public Class Inner1A : Inherits Outer(Of T)
      Public Sub New(value As T)
         MyBase.New(value)
      End Sub
   End Class

   Public Class Inner1B(Of U) : Inherits Outer(Of T)
      Dim value2 As U

      Public Sub New(value1 As T, value2 As U)
         MyBase.New(value1)
         Me.value2 = value2
      End Sub
   End Class
End Class

Public Module Example
   Public Sub Main()
      Dim inst1 As New Outer(Of String)("This")
      Console.WriteLine(inst1)

      Dim inst2 As New Outer(Of String).Inner1A("Another")
      Console.WriteLine(inst2)

      Dim inst3 As New Outer(Of String).Inner1B(Of Integer)("That", 2)
      Console.WriteLine(inst3)
   End Sub
End Module
' The example displays the following output:
'       Outer`1[System.String]
'       Outer`1+Inner1A[System.String]
'       Outer`1+Inner1B`1[System.String,System.Int32]
```

<span data-ttu-id="8fc7a-551">泛型类型名称采用 *name*'*n* 格式进行编码，其中 *name* 是类型名称， *\`* 是字符文本，*n* 是在类型上声明的参数数目，或对于嵌套泛型类型为最近引入的类型参数的数目。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-551">Generic type names are encoded in the form *name*'*n*, where *name* is the type name, *\`* is a character literal, and *n* is the number of parameters declared on the type, or, for nested generic types, the number of newly introduced type parameters.</span></span> <span data-ttu-id="8fc7a-552">此泛型类型名称的编码主要对使用反射来访问库中符合 CLS 的泛型类型的开发人员很有用。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-552">This encoding of generic type names is primarily of interest to developers who use reflection to access CLS-complaint generic types in a library.</span></span>

<span data-ttu-id="8fc7a-553">如果将约束应用于泛型类型，则任何用作约束的类型也必须符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-553">If constraints are applied to a generic type, any types used as constraints must also be CLS-compliant.</span></span> <span data-ttu-id="8fc7a-554">下面的示例定义一个名为 `BaseClass` 的不符合 CLS 的类和一个其类型参数必须派生自 `BaseCollection` 的名为 `BaseClass` 的泛型类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-554">The following example defines a class named `BaseClass` that is not CLS-compliant and a generic class named `BaseCollection` whose type parameter must derive from `BaseClass`.</span></span> <span data-ttu-id="8fc7a-555">但由于 `BaseClass` 不符合 CLS，因此编译器会发出警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-555">But because `BaseClass` is not CLS-compliant, the compiler emits a warning.</span></span>

```csharp
using System;

[assembly:CLSCompliant(true)]

[CLSCompliant(false)] public class BaseClass
{}

public class BaseCollection<T> where T : BaseClass
{}
// Attempting to compile the example displays the following output:
//    warning CS3024: Constraint type 'BaseClass' is not CLS-compliant
```

```vb
Assembly: CLSCompliant(True)>

<CLSCompliant(False)> Public Class BaseClass
End Class

Public Class BaseCollection(Of T As BaseClass)
End Class
' Attempting to compile the example displays the following output:
'    warning BC40040: Generic parameter constraint type 'BaseClass' is not
'    CLS-compliant.
'
'    Public Class BaseCollection(Of T As BaseClass)
'                                        ~~~~~~~~~
```

<span data-ttu-id="8fc7a-556">如果泛型类型派生自泛型基本类型，则其必须重新声明所有约束，以确保也满足对基本类型的约束。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-556">If a generic type is derived from a generic base type, it must redeclare any constraints so that it can guarantee that constraints on the base type are also satisfied.</span></span> <span data-ttu-id="8fc7a-557">下面的示例定义可表示任何数值类型的 `Number<T>`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-557">The following example defines a `Number<T>` that can represent any numeric type.</span></span> <span data-ttu-id="8fc7a-558">它还定义表示浮点值的 `FloatingPoint<T>` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-558">It also defines a `FloatingPoint<T>` class that represents a floating point value.</span></span> <span data-ttu-id="8fc7a-559">但是，源代码无法编译，因为它未将 `Number<T>` 上（T 必须是值类型）的约束应用于 `FloatingPoint<T>`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-559">However, the source code fails to compile, because it does not apply the constraint on `Number<T>` (that T must be a value type) to `FloatingPoint<T>`.</span></span>

```csharp
using System;

[assembly:CLSCompliant(true)]

public class Number<T> where T : struct
{
   // use Double as the underlying type, since its range is a superset of
   // the ranges of all numeric types except BigInteger.
   protected double number;

   public Number(T value)
   {
      try {
         this.number = Convert.ToDouble(value);
      }
      catch (OverflowException e) {
         throw new ArgumentException("value is too large.", e);
      }
      catch (InvalidCastException e) {
         throw new ArgumentException("The value parameter is not numeric.", e);
      }
   }

   public T Add(T value)
   {
      return (T) Convert.ChangeType(number + Convert.ToDouble(value), typeof(T));
   }

   public T Subtract(T value)
   {
      return (T) Convert.ChangeType(number - Convert.ToDouble(value), typeof(T));
   }
}

public class FloatingPoint<T> : Number<T>
{
   public FloatingPoint(T number) : base(number)
   {
      if (typeof(float) == number.GetType() ||
          typeof(double) == number.GetType() ||
          typeof(decimal) == number.GetType())
         this.number = Convert.ToDouble(number);
      else
         throw new ArgumentException("The number parameter is not a floating-point number.");
   }
}
// The attempt to compile the example displays the following output:
//       error CS0453: The type 'T' must be a non-nullable value type in
//               order to use it as parameter 'T' in the generic type or method 'Number<T>'
```

```vb
<Assembly:CLSCompliant(True)>

Public Class Number(Of T As Structure)
   ' Use Double as the underlying type, since its range is a superset of
   ' the ranges of all numeric types except BigInteger.
   Protected number As Double

   Public Sub New(value As T)
      Try
         Me.number = Convert.ToDouble(value)
      Catch e As OverflowException
         Throw New ArgumentException("value is too large.", e)
      Catch e As InvalidCastException
         Throw New ArgumentException("The value parameter is not numeric.", e)
      End Try
   End Sub

   Public Function Add(value As T) As T
      Return CType(Convert.ChangeType(number + Convert.ToDouble(value), GetType(T)), T)
   End Function

   Public Function Subtract(value As T) As T
      Return CType(Convert.ChangeType(number - Convert.ToDouble(value), GetType(T)), T)
   End Function
End Class

Public Class FloatingPoint(Of T) : Inherits Number(Of T)
   Public Sub New(number As T)
      MyBase.New(number)
      If TypeOf number Is Single Or
               TypeOf number Is Double Or
               TypeOf number Is Decimal Then
         Me.number = Convert.ToDouble(number)
      Else
         throw new ArgumentException("The number parameter is not a floating-point number.")
      End If
   End Sub
End Class
' The attempt to compile the example displays the following output:
'    error BC32105: Type argument 'T' does not satisfy the 'Structure'
'    constraint for type parameter 'T'.
'
'    Public Class FloatingPoint(Of T) : Inherits Number(Of T)
'                                                          ~
```

<span data-ttu-id="8fc7a-560">如果将此约束添加到 `FloatingPoint<T>` 类中，则该示例成功编译。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-560">The example compiles successfully if the constraint is added to the `FloatingPoint<T>` class.</span></span>

```csharp
using System;

[assembly:CLSCompliant(true)]

public class Number<T> where T : struct
{
   // use Double as the underlying type, since its range is a superset of
   // the ranges of all numeric types except BigInteger.
   protected double number;

   public Number(T value)
   {
      try {
         this.number = Convert.ToDouble(value);
      }
      catch (OverflowException e) {
         throw new ArgumentException("value is too large.", e);
      }
      catch (InvalidCastException e) {
         throw new ArgumentException("The value parameter is not numeric.", e);
      }
   }

   public T Add(T value)
   {
      return (T) Convert.ChangeType(number + Convert.ToDouble(value), typeof(T));
   }

   public T Subtract(T value)
   {
      return (T) Convert.ChangeType(number - Convert.ToDouble(value), typeof(T));
   }
}

public class FloatingPoint<T> : Number<T> where T : struct
{
   public FloatingPoint(T number) : base(number)
   {
      if (typeof(float) == number.GetType() ||
          typeof(double) == number.GetType() ||
          typeof(decimal) == number.GetType())
         this.number = Convert.ToDouble(number);
      else
         throw new ArgumentException("The number parameter is not a floating-point number.");
   }
}
```

```vb
<Assembly:CLSCompliant(True)>

Public Class Number(Of T As Structure)
   ' Use Double as the underlying type, since its range is a superset of
   ' the ranges of all numeric types except BigInteger.
   Protected number As Double

   Public Sub New(value As T)
      Try
         Me.number = Convert.ToDouble(value)
      Catch e As OverflowException
         Throw New ArgumentException("value is too large.", e)
      Catch e As InvalidCastException
         Throw New ArgumentException("The value parameter is not numeric.", e)
      End Try
   End Sub

   Public Function Add(value As T) As T
      Return CType(Convert.ChangeType(number + Convert.ToDouble(value), GetType(T)), T)
   End Function

   Public Function Subtract(value As T) As T
      Return CType(Convert.ChangeType(number - Convert.ToDouble(value), GetType(T)), T)
   End Function
End Class

Public Class FloatingPoint(Of T As Structure) : Inherits Number(Of T)
   Public Sub New(number As T)
      MyBase.New(number)
      If TypeOf number Is Single Or
               TypeOf number Is Double Or
               TypeOf number Is Decimal Then
         Me.number = Convert.ToDouble(number)
      Else
         throw new ArgumentException("The number parameter is not a floating-point number.")
      End If
   End Sub
End Class
```

<span data-ttu-id="8fc7a-561">公共语言规范对嵌套类型和受保护成员规定了一个保守的按实例化模型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-561">The Common Language Specification imposes a conservative per-instantiation model for nested types and protected members.</span></span> <span data-ttu-id="8fc7a-562">开放式泛型类型不能公开具有包含嵌套的、受保护的泛型类型的特定实例化的签名的字段或成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-562">Open generic types cannot expose fields or members with signatures that contain a specific instantiation of a nested, protected generic type.</span></span> <span data-ttu-id="8fc7a-563">扩大泛型基类或接口的特定实例化的非泛型类型不能公开带签名的字段或成员，此类字段或成员包含嵌套的、受保护的泛型类型的不同实例化。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-563">Non-generic types that extend a specific instantiation of a generic base class or interface cannot expose fields or members with signatures that contain a different instantiation of a nested, protected generic type.</span></span>

<span data-ttu-id="8fc7a-564">下面的示例定义一个泛型类型 `C1<T>` 和一个受保护的类 `C1<T>.N`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-564">The following example defines a generic type, `C1<T>`, and a protected class, `C1<T>.N`.</span></span> <span data-ttu-id="8fc7a-565">`C1<T>` 有两种方法：`M1` 和 `M2`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-565">`C1<T>` has two methods, `M1` and `M2`.</span></span> <span data-ttu-id="8fc7a-566">但是，`M1` 并不符合 CLS，因为它尝试从 `C1<T>` 返回 `C1<int>.N` 对象。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-566">However, `M1` is not CLS-compliant because it tries to return a `C1<int>.N` object from `C1<T>`.</span></span> <span data-ttu-id="8fc7a-567">另一个名为 `C2` 的类派生自 `C1<long>`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-567">A second class, `C2`, is derived from `C1<long>`.</span></span> <span data-ttu-id="8fc7a-568">它有两种方法：`M3` 和 `M4`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-568">It has two methods, `M3` and `M4`.</span></span> <span data-ttu-id="8fc7a-569">`M3` 不符合 CLS，因为它尝试从 `C1<long>` 的子类中返回 `C1<int>.N` 对象。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-569">`M3` is not CLS-compliant because it tries to return a `C1<int>.N` object from a subclass of `C1<long>`.</span></span> <span data-ttu-id="8fc7a-570">语言编译器可能具有更高限制。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-570">Language compilers can be even more restrictive.</span></span> <span data-ttu-id="8fc7a-571">在此示例中，Visual Basic 在尝试编译 `M4` 时显示错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-571">In this example, Visual Basic displays an error when it tries to compile `M4`.</span></span>

```csharp
using System;

[assembly:CLSCompliant(true)]

public class C1<T>
{
   protected class N { }

   protected void M1(C1<int>.N n) { } // Not CLS-compliant - C1<int>.N not
                                      // accessible from within C1<T> in all
                                      // languages
   protected void M2(C1<T>.N n) { }   // CLS-compliant – C1<T>.N accessible
                                      // inside C1<T>
}

public class C2 : C1<long>
{
   protected void M3(C1<int>.N n) { }  // Not CLS-compliant – C1<int>.N is not
                                       // accessible in C2 (extends C1<long>)

   protected void M4(C1<long>.N n) { } // CLS-compliant, C1<long>.N is
                                       // accessible in C2 (extends C1<long>)
}
// Attempting to compile the example displays output like the following:
//       Generics4.cs(9,22): warning CS3001: Argument type 'C1<int>.N' is not CLS-compliant
//       Generics4.cs(18,22): warning CS3001: Argument type 'C1<int>.N' is not CLS-compliant
```

```vb
<Assembly:CLSCompliant(True)>

Public Class C1(Of T)
   Protected Class N
   End Class

   Protected Sub M1(n As C1(Of Integer).N)   ' Not CLS-compliant - C1<int>.N not
                                             ' accessible from within C1(Of T) in all
   End Sub                                   ' languages

   Protected Sub M2(n As C1(Of T).N)     ' CLS-compliant – C1(Of T).N accessible
   End Sub                               ' inside C1(Of T)
End Class

Public Class C2 : Inherits C1(Of Long)
   Protected Sub M3(n As C1(Of Integer).N)   ' Not CLS-compliant – C1(Of Integer).N is not
   End Sub                                   ' accessible in C2 (extends C1(Of Long))

   Protected Sub M4(n As C1(Of Long).N)
   End Sub
End Class
' Attempting to compile the example displays output like the following:
'    error BC30508: 'n' cannot expose type 'C1(Of Integer).N' in namespace
'    '<Default>' through class 'C1'.
'
'       Protected Sub M1(n As C1(Of Integer).N)   ' Not CLS-compliant - C1<int>.N not
'                             ~~~~~~~~~~~~~~~~
'    error BC30389: 'C1(Of T).N' is not accessible in this context because
'    it is 'Protected'.
'
'       Protected Sub M3(n As C1(Of Integer).N)   ' Not CLS-compliant - C1(Of Integer).N is not
'
'                             ~~~~~~~~~~~~~~~~
'
'    error BC30389: 'C1(Of T).N' is not accessible in this context because it is 'Protected'.
'
'       Protected Sub M4(n As C1(Of Long).N)
'                             ~~~~~~~~~~~~~
```

### <a name="constructors"></a><span data-ttu-id="8fc7a-572">构造函数</span><span class="sxs-lookup"><span data-stu-id="8fc7a-572">Constructors</span></span>

<span data-ttu-id="8fc7a-573">符合 CLS 的类和结构中的构造函数必须遵循下列规则：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-573">Constructors in CLS-compliant classes and structures must follow these rules:</span></span>

* <span data-ttu-id="8fc7a-574">派生类的构造函数必须先调用其基类的实例构造函数，然后才能访问继承的实例数据。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-574">A constructor of a derived class must call the instance constructor of its base class before it accesses inherited instance data.</span></span> <span data-ttu-id="8fc7a-575">存在此要求是因为基类构造函数并不由它们的派生类继承。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-575">This requirement is due to the fact that base class constructors are not inherited by their derived classes.</span></span> <span data-ttu-id="8fc7a-576">此规则不适用于不支持直接继承的结构。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-576">This rule does not apply to structures, which do not support direct inheritance.</span></span>

  <span data-ttu-id="8fc7a-577">通常，编译器独立地强制实施 CLS 遵从性的此规则，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-577">Typically, compilers enforce this rule independently of CLS compliance, as the following example shows.</span></span> <span data-ttu-id="8fc7a-578">它创建派生自 `Doctor` 类的 `Person` 类，但 `Doctor` 类无法调用 `Person` 类构造函数来初始化继承的实例字段。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-578">It creates a `Doctor` class that is derived from a `Person` class, but the `Doctor` class fails to call the `Person` class constructor to initialize inherited instance fields.</span></span>

    ```csharp
    using System;

    [assembly: CLSCompliant(true)]

    public class Person
    {
    private string fName, lName, _id;

    public Person(string firstName, string lastName, string id)
    {
        if (String.IsNullOrEmpty(firstName + lastName))
            throw new ArgumentNullException("Either a first name or a last name must be provided.");

        fName = firstName;
        lName = lastName;
        _id = id;
    }

    public string FirstName
    {
        get { return fName; }
    }

    public string LastName
    {
        get { return lName; }
    }

    public string Id
    {
        get { return _id; }
    }

    public override string ToString()
    {
        return String.Format("{0}{1}{2}", fName,
                            String.IsNullOrEmpty(fName) ?  "" : " ",
                            lName);
    }
    }

    public class Doctor : Person
    {
    public Doctor(string firstName, string lastName, string id)
    {
    }

    public override string ToString()
    {
        return "Dr. " + base.ToString();
    }
    }
    // Attempting to compile the example displays output like the following:
    //    ctor1.cs(45,11): error CS1729: 'Person' does not contain a constructor that takes 0
    //            arguments
    //    ctor1.cs(10,11): (Location of symbol related to previous error)
    ```

    ```vb
    <Assembly: CLSCompliant(True)>

    Public Class Person
       Private fName, lName, _id As String

       Public Sub New(firstName As String, lastName As String, id As String)
          If String.IsNullOrEmpty(firstName + lastName) Then
             Throw New ArgumentNullException("Either a first name or a last name must be provided.")
          End If

          fName = firstName
          lName = lastName
          _id = id
       End Sub

       Public ReadOnly Property FirstName As String
          Get
             Return fName
          End Get
       End Property

       Public ReadOnly Property LastName As String
          Get
             Return lName
          End Get
       End Property

       Public ReadOnly Property Id As String
          Get
             Return _id
          End Get
       End Property

       Public Overrides Function ToString() As String
          Return String.Format("{0}{1}{2}", fName,
                               If(String.IsNullOrEmpty(fName), "", " "),
                               lName)
       End Function
    End Class

    Public Class Doctor : Inherits Person
       Public Sub New(firstName As String, lastName As String, id As String)
       End Sub

       Public Overrides Function ToString() As String
          Return "Dr. " + MyBase.ToString()
       End Function
    End Class
    ' Attempting to compile the example displays output like the following:
    '    Ctor1.vb(46) : error BC30148: First statement of this 'Sub New' must be a call
    '    to 'MyBase.New' or 'MyClass.New' because base class 'Person' of 'Doctor' does
    '    not have an accessible 'Sub New' that can be called with no arguments.
    '
    '       Public Sub New()
    '                  ~~~
    ````

* <span data-ttu-id="8fc7a-579">只有在创建对象时才能调用对象构造函数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-579">An object constructor cannot be called except to create an object.</span></span> <span data-ttu-id="8fc7a-580">此外，不能将一个对象初始化两次。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-580">In addition, an object cannot be initialized twice.</span></span> <span data-ttu-id="8fc7a-581">例如，这意味着 `Object.MemberwiseClone` 不得调用构造函数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-581">For example, this means that `Object.MemberwiseClone` must not call constructors.</span></span>

### <a name="properties"></a><span data-ttu-id="8fc7a-582">属性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-582">Properties</span></span>

<span data-ttu-id="8fc7a-583">符合 CLS 的类型的属性必须遵循下列规则：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-583">Properties in CLS-compliant types must follow these rules:</span></span>

* <span data-ttu-id="8fc7a-584">属性必须具有 setter 和/或 getter。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-584">A property must have a setter, a getter, or both.</span></span> <span data-ttu-id="8fc7a-585">在程序集中，这些作为特殊方法实现，这意味着它们将显示为单独的方法（getter 命名为 `get`\_*propertyname*，setter 命名为 `set`\_*propertyname*），且在程序集元数据中标记为 `SpecialName`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-585">In an assembly, these are implemented as special methods, which means that they will appear as separate methods (the getter is named `get`\_*propertyname* and the setter is `set`\_*propertyname*) marked as `SpecialName` in the assembly's metadata.</span></span> <span data-ttu-id="8fc7a-586">C# 编译器会自动实施此规则，无需应用 <xref:System.CLSCompliantAttribute> 特性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-586">The C# compiler enforces this rule automatically without the need to apply the <xref:System.CLSCompliantAttribute> attribute.</span></span>

* <span data-ttu-id="8fc7a-587">属性的类型是属性 getter 的返回类型和 setter 的最后一个自变量。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-587">A property's type is the return type of the property getter and the last argument of the setter.</span></span> <span data-ttu-id="8fc7a-588">这些类型必须符合 CLS，并且不能通过引用将参数分配到属性中（即它们不能为托管指针）。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-588">These types must be CLS compliant, and arguments cannot be assigned to the property by reference (that is, they cannot be managed pointers).</span></span>

* <span data-ttu-id="8fc7a-589">如果属性包含 getter 和 setter 两者，则它们必须都是虚拟的、静态的或实例。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-589">If a property has both a getter and a setter, they must both be virtual, both static, or both instance.</span></span> <span data-ttu-id="8fc7a-590">C# 编译器通过它们的属性定义语法自动实施此规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-590">The C# compiler automatically enforces this rule through property definition syntax.</span></span>

### <a name="events"></a><span data-ttu-id="8fc7a-591">事件</span><span class="sxs-lookup"><span data-stu-id="8fc7a-591">Events</span></span>

<span data-ttu-id="8fc7a-592">事件由其名称和类型定义。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-592">An event is defined by its name and its type.</span></span> <span data-ttu-id="8fc7a-593">事件类型是用于指示事件的委托。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-593">The event type is a delegate that is used to indicate the event.</span></span> <span data-ttu-id="8fc7a-594">例如，`DbConnection.StateChange` 事件的类型为 `StateChangeEventHandler`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-594">For example, the `DbConnection.StateChange` event is of type `StateChangeEventHandler`.</span></span> <span data-ttu-id="8fc7a-595">除事件本身外，带有基于事件名称的名称的三种方法提供事件的实现并在程序集的元数据中标记为 `SpecialName`：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-595">In addition to the event itself, three methods with names based on the event name provide the event's implementation and are marked as `SpecialName` in the assembly's metadata:</span></span>

* <span data-ttu-id="8fc7a-596">用于添加事件处理程序的名为 `add`_*EventName* 的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-596">A method for adding an event handler, named `add`_*EventName*.</span></span> <span data-ttu-id="8fc7a-597">例如，`DbConnection.StateChange` 事件的事件订阅方法名为 `add_StateChange`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-597">For example, the event subscription method for the `DbConnection.StateChange` event is named `add_StateChange`.</span></span>

* <span data-ttu-id="8fc7a-598">用于移除事件处理程序的名为 `remove`_*EventName* 的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-598">A method for removing an event handler, named `remove`_*EventName*.</span></span> <span data-ttu-id="8fc7a-599">例如，`DbConnection.StateChange` 事件的移除方法名为 `remove_StateChange`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-599">For example, the removal method for the `DbConnection.StateChange` event is named `remove_StateChange`.</span></span>

* <span data-ttu-id="8fc7a-600">用于指示事件已发生的名为 `raise`\_EventName 的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-600">A method for indicating that the event has occurred, named `raise`\_*EventName*.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc7a-601">大多数关于事件的公共语言规范的规则都通过语言编译器实施，且对组件开发人员是透明的。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-601">Most of the Common Language Specification's rules regarding events are implemented by language compilers and are transparent to component developers.</span></span>

<span data-ttu-id="8fc7a-602">用于添加、移除和引发事件的方法必须拥有相同的可访问性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-602">The methods for adding, removing, and raising the event must have the same accessibility.</span></span> <span data-ttu-id="8fc7a-603">它们还必须都为静态、实例或虚拟的。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-603">They must also all be static, instance, or virtual.</span></span> <span data-ttu-id="8fc7a-604">用于添加和移除事件的方法具有一个类型为事件委托类型的参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-604">The methods for adding and removing an event have one parameter whose type is the event delegate type.</span></span> <span data-ttu-id="8fc7a-605">添加和移除方法必须同时存在或同时不存在。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-605">The add and remove methods must both be present or both be absent.</span></span>

<span data-ttu-id="8fc7a-606">如果两个读取之间的温度更改等于或超过阈值，则下面的示例将定义一个名为 `Temperature` 的类，该类会引发 `TemperatureChanged` 事件且符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-606">The following example defines a CLS-compliant class named `Temperature` that raises a `TemperatureChanged` event if the change in temperature between two readings equals or exceeds a threshold value.</span></span> <span data-ttu-id="8fc7a-607">`Temperature` 类显式定义 `raise_TemperatureChanged` 方法，以便其可以有选择地执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-607">The `Temperature` class explicitly defines a `raise_TemperatureChanged` method so that it can selectively execute event handlers.</span></span>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

[assembly: CLSCompliant(true)]

public class TemperatureChangedEventArgs : EventArgs
{
   private Decimal originalTemp;
   private Decimal newTemp;
   private DateTimeOffset when;

   public TemperatureChangedEventArgs(Decimal original, Decimal @new, DateTimeOffset time)
   {
      originalTemp = original;
      newTemp = @new;
      when = time;
   }

   public Decimal OldTemperature
   {
      get { return originalTemp; }
   }

   public Decimal CurrentTemperature
   {
      get { return newTemp; }
   }

   public DateTimeOffset Time
   {
      get { return when; }
   }
}

public delegate void TemperatureChanged(Object sender, TemperatureChangedEventArgs e);

public class Temperature
{
   private struct TemperatureInfo
   {
      public Decimal Temperature;
      public DateTimeOffset Recorded;
   }

   public event TemperatureChanged TemperatureChanged;

   private Decimal previous;
   private Decimal current;
   private Decimal tolerance;
   private List<TemperatureInfo> tis = new List<TemperatureInfo>();

   public Temperature(Decimal temperature, Decimal tolerance)
   {
      current = temperature;
      TemperatureInfo ti = new TemperatureInfo();
      ti.Temperature = temperature;
      tis.Add(ti);
      ti.Recorded = DateTimeOffset.UtcNow;
      this.tolerance = tolerance;
   }

   public Decimal CurrentTemperature
   {
      get { return current; }
      set {
         TemperatureInfo ti = new TemperatureInfo();
         ti.Temperature = value;
         ti.Recorded = DateTimeOffset.UtcNow;
         previous = current;
         current = value;
         if (Math.Abs(current - previous) >= tolerance)
            raise_TemperatureChanged(new TemperatureChangedEventArgs(previous, current, ti.Recorded));
      }
   }

   public void raise_TemperatureChanged(TemperatureChangedEventArgs eventArgs)
   {
      if (TemperatureChanged == null)
         return;

      foreach (TemperatureChanged d in TemperatureChanged.GetInvocationList()) {
         if (d.Method.Name.Contains("Duplicate"))
            Console.WriteLine("Duplicate event handler; event handler not executed.");
         else
            d.Invoke(this, eventArgs);
      }
   }
}

public class Example
{
   public Temperature temp;

   public static void Main()
   {
      Example ex = new Example();
   }

   public Example()
   {
      temp = new Temperature(65, 3);
      temp.TemperatureChanged += this.TemperatureNotification;
      RecordTemperatures();
      Example ex = new Example(temp);
      ex.RecordTemperatures();
   }

   public Example(Temperature t)
   {
      temp = t;
      RecordTemperatures();
   }

   public void RecordTemperatures()
   {
      temp.TemperatureChanged += this.DuplicateTemperatureNotification;
      temp.CurrentTemperature = 66;
      temp.CurrentTemperature = 63;
   }

   internal void TemperatureNotification(Object sender, TemperatureChangedEventArgs e)
   {
      Console.WriteLine("Notification 1: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature);
   }

   public void DuplicateTemperatureNotification(Object sender, TemperatureChangedEventArgs e)
   {
      Console.WriteLine("Notification 2: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature);
   }
}
```

```vb
Imports System.Collections
Imports System.Collections.Generic

<Assembly: CLSCompliant(True)>

Public Class TemperatureChangedEventArgs   : Inherits EventArgs
   Private originalTemp As Decimal
   Private newTemp As Decimal
   Private [when] As DateTimeOffset

   Public Sub New(original As Decimal, [new] As Decimal, [time] As DateTimeOffset)
      originalTemp = original
      newTemp = [new]
      [when] = [time]
   End Sub

   Public ReadOnly Property OldTemperature As Decimal
      Get
         Return originalTemp
      End Get
   End Property

   Public ReadOnly Property CurrentTemperature As Decimal
      Get
         Return newTemp
      End Get
   End Property

   Public ReadOnly Property [Time] As DateTimeOffset
      Get
         Return [when]
      End Get
   End Property
End Class

Public Delegate Sub TemperatureChanged(sender As Object, e As TemperatureChangedEventArgs)

Public Class Temperature
   Private Structure TemperatureInfo
      Dim Temperature As Decimal
      Dim Recorded As DateTimeOffset
   End Structure

   Public Event TemperatureChanged As TemperatureChanged

   Private previous As Decimal
   Private current As Decimal
   Private tolerance As Decimal
   Private tis As New List(Of TemperatureInfo)

   Public Sub New(temperature As Decimal, tolerance As Decimal)
      current = temperature
      Dim ti As New TemperatureInfo()
      ti.Temperature = temperature
      ti.Recorded = DateTimeOffset.UtcNow
      tis.Add(ti)
      Me.tolerance = tolerance
   End Sub

   Public Property CurrentTemperature As Decimal
      Get
         Return current
      End Get
      Set
         Dim ti As New TemperatureInfo
         ti.Temperature = value
         ti.Recorded = DateTimeOffset.UtcNow
         previous = current
         current = value
         If Math.Abs(current - previous) >= tolerance Then
            raise_TemperatureChanged(New TemperatureChangedEventArgs(previous, current, ti.Recorded))
         End If
      End Set
   End Property

   Public Sub raise_TemperatureChanged(eventArgs As TemperatureChangedEventArgs)
      If TemperatureChangedEvent Is Nothing Then Exit Sub

      Dim ListenerList() As System.Delegate = TemperatureChangedEvent.GetInvocationList()
      For Each d As TemperatureChanged In TemperatureChangedEvent.GetInvocationList()
         If d.Method.Name.Contains("Duplicate") Then
            Console.WriteLine("Duplicate event handler; event handler not executed.")
         Else
            d.Invoke(Me, eventArgs)
         End If
      Next
   End Sub
End Class

Public Class Example
   Public WithEvents temp As Temperature

   Public Shared Sub Main()
      Dim ex As New Example()
   End Sub

   Public Sub New()
      temp = New Temperature(65, 3)
      RecordTemperatures()
      Dim ex As New Example(temp)
      ex.RecordTemperatures()
   End Sub

   Public Sub New(t As Temperature)
      temp = t
      RecordTemperatures()
   End Sub

   Public Sub RecordTemperatures()
      temp.CurrentTemperature = 66
      temp.CurrentTemperature = 63

   End Sub

   Friend Shared Sub TemperatureNotification(sender As Object, e As TemperatureChangedEventArgs) _
          Handles temp.TemperatureChanged
      Console.WriteLine("Notification 1: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature)
   End Sub

   Friend Shared Sub DuplicateTemperatureNotification(sender As Object, e As TemperatureChangedEventArgs) _
          Handles temp.TemperatureChanged
      Console.WriteLine("Notification 2: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature)
   End Sub
End Class
```

### <a name="overloads"></a><span data-ttu-id="8fc7a-608">Overloads</span><span class="sxs-lookup"><span data-stu-id="8fc7a-608">Overloads</span></span>

<span data-ttu-id="8fc7a-609">公共语言规范对重载成员有下列要求：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-609">The Common Language Specification imposes the following requirements on overloaded members:</span></span>

* <span data-ttu-id="8fc7a-610">成员可以根据参数数量和任何参数的类型进行重载。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-610">Members can be overloaded based on the number of parameters and the type of any parameter.</span></span> <span data-ttu-id="8fc7a-611">在重载间进行区分时，不考虑应用于方法或其参数的调用约定、返回类型、自定义修饰符，也不考虑是按照值还是引用传递参数。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-611">Calling convention, return type, custom modifiers applied to the method or its parameter, and whether parameters are passed by value or by reference are not considered when differentiating between overloads.</span></span> <span data-ttu-id="8fc7a-612">有关示例，请参阅[命名约定](#naming-conventions)部分中名称在范围内必须是唯一的代码需求。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-612">For an example, see the code for the requirement that names must be unique within a scope in the [Naming conventions](#naming-conventions) section.</span></span>

* <span data-ttu-id="8fc7a-613">只可重载属性和方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-613">Only properties and methods can be overloaded.</span></span> <span data-ttu-id="8fc7a-614">无法重载字段和事件。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-614">Fields and events cannot be overloaded.</span></span>

* <span data-ttu-id="8fc7a-615">泛型方法可以基于其泛型参数的数目进行重载。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-615">Generic methods can be overloaded based on the number of their generic parameters.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc7a-616">`op_Explicit` 和 `op_Implicit` 运算符是返回值不被视为重载决策的方法签名的一部分的规则的例外情况。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-616">The `op_Explicit` and `op_Implicit` operators are exceptions to the rule that return value is not considered part of a method signature for overload resolution.</span></span> <span data-ttu-id="8fc7a-617">可以基于这两个运算符的参数和返回值对其进行重载。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-617">These two operators can be overloaded based on both their parameters and their return value.</span></span>

### <a name="exceptions"></a><span data-ttu-id="8fc7a-618">异常</span><span class="sxs-lookup"><span data-stu-id="8fc7a-618">Exceptions</span></span>

<span data-ttu-id="8fc7a-619">异常对象必须从 [System.Exception](xref:System.Exception) 派生，或从派生自 `System.Exception` 的另一个类型派生。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-619">Exception objects must derive from [System.Exception](xref:System.Exception) or from another type derived from `System.Exception`.</span></span> <span data-ttu-id="8fc7a-620">下面的示例说明了当名为 `ErrorClass` 的自定义类用于异常处理时产生的编译器错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-620">The following example illustrates the compiler error that results when a custom class named `ErrorClass` is used for exception handling.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ErrorClass
{
   string msg;

   public ErrorClass(string errorMessage)
   {
      msg = errorMessage;
   }

   public string Message
   {
      get { return msg; }
   }
}

public static class StringUtilities
{
   public static string[] SplitString(this string value, int index)
   {
      if (index < 0 | index > value.Length) {
         ErrorClass badIndex = new ErrorClass("The index is not within the string.");
         throw badIndex;
      }
      string[] retVal = { value.Substring(0, index - 1),
                          value.Substring(index) };
      return retVal;
   }
}
// Compilation produces a compiler error like the following:
//    Exceptions1.cs(26,16): error CS0155: The type caught or thrown must be derived from
//            System.Exception
```

```vb
Imports System.Runtime.CompilerServices

<Assembly: CLSCompliant(True)>

Public Class ErrorClass
   Dim msg As String

   Public Sub New(errorMessage As String)
      msg = errorMessage
   End Sub

   Public ReadOnly Property Message As String
      Get
         Return msg
      End Get
   End Property
End Class

Public Module StringUtilities
   <Extension()> Public Function SplitString(value As String, index As Integer) As String()
      If index < 0 Or index > value.Length Then
         Dim BadIndex As New ErrorClass("The index is not within the string.")
         Throw BadIndex
      End If
      Dim retVal() As String = { value.Substring(0, index - 1),
                                 value.Substring(index) }
      Return retVal
   End Function
End Module
' Compilation produces a compiler error like the following:
'    Exceptions1.vb(27) : error BC30665: 'Throw' operand must derive from 'System.Exception'.
'
'             Throw BadIndex
'             ~~~~~~~~~~~~~~
```

<span data-ttu-id="8fc7a-621">若要更正此错误，`ErrorClass` 类必须继承自 `System.Exception`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-621">To correct this error, the `ErrorClass` class must inherit from `System.Exception`.</span></span> <span data-ttu-id="8fc7a-622">此外，必须重写 Message 属性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-622">In addition, the Message property must be overridden.</span></span> <span data-ttu-id="8fc7a-623">下面的示例更正这些错误以定义符合 CLS 的 `ErrorClass` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-623">The following example corrects these errors to define an `ErrorClass` class that is CLS-compliant.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ErrorClass : Exception
{
   string msg;

   public ErrorClass(string errorMessage)
   {
      msg = errorMessage;
   }

   public override string Message
   {
      get { return msg; }
   }
}

public static class StringUtilities
{
   public static string[] SplitString(this string value, int index)
   {
      if (index < 0 | index > value.Length) {
         ErrorClass badIndex = new ErrorClass("The index is not within the string.");
         throw badIndex;
      }
      string[] retVal = { value.Substring(0, index - 1),
                          value.Substring(index) };
      return retVal;
   }
}
```

```vb
Imports System.Runtime.CompilerServices

<Assembly: CLSCompliant(True)>

Public Class ErrorClass : Inherits Exception
   Dim msg As String

   Public Sub New(errorMessage As String)
      msg = errorMessage
   End Sub

   Public Overrides ReadOnly Property Message As String
      Get
         Return msg
      End Get
   End Property
End Class

Public Module StringUtilities
   <Extension()> Public Function SplitString(value As String, index As Integer) As String()
      If index < 0 Or index > value.Length Then
         Dim BadIndex As New ErrorClass("The index is not within the string.")
         Throw BadIndex
      End If
      Dim retVal() As String = { value.Substring(0, index - 1),
                                 value.Substring(index) }
      Return retVal
   End Function
End Module
```

### <a name="attributes"></a><span data-ttu-id="8fc7a-624">特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-624">Attributes</span></span>

<span data-ttu-id="8fc7a-625">在 .NET 程序集中，自定义特性提供了一个可扩展机制，用于存储自定义特性和检索有关编程对象（如程序集、类型、成员和方法参数）的元数据。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-625">In .NET assemblies, custom attributes provide an extensible mechanism for storing custom attributes and retrieving metadata about programming objects, such as assemblies, types, members, and method parameters.</span></span> <span data-ttu-id="8fc7a-626">自定义特性必须从 [System.Attribute](xref:System.Attribute) 派生或从派生自 `System.Attribute` 的类型派生。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-626">Custom attributes must derive from [System.Attribute](xref:System.Attribute) or from a type derived from `System.Attribute`.</span></span>

<span data-ttu-id="8fc7a-627">下面的示例与此规则冲突。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-627">The following example violates this rule.</span></span> <span data-ttu-id="8fc7a-628">它定义了不是从 `NumericAttribute` 派生的 `System.Attribute` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-628">It defines a `NumericAttribute` class that does not derive from `System.Attribute`.</span></span> <span data-ttu-id="8fc7a-629">编译器错误仅当应用不符合 CLS 的特性时会出现，而在定义类时不会出现。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-629">A compiler error results only when the non-CLS-compliant attribute is applied, not when the class is defined.</span></span>

```csharp
using System;

[assembly: CLSCompliant(true)]

[AttributeUsageAttribute(AttributeTargets.Class | AttributeTargets.Struct)]
public class NumericAttribute
{
   private bool _isNumeric;

   public NumericAttribute(bool isNumeric)
   {
      _isNumeric = isNumeric;
   }

   public bool IsNumeric
   {
      get { return _isNumeric; }
   }
}

[Numeric(true)] public struct UDouble
{
   double Value;
}
// Compilation produces a compiler error like the following:
//    Attribute1.cs(22,2): error CS0616: 'NumericAttribute' is not an attribute class
//    Attribute1.cs(7,14): (Location of symbol related to previous error)
```

```vb
<Assembly: CLSCompliant(True)>

<AttributeUsageAttribute(AttributeTargets.Class Or AttributeTargets.Struct)> _
Public Class NumericAttribute
   Private _isNumeric As Boolean

   Public Sub New(isNumeric As Boolean)
      _isNumeric = isNumeric
   End Sub

   Public ReadOnly Property IsNumeric As Boolean
      Get
         Return _isNumeric
      End Get
   End Property
End Class

<Numeric(True)> Public Structure UDouble
   Dim Value As Double
End Structure
' Compilation produces a compiler error like the following:
'    error BC31504: 'NumericAttribute' cannot be used as an attribute because it
'    does not inherit from 'System.Attribute'.
'
'    <Numeric(True)> Public Structure UDouble
'     ~~~~~~~~~~~~~
```

<span data-ttu-id="8fc7a-630">构造函数或符合 CLS 的特性的属性只能公开以下类型：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-630">The constructor or the properties of a CLS-compliant attribute can expose only the following types:</span></span>

* [<span data-ttu-id="8fc7a-631">布尔值</span><span class="sxs-lookup"><span data-stu-id="8fc7a-631">Boolean</span></span>](xref:System.Boolean)

* [<span data-ttu-id="8fc7a-632">Byte</span><span class="sxs-lookup"><span data-stu-id="8fc7a-632">Byte</span></span>](xref:System.Byte)

* [<span data-ttu-id="8fc7a-633">Char</span><span class="sxs-lookup"><span data-stu-id="8fc7a-633">Char</span></span>](xref:System.Char)

* [<span data-ttu-id="8fc7a-634">双精度</span><span class="sxs-lookup"><span data-stu-id="8fc7a-634">Double</span></span>](xref:System.Double)

* [<span data-ttu-id="8fc7a-635">Int16</span><span class="sxs-lookup"><span data-stu-id="8fc7a-635">Int16</span></span>](xref:System.Int16)

* [<span data-ttu-id="8fc7a-636">Int32</span><span class="sxs-lookup"><span data-stu-id="8fc7a-636">Int32</span></span>](xref:System.Int32)

* [<span data-ttu-id="8fc7a-637">Int64</span><span class="sxs-lookup"><span data-stu-id="8fc7a-637">Int64</span></span>](xref:System.Int64)

* [<span data-ttu-id="8fc7a-638">单精度</span><span class="sxs-lookup"><span data-stu-id="8fc7a-638">Single</span></span>](xref:System.Single)

* [<span data-ttu-id="8fc7a-639">字符串</span><span class="sxs-lookup"><span data-stu-id="8fc7a-639">String</span></span>](xref:System.String)

* [<span data-ttu-id="8fc7a-640">Type</span><span class="sxs-lookup"><span data-stu-id="8fc7a-640">Type</span></span>](xref:System.Type)

* <span data-ttu-id="8fc7a-641">基础类型为 `Byte`、`Int16`、`Int32` 或 `Int64` 的任意枚举类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-641">Any enumeration type whose underlying type is `Byte`, `Int16`, `Int32`, or `Int64`.</span></span>

<span data-ttu-id="8fc7a-642">下面的示例定义了从 [Attribute](xref:System.Attribute) 派生的 `DescriptionAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-642">The following example defines a `DescriptionAttribute` class that derives from [Attribute](xref:System.Attribute).</span></span> <span data-ttu-id="8fc7a-643">类构造函数具有 `Descriptor` 类型的参数，因此，该类不符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-643">The class constructor has a parameter of type `Descriptor`, so the class is not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-644">C# 编译器会发出警告，但编译成功。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-644">The C# compiler emits a warning but compiles successfully.</span></span>

```csharp
using System;

[assembly:CLSCompliantAttribute(true)]

public enum DescriptorType { type, member };

public class Descriptor
{
   public DescriptorType Type;
   public String Description;
}

[AttributeUsage(AttributeTargets.All)]
public class DescriptionAttribute : Attribute
{
   private Descriptor desc;

   public DescriptionAttribute(Descriptor d)
   {
      desc = d;
   }

   public Descriptor Descriptor
   { get { return desc; } }
}
// Attempting to compile the example displays output like the following:
//       warning CS3015: 'DescriptionAttribute' has no accessible
//               constructors which use only CLS-compliant types
```

```vb
<Assembly:CLSCompliantAttribute(True)>

Public Enum DescriptorType As Integer
   Type = 0
   Member = 1
End Enum

Public Class Descriptor
   Public Type As DescriptorType
   Public Description As String
End Class

<AttributeUsage(AttributeTargets.All)> _
Public Class DescriptionAttribute : Inherits Attribute
   Private desc As Descriptor

   Public Sub New(d As Descriptor)
      desc = d
   End Sub

   Public ReadOnly Property Descriptor As Descriptor
      Get
         Return desc
      End Get
   End Property
End Class
```

## <a name="the-clscompliantattribute-attribute"></a><span data-ttu-id="8fc7a-645">CLSCompliantAttribute 特性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-645">The CLSCompliantAttribute attribute</span></span>

<span data-ttu-id="8fc7a-646">[CLSCompliantAttribute](xref:System.CLSCompliantAttribute) 特性用于指示程序元素是否使用公共语言规范进行编译。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-646">The [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) attribute is used to indicate whether a program element complies with the Common Language Specification.</span></span> <span data-ttu-id="8fc7a-647">`CLSCompliantAttribute.CLSCompliantAttribute(Boolean)` 构造函数包含一个必需的参数 *isCompliant*，此参数指示该程序元素是否符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-647">The `CLSCompliantAttribute.CLSCompliantAttribute(Boolean)` constructor includes a single required parameter, *isCompliant*, that indicates whether the program element is CLS-compliant.</span></span>

<span data-ttu-id="8fc7a-648">编译时，编译器检测到假定为符合 CLS 的不合规元素，并发出警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-648">At compile time, the compiler detects non-compliant elements that are presumed to be CLS-compliant and emits a warning.</span></span> <span data-ttu-id="8fc7a-649">编译器不会对显式声明为不符合标准的类型或成员发出警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-649">The compiler does not emit warnings for types or members that are explicitly declared to be non-compliant.</span></span>

<span data-ttu-id="8fc7a-650">组件开发人员可以通过两种方法使用 `CLSCompliantAttribute` 特性：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-650">Component developers can use the `CLSCompliantAttribute` attribute in two ways:</span></span>

* <span data-ttu-id="8fc7a-651">定义由组件公开的公共接口的符合 CLS 的部件以及不符合 CLS 的部件。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-651">To define the parts of the public interface exposed by a component that are CLS-compliant and the parts that are not CLS-compliant.</span></span> <span data-ttu-id="8fc7a-652">如果特性用于将特定程序元素标记为符合 CLS，则使用该特性可保证能通过面向 .NET 的所有语言和工具访问这些元素。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-652">When the attribute is used to mark particular program elements as CLS-compliant, its use guarantees that those elements are accessible from all languages and tools that target .NET.</span></span>

* <span data-ttu-id="8fc7a-653">确保组件库的公共接口仅公开符合 CLS 的程序元素。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-653">To ensure that the component library's public interface exposes only program elements that are CLS-compliant.</span></span> <span data-ttu-id="8fc7a-654">如果元素不符合 CLS，则编译器通常会发出一个警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-654">If elements are not CLS-compliant, compilers will generally issue a warning.</span></span>

> [!WARNING]
> <span data-ttu-id="8fc7a-655">在某些情况下，语言编译器执行符合 CLS 的规则，而不管是否使用 `CLSCompliantAttribute` 特性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-655">In some cases, language compilers enforce CLS-compliant rules regardless of whether the `CLSCompliantAttribute` attribute is used.</span></span> <span data-ttu-id="8fc7a-656">例如，在接口中定义 `*static` 成员会违反 CLS 规则。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-656">For example, defining a `*static` member in an interface violates a CLS rule.</span></span> <span data-ttu-id="8fc7a-657">但是，如果在接口中定义 `*static` 成员，C# 编译器会显示错误消息且无法编译应用。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-657">However, if you define a `*static` member in an interface, the C# compiler displays an error message and fails to compile the app.</span></span>

<span data-ttu-id="8fc7a-658">`CLSCompliantAttribute` 特性标记为具有 `AttributeTargets.All` 值的 [AttributeUsageAttribute](xref:System.AttributeUsageAttribute) 特性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-658">The `CLSCompliantAttribute` attribute is marked with an [AttributeUsageAttribute](xref:System.AttributeUsageAttribute) attribute that has a value of `AttributeTargets.All`.</span></span> <span data-ttu-id="8fc7a-659">利用此值，您可以将 `CLSCompliantAttribute` 特性应用于任何程序元素，包括程序集、模块、类型（类、结构、枚举、接口和委托）、类型成员（构造函数、方法、属性、字段和事件）、参数、泛型参数和返回值。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-659">This value allows you to apply the `CLSCompliantAttribute` attribute to any program element, including assemblies, modules, types (classes, structures, enumerations, interfaces, and delegates), type members (constructors, methods, properties, fields, and events), parameters, generic parameters, and return values.</span></span> <span data-ttu-id="8fc7a-660">但实际上，您只应将该特性应用于程序集、类型和类型成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-660">However, in practice, you should apply the attribute only to assemblies, types, and type members.</span></span> <span data-ttu-id="8fc7a-661">否则，编译器在库的公共接口中遇到不符合标准的参数、泛型参数或返回值时，将忽略此特性并继续生成编译器警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-661">Otherwise, compilers ignore the attribute and continue to generate compiler warnings whenever they encounter a non-compliant parameter, generic parameter, or return value in your library's public interface.</span></span>

<span data-ttu-id="8fc7a-662">`CLSCompliantAttribute` 特性的值由包含的程序元素继承。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-662">The value of the `CLSCompliantAttribute` attribute is inherited by contained program elements.</span></span> <span data-ttu-id="8fc7a-663">例如，如果程序集标记为符合 CLS，则其类型也符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-663">For example, if an assembly is marked as CLS-compliant, its types are also CLS-compliant.</span></span> <span data-ttu-id="8fc7a-664">如果类型标记为符合 CLS，则其嵌套的类型和成员也符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-664">If a type is marked as CLS-compliant, its nested types and members are also CLS-compliant.</span></span>

<span data-ttu-id="8fc7a-665">您可以通过将 `CLSCompliantAttribute` 特性应用到包含的编程元素来显式重写继承的遵从性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-665">You can explicitly override the inherited compliance by applying the `CLSCompliantAttribute` attribute to a contained program element.</span></span> <span data-ttu-id="8fc7a-666">例如，可以使用 isCompliant 值为 `false` 的 `CLSCompliantAttribute` 特性来定义符合标准的程序集中不符合标准的类型，还可以使用 isComplian 值为 `true` 的特性来定义不符合标准的程序集中符合标准的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-666">For example, you can use the `CLSCompliantAttribute` attribute with an *isCompliant* value of `false` to define a non-compliant type in a compliant assembly, and you can use the attribute with an *isCompliant* value of `true` to define a compliant type in a non-compliant assembly.</span></span> <span data-ttu-id="8fc7a-667">您还可以在符合标准的类型中定义不符合标准的成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-667">You can also define non-compliant members in a compliant type.</span></span> <span data-ttu-id="8fc7a-668">但是，不符合标准的类型无法拥有符合标准的成员，因此无法使用 *isCompliant* 值为 `true` 的特性从一个不符合标准的类型重写继承。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-668">However, a non-compliant type cannot have compliant members, so you cannot use the attribute with an *isCompliant* value of `true` to override inheritance from a non-compliant type.</span></span>

<span data-ttu-id="8fc7a-669">在开发组件时，应始终使用 `CLSCompliantAttribute` 特性来指示您的程序集、其类型及其成员是否符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-669">When you are developing components, you should always use the `CLSCompliantAttribute` attribute to indicate whether your assembly, its types, and its members are CLS-compliant.</span></span>

<span data-ttu-id="8fc7a-670">创建符合 CLS 的组件：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-670">To create CLS-compliant components:</span></span>

1. <span data-ttu-id="8fc7a-671">使用 `CLSCompliantAttribute` 将程序集标记为符合 CLS。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-671">Use the `CLSCompliantAttribute` to mark you assembly as CLS-compliant.</span></span>

2. <span data-ttu-id="8fc7a-672">将程序集中不符合 CLS 的所有公开的类型标记为不符合标准。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-672">Mark any publicly exposed types in the assembly that are not CLS-compliant as non-compliant.</span></span>

3. <span data-ttu-id="8fc7a-673">将符合 CLS 的类型中的所有公开的成员标记为不符合标准。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-673">Mark any publicly exposed members in CLS-compliant types as non-compliant.</span></span>

4. <span data-ttu-id="8fc7a-674">为不符合 CLS 的成员提供符合 CLS 的替代项。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-674">Provide a CLS-compliant alternative for non-CLS-compliant members.</span></span>

<span data-ttu-id="8fc7a-675">如果已成功标记所有不符合标准的类型和成员，您的编译器不会发出任何不符合警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-675">If you've successfully marked all your non-compliant types and members, your compiler should not emit any non-compliance warnings.</span></span> <span data-ttu-id="8fc7a-676">但是，您应指出哪些成员不符合 CLS 并在产品文档中列出其不符合 CLS 的替代项。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-676">However, you should indicate which members are not CLS-compliant and list their CLS-compliant alternatives in your product documentation.</span></span>

<span data-ttu-id="8fc7a-677">下面的示例使用 `CLSCompliantAttribute` 特性定义符合 CLS 的程序集和类型 `CharacterUtilities`，该类型具有两个不符合 CLS 的成员。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-677">The following example uses the `CLSCompliantAttribute` attribute to define a CLS-compliant assembly and a type, `CharacterUtilities`, that has two non-CLS-compliant members.</span></span> <span data-ttu-id="8fc7a-678">由于这两个成员标记有 `CLSCompliant(false)` 特性，因此编译器不生成任何警告。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-678">Because both members are tagged with the `CLSCompliant(false)` attribute, the compiler produces no warnings.</span></span> <span data-ttu-id="8fc7a-679">该类还为两种方法提供符合 CLS 的替代项。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-679">The class also provides a CLS-compliant alternative for both methods.</span></span> <span data-ttu-id="8fc7a-680">通常，我们只向 `ToUTF16` 方法添加两个重载，以便提供符合 CLS 的替代项。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-680">Ordinarily, we would just add two overloads to the `ToUTF16` method to provide CLS-compliant alternatives.</span></span> <span data-ttu-id="8fc7a-681">但是，由于无法基于返回值重载这些方法，因此符合 CLS 的方法的名称不同于不符合标准的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-681">However, because methods cannot be overloaded based on return value, the names of the CLS-compliant methods are different from the names of the non-compliant methods.</span></span>

```csharp
using System;
using System.Text;

[assembly:CLSCompliant(true)]

public class CharacterUtilities
{
   [CLSCompliant(false)] public static ushort ToUTF16(String s)
   {
      s = s.Normalize(NormalizationForm.FormC);
      return Convert.ToUInt16(s[0]);
   }

   [CLSCompliant(false)] public static ushort ToUTF16(Char ch)
   {
      return Convert.ToUInt16(ch);
   }

   // CLS-compliant alternative for ToUTF16(String).
   public static int ToUTF16CodeUnit(String s)
   {
      s = s.Normalize(NormalizationForm.FormC);
      return (int) Convert.ToUInt16(s[0]);
   }

   // CLS-compliant alternative for ToUTF16(Char).
   public static int ToUTF16CodeUnit(Char ch)
   {
      return Convert.ToInt32(ch);
   }

   public bool HasMultipleRepresentations(String s)
   {
      String s1 = s.Normalize(NormalizationForm.FormC);
      return s.Equals(s1);
   }

   public int GetUnicodeCodePoint(Char ch)
   {
      if (Char.IsSurrogate(ch))
         throw new ArgumentException("ch cannot be a high or low surrogate.");

      return Char.ConvertToUtf32(ch.ToString(), 0);
   }

   public int GetUnicodeCodePoint(Char[] chars)
   {
      if (chars.Length > 2)
         throw new ArgumentException("The array has too many characters.");

      if (chars.Length == 2) {
         if (! Char.IsSurrogatePair(chars[0], chars[1]))
            throw new ArgumentException("The array must contain a low and a high surrogate.");
         else
            return Char.ConvertToUtf32(chars[0], chars[1]);
      }
      else {
         return Char.ConvertToUtf32(chars.ToString(), 0);
      }
   }
}
```

```vb
Imports System.Text

<Assembly:CLSCompliant(True)>

Public Class CharacterUtilities
   <CLSCompliant(False)> Public Shared Function ToUTF16(s As String) As UShort
      s = s.Normalize(NormalizationForm.FormC)
      Return Convert.ToUInt16(s(0))
   End Function

   <CLSCompliant(False)> Public Shared Function ToUTF16(ch As Char) As UShort
      Return Convert.ToUInt16(ch)
   End Function

   ' CLS-compliant alternative for ToUTF16(String).
   Public Shared Function ToUTF16CodeUnit(s As String) As Integer
      s = s.Normalize(NormalizationForm.FormC)
      Return CInt(Convert.ToInt16(s(0)))
   End Function

   ' CLS-compliant alternative for ToUTF16(Char).
   Public Shared Function ToUTF16CodeUnit(ch As Char) As Integer
      Return Convert.ToInt32(ch)
   End Function

   Public Function HasMultipleRepresentations(s As String) As Boolean
      Dim s1 As String = s.Normalize(NormalizationForm.FormC)
      Return s.Equals(s1)
   End Function

   Public Function GetUnicodeCodePoint(ch As Char) As Integer
      If Char.IsSurrogate(ch) Then
         Throw New ArgumentException("ch cannot be a high or low surrogate.")
      End If
      Return Char.ConvertToUtf32(ch.ToString(), 0)
   End Function

   Public Function GetUnicodeCodePoint(chars() As Char) As Integer
      If chars.Length > 2 Then
         Throw New ArgumentException("The array has too many characters.")
      End If
      If chars.Length = 2 Then
         If Not Char.IsSurrogatePair(chars(0), chars(1)) Then
            Throw New ArgumentException("The array must contain a low and a high surrogate.")
         Else
            Return Char.ConvertToUtf32(chars(0), chars(1))
         End If
      Else
         Return Char.ConvertToUtf32(chars.ToString(), 0)
      End If
   End Function
End Class
```

<span data-ttu-id="8fc7a-682">如果您开发的是应用程序而不是库（即，如果不公开可由其他应用程序开发人员使用的类型或成员），则只有在您的语言不支持程序元素时，您的应用程序使用的程序元素的 CLS 遵从性才会引起关注。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-682">If you are developing an app rather than a library (that is, if you aren't exposing types or members that can be consumed by other app developers), the CLS compliance of the program elements that your app consumes are of interest only if your language does not support them.</span></span> <span data-ttu-id="8fc7a-683">在这种情况下，当您尝试使用不符合 CLS 的元素时，您的语言编译器将生成错误。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-683">In that case, your language compiler will generate an error when you try to use a non-CLS-compliant element.</span></span>

## <a name="cross-language-interoperability"></a><span data-ttu-id="8fc7a-684">跨语言互操作性</span><span class="sxs-lookup"><span data-stu-id="8fc7a-684">Cross-language interoperability</span></span>

<span data-ttu-id="8fc7a-685">语言独立性可能有许多含义。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-685">Language independence has a number of possible meanings.</span></span> <span data-ttu-id="8fc7a-686">其中一种含义涉及到从使用一种语言编写的应用取用以另一种语言编写的类型。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-686">One meaning involves seamlessly consuming types written in one language from an app written in another language.</span></span> <span data-ttu-id="8fc7a-687">本文介绍第二个含义，涉及将用多种语言编写的代码组合到一个 .NET 程序集。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-687">A second meaning, which is the focus of this article, involves combining code written in multiple languages into a single .NET assembly.</span></span>

<span data-ttu-id="8fc7a-688">以下示例通过创建一个名为 Utilities.dll 的包含两个类（`NumericLib` 和 `StringLib`）的类库演示了跨语言互操作性。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-688">The following example illustrates cross-language interoperability by creating a class library named Utilities.dll that includes two classes, `NumericLib` and `StringLib`.</span></span> <span data-ttu-id="8fc7a-689">`NumericLib` 类用 C# 编写类，`StringLib` 类用 Visual Basic 编写。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-689">The `NumericLib` class is written in C#, and the `StringLib` class is written in Visual Basic.</span></span> <span data-ttu-id="8fc7a-690">以下是 `StringUtil.vb` 的源代码，该源代码在其 `StringLib` 类中包含单个成员 `ToTitleCase`。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-690">Here's the source code for `StringUtil.vb`, which includes a single member, `ToTitleCase`, in its `StringLib` class.</span></span>

```vb
Imports System.Collections.Generic
Imports System.Runtime.CompilerServices

Public Module StringLib
   Private exclusions As List(Of String)

   Sub New()
      Dim words() As String = { "a", "an", "and", "of", "the" }
      exclusions = New List(Of String)
      exclusions.AddRange(words)
   End Sub

   <Extension()> _
   Public Function ToTitleCase(title As String) As String
      Dim words() As String = title.Split()
      Dim result As String = String.Empty

      For ctr As Integer = 0 To words.Length - 1
         Dim word As String = words(ctr)
         If ctr = 0 OrElse Not exclusions.Contains(word.ToLower()) Then
            result += word.Substring(0, 1).ToUpper() + _
                      word.Substring(1).ToLower()
         Else
            result += word.ToLower()
         End If
         If ctr <= words.Length - 1 Then
            result += " "
         End If
      Next
      Return result
   End Function
End Module
```

<span data-ttu-id="8fc7a-691">以下是 NumberUtil.cs 的源代码，定义具有 `NumericLib` 和 `IsEven` 两个成员的 `NearZero` 类。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-691">Here's the source code for NumberUtil.cs, which defines a `NumericLib` class that has two members, `IsEven` and `NearZero`.</span></span>

```csharp
using System;

public static class NumericLib
{
   public static bool IsEven(this IConvertible number)
   {
      if (number is Byte ||
          number is SByte ||
          number is Int16 ||
          number is UInt16 ||
          number is Int32 ||
          number is UInt32 ||
          number is Int64)
         return ((long) number) % 2 == 0;
      else if (number is UInt64)
         return ((ulong) number) %2 == 0;
      else
         throw new NotSupportedException("IsEven called for a non-integer value.");
   }

   public static bool NearZero(double number)
   {
      return number < .00001;
   }
}
```

<span data-ttu-id="8fc7a-692">若要将两个类打包到单个程序集中，必须将它们编译到模块中。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-692">To package the two classes in a single assembly, you must compile them into modules.</span></span> <span data-ttu-id="8fc7a-693">要将 Visual Basic 源代码文件编译到模块，请使用此命令：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-693">To compile the Visual Basic source code file into a module, use this command:</span></span>

```console
vbc /t:module StringUtil.vb
```

<span data-ttu-id="8fc7a-694">要将 C# 源代码文件编译到模块，请使用此命令：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-694">To compile the C# source code file into a module, use this command:</span></span>

```console
csc /t:module NumberUtil.cs
```

<span data-ttu-id="8fc7a-695">然后，使用链接工具 (Link.exe) 将两个模块编译到一个程序集：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-695">You then use the Link tool (Link.exe) to compile the two modules into an assembly:</span></span>

```console
link numberutil.netmodule stringutil.netmodule /out:UtilityLib.dll /dll
```

<span data-ttu-id="8fc7a-696">然后以下实例调用 `NumericLib.NearZero` 和 `StringLib.ToTitleCase` 方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-696">The following example then calls the `NumericLib.NearZero` and `StringLib.ToTitleCase` methods.</span></span> <span data-ttu-id="8fc7a-697">Visual Basic 代码和 C# 代码都能够访问这两个类中的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc7a-697">Both the Visual Basic code and the C# code are able to access the methods in both classes.</span></span>

```csharp
using System;

public class Example
{
   public static void Main()
   {
      Double dbl = 0.0 - Double.Epsilon;
      Console.WriteLine(NumericLib.NearZero(dbl));

      string s = "war and peace";
      Console.WriteLine(s.ToTitleCase());
   }
}
// The example displays the following output:
//       True
//       War and Peace
```

```vb
Module Example
   Public Sub Main()
      Dim dbl As Double = 0.0 - Double.Epsilon
      Console.WriteLine(NumericLib.NearZero(dbl))

      Dim s As String = "war and peace"
      Console.WriteLine(s.ToTitleCase())
   End Sub
End Module
' The example displays the following output:
'       True
'       War and Peace
```

<span data-ttu-id="8fc7a-698">要编译 Visual Basic 代码，请使用此命令：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-698">To compile the Visual Basic code, use this command:</span></span>

```console
vbc example.vb /r:UtilityLib.dll
```

<span data-ttu-id="8fc7a-699">要使用 C# 进行编译，请将编译器的名称从 vbc 更改为 csc，将文件扩展名从 .vb 更改为 .cs：</span><span class="sxs-lookup"><span data-stu-id="8fc7a-699">To compile with C#, change the name of the compiler from vbc to csc, and change the file extension from .vb to .cs:</span></span>

```console
csc example.cs /r:UtilityLib.dll
```
