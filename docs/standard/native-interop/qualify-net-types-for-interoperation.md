---
title: 为 COM 互操作限定 .NET 类型
description: 本文提供了一些指导原则，可帮助你为 COM 互操作向 COM 应用程序公开 .NET 程序集中的类型。
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET components to COM
- COM interop, qualifying .NET types
- qualifying .NET types for interoperation
- interoperation with unmanaged code, qualifying .NET types
- interoperation with unmanaged code, exposing .NET components
- COM interop, exposing COM components
ms.assetid: 4b8afb52-fb8d-4e65-b47c-fd82956a3cdd
ms.openlocfilehash: 3fa9f0d5d8dd4d532fc510a1d946eddf32016748
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187757"
---
# <a name="qualifying-net-types-for-com-interoperation"></a><span data-ttu-id="d4791-103">为 COM 互操作限定 .NET 类型</span><span class="sxs-lookup"><span data-stu-id="d4791-103">Qualifying .NET Types for COM Interoperation</span></span>
<span data-ttu-id="d4791-104">若要向 COM 应用程序公开程序集中的类型，请考虑 COM 互操作在设计时的需求。</span><span class="sxs-lookup"><span data-stu-id="d4791-104">If you intend to expose types in an assembly to COM applications, consider the requirements of COM interop at design time.</span></span> <span data-ttu-id="d4791-105">如果符合以下准则，托管类型（类、接口、结构和枚举）将与 COM 类型无缝集成：</span><span class="sxs-lookup"><span data-stu-id="d4791-105">Managed types (class, interface, structure, and enumeration) seamlessly integrate with COM types when you adhere to the following guidelines:</span></span>  
  
- <span data-ttu-id="d4791-106">类应显式实现接口。</span><span class="sxs-lookup"><span data-stu-id="d4791-106">Classes should implement interfaces explicitly.</span></span>  
  
     <span data-ttu-id="d4791-107">尽管 COM 互操作提供了一种机制，用于自动生成包含类的所有成员及其基类成员的接口，但最好还是提供显式接口。</span><span class="sxs-lookup"><span data-stu-id="d4791-107">Although COM interop provides a mechanism to automatically generate an interface containing all members of the class and the members of its base class, it is far better to provide explicit interfaces.</span></span> <span data-ttu-id="d4791-108">自动生成的接口称为类接口。</span><span class="sxs-lookup"><span data-stu-id="d4791-108">The automatically generated interface is called the class interface.</span></span> <span data-ttu-id="d4791-109">有关指南，请参阅[类接口简介](com-callable-wrapper.md#introducing-the-class-interface)。</span><span class="sxs-lookup"><span data-stu-id="d4791-109">For guidelines, see [Introducing the class interface](com-callable-wrapper.md#introducing-the-class-interface).</span></span>  
  
     <span data-ttu-id="d4791-110">可以使用 Visual Basic、C# 和 C++ 将接口定义合并在代码中，而无需使用接口定义语言 (IDL) 或其等效语言。</span><span class="sxs-lookup"><span data-stu-id="d4791-110">You can use Visual Basic, C#, and C++ to incorporate interface definitions in your code, instead of having to use Interface Definition Language (IDL) or its equivalent.</span></span> <span data-ttu-id="d4791-111">有关语法的详细信息，请参见语言文档。</span><span class="sxs-lookup"><span data-stu-id="d4791-111">For syntax details, see your language documentation.</span></span>  
  
- <span data-ttu-id="d4791-112">托管的类型必须是公共的。</span><span class="sxs-lookup"><span data-stu-id="d4791-112">Managed types must be public.</span></span>  
  
     <span data-ttu-id="d4791-113">只有程序集中的公共类型才会注册并导出到类型库中。</span><span class="sxs-lookup"><span data-stu-id="d4791-113">Only public types in an assembly are registered and exported to the type library.</span></span> <span data-ttu-id="d4791-114">因此只有公共类型才对 COM 可见。</span><span class="sxs-lookup"><span data-stu-id="d4791-114">As a result, only public types are visible to COM.</span></span>  
  
     <span data-ttu-id="d4791-115">托管类型会向其他未向 COM 公开的托管代码公开功能。</span><span class="sxs-lookup"><span data-stu-id="d4791-115">Managed types expose features to other managed code that might not be exposed to COM.</span></span> <span data-ttu-id="d4791-116">例如，参数化的构造函数、静态方法和常数字段不会向 COM 客户端公开。</span><span class="sxs-lookup"><span data-stu-id="d4791-116">For instance, parameterized constructors, static methods, and constant fields are not exposed to COM clients.</span></span> <span data-ttu-id="d4791-117">此外，运行时在类型中和类型外封送数据时，数据可能会被复制或转换。</span><span class="sxs-lookup"><span data-stu-id="d4791-117">Further, as the runtime marshals data in and out of a type, the data might be copied or transformed.</span></span>  
  
- <span data-ttu-id="d4791-118">方法、属性、字段和事件必须是公共的。</span><span class="sxs-lookup"><span data-stu-id="d4791-118">Methods, properties, fields, and events must be public.</span></span>  
  
     <span data-ttu-id="d4791-119">如果要对 COM 可见，公共类型的成员也必须是公共的。</span><span class="sxs-lookup"><span data-stu-id="d4791-119">Members of public types must also be public if they are to be visible to COM.</span></span> <span data-ttu-id="d4791-120">通过应用 <xref:System.Runtime.InteropServices.ComVisibleAttribute>，可以限制程序集、公共类型或公共类型的公共成员的可见性。</span><span class="sxs-lookup"><span data-stu-id="d4791-120">You can restrict the visibility of an assembly, a public type, or public members of a public type by applying the <xref:System.Runtime.InteropServices.ComVisibleAttribute>.</span></span> <span data-ttu-id="d4791-121">默认情况下，所有公共类型和成员都是可见的。</span><span class="sxs-lookup"><span data-stu-id="d4791-121">By default, all public types and members are visible.</span></span>  
  
- <span data-ttu-id="d4791-122">具备公共无参数构造函数的类型才能从 COM 中激活。</span><span class="sxs-lookup"><span data-stu-id="d4791-122">Types must have a public parameterless constructor to be activated from COM.</span></span>  
  
     <span data-ttu-id="d4791-123">托管的公共类型对于 COM 是可见的。</span><span class="sxs-lookup"><span data-stu-id="d4791-123">Managed, public types are visible to COM.</span></span> <span data-ttu-id="d4791-124">但是如果没有公共无参数构造函数（不带任何参数的构造函数），COM 客户端无法创建该类型。</span><span class="sxs-lookup"><span data-stu-id="d4791-124">However, without a public parameterless constructor (a constructor with no arguments), COM clients cannot create the type.</span></span> <span data-ttu-id="d4791-125">如果该类型由其他方法激活，COM 客户端仍可使用该类型。</span><span class="sxs-lookup"><span data-stu-id="d4791-125">COM clients can still use the type if it is activated by some other means.</span></span>  
  
- <span data-ttu-id="d4791-126">类型不能是抽象的。</span><span class="sxs-lookup"><span data-stu-id="d4791-126">Types cannot be abstract.</span></span>  
  
     <span data-ttu-id="d4791-127">COM 客户端和 .NET 客户端都不能创建抽象的类型。</span><span class="sxs-lookup"><span data-stu-id="d4791-127">Neither COM clients nor .NET clients can create abstract types.</span></span>  
  
 <span data-ttu-id="d4791-128">导出到 COM 后，托管类型的继承层次结构将被展平。</span><span class="sxs-lookup"><span data-stu-id="d4791-128">When exported to COM, the inheritance hierarchy of a managed type is flattened.</span></span> <span data-ttu-id="d4791-129">托管和非托管环境之间的版本控制也会有所不同。</span><span class="sxs-lookup"><span data-stu-id="d4791-129">Versioning also differs between managed and unmanaged environments.</span></span> <span data-ttu-id="d4791-130">向 COM 公开的类型不具有其他托管类型相同的版本控制特性。</span><span class="sxs-lookup"><span data-stu-id="d4791-130">Types exposed to COM do not have the same versioning characteristics as other managed types.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d4791-131">请参阅</span><span class="sxs-lookup"><span data-stu-id="d4791-131">See also</span></span>

- <xref:System.Runtime.InteropServices.ComVisibleAttribute>
- [<span data-ttu-id="d4791-132">向 COM 公开 .NET Framework 组件</span><span class="sxs-lookup"><span data-stu-id="d4791-132">Exposing .NET Framework Components to COM</span></span>](../../framework/interop/exposing-dotnet-components-to-com.md)
- [<span data-ttu-id="d4791-133">类接口简介</span><span class="sxs-lookup"><span data-stu-id="d4791-133">Introducing the class interface</span></span>](com-callable-wrapper.md#introducing-the-class-interface)
- [<span data-ttu-id="d4791-134">应用互操作属性</span><span class="sxs-lookup"><span data-stu-id="d4791-134">Applying Interop Attributes</span></span>](apply-interop-attributes.md)
- [<span data-ttu-id="d4791-135">打包用于 COM 的 .NET Framework 程序集</span><span class="sxs-lookup"><span data-stu-id="d4791-135">Packaging a .NET Framework Assembly for COM</span></span>](../../framework/interop/packaging-an-assembly-for-com.md)
