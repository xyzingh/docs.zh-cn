---
title: SYSLIB0002 错误
description: 了解有关产生编译时错误 SYSLIB0002 的过时信息。
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 00fd42975c9286221b75c87caef8d2109b9b7100
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333062"
---
# <a name="syslib0002-principalpermissionattribute-is-obsolete"></a><span data-ttu-id="7b492-103">SYSLIB0002：PrincipalPermissionAttribute 已过时</span><span class="sxs-lookup"><span data-stu-id="7b492-103">SYSLIB0002: PrincipalPermissionAttribute is obsolete</span></span>

<span data-ttu-id="7b492-104">从 .NET 5.0 开始，<xref:System.Security.Permissions.PrincipalPermissionAttribute> 构造函数已过时并产生编译时错误 `SYSLIB0002`。</span><span class="sxs-lookup"><span data-stu-id="7b492-104">The <xref:System.Security.Permissions.PrincipalPermissionAttribute> constructor is obsolete and produces compile-time error `SYSLIB0002`, starting in .NET 5.0.</span></span> <span data-ttu-id="7b492-105">不能实例化此属性或将其应用于方法。</span><span class="sxs-lookup"><span data-stu-id="7b492-105">You cannot instantiate this attribute or apply it to a method.</span></span>

<span data-ttu-id="7b492-106">与其他过时警告不同，无法禁止显示此错误。</span><span class="sxs-lookup"><span data-stu-id="7b492-106">Unlike other obsoletion warnings, you can't suppress the error.</span></span>

## <a name="workarounds"></a><span data-ttu-id="7b492-107">工作区</span><span class="sxs-lookup"><span data-stu-id="7b492-107">Workarounds</span></span>

- <span data-ttu-id="7b492-108">如果要将属性应用于 ASP.NET MVC 操作方法，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="7b492-108">If you're applying the attribute to an ASP.NET MVC action method:</span></span>

  <span data-ttu-id="7b492-109">考虑使用 ASP.NET 的内置授权基础结构。</span><span class="sxs-lookup"><span data-stu-id="7b492-109">Consider using ASP.NET's built-in authorization infrastructure.</span></span> <span data-ttu-id="7b492-110">以下代码演示如何使用 <xref:System.Web.Mvc.AuthorizeAttribute> 属性来为控制器添加批注。</span><span class="sxs-lookup"><span data-stu-id="7b492-110">The following code demonstrates how to annotate a controller with an <xref:System.Web.Mvc.AuthorizeAttribute> attribute.</span></span> <span data-ttu-id="7b492-111">ASP.NET 运行时将在执行操作之前向用户授权。</span><span class="sxs-lookup"><span data-stu-id="7b492-111">The ASP.NET runtime will authorize the user before performing the action.</span></span>

  ```csharp
  using Microsoft.AspNetCore.Authorization;

  namespace MySampleApp
  {
      [Authorize(Roles = "Administrator")]
      public class AdministrationController : Controller
      {
          public ActionResult MyAction()
          {
              // This code won't run unless the current user
              // is in the 'Administrator' role.
          }
      }
  }
  ```

  <span data-ttu-id="7b492-112">有关详细信息，请参阅 [ASP.NET Core 中基于角色的授权](/aspnet/core/security/authorization/roles)和 [ASP.NET Core 中的授权简介](/aspnet/core/security/authorization/introduction)。</span><span class="sxs-lookup"><span data-stu-id="7b492-112">For more information, see [Role-based authorization in ASP.NET Core](/aspnet/core/security/authorization/roles) and [Introduction to authorization in ASP.NET Core](/aspnet/core/security/authorization/introduction).</span></span>

- <span data-ttu-id="7b492-113">如果要将属性应用到 Web 应用上下文之外的库代码，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="7b492-113">If you're applying the attribute to library code outside the context of a web app:</span></span>

  <span data-ttu-id="7b492-114">通过调用 <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType> 方法，在方法开始时手动执行检查。</span><span class="sxs-lookup"><span data-stu-id="7b492-114">Perform the checks manually at the beginning of your method by calling the <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType> method.</span></span>

  ```csharp
  using System.Threading;

  void DoSomething()
  {
      if (Thread.CurrentPrincipal == null
          || !Thread.CurrentPrincipal.IsInRole("Administrators"))
      {
          throw new Exception("User is anonymous or isn't an admin.");
      }

      // Code that should run only when user is an administrator.
  }
  ```

## <a name="see-also"></a><span data-ttu-id="7b492-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7b492-115">See also</span></span>

- [<span data-ttu-id="7b492-116">PrincipalPermissionAttribute 已过时，报告为错误</span><span class="sxs-lookup"><span data-stu-id="7b492-116">PrincipalPermissionAttribute is obsolete as error</span></span>](3.1-5.0.md#principalpermissionattribute-is-obsolete-as-error)
