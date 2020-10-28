---
title: 在可移植子集项目中添加服务引用
ms.date: 03/30/2017
ms.assetid: 61ccfe0f-a34b-40ca-8f5e-725fa1b8095e
ms.openlocfilehash: e9a0d3fbc75a8c64af892f74acedfc41dc115da3
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687706"
---
# <a name="add-service-reference-in-a-portable-subset-project"></a><span data-ttu-id="1cc67-102">在可移植子集项目中添加服务引用</span><span class="sxs-lookup"><span data-stu-id="1cc67-102">Add Service Reference in a Portable Subset Project</span></span>

<span data-ttu-id="1cc67-103">可移植子集项目使 .NET 程序集编程人员能够维护单个源树和生成系统，同时仍支持 (桌面、Silverlight、Windows Phone 和 Xbox) 的多个 .NET 实现。</span><span class="sxs-lookup"><span data-stu-id="1cc67-103">Portable subset projects enable .NET assembly programmers to maintain a single source tree and build system while still supporting multiple .NET implementations (desktop, Silverlight, Windows Phone, and Xbox).</span></span> <span data-ttu-id="1cc67-104">可移植子集项目仅引用可在任何 .NET 实现上使用的 .NET 程序集的可移植库。</span><span class="sxs-lookup"><span data-stu-id="1cc67-104">Portable subset projects only reference portable libraries that are .NET assemblies that can be used on any .NET implementation.</span></span>
  
## <a name="add-service-reference-details"></a><span data-ttu-id="1cc67-105">添加服务引用详细信息</span><span class="sxs-lookup"><span data-stu-id="1cc67-105">Add Service Reference Details</span></span>  
 <span data-ttu-id="1cc67-106">在可移植子集项目中添加服务引用时，将强制执行以下限制： </span><span class="sxs-lookup"><span data-stu-id="1cc67-106">When adding a service reference in a portable subset project the following restrictions are enforced:</span></span>  
  
1. <span data-ttu-id="1cc67-107">对于 <xref:System.Xml.Serialization.XmlSerializer>，仅允许文本编码。</span><span class="sxs-lookup"><span data-stu-id="1cc67-107">For <xref:System.Xml.Serialization.XmlSerializer>, only literal encodings are allowed.</span></span> <span data-ttu-id="1cc67-108">SOAP 编码在导入过程中生成错误。</span><span class="sxs-lookup"><span data-stu-id="1cc67-108">SOAP encodings generate an error during import.</span></span>  
  
2. <span data-ttu-id="1cc67-109">针对使用 <xref:System.Runtime.Serialization.DataContractSerializer> 方案的服务，提供了数据协定代理项以确保重用的类型仅来自可移植子集。</span><span class="sxs-lookup"><span data-stu-id="1cc67-109">For services that use <xref:System.Runtime.Serialization.DataContractSerializer> scenarios, a data contract surrogate is provided to ensure that reused types come only from the portable subset.</span></span>  
  
3. <span data-ttu-id="1cc67-110">将忽略依赖可移植库中不支持的绑定的终结点（除没有事务流、可靠会话或 MTOM 编码的 <xref:System.ServiceModel.BasicHttpBinding>、<xref:System.ServiceModel.WSHttpBinding> 的绑定以及等效的自定义绑定之外的所有绑定）。</span><span class="sxs-lookup"><span data-stu-id="1cc67-110">Endpoints which rely on bindings not supported in portable libraries (all bindings except <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.WSHttpBinding> without transaction flow, reliable sessions, or MTOM encoding, and equivalent custom bindings) are ignored.</span></span>  
  
4. <span data-ttu-id="1cc67-111">在导入之前的所有操作中，将从所有消息描述删除消息标头。</span><span class="sxs-lookup"><span data-stu-id="1cc67-111">Message headers are deleted from all message descriptions in all operations before import.</span></span>  
  
5. <span data-ttu-id="1cc67-112">将从生成的客户端代理代码删除不可移植的特性 <xref:System.ComponentModel.DesignerCategoryAttribute>、<xref:System.SerializableAttribute> 和 <xref:System.ServiceModel.TransactionFlowAttribute>。</span><span class="sxs-lookup"><span data-stu-id="1cc67-112">Non-portable attributes <xref:System.ComponentModel.DesignerCategoryAttribute>, <xref:System.SerializableAttribute>, and <xref:System.ServiceModel.TransactionFlowAttribute> are removed from generated client proxy code.</span></span>  
  
6. <span data-ttu-id="1cc67-113">将从 <xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.OperationContractAttribute> 和 <xref:System.ServiceModel.FaultContractAttribute> 删除不可移植的属性 ProtectionLevel、SessionMode、IsInitiating、IsTerminating。</span><span class="sxs-lookup"><span data-stu-id="1cc67-113">Non-portable properties ProtectionLevel, SessionMode, IsInitiating, IsTerminating are removed from <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.OperationContractAttribute>, and <xref:System.ServiceModel.FaultContractAttribute>.</span></span>  
  
7. <span data-ttu-id="1cc67-114">所有服务操作都是作为客户端代理上的异步操作生成的。</span><span class="sxs-lookup"><span data-stu-id="1cc67-114">All service operations are generated as asynchronous operations on the client proxy.</span></span>  
  
8. <span data-ttu-id="1cc67-115">将删除所生成的使用不可移植类型的客户端构造函数。</span><span class="sxs-lookup"><span data-stu-id="1cc67-115">Generated client constructors which use non-portable types are removed.</span></span>  
  
9. <span data-ttu-id="1cc67-116">在生成的客户端上公开一个 <xref:System.Net.CookieContainer> 实例。</span><span class="sxs-lookup"><span data-stu-id="1cc67-116">A <xref:System.Net.CookieContainer> instance is exposed on the generated client.</span></span>  
  
10. <span data-ttu-id="1cc67-117">在文件顶部插入注释以标识代码生成器的程序集和版本：`// This code was auto-generated by Microsoft.VisualStudio.Portable.AddServiceReference, version 1.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="1cc67-117">A comment is inserted at the top of the file identifying the assembly and version of the code generator:`// This code was auto-generated by Microsoft.VisualStudio.Portable.AddServiceReference, version 1.0.0.0`</span></span>  
  
11. <span data-ttu-id="1cc67-118">不支持 <xref:System.Runtime.Serialization.ISerializable> 接口。</span><span class="sxs-lookup"><span data-stu-id="1cc67-118">The <xref:System.Runtime.Serialization.ISerializable> interface is not supported.</span></span>  
  
12. <span data-ttu-id="1cc67-119">不支持 Net.Tcp 和 PollingDuplex 绑定</span><span class="sxs-lookup"><span data-stu-id="1cc67-119">Net.Tcp and PollingDuplex bindings are not supported</span></span>  
  
13. <span data-ttu-id="1cc67-120">始终将 <xref:System.Runtime.Serialization.DataContractSerializer> 用于错误。</span><span class="sxs-lookup"><span data-stu-id="1cc67-120">The <xref:System.Runtime.Serialization.DataContractSerializer> will always be used for faults.</span></span>  
  
14. <span data-ttu-id="1cc67-121">可移植子集项目中不支持 <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A>。</span><span class="sxs-lookup"><span data-stu-id="1cc67-121"><xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> is not supported in portable subset projects.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1cc67-122">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1cc67-122">See also</span></span>

- [<span data-ttu-id="1cc67-123">使用 WCF 客户端访问服务</span><span class="sxs-lookup"><span data-stu-id="1cc67-123">Accessing Services Using a WCF Client</span></span>](accessing-services-using-a-wcf-client.md)
- [<span data-ttu-id="1cc67-124">可移植类库</span><span class="sxs-lookup"><span data-stu-id="1cc67-124">Portable Class Library</span></span>](../cross-platform/portable-class-library.md)
