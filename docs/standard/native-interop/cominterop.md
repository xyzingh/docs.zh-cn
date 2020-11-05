---
title: .NET 中的 COM 互操作
description: 了解如何在 .NET 中与 COM 库进行互操作。
ms.date: 07/11/2019
ms.openlocfilehash: 9c436019c800a68ffe2cd5011e14bd804384afaa
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187770"
---
# <a name="com-interop-in-net"></a><span data-ttu-id="84343-103">.NET 中的 COM 互操作</span><span class="sxs-lookup"><span data-stu-id="84343-103">COM Interop in .NET</span></span>

<span data-ttu-id="84343-104">组件对象模型 (COM) 允许对象向其他组件公开其功能并在 Windows 平台上托管应用程序。</span><span class="sxs-lookup"><span data-stu-id="84343-104">The Component Object Model (COM) lets an object expose its functionality to other components and to host applications on Windows platforms.</span></span> <span data-ttu-id="84343-105">为帮助用户实现与其现有代码库的互操作，.NET Framework 始终为与 COM 库进行互操作提供强大支持。</span><span class="sxs-lookup"><span data-stu-id="84343-105">To help enable users to interoperate with their existing code bases, .NET Framework has always provided strong support for interoperating with COM libraries.</span></span> <span data-ttu-id="84343-106">在 .NET Core 3.0 中，此支持中的很大一部分已添加到 Windows 上的 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="84343-106">In .NET Core 3.0, a large portion of this support has been added to .NET Core on Windows.</span></span> <span data-ttu-id="84343-107">此处的文档说明了公共 COM 互操作技术的工作原理，以及如何利用它们与现有 COM 库进行互操作。</span><span class="sxs-lookup"><span data-stu-id="84343-107">The documentation here explains how the common COM interop technologies work and how you can utilize them to interoperate with your existing COM libraries.</span></span>

- [<span data-ttu-id="84343-108">COM 包装</span><span class="sxs-lookup"><span data-stu-id="84343-108">COM Wrappers</span></span>](./com-wrappers.md)
- [<span data-ttu-id="84343-109">COM 可调用包装器</span><span class="sxs-lookup"><span data-stu-id="84343-109">COM Callable Wrappers</span></span>](./com-callable-wrapper.md)
- [<span data-ttu-id="84343-110">运行时可调用包装器</span><span class="sxs-lookup"><span data-stu-id="84343-110">Runtime Callable Wrappers</span></span>](./runtime-callable-wrapper.md)
- [<span data-ttu-id="84343-111">为 COM 互操作限定 .NET 类型</span><span class="sxs-lookup"><span data-stu-id="84343-111">Qualifying .NET Types for COM Interoperation</span></span>](./qualify-net-types-for-interoperation.md)
