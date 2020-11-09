---
title: .NET Core 和 .NET 5+ 上不支持的 API
titleSuffix: ''
description: 了解哪些 .NET API 始终在 .NET Core 和 .NET 5.0 及更高版本上引发异常。
ms.date: 10/13/2020
ms.openlocfilehash: 51d73557a48910d9cb1c4d3cdced34dfe4d849d8
ms.sourcegitcommit: 6bef8abde346c59771a35f4f76bf037ff61c5ba3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "94329776"
---
# <a name="apis-that-always-throw-exceptions-on-net-core-and-net-5"></a><span data-ttu-id="17eb4-103">始终在 .NET Core 和 .NET 5+ 上引发异常的 API</span><span class="sxs-lookup"><span data-stu-id="17eb4-103">APIs that always throw exceptions on .NET Core and .NET 5+</span></span>

<span data-ttu-id="17eb4-104">以下 API 将始终在所有或部分平台上的 .NET 5.0 及更高版本（包括所有 .NET Core 版本）中引发 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="17eb4-104">The following APIs will always throw a <xref:System.PlatformNotSupportedException> on .NET 5.0 and later versions (including all versions of .NET Core) on all or a subset of platforms.</span></span>

<span data-ttu-id="17eb4-105">本文按命名空间组织受影响的 API。</span><span class="sxs-lookup"><span data-stu-id="17eb4-105">This article organizes the affected APIs by namespace.</span></span>

> [!NOTE]
>
> - <span data-ttu-id="17eb4-106">本文是当前正在进行的工作。</span><span class="sxs-lookup"><span data-stu-id="17eb4-106">This article is a work-in-progress.</span></span> <span data-ttu-id="17eb4-107">它不是在 .NET 5+ 上引发异常的 API 的完整列表。</span><span class="sxs-lookup"><span data-stu-id="17eb4-107">It is not a complete list of APIs that throw exceptions on .NET 5+.</span></span>
> - <span data-ttu-id="17eb4-108">本文不包括在 .NET 5+ 上引发的二进制序列化的显式接口实现。</span><span class="sxs-lookup"><span data-stu-id="17eb4-108">This article does not include the explicit interface implementations for binary serialization that throw on .NET 5+.</span></span> <span data-ttu-id="17eb4-109">有关详细信息，请参阅 [.NET Core 中的二进制序列化](../../standard/serialization/binary-serialization.md#net-core)。</span><span class="sxs-lookup"><span data-stu-id="17eb4-109">For more information, see [Binary serialization in .NET Core](../../standard/serialization/binary-serialization.md#net-core).</span></span>

## <a name="system"></a><span data-ttu-id="17eb4-110">系统</span><span class="sxs-lookup"><span data-stu-id="17eb4-110">System</span></span>

| <span data-ttu-id="17eb4-111">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-111">Member</span></span> | <span data-ttu-id="17eb4-112">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-112">Platforms that throw</span></span> |
| - | - |
| <xref:System.AppDomain.CreateDomain%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-113">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-113">All</span></span> |
| <xref:System.AppDomain.ExecuteAssembly(System.String,System.String[],System.Byte[],System.Configuration.Assemblies.AssemblyHashAlgorithm)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-114">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-114">All</span></span> |
| <xref:System.Console.CapsLock?displayProperty=nameWithType> | <span data-ttu-id="17eb4-115">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-115">Linux and macOS</span></span> |
| <xref:System.Console.NumberLock?displayProperty=nameWithType> | <span data-ttu-id="17eb4-116">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-116">Linux and macOS</span></span> |
| <xref:System.Delegate.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-117">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-117">All</span></span> |
| <xref:System.Exception.SerializeObjectState?displayProperty=nameWithType> | <span data-ttu-id="17eb4-118">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-118">All</span></span> |
| <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType> | <span data-ttu-id="17eb4-119">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-119">All</span></span> |
| <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType> | <span data-ttu-id="17eb4-120">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-120">All</span></span> |
| <xref:System.OperatingSystem.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-121">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-121">All</span></span> |
| <xref:System.Type.ReflectionOnlyGetType(System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-122">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-122">All</span></span> |

## <a name="systemcodedomcompiler"></a><span data-ttu-id="17eb4-123">System.CodeDom.Compiler</span><span class="sxs-lookup"><span data-stu-id="17eb4-123">System.CodeDom.Compiler</span></span>

| <span data-ttu-id="17eb4-124">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-124">Member</span></span> | <span data-ttu-id="17eb4-125">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-125">Platforms that throw</span></span> |
| - | - |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-126">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-126">All</span></span> |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-127">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-127">All</span></span> |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-128">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-128">All</span></span> |

## <a name="systemcollectionsspecialized"></a><span data-ttu-id="17eb4-129">System.Collections.Specialized</span><span class="sxs-lookup"><span data-stu-id="17eb4-129">System.Collections.Specialized</span></span>

| <span data-ttu-id="17eb4-130">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-130">Member</span></span> | <span data-ttu-id="17eb4-131">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-131">Platforms that throw</span></span> |
| - | - |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-132">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-132">All</span></span> |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-133">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-133">All</span></span> |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.OnDeserialization(System.Object)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-134">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-134">All</span></span> |

## <a name="systemconfiguration"></a><span data-ttu-id="17eb4-135">System.Configuration</span><span class="sxs-lookup"><span data-stu-id="17eb4-135">System.Configuration</span></span>

| <span data-ttu-id="17eb4-136">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-136">Member</span></span> | <span data-ttu-id="17eb4-137">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-137">Platforms that throw</span></span> |
| - | - |
| <span data-ttu-id="17eb4-138"><xref:System.Configuration.RsaProtectedConfigurationProvider?displayProperty=nameWithType>（所有成员）</span><span class="sxs-lookup"><span data-stu-id="17eb4-138"><xref:System.Configuration.RsaProtectedConfigurationProvider?displayProperty=nameWithType> (all members)</span></span> | <span data-ttu-id="17eb4-139">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-139">All</span></span> |

## <a name="systemconsole"></a><span data-ttu-id="17eb4-140">System.Console</span><span class="sxs-lookup"><span data-stu-id="17eb4-140">System.Console</span></span>

| <span data-ttu-id="17eb4-141">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-141">Member</span></span> | <span data-ttu-id="17eb4-142">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-142">Platforms that throw</span></span> |
| - | - |
| <xref:System.Console.Beep?displayProperty=nameWithType> | <span data-ttu-id="17eb4-143">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-143">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-144"><xref:System.Console.BufferHeight?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-144"><xref:System.Console.BufferHeight?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-145">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-145">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-146"><xref:System.Console.BufferWidth?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-146"><xref:System.Console.BufferWidth?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-147">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-147">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-148"><xref:System.Console.CursorSize?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-148"><xref:System.Console.CursorSize?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-149">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-149">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-150"><xref:System.Console.CursorVisible?displayProperty=nameWithType>（仅获取）</span><span class="sxs-lookup"><span data-stu-id="17eb4-150"><xref:System.Console.CursorVisible?displayProperty=nameWithType> (get only)</span></span> | <span data-ttu-id="17eb4-151">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-151">Linux and macOS</span></span> |
| <xref:System.Console.MoveBufferArea%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-152">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-152">Linux and macOS</span></span> |
| <xref:System.Console.SetWindowPosition%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-153">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-153">Linux and macOS</span></span> |
| <xref:System.Console.SetWindowSize%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-154">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-154">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-155"><xref:System.Console.Title?displayProperty=nameWithType>（仅获取）</span><span class="sxs-lookup"><span data-stu-id="17eb4-155"><xref:System.Console.Title?displayProperty=nameWithType> (get only)</span></span> | <span data-ttu-id="17eb4-156">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-156">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-157"><xref:System.Console.WindowHeight?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-157"><xref:System.Console.WindowHeight?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-158">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-158">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-159"><xref:System.Console.WindowLeft?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-159"><xref:System.Console.WindowLeft?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-160">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-160">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-161"><xref:System.Console.WindowTop?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-161"><xref:System.Console.WindowTop?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-162">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-162">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-163"><xref:System.Console.WindowWidth?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-163"><xref:System.Console.WindowWidth?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-164">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-164">Linux and macOS</span></span> |

## <a name="systemdatacommon"></a><span data-ttu-id="17eb4-165">System.Data.Common</span><span class="sxs-lookup"><span data-stu-id="17eb4-165">System.Data.Common</span></span>

| <span data-ttu-id="17eb4-166">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-166">Member</span></span> | <span data-ttu-id="17eb4-167">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-167">Platforms that throw</span></span> |
| - | - |
| <span data-ttu-id="17eb4-168"><xref:System.Data.Common.DbDataReader.GetSchemaTable%2A?displayProperty=nameWithType>（引发 <xref:System.NotSupportedException>）</span><span class="sxs-lookup"><span data-stu-id="17eb4-168"><xref:System.Data.Common.DbDataReader.GetSchemaTable%2A?displayProperty=nameWithType> (throws <xref:System.NotSupportedException>)</span></span> | <span data-ttu-id="17eb4-169">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-169">All</span></span> |

## <a name="systemdiagnosticsprocess"></a><span data-ttu-id="17eb4-170">System.Diagnostics.Process</span><span class="sxs-lookup"><span data-stu-id="17eb4-170">System.Diagnostics.Process</span></span>

| <span data-ttu-id="17eb4-171">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-171">Member</span></span> | <span data-ttu-id="17eb4-172">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-172">Platforms that throw</span></span> |
| - | - |
| <span data-ttu-id="17eb4-173"><xref:System.Diagnostics.Process.MaxWorkingSet?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-173"><xref:System.Diagnostics.Process.MaxWorkingSet?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-174">Linux</span><span class="sxs-lookup"><span data-stu-id="17eb4-174">Linux</span></span> |
| <span data-ttu-id="17eb4-175"><xref:System.Diagnostics.Process.MinWorkingSet?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-175"><xref:System.Diagnostics.Process.MinWorkingSet?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-176">Linux</span><span class="sxs-lookup"><span data-stu-id="17eb4-176">Linux</span></span> |
| <xref:System.Diagnostics.Process.ProcessorAffinity?displayProperty=nameWithType> | <span data-ttu-id="17eb4-177">macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-177">macOS</span></span> |
| <xref:System.Diagnostics.Process.MainWindowHandle?displayProperty=nameWithType> | <span data-ttu-id="17eb4-178">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-178">Linux and macOS</span></span> |
| <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-179">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-179">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.UserName?displayProperty=nameWithType> | <span data-ttu-id="17eb4-180">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-180">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.PasswordInClearText?displayProperty=nameWithType> | <span data-ttu-id="17eb4-181">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-181">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.Domain?displayProperty=nameWithType> | <span data-ttu-id="17eb4-182">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-182">Linux and macOS</span></span> |
| <xref:System.Diagnostics.ProcessStartInfo.LoadUserProfile?displayProperty=nameWithType> | <span data-ttu-id="17eb4-183">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-183">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-184"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-184"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-185">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-185">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-186"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType>（仅获取）</span><span class="sxs-lookup"><span data-stu-id="17eb4-186"><xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (get only)</span></span> | <span data-ttu-id="17eb4-187">macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-187">macOS</span></span> |
| <span data-ttu-id="17eb4-188"><xref:System.Diagnostics.ProcessThread.ProcessorAffinity?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-188"><xref:System.Diagnostics.ProcessThread.ProcessorAffinity?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-189">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-189">Linux and macOS</span></span> |

## <a name="systemio"></a><span data-ttu-id="17eb4-190">System.IO</span><span class="sxs-lookup"><span data-stu-id="17eb4-190">System.IO</span></span>

| <span data-ttu-id="17eb4-191">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-191">Member</span></span> | <span data-ttu-id="17eb4-192">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-192">Platforms that throw</span></span> |
| - | - |
| <xref:System.IO.FileSystemInfo.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-193">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-193">All</span></span> |
| <xref:System.IO.FileSystemInfo.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-194">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-194">All</span></span> |

## <a name="systemiopipes"></a><span data-ttu-id="17eb4-195">System.IO.Pipes</span><span class="sxs-lookup"><span data-stu-id="17eb4-195">System.IO.Pipes</span></span>

| <span data-ttu-id="17eb4-196">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-196">Member</span></span> | <span data-ttu-id="17eb4-197">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-197">Platforms that throw</span></span> |
| - | - |
| <xref:System.IO.Pipes.NamedPipeClientStream.NumberOfServerInstances?displayProperty=nameWithType> | <span data-ttu-id="17eb4-198">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-198">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName?displayProperty=nameWithType> | <span data-ttu-id="17eb4-199">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-199">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.PipeStream.InBufferSize?displayProperty=nameWithType> | <span data-ttu-id="17eb4-200">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-200">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.PipeStream.OutBufferSize?displayProperty=nameWithType> | <span data-ttu-id="17eb4-201">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-201">Linux and macOS</span></span> |
| <span data-ttu-id="17eb4-202"><xref:System.IO.Pipes.PipeStream.ReadMode?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-202"><xref:System.IO.Pipes.PipeStream.ReadMode?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-203">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-203">Linux and macOS</span></span> |
| <xref:System.IO.Pipes.PipeStream.WaitForPipeDrain?displayProperty=nameWithType> | <span data-ttu-id="17eb4-204">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-204">Linux and macOS</span></span> |

## <a name="systemmedia"></a><span data-ttu-id="17eb4-205">System.Media</span><span class="sxs-lookup"><span data-stu-id="17eb4-205">System.Media</span></span>

| <span data-ttu-id="17eb4-206">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-206">Member</span></span> | <span data-ttu-id="17eb4-207">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-207">Platforms that throw</span></span> |
| - | - |
| <xref:System.Media.SoundPlayer.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-208">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-208">All</span></span> |

## <a name="systemnet"></a><span data-ttu-id="17eb4-209">System.Net</span><span class="sxs-lookup"><span data-stu-id="17eb4-209">System.Net</span></span>

| <span data-ttu-id="17eb4-210">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-210">Member</span></span> | <span data-ttu-id="17eb4-211">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-211">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.AuthenticationManager.Authenticate(System.String,System.Net.WebRequest,System.Net.ICredentials)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-212">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-212">All</span></span> |
| <xref:System.Net.AuthenticationManager.PreAuthenticate(System.Net.WebRequest,System.Net.ICredentials)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-213">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-213">All</span></span> |
| <xref:System.Net.FileWebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-214">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-214">All</span></span> |
| <xref:System.Net.FileWebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-215">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-215">All</span></span> |
| <xref:System.Net.FileWebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-216">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-216">All</span></span> |
| <xref:System.Net.FileWebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-217">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-217">All</span></span> |
| <xref:System.Net.HttpWebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-218">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-218">All</span></span> |
| <xref:System.Net.HttpWebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-219">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-219">All</span></span> |
| <xref:System.Net.HttpWebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-220">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-220">All</span></span> |
| <xref:System.Net.HttpWebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-221">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-221">All</span></span> |
| <xref:System.Net.WebProxy.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-222">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-222">All</span></span> |
| <xref:System.Net.WebProxy.GetDefaultProxy?displayProperty=nameWithType> | <span data-ttu-id="17eb4-223">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-223">All</span></span> |
| <xref:System.Net.WebProxy.GetObjectData%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-224">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-224">All</span></span> |
| <xref:System.Net.WebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-225">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-225">All</span></span> |
| <xref:System.Net.WebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-226">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-226">All</span></span> |
| <xref:System.Net.WebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-227">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-227">All</span></span> |
| <xref:System.Net.WebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-228">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-228">All</span></span> |

## <a name="systemnetnetworkinformation"></a><span data-ttu-id="17eb4-229">System.Net.NetworkInformation</span><span class="sxs-lookup"><span data-stu-id="17eb4-229">System.Net.NetworkInformation</span></span>

| <span data-ttu-id="17eb4-230">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-230">Member</span></span> | <span data-ttu-id="17eb4-231">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-231">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.NetworkInformation.Ping.Send%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-232">Windows (UWP)</span><span class="sxs-lookup"><span data-stu-id="17eb4-232">Windows (UWP)</span></span> |

## <a name="systemnetsockets"></a><span data-ttu-id="17eb4-233">System.Net.Sockets</span><span class="sxs-lookup"><span data-stu-id="17eb4-233">System.Net.Sockets</span></span>

| <span data-ttu-id="17eb4-234">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-234">Member</span></span> | <span data-ttu-id="17eb4-235">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-235">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.Sockets.Socket.%23ctor(System.Net.Sockets.SocketInformation)> | <span data-ttu-id="17eb4-236">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-236">All</span></span> |
| <xref:System.Net.Sockets.Socket.DuplicateAndClose(System.Int32)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-237">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-237">All</span></span> |

## <a name="systemnetwebsockets"></a><span data-ttu-id="17eb4-238">System.Net.WebSockets</span><span class="sxs-lookup"><span data-stu-id="17eb4-238">System.Net.WebSockets</span></span>

| <span data-ttu-id="17eb4-239">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-239">Member</span></span> | <span data-ttu-id="17eb4-240">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-240">Platforms that throw</span></span> |
| - | - |
| <xref:System.Net.WebSockets.WebSocket.RegisterPrefixes?displayProperty=nameWithType> | <span data-ttu-id="17eb4-241">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-241">All</span></span> |

## <a name="systemreflection"></a><span data-ttu-id="17eb4-242">System.Reflection</span><span class="sxs-lookup"><span data-stu-id="17eb4-242">System.Reflection</span></span>

| <span data-ttu-id="17eb4-243">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-243">Member</span></span> | <span data-ttu-id="17eb4-244">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-244">Platforms that throw</span></span> |
| - | - |
| <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-245">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-245">All</span></span> |
| <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom(System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-246">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-246">All</span></span> |
| <xref:System.Reflection.AssemblyName.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-247">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-247">All</span></span> |
| <xref:System.Reflection.AssemblyName.OnDeserialization(System.Object)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-248">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-248">All</span></span> |
| <xref:System.Reflection.StrongNameKeyPair.%23ctor(System.String)> | <span data-ttu-id="17eb4-249">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-249">All</span></span> |
| <xref:System.Reflection.StrongNameKeyPair.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-250">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-250">All</span></span> |
| <xref:System.Reflection.StrongNameKeyPair.PublicKey?displayProperty=nameWithType> | <span data-ttu-id="17eb4-251">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-251">All</span></span> |

## <a name="systemruntimecompilerservices"></a><span data-ttu-id="17eb4-252">System.Runtime.CompilerServices</span><span class="sxs-lookup"><span data-stu-id="17eb4-252">System.Runtime.CompilerServices</span></span>

| <span data-ttu-id="17eb4-253">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-253">Member</span></span> | <span data-ttu-id="17eb4-254">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-254">Platforms that throw</span></span> |
| - | - |
| <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator?displayProperty=nameWithType> | <span data-ttu-id="17eb4-255">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-255">All</span></span> |

## <a name="systemruntimeinteropservices"></a><span data-ttu-id="17eb4-256">System.Runtime.InteropServices</span><span class="sxs-lookup"><span data-stu-id="17eb4-256">System.Runtime.InteropServices</span></span>

| <span data-ttu-id="17eb4-257">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-257">Member</span></span> | <span data-ttu-id="17eb4-258">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-258">Platforms that throw</span></span> |
| - | - |
| <xref:System.Runtime.InteropServices.Marshal.GetIDispatchForObject(System.Object)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-259">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-259">All</span></span> |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.SystemConfigurationFile?displayProperty=nameWithType> | <span data-ttu-id="17eb4-260">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-260">All</span></span> |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeInterfaceAsIntPtr(System.Guid,System.Guid)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-261">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-261">All</span></span> |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeInterfaceAsObject(System.Guid,System.Guid)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-262">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-262">All</span></span> |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.StringToHString(System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-263">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-263">Linux and macOS</span></span> |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.PtrToStringHString(System.IntPtr)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-264">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-264">Linux and macOS</span></span> |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.FreeHString(System.IntPtr)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-265">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-265">Linux and macOS</span></span> |

## <a name="systemruntimeserialization"></a><span data-ttu-id="17eb4-266">System.Runtime.Serialization</span><span class="sxs-lookup"><span data-stu-id="17eb4-266">System.Runtime.Serialization</span></span>

| <span data-ttu-id="17eb4-267">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-267">Member</span></span> | <span data-ttu-id="17eb4-268">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-268">Platforms that throw</span></span> |
| - | - |
| <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas?displayProperty=nameWithType> | <span data-ttu-id="17eb4-269">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-269">All</span></span> |

## <a name="systemsecurity"></a><span data-ttu-id="17eb4-270">System.Security</span><span class="sxs-lookup"><span data-stu-id="17eb4-270">System.Security</span></span>

| <span data-ttu-id="17eb4-271">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-271">Member</span></span> | <span data-ttu-id="17eb4-272">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-272">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.CodeAccessPermission.Deny?displayProperty=nameWithType> | <span data-ttu-id="17eb4-273">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-273">All</span></span> |
| <xref:System.Security.CodeAccessPermission.PermitOnly?displayProperty=nameWithType> | <span data-ttu-id="17eb4-274">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-274">All</span></span> |
| <xref:System.Security.PermissionSet.ConvertPermissionSet(System.String,System.Byte[],System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-275">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-275">All</span></span> |
| <xref:System.Security.PermissionSet.Deny?displayProperty=nameWithType> | <span data-ttu-id="17eb4-276">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-276">All</span></span> |
| <xref:System.Security.PermissionSet.PermitOnly?displayProperty=nameWithType> | <span data-ttu-id="17eb4-277">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-277">All</span></span> |
| <xref:System.Security.SecurityContext.Capture?displayProperty=nameWithType> | <span data-ttu-id="17eb4-278">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-278">All</span></span> |
| <xref:System.Security.SecurityContext.CreateCopy?displayProperty=nameWithType> | <span data-ttu-id="17eb4-279">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-279">All</span></span> |
| <xref:System.Security.SecurityContext.Dispose?displayProperty=nameWithType> | <span data-ttu-id="17eb4-280">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-280">All</span></span> |
| <xref:System.Security.SecurityContext.IsFlowSuppressed?displayProperty=nameWithType> | <span data-ttu-id="17eb4-281">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-281">All</span></span> |
| <xref:System.Security.SecurityContext.IsWindowsIdentityFlowSuppressed?displayProperty=nameWithType> | <span data-ttu-id="17eb4-282">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-282">All</span></span> |
| <xref:System.Security.SecurityContext.RestoreFlow?displayProperty=nameWithType> | <span data-ttu-id="17eb4-283">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-283">All</span></span> |
| <xref:System.Security.SecurityContext.Run(System.Security.SecurityContext,System.Threading.ContextCallback,System.Object)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-284">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-284">All</span></span> |
| <xref:System.Security.SecurityContext.SuppressFlow?displayProperty=nameWithType> | <span data-ttu-id="17eb4-285">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-285">All</span></span> |
| <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity?displayProperty=nameWithType> | <span data-ttu-id="17eb4-286">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-286">All</span></span> |

## <a name="systemsecurityclaims"></a><span data-ttu-id="17eb4-287">System.Security.Claims</span><span class="sxs-lookup"><span data-stu-id="17eb4-287">System.Security.Claims</span></span>

| <span data-ttu-id="17eb4-288">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-288">Member</span></span> | <span data-ttu-id="17eb4-289">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-289">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Claims.ClaimsPrincipal.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-290">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-290">All</span></span> |
| <xref:System.Security.Claims.ClaimsPrincipal.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-291">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-291">All</span></span> |
| <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Runtime.Serialization.SerializationInfo)> | <span data-ttu-id="17eb4-292">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-292">All</span></span> |
| <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-293">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-293">All</span></span> |
| <xref:System.Security.Claims.ClaimsIdentity.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-294">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-294">All</span></span> |

## <a name="systemsecuritycryptography"></a><span data-ttu-id="17eb4-295">System.Security.Cryptography</span><span class="sxs-lookup"><span data-stu-id="17eb4-295">System.Security.Cryptography</span></span>

| <span data-ttu-id="17eb4-296">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-296">Member</span></span> | <span data-ttu-id="17eb4-297">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-297">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-298">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-298">All</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.%23ctor%2A> | <span data-ttu-id="17eb4-299">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-299">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Accessible?displayProperty=nameWithType> | <span data-ttu-id="17eb4-300">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-300">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Exportable?displayProperty=nameWithType> | <span data-ttu-id="17eb4-301">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-301">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.HardwareDevice?displayProperty=nameWithType> | <span data-ttu-id="17eb4-302">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-302">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.KeyContainerName?displayProperty=nameWithType> | <span data-ttu-id="17eb4-303">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-303">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.KeyNumber?displayProperty=nameWithType> | <span data-ttu-id="17eb4-304">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-304">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.MachineKeyStore?displayProperty=nameWithType> | <span data-ttu-id="17eb4-305">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-305">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Protected?displayProperty=nameWithType> | <span data-ttu-id="17eb4-306">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-306">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.ProviderName?displayProperty=nameWithType> | <span data-ttu-id="17eb4-307">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-307">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.ProviderType?displayProperty=nameWithType> | <span data-ttu-id="17eb4-308">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-308">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.RandomlyGenerated?displayProperty=nameWithType> | <span data-ttu-id="17eb4-309">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-309">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Removable?displayProperty=nameWithType> | <span data-ttu-id="17eb4-310">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-310">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.UniqueKeyContainerName?displayProperty=nameWithType> | <span data-ttu-id="17eb4-311">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-311">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <span data-ttu-id="17eb4-312">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-312">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <span data-ttu-id="17eb4-313">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-313">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-314">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-314">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.HashCore%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-315">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-315">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.HashFinal%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-316">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-316">All</span></span> |
| <xref:System.Security.Cryptography.HMAC.Initialize%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-317">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-317">All</span></span> |
| <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <span data-ttu-id="17eb4-318">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-318">All</span></span> |
| <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-319">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-319">All</span></span> |
| <xref:System.Security.Cryptography.ProtectedData.Protect%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-320">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-320">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-321">Linux 和 macOS</span><span class="sxs-lookup"><span data-stu-id="17eb4-321">Linux and macOS</span></span> |
| <xref:System.Security.Cryptography.RSA.FromXmlString%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-322">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-322">All</span></span> |
| <xref:System.Security.Cryptography.RSA.ToXmlString%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-323">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-323">All</span></span> |
| <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <span data-ttu-id="17eb4-324">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-324">All</span></span> |
| <xref:System.Security.Cryptography.SymmetricAlgorithm.Create(System.String)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-325">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-325">All</span></span> |

## <a name="systemsecuritycryptographypkcs"></a><span data-ttu-id="17eb4-326">System.Security.Cryptography.Pkcs</span><span class="sxs-lookup"><span data-stu-id="17eb4-326">System.Security.Cryptography.Pkcs</span></span>

| <span data-ttu-id="17eb4-327">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-327">Member</span></span> | <span data-ttu-id="17eb4-328">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-328">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Cryptography.Pkcs.CmsSigner.%23ctor(System.Security.Cryptography.CspParameters)> | <span data-ttu-id="17eb4-329">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-329">All</span></span> |
| <xref:System.Security.Cryptography.Pkcs.SignerInfo.ComputeCounterSignature?displayProperty=nameWithType> | <span data-ttu-id="17eb4-330">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-330">All</span></span> |

## <a name="systemsecuritycryptographyx509certificates"></a><span data-ttu-id="17eb4-331">System.Security.Cryptography.X509Certificates</span><span class="sxs-lookup"><span data-stu-id="17eb4-331">System.Security.Cryptography.X509Certificates</span></span>

| <span data-ttu-id="17eb4-332">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-332">Member</span></span> | <span data-ttu-id="17eb4-333">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-333">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-334">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-334">All</span></span> |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate.Import%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-335">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-335">All</span></span> |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-336">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-336">All</span></span> |
| <span data-ttu-id="17eb4-337"><xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType>（仅设置）</span><span class="sxs-lookup"><span data-stu-id="17eb4-337"><xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> (set only)</span></span> | <span data-ttu-id="17eb4-338">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-338">All</span></span> |

## <a name="systemsecurityauthenticationextendedprotection"></a><span data-ttu-id="17eb4-339">System.Security.Authentication.ExtendedProtection</span><span class="sxs-lookup"><span data-stu-id="17eb4-339">System.Security.Authentication.ExtendedProtection</span></span>

| <span data-ttu-id="17eb4-340">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-340">Member</span></span> | <span data-ttu-id="17eb4-341">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-341">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-342">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-342">All</span></span> |

## <a name="systemsecuritypolicy"></a><span data-ttu-id="17eb4-343">System.Security.Policy</span><span class="sxs-lookup"><span data-stu-id="17eb4-343">System.Security.Policy</span></span>

| <span data-ttu-id="17eb4-344">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-344">Member</span></span> | <span data-ttu-id="17eb4-345">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-345">Platforms that throw</span></span> |
| - | - |
| <xref:System.Security.Policy.Hash.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-346">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-346">All</span></span> |

## <a name="systemserviceprocessservicecontroller"></a><span data-ttu-id="17eb4-347">System.ServiceProcess.ServiceController</span><span class="sxs-lookup"><span data-stu-id="17eb4-347">System.ServiceProcess.ServiceController</span></span>

| <span data-ttu-id="17eb4-348">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-348">Member</span></span> | <span data-ttu-id="17eb4-349">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-349">Platforms that throw</span></span> |
| - | - |
| <xref:System.ServiceProcess.TimeoutException.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | <span data-ttu-id="17eb4-350">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-350">All</span></span> |

## <a name="systemtextregularexpressions"></a><span data-ttu-id="17eb4-351">System.Text.RegularExpressions</span><span class="sxs-lookup"><span data-stu-id="17eb4-351">System.Text.RegularExpressions</span></span>

| <span data-ttu-id="17eb4-352">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-352">Member</span></span> | <span data-ttu-id="17eb4-353">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-353">Platforms that throw</span></span> |
| - | - |
| <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-354">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-354">All</span></span> |

## <a name="systemthreading"></a><span data-ttu-id="17eb4-355">System.Threading</span><span class="sxs-lookup"><span data-stu-id="17eb4-355">System.Threading</span></span>

| <span data-ttu-id="17eb4-356">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-356">Member</span></span> | <span data-ttu-id="17eb4-357">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-357">Platforms that throw</span></span> |
| - | - |
| <xref:System.Threading.CompressedStack.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-358">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-358">All</span></span> |
| <xref:System.Threading.ExecutionContext.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-359">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-359">All</span></span> |
| <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> | <span data-ttu-id="17eb4-360">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-360">All</span></span> |
| <xref:System.Threading.Thread.ResetAbort?displayProperty=nameWithType> | <span data-ttu-id="17eb4-361">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-361">All</span></span> |
| <xref:System.Threading.Thread.Resume?displayProperty=nameWithType> | <span data-ttu-id="17eb4-362">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-362">All</span></span> |
| <xref:System.Threading.Thread.Suspend?displayProperty=nameWithType> | <span data-ttu-id="17eb4-363">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-363">All</span></span> |

## <a name="systemxml"></a><span data-ttu-id="17eb4-364">System.Xml</span><span class="sxs-lookup"><span data-stu-id="17eb4-364">System.Xml</span></span>

| <span data-ttu-id="17eb4-365">成员</span><span class="sxs-lookup"><span data-stu-id="17eb4-365">Member</span></span> | <span data-ttu-id="17eb4-366">引发异常的平台</span><span class="sxs-lookup"><span data-stu-id="17eb4-366">Platforms that throw</span></span> |
| - | - |
| <xref:System.Xml.XmlDictionaryReader.CreateMtomReader(System.Byte[],System.Int32,System.Int32,System.Text.Encoding[],System.String,System.Xml.XmlDictionaryReaderQuotas,System.Int32,System.Xml.OnXmlDictionaryReaderClose)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-367">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-367">All</span></span> |
| <xref:System.Xml.XmlDictionaryReader.CreateMtomReader(System.IO.Stream,System.Text.Encoding[],System.String,System.Xml.XmlDictionaryReaderQuotas,System.Int32,System.Xml.OnXmlDictionaryReaderClose)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-368">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-368">All</span></span> |
| <xref:System.Xml.XmlDictionaryWriter.CreateMtomWriter(System.IO.Stream,System.Text.Encoding,System.Int32,System.String,System.String,System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType> | <span data-ttu-id="17eb4-369">All</span><span class="sxs-lookup"><span data-stu-id="17eb4-369">All</span></span> |

## <a name="see-also"></a><span data-ttu-id="17eb4-370">另请参阅</span><span class="sxs-lookup"><span data-stu-id="17eb4-370">See also</span></span>

- [<span data-ttu-id="17eb4-371">从 .NET Framework 迁移到 .NET Core 的中断性变更</span><span class="sxs-lookup"><span data-stu-id="17eb4-371">Breaking changes for migration from .NET Framework to .NET Core</span></span>](fx-core.md)
- [<span data-ttu-id="17eb4-372">.NET Core 中的二进制序列化</span><span class="sxs-lookup"><span data-stu-id="17eb4-372">Binary serialization in .NET Core</span></span>](../../standard/serialization/binary-serialization.md#net-core)
- [<span data-ttu-id="17eb4-373">.NET 可移植性分析器</span><span class="sxs-lookup"><span data-stu-id="17eb4-373">.NET portability analyzer</span></span>](../../standard/analyzers/portability-analyzer.md)
