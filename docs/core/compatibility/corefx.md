---
title: 基类库的重大更改
description: 列出核心 .NET 库中的重大更改。
ms.date: 07/27/2020
ms.openlocfilehash: 900fd4e0e071f19aa286dec84632006870822f26
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434907"
---
# <a name="core-net-libraries-breaking-changes"></a><span data-ttu-id="2f164-103">核心 .NET 库重大更改</span><span class="sxs-lookup"><span data-stu-id="2f164-103">Core .NET libraries breaking changes</span></span>

<span data-ttu-id="2f164-104">核心 .NET 库提供了 .NET Core 使用的基元和其他常规类型。</span><span class="sxs-lookup"><span data-stu-id="2f164-104">The core .NET libraries provide the primitives and other general types used by .NET Core.</span></span>

<span data-ttu-id="2f164-105">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="2f164-105">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="2f164-106">重大更改</span><span class="sxs-lookup"><span data-stu-id="2f164-106">Breaking change</span></span> | <span data-ttu-id="2f164-107">引入的版本</span><span class="sxs-lookup"><span data-stu-id="2f164-107">Version introduced</span></span> |
| - | :-: |
| [<span data-ttu-id="2f164-108">全局程序集缓存 API 已过时</span><span class="sxs-lookup"><span data-stu-id="2f164-108">Global assembly cache APIs are obsolete</span></span>](#global-assembly-cache-apis-are-obsolete) | <span data-ttu-id="2f164-109">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-109">5.0</span></span> |
| [<span data-ttu-id="2f164-110">远程处理 API 已过时</span><span class="sxs-lookup"><span data-stu-id="2f164-110">Remoting APIs are obsolete</span></span>](#remoting-apis-are-obsolete) | <span data-ttu-id="2f164-111">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-111">5.0</span></span> |
| [<span data-ttu-id="2f164-112">大多数代码访问安全 API 已过时</span><span class="sxs-lookup"><span data-stu-id="2f164-112">Most code access security APIs are obsolete</span></span>](#most-code-access-security-apis-are-obsolete) | <span data-ttu-id="2f164-113">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-113">5.0</span></span> |
| [<span data-ttu-id="2f164-114">API 已过时并带有非默认诊断 ID</span><span class="sxs-lookup"><span data-stu-id="2f164-114">API obsoletions with non-default diagnostic IDs</span></span>](#api-obsoletions-with-non-default-diagnostic-ids) | <span data-ttu-id="2f164-115">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-115">5.0</span></span> |
| [<span data-ttu-id="2f164-116">FrameworkDescription 的值是 .NET 而不是 .NET Core</span><span class="sxs-lookup"><span data-stu-id="2f164-116">FrameworkDescription's value is .NET instead of .NET Core</span></span>](#frameworkdescriptions-value-is-net-instead-of-net-core) | <span data-ttu-id="2f164-117">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-117">5.0</span></span> |
| [<span data-ttu-id="2f164-118">针对单个文件发布格式的与程序集相关的 API 行为更改</span><span class="sxs-lookup"><span data-stu-id="2f164-118">Assembly-related API behavior changes for single-file publishing format</span></span>](#assembly-related-api-behavior-changes-for-single-file-publishing-format) | <span data-ttu-id="2f164-119">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-119">5.0</span></span> |
| [<span data-ttu-id="2f164-120"> 中的标记顺序是相反的</span><span class="sxs-lookup"><span data-stu-id="2f164-120">Order of tags in Activity.Tags is reversed</span></span>](#order-of-tags-in-activitytags-is-reversed) | <span data-ttu-id="2f164-121">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-121">5.0</span></span> |
| [<span data-ttu-id="2f164-122">RC1 中的参数名称已更改</span><span class="sxs-lookup"><span data-stu-id="2f164-122">Parameter names changed in RC1</span></span>](#parameter-names-changed-in-rc1) | <span data-ttu-id="2f164-123">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-123">5.0</span></span> |
| [<span data-ttu-id="2f164-124">已重命名或已删除 OSPlatform 属性</span><span class="sxs-lookup"><span data-stu-id="2f164-124">OSPlatform attributes renamed or removed</span></span>](#osplatform-attributes-renamed-or-removed) | <span data-ttu-id="2f164-125">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-125">5.0</span></span> |
| [<span data-ttu-id="2f164-126">Thread.Abort 已过时</span><span class="sxs-lookup"><span data-stu-id="2f164-126">Thread.Abort is obsolete</span></span>](#threadabort-is-obsolete) | <span data-ttu-id="2f164-127">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-127">5.0</span></span> |
| [<span data-ttu-id="2f164-128">ConsoleLoggerOptions 上已过时的属性</span><span class="sxs-lookup"><span data-stu-id="2f164-128">Obsolete properties on ConsoleLoggerOptions</span></span>](#obsolete-properties-on-consoleloggeroptions) | <span data-ttu-id="2f164-129">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-129">5.0</span></span> |
| [<span data-ttu-id="2f164-130">嵌套类型的硬件内部 IsSupported 检查可能有所不同</span><span class="sxs-lookup"><span data-stu-id="2f164-130">Hardware intrinsic IsSupported checks may differ for nested types</span></span>](#hardware-intrinsic-issupported-checks-may-differ-for-nested-types) | <span data-ttu-id="2f164-131">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-131">5.0</span></span> |
| [<span data-ttu-id="2f164-132">引用程序集中的参数名称已更改</span><span class="sxs-lookup"><span data-stu-id="2f164-132">Parameter names changed in reference assemblies</span></span>](#parameter-names-changed-in-reference-assemblies) | <span data-ttu-id="2f164-133">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-133">5.0</span></span> |
| [<span data-ttu-id="2f164-134">在 Unix 上正确分析包含非 ASCII 字符的 URI 路径</span><span class="sxs-lookup"><span data-stu-id="2f164-134">URI paths with non-ASCII characters parse correctly on Unix</span></span>](#uri-paths-with-non-ascii-characters-parse-correctly-on-unix) | <span data-ttu-id="2f164-135">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-135">5.0</span></span> |
| [<span data-ttu-id="2f164-136">Unix 上 UNC 路径的 URI 识别</span><span class="sxs-lookup"><span data-stu-id="2f164-136">Uri recognition of UNC paths on Unix</span></span>](#uri-recognition-of-unc-paths-on-unix) | <span data-ttu-id="2f164-137">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-137">5.0</span></span> |
| [<span data-ttu-id="2f164-138">Environment.OSVersion 返回正确的操作系统版本</span><span class="sxs-lookup"><span data-stu-id="2f164-138">Environment.OSVersion returns the correct operating system version</span></span>](#environmentosversion-returns-the-correct-operating-system-version) | <span data-ttu-id="2f164-139">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-139">5.0</span></span> |
| [<span data-ttu-id="2f164-140">增加了 LINQ OrderBy.First{OrDefault} 的复杂度</span><span class="sxs-lookup"><span data-stu-id="2f164-140">Complexity of LINQ OrderBy.First{OrDefault} increased</span></span>](#complexity-of-linq-orderbyfirstordefault-increased) | <span data-ttu-id="2f164-141">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-141">5.0</span></span> |
| [<span data-ttu-id="2f164-142">IntPtr 和 UIntPtr 实现 IFormattable</span><span class="sxs-lookup"><span data-stu-id="2f164-142">IntPtr and UIntPtr implement IFormattable</span></span>](#intptr-and-uintptr-implement-iformattable) | <span data-ttu-id="2f164-143">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-143">5.0</span></span> |
| [<span data-ttu-id="2f164-144">PrincipalPermissionAttribute 已过时，报告为错误</span><span class="sxs-lookup"><span data-stu-id="2f164-144">PrincipalPermissionAttribute is obsolete as error</span></span>](#principalpermissionattribute-is-obsolete-as-error) | <span data-ttu-id="2f164-145">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-145">5.0</span></span> |
| [<span data-ttu-id="2f164-146">BinaryFormatter 序列化方法已过时，并且已在 ASP.NET 应用中禁用</span><span class="sxs-lookup"><span data-stu-id="2f164-146">BinaryFormatter serialization methods are obsolete and prohibited in ASP.NET apps</span></span>](#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps) | <span data-ttu-id="2f164-147">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-147">5.0</span></span> |
| [<span data-ttu-id="2f164-148">UTF-7 代码路径已过时</span><span class="sxs-lookup"><span data-stu-id="2f164-148">UTF-7 code paths are obsolete</span></span>](#utf-7-code-paths-are-obsolete) | <span data-ttu-id="2f164-149">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-149">5.0</span></span> |
| [<span data-ttu-id="2f164-150">对于不支持的类型，Vector\<T> 始终引发 NotSupportedException</span><span class="sxs-lookup"><span data-stu-id="2f164-150">Vector\<T> always throws NotSupportedException for unsupported types</span></span>](#vectort-always-throws-notsupportedexception-for-unsupported-types) | <span data-ttu-id="2f164-151">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-151">5.0</span></span> |
| [<span data-ttu-id="2f164-152">默认 ActivityIdFormat 为 W3C</span><span class="sxs-lookup"><span data-stu-id="2f164-152">Default ActivityIdFormat is W3C</span></span>](#default-activityidformat-is-w3c) | <span data-ttu-id="2f164-153">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-153">5.0</span></span> |
| [<span data-ttu-id="2f164-154">Vector2.Lerp 和 Vector4.Lerp 的行为变更</span><span class="sxs-lookup"><span data-stu-id="2f164-154">Behavior change for Vector2.Lerp and Vector4.Lerp</span></span>](#behavior-change-for-vector2lerp-and-vector4lerp) | <span data-ttu-id="2f164-155">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-155">5.0</span></span> |
| [<span data-ttu-id="2f164-156">SSE 和 SSE2 CompareGreaterThan 方法正确处理 NaN 输入</span><span class="sxs-lookup"><span data-stu-id="2f164-156">SSE and SSE2 CompareGreaterThan methods properly handle NaN inputs</span></span>](#sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs) | <span data-ttu-id="2f164-157">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-157">5.0</span></span> |
| [<span data-ttu-id="2f164-158">如果实例已存在，CounterSet.CreateCounterSetInstance 现在将引发 InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="2f164-158">CounterSet.CreateCounterSetInstance now throws InvalidOperationException if instance already exist</span></span>](#countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists) | <span data-ttu-id="2f164-159">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-159">5.0</span></span> |
| [<span data-ttu-id="2f164-160">Microsoft.DotNet.PlatformAbstractions 包已删除</span><span class="sxs-lookup"><span data-stu-id="2f164-160">Microsoft.DotNet.PlatformAbstractions package removed</span></span>](#microsoftdotnetplatformabstractions-package-removed) | <span data-ttu-id="2f164-161">5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-161">5.0</span></span> |
| [<span data-ttu-id="2f164-162">报告版本的 API 现在报告产品版本而不是文件版本</span><span class="sxs-lookup"><span data-stu-id="2f164-162">APIs that report version now report product and not file version</span></span>](#apis-that-report-version-now-report-product-and-not-file-version) | <span data-ttu-id="2f164-163">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-163">3.0</span></span> |
| [<span data-ttu-id="2f164-164">自定义 EncoderFallbackBuffer 实例无法递归回退</span><span class="sxs-lookup"><span data-stu-id="2f164-164">Custom EncoderFallbackBuffer instances cannot fall back recursively</span></span>](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | <span data-ttu-id="2f164-165">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-165">3.0</span></span> |
| [<span data-ttu-id="2f164-166">浮点格式设置和分析行为变更</span><span class="sxs-lookup"><span data-stu-id="2f164-166">Floating point formatting and parsing behavior changes</span></span>](#floating-point-formatting-and-parsing-behavior-changed) | <span data-ttu-id="2f164-167">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-167">3.0</span></span> |
| [<span data-ttu-id="2f164-168">浮点分析操作不再失败或引发 OverflowException</span><span class="sxs-lookup"><span data-stu-id="2f164-168">Floating-point parsing operations no longer fail or throw an OverflowException</span></span>](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | <span data-ttu-id="2f164-169">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-169">3.0</span></span> |
| [<span data-ttu-id="2f164-170">InvalidAsynchronousStateException 已移到另一个程序集</span><span class="sxs-lookup"><span data-stu-id="2f164-170">InvalidAsynchronousStateException moved to another assembly</span></span>](#invalidasynchronousstateexception-moved-to-another-assembly) | <span data-ttu-id="2f164-171">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-171">3.0</span></span> |
| [<span data-ttu-id="2f164-172">替换格式错误的 UTF-8 字节序列将遵循 Unicode 准则</span><span class="sxs-lookup"><span data-stu-id="2f164-172">Replacing ill-formed UTF-8 byte sequences follows Unicode guidelines</span></span>](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | <span data-ttu-id="2f164-173">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-173">3.0</span></span> |
| [<span data-ttu-id="2f164-174">TypeDescriptionProviderAttribute 已移到另一个程序集</span><span class="sxs-lookup"><span data-stu-id="2f164-174">TypeDescriptionProviderAttribute moved to another assembly</span></span>](#typedescriptionproviderattribute-moved-to-another-assembly) | <span data-ttu-id="2f164-175">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-175">3.0</span></span> |
| [<span data-ttu-id="2f164-176">ZipArchiveEntry 不再处理条目大小不一致的存档</span><span class="sxs-lookup"><span data-stu-id="2f164-176">ZipArchiveEntry no longer handles archives with inconsistent entry sizes</span></span>](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | <span data-ttu-id="2f164-177">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-177">3.0</span></span> |
| [<span data-ttu-id="2f164-178">FieldInfo.SetValue 将对静态、仅初始化字段引发异常</span><span class="sxs-lookup"><span data-stu-id="2f164-178">FieldInfo.SetValue throws exception for static, init-only fields</span></span>](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | <span data-ttu-id="2f164-179">3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-179">3.0</span></span> |
| [<span data-ttu-id="2f164-180">添加到内置结构类型的私有字段</span><span class="sxs-lookup"><span data-stu-id="2f164-180">Private fields added to built-in struct types</span></span>](#private-fields-added-to-built-in-struct-types) | <span data-ttu-id="2f164-181">2.1</span><span class="sxs-lookup"><span data-stu-id="2f164-181">2.1</span></span> |
| [<span data-ttu-id="2f164-182">UseShellExecute 默认值更改</span><span class="sxs-lookup"><span data-stu-id="2f164-182">Change in default value of UseShellExecute</span></span>](#change-in-default-value-of-useshellexecute) | <span data-ttu-id="2f164-183">2.1</span><span class="sxs-lookup"><span data-stu-id="2f164-183">2.1</span></span> |
| [<span data-ttu-id="2f164-184">macOS 上的 OpenSSL 版本</span><span class="sxs-lookup"><span data-stu-id="2f164-184">OpenSSL versions on macOS</span></span>](#openssl-versions-on-macos) | <span data-ttu-id="2f164-185">2.1</span><span class="sxs-lookup"><span data-stu-id="2f164-185">2.1</span></span> |
| [<span data-ttu-id="2f164-186">FileSystemInfo.Attributes 引发的 UnauthorizedAccessException</span><span class="sxs-lookup"><span data-stu-id="2f164-186">UnauthorizedAccessException thrown by FileSystemInfo.Attributes</span></span>](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | <span data-ttu-id="2f164-187">1.0</span><span class="sxs-lookup"><span data-stu-id="2f164-187">1.0</span></span> |
| [<span data-ttu-id="2f164-188">不支持处理损坏的进程状态异常</span><span class="sxs-lookup"><span data-stu-id="2f164-188">Handling corrupted-process-state exceptions is not supported</span></span>](#handling-corrupted-state-exceptions-is-not-supported) | <span data-ttu-id="2f164-189">1.0</span><span class="sxs-lookup"><span data-stu-id="2f164-189">1.0</span></span> |
| [<span data-ttu-id="2f164-190">UriBuilder 属性不再预置前导字符</span><span class="sxs-lookup"><span data-stu-id="2f164-190">UriBuilder properties no longer prepend leading characters</span></span>](#uribuilder-properties-no-longer-prepend-leading-characters) | <span data-ttu-id="2f164-191">1.0</span><span class="sxs-lookup"><span data-stu-id="2f164-191">1.0</span></span> |
| [<span data-ttu-id="2f164-192">Process.StartInfo 对未启动的进程引发 InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="2f164-192">Process.StartInfo throws InvalidOperationException for processes you didn't start</span></span>](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | <span data-ttu-id="2f164-193">1.0</span><span class="sxs-lookup"><span data-stu-id="2f164-193">1.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="2f164-194">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="2f164-194">.NET 5.0</span></span>

[!INCLUDE [remoting-apis-obsolete](../../../includes/core-changes/corefx/5.0/remoting-apis-obsolete.md)]

***

[!INCLUDE [globalassemblycache-property-obsolete](../../../includes/core-changes/corefx/5.0/global-assembly-cache-apis-obsolete.md)]

<span data-ttu-id="2f164-195">\*\*_</span><span class="sxs-lookup"><span data-stu-id="2f164-195">\*\*_</span></span>

[!INCLUDE [code-access-security-apis-obsolete](../../../includes/core-changes/corefx/5.0/code-access-security-apis-obsolete.md)]

_*_

[!INCLUDE [obsolete-apis-with-custom-diagnostics](../../../includes/core-changes/corefx/5.0/obsolete-apis-with-custom-diagnostics.md)]

_*_

[!INCLUDE [frameworkdescription-returns-net-not-net-core](../../../includes/core-changes/corefx/5.0/frameworkdescription-returns-net-not-net-core.md)]

_*_

[!INCLUDE [assembly-api-behavior-changes-for-single-file-publish](../../../includes/core-changes/corefx/5.0/assembly-api-behavior-changes-for-single-file-publish.md)]

_*_

[!INCLUDE [reverse-order-of-tags-in-activity-property](../../../includes/core-changes/corefx/5.0/reverse-order-of-tags-in-activity-property.md)]

_*_

[!INCLUDE [reference-assembly-parameter-names-rc1](../../../includes/core-changes/corefx/5.0/reference-assembly-parameter-names-rc1.md)]

_*_

[!INCLUDE [os-platform-attributes-renamed](../../../includes/core-changes/corefx/5.0/os-platform-attributes-renamed.md)]

_*_

[!INCLUDE [thread-abort-obsolete](../../../includes/core-changes/corefx/5.0/thread-abort-obsolete.md)]

_*_

[!INCLUDE [obsolete-consoleloggeroptions-properties](../../../includes/core-changes/corefx/5.0/obsolete-consoleloggeroptions-properties.md)]

_*_

[!INCLUDE [hardware-instrinsics-issupported-checks](../../../includes/core-changes/corefx/5.0/hardware-instrinsics-issupported-checks.md)]

_*_

[!INCLUDE [reference-assembly-parameter-names](../../../includes/core-changes/corefx/5.0/reference-assembly-parameter-names.md)]

_*_

[!INCLUDE [non-ascii-chars-in-uri-parsed-correctly](../../../includes/core-changes/corefx/5.0/non-ascii-chars-in-uri-parsed-correctly.md)]

_*_

[!INCLUDE [unc-path-recognition-unix](../../../includes/core-changes/corefx/5.0/unc-path-recognition-unix.md)]

_*_

[!INCLUDE [environment-osversion-returns-correct-version](../../../includes/core-changes/corefx/5.0/environment-osversion-returns-correct-version.md)]

_*_

[!INCLUDE [orderby-firstordefault-complexity-increase](../../../includes/core-changes/corefx/5.0/orderby-firstordefault-complexity-increase.md)]

_*_

[!INCLUDE [intptr-uintptr-implement-iformattable](../../../includes/core-changes/corefx/5.0/intptr-uintptr-implement-iformattable.md)]

_*_

[!INCLUDE [principalpermissionattribute-obsolete](../../../includes/core-changes/corefx/5.0/principalpermissionattribute-obsolete.md)]

_*_

[!INCLUDE [binaryformatter-serialization-obsolete](../../../includes/core-changes/corefx/5.0/binaryformatter-serialization-obsolete.md)]

_*_

[!INCLUDE [utf-7-code-paths-obsolete](../../../includes/core-changes/corefx/5.0/utf-7-code-paths-obsolete.md)]

_*_

[!INCLUDE [vectort-throws-notsupportedexception](../../../includes/core-changes/corefx/5.0/vectort-throws-notsupportedexception.md)]

_*_

[!INCLUDE [default-activityidformat-changed](../../../includes/core-changes/corefx/5.0/default-activityidformat-changed.md)]

_*_

[!INCLUDE [vector-lerp-behavior-change](../../../includes/core-changes/corefx/5.0/vector-lerp-behavior-change.md)]

_*_

[!INCLUDE [sse-comparegreaterthan-intrinsics](../../../includes/core-changes/corefx/5.0/sse-comparegreaterthan-intrinsics.md)]

_*_

[!INCLUDE [createcountersetinstance-throws-invalidoperation](../../../includes/core-changes/corefx/5.0/createcountersetinstance-throws-invalidoperation.md)]

_*_

[!INCLUDE [platformabstractions-package-removed](../../../includes/core-changes/corefx/5.0/platformabstractions-package-removed.md)]

_*_

## <a name="net-core-30"></a><span data-ttu-id="2f164-196">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="2f164-196">.NET Core 3.0</span></span>

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

_*_

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

_*_

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

_*_

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

_*_

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

_*_

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

_*_

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

_*_

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

_*_

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

_*_

## <a name="net-core-21"></a><span data-ttu-id="2f164-197">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="2f164-197">.NET Core 2.1</span></span>

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

_*_

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

_*_

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

_*_

## <a name="net-core-10"></a><span data-ttu-id="2f164-198">.NET Core 1.0</span><span class="sxs-lookup"><span data-stu-id="2f164-198">.NET Core 1.0</span></span>

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

_*_

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

_*_

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

_*_

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

<span data-ttu-id="2f164-199">_\*\*</span><span class="sxs-lookup"><span data-stu-id="2f164-199">_\*\*</span></span>
