---
title: 基类库的重大更改
description: 列出核心 .NET 库中的重大更改。
ms.date: 07/27/2020
ms.openlocfilehash: 3ecf0e81a3adef097aafb760dc44498d7263f0b6
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050555"
---
# <a name="core-net-libraries-breaking-changes"></a><span data-ttu-id="f4548-103">核心 .NET 库重大更改</span><span class="sxs-lookup"><span data-stu-id="f4548-103">Core .NET libraries breaking changes</span></span>

<span data-ttu-id="f4548-104">核心 .NET 库提供了 .NET Core 使用的基元和其他常规类型。</span><span class="sxs-lookup"><span data-stu-id="f4548-104">The core .NET libraries provide the primitives and other general types used by .NET Core.</span></span>

<span data-ttu-id="f4548-105">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="f4548-105">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="f4548-106">重大更改</span><span class="sxs-lookup"><span data-stu-id="f4548-106">Breaking change</span></span> | <span data-ttu-id="f4548-107">引入的版本</span><span class="sxs-lookup"><span data-stu-id="f4548-107">Version introduced</span></span> |
| - | :-: |
| [<span data-ttu-id="f4548-108">FrameworkDescription 的值是 .NET 而不是 .NET Core</span><span class="sxs-lookup"><span data-stu-id="f4548-108">FrameworkDescription's value is .NET instead of .NET Core</span></span>](#frameworkdescriptions-value-is-net-instead-of-net-core) | <span data-ttu-id="f4548-109">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-109">5.0</span></span> |
| [<span data-ttu-id="f4548-110">针对单个文件发布格式的与程序集相关的 API 行为更改</span><span class="sxs-lookup"><span data-stu-id="f4548-110">Assembly-related API behavior changes for single-file publishing format</span></span>](#assembly-related-api-behavior-changes-for-single-file-publishing-format) | <span data-ttu-id="f4548-111">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-111">5.0</span></span> |
| [<span data-ttu-id="f4548-112"> 中的标记顺序是相反的</span><span class="sxs-lookup"><span data-stu-id="f4548-112">Order of tags in Activity.Tags is reversed</span></span>](#order-of-tags-in-activitytags-is-reversed) | <span data-ttu-id="f4548-113">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-113">5.0</span></span> |
| [<span data-ttu-id="f4548-114">RC1 中的参数名称已更改</span><span class="sxs-lookup"><span data-stu-id="f4548-114">Parameter names changed in RC1</span></span>](#parameter-names-changed-in-rc1) | <span data-ttu-id="f4548-115">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-115">5.0</span></span> |
| [<span data-ttu-id="f4548-116">已重命名或已删除 OSPlatform 属性</span><span class="sxs-lookup"><span data-stu-id="f4548-116">OSPlatform attributes renamed or removed</span></span>](#osplatform-attributes-renamed-or-removed) | <span data-ttu-id="f4548-117">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-117">5.0</span></span> |
| [<span data-ttu-id="f4548-118">Thread.Abort 已过时</span><span class="sxs-lookup"><span data-stu-id="f4548-118">Thread.Abort is obsolete</span></span>](#threadabort-is-obsolete) | <span data-ttu-id="f4548-119">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-119">5.0</span></span> |
| [<span data-ttu-id="f4548-120">ConsoleLoggerOptions 上已过时的属性</span><span class="sxs-lookup"><span data-stu-id="f4548-120">Obsolete properties on ConsoleLoggerOptions</span></span>](#obsolete-properties-on-consoleloggeroptions) | <span data-ttu-id="f4548-121">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-121">5.0</span></span> |
| [<span data-ttu-id="f4548-122">嵌套类型的硬件内部 IsSupported 检查可能有所不同</span><span class="sxs-lookup"><span data-stu-id="f4548-122">Hardware intrinsic IsSupported checks may differ for nested types</span></span>](#hardware-intrinsic-issupported-checks-may-differ-for-nested-types) | <span data-ttu-id="f4548-123">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-123">5.0</span></span> |
| [<span data-ttu-id="f4548-124">引用程序集中的参数名称已更改</span><span class="sxs-lookup"><span data-stu-id="f4548-124">Parameter names changed in reference assemblies</span></span>](#parameter-names-changed-in-reference-assemblies) | <span data-ttu-id="f4548-125">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-125">5.0</span></span> |
| [<span data-ttu-id="f4548-126">在 Unix 上正确分析包含非 ASCII 字符的 URI 路径</span><span class="sxs-lookup"><span data-stu-id="f4548-126">URI paths with non-ASCII characters parse correctly on Unix</span></span>](#uri-paths-with-non-ascii-characters-parse-correctly-on-unix) | <span data-ttu-id="f4548-127">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-127">5.0</span></span> |
| [<span data-ttu-id="f4548-128">Unix 上 UNC 路径的 URI 识别</span><span class="sxs-lookup"><span data-stu-id="f4548-128">Uri recognition of UNC paths on Unix</span></span>](#uri-recognition-of-unc-paths-on-unix) | <span data-ttu-id="f4548-129">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-129">5.0</span></span> |
| [<span data-ttu-id="f4548-130">Environment.OSVersion 返回正确的操作系统版本</span><span class="sxs-lookup"><span data-stu-id="f4548-130">Environment.OSVersion returns the correct operating system version</span></span>](#environmentosversion-returns-the-correct-operating-system-version) | <span data-ttu-id="f4548-131">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-131">5.0</span></span> |
| [<span data-ttu-id="f4548-132">增加了 LINQ OrderBy.First{OrDefault} 的复杂度</span><span class="sxs-lookup"><span data-stu-id="f4548-132">Complexity of LINQ OrderBy.First{OrDefault} increased</span></span>](#complexity-of-linq-orderbyfirstordefault-increased) | <span data-ttu-id="f4548-133">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-133">5.0</span></span> |
| [<span data-ttu-id="f4548-134">IntPtr 和 UIntPtr 实现 IFormattable</span><span class="sxs-lookup"><span data-stu-id="f4548-134">IntPtr and UIntPtr implement IFormattable</span></span>](#intptr-and-uintptr-implement-iformattable) | <span data-ttu-id="f4548-135">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-135">5.0</span></span> |
| [<span data-ttu-id="f4548-136">PrincipalPermissionAttribute 已过时，报告为错误</span><span class="sxs-lookup"><span data-stu-id="f4548-136">PrincipalPermissionAttribute is obsolete as error</span></span>](#principalpermissionattribute-is-obsolete-as-error) | <span data-ttu-id="f4548-137">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-137">5.0</span></span> |
| [<span data-ttu-id="f4548-138">BinaryFormatter 序列化方法已过时，并且已在 ASP.NET 应用中禁用</span><span class="sxs-lookup"><span data-stu-id="f4548-138">BinaryFormatter serialization methods are obsolete and prohibited in ASP.NET apps</span></span>](#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps) | <span data-ttu-id="f4548-139">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-139">5.0</span></span> |
| [<span data-ttu-id="f4548-140">UTF-7 代码路径已过时</span><span class="sxs-lookup"><span data-stu-id="f4548-140">UTF-7 code paths are obsolete</span></span>](#utf-7-code-paths-are-obsolete) | <span data-ttu-id="f4548-141">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-141">5.0</span></span> |
| [<span data-ttu-id="f4548-142">对于不支持的类型，Vector\<T> 始终引发 NotSupportedException</span><span class="sxs-lookup"><span data-stu-id="f4548-142">Vector\<T> always throws NotSupportedException for unsupported types</span></span>](#vectort-always-throws-notsupportedexception-for-unsupported-types) | <span data-ttu-id="f4548-143">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-143">5.0</span></span> |
| [<span data-ttu-id="f4548-144">默认 ActivityIdFormat 为 W3C</span><span class="sxs-lookup"><span data-stu-id="f4548-144">Default ActivityIdFormat is W3C</span></span>](#default-activityidformat-is-w3c) | <span data-ttu-id="f4548-145">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-145">5.0</span></span> |
| [<span data-ttu-id="f4548-146">Vector2.Lerp 和 Vector4.Lerp 的行为变更</span><span class="sxs-lookup"><span data-stu-id="f4548-146">Behavior change for Vector2.Lerp and Vector4.Lerp</span></span>](#behavior-change-for-vector2lerp-and-vector4lerp) | <span data-ttu-id="f4548-147">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-147">5.0</span></span> |
| [<span data-ttu-id="f4548-148">SSE 和 SSE2 CompareGreaterThan 方法正确处理 NaN 输入</span><span class="sxs-lookup"><span data-stu-id="f4548-148">SSE and SSE2 CompareGreaterThan methods properly handle NaN inputs</span></span>](#sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs) | <span data-ttu-id="f4548-149">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-149">5.0</span></span> |
| [<span data-ttu-id="f4548-150">如果实例已存在，CounterSet.CreateCounterSetInstance 现在将引发 InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="f4548-150">CounterSet.CreateCounterSetInstance now throws InvalidOperationException if instance already exist</span></span>](#countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists) | <span data-ttu-id="f4548-151">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-151">5.0</span></span> |
| [<span data-ttu-id="f4548-152">Microsoft.DotNet.PlatformAbstractions 包已删除</span><span class="sxs-lookup"><span data-stu-id="f4548-152">Microsoft.DotNet.PlatformAbstractions package removed</span></span>](#microsoftdotnetplatformabstractions-package-removed) | <span data-ttu-id="f4548-153">5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-153">5.0</span></span> |
| [<span data-ttu-id="f4548-154">报告版本的 API 现在报告产品版本而不是文件版本</span><span class="sxs-lookup"><span data-stu-id="f4548-154">APIs that report version now report product and not file version</span></span>](#apis-that-report-version-now-report-product-and-not-file-version) | <span data-ttu-id="f4548-155">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-155">3.0</span></span> |
| [<span data-ttu-id="f4548-156">自定义 EncoderFallbackBuffer 实例无法递归回退</span><span class="sxs-lookup"><span data-stu-id="f4548-156">Custom EncoderFallbackBuffer instances cannot fall back recursively</span></span>](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | <span data-ttu-id="f4548-157">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-157">3.0</span></span> |
| [<span data-ttu-id="f4548-158">浮点格式设置和分析行为变更</span><span class="sxs-lookup"><span data-stu-id="f4548-158">Floating point formatting and parsing behavior changes</span></span>](#floating-point-formatting-and-parsing-behavior-changed) | <span data-ttu-id="f4548-159">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-159">3.0</span></span> |
| [<span data-ttu-id="f4548-160">浮点分析操作不再失败或引发 OverflowException</span><span class="sxs-lookup"><span data-stu-id="f4548-160">Floating-point parsing operations no longer fail or throw an OverflowException</span></span>](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | <span data-ttu-id="f4548-161">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-161">3.0</span></span> |
| [<span data-ttu-id="f4548-162">InvalidAsynchronousStateException 已移到另一个程序集</span><span class="sxs-lookup"><span data-stu-id="f4548-162">InvalidAsynchronousStateException moved to another assembly</span></span>](#invalidasynchronousstateexception-moved-to-another-assembly) | <span data-ttu-id="f4548-163">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-163">3.0</span></span> |
| [<span data-ttu-id="f4548-164">替换格式错误的 UTF-8 字节序列将遵循 Unicode 准则</span><span class="sxs-lookup"><span data-stu-id="f4548-164">Replacing ill-formed UTF-8 byte sequences follows Unicode guidelines</span></span>](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | <span data-ttu-id="f4548-165">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-165">3.0</span></span> |
| [<span data-ttu-id="f4548-166">TypeDescriptionProviderAttribute 已移到另一个程序集</span><span class="sxs-lookup"><span data-stu-id="f4548-166">TypeDescriptionProviderAttribute moved to another assembly</span></span>](#typedescriptionproviderattribute-moved-to-another-assembly) | <span data-ttu-id="f4548-167">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-167">3.0</span></span> |
| [<span data-ttu-id="f4548-168">ZipArchiveEntry 不再处理条目大小不一致的存档</span><span class="sxs-lookup"><span data-stu-id="f4548-168">ZipArchiveEntry no longer handles archives with inconsistent entry sizes</span></span>](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | <span data-ttu-id="f4548-169">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-169">3.0</span></span> |
| [<span data-ttu-id="f4548-170">FieldInfo.SetValue 将对静态、仅初始化字段引发异常</span><span class="sxs-lookup"><span data-stu-id="f4548-170">FieldInfo.SetValue throws exception for static, init-only fields</span></span>](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | <span data-ttu-id="f4548-171">3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-171">3.0</span></span> |
| [<span data-ttu-id="f4548-172">添加到内置结构类型的私有字段</span><span class="sxs-lookup"><span data-stu-id="f4548-172">Private fields added to built-in struct types</span></span>](#private-fields-added-to-built-in-struct-types) | <span data-ttu-id="f4548-173">2.1</span><span class="sxs-lookup"><span data-stu-id="f4548-173">2.1</span></span> |
| [<span data-ttu-id="f4548-174">UseShellExecute 默认值更改</span><span class="sxs-lookup"><span data-stu-id="f4548-174">Change in default value of UseShellExecute</span></span>](#change-in-default-value-of-useshellexecute) | <span data-ttu-id="f4548-175">2.1</span><span class="sxs-lookup"><span data-stu-id="f4548-175">2.1</span></span> |
| [<span data-ttu-id="f4548-176">macOS 上的 OpenSSL 版本</span><span class="sxs-lookup"><span data-stu-id="f4548-176">OpenSSL versions on macOS</span></span>](#openssl-versions-on-macos) | <span data-ttu-id="f4548-177">2.1</span><span class="sxs-lookup"><span data-stu-id="f4548-177">2.1</span></span> |
| [<span data-ttu-id="f4548-178">FileSystemInfo.Attributes 引发的 UnauthorizedAccessException</span><span class="sxs-lookup"><span data-stu-id="f4548-178">UnauthorizedAccessException thrown by FileSystemInfo.Attributes</span></span>](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | <span data-ttu-id="f4548-179">1.0</span><span class="sxs-lookup"><span data-stu-id="f4548-179">1.0</span></span> |
| [<span data-ttu-id="f4548-180">不支持处理损坏的进程状态异常</span><span class="sxs-lookup"><span data-stu-id="f4548-180">Handling corrupted-process-state exceptions is not supported</span></span>](#handling-corrupted-state-exceptions-is-not-supported) | <span data-ttu-id="f4548-181">1.0</span><span class="sxs-lookup"><span data-stu-id="f4548-181">1.0</span></span> |
| [<span data-ttu-id="f4548-182">UriBuilder 属性不再预置前导字符</span><span class="sxs-lookup"><span data-stu-id="f4548-182">UriBuilder properties no longer prepend leading characters</span></span>](#uribuilder-properties-no-longer-prepend-leading-characters) | <span data-ttu-id="f4548-183">1.0</span><span class="sxs-lookup"><span data-stu-id="f4548-183">1.0</span></span> |
| [<span data-ttu-id="f4548-184">Process.StartInfo 对未启动的进程引发 InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="f4548-184">Process.StartInfo throws InvalidOperationException for processes you didn't start</span></span>](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | <span data-ttu-id="f4548-185">1.0</span><span class="sxs-lookup"><span data-stu-id="f4548-185">1.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="f4548-186">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="f4548-186">.NET 5.0</span></span>

[!INCLUDE [frameworkdescription-returns-net-not-net-core](../../../includes/core-changes/corefx/5.0/frameworkdescription-returns-net-not-net-core.md)]

***

[!INCLUDE [assembly-api-behavior-changes-for-single-file-publish](../../../includes/core-changes/corefx/5.0/assembly-api-behavior-changes-for-single-file-publish.md)]

***

[!INCLUDE [reverse-order-of-tags-in-activity-property](../../../includes/core-changes/corefx/5.0/reverse-order-of-tags-in-activity-property.md)]

***

[!INCLUDE [reference-assembly-parameter-names-rc1](../../../includes/core-changes/corefx/5.0/reference-assembly-parameter-names-rc1.md)]

***

[!INCLUDE [os-platform-attributes-renamed](../../../includes/core-changes/corefx/5.0/os-platform-attributes-renamed.md)]

***

[!INCLUDE [thread-abort-obsolete](../../../includes/core-changes/corefx/5.0/thread-abort-obsolete.md)]

***

[!INCLUDE [obsolete-consoleloggeroptions-properties](../../../includes/core-changes/corefx/5.0/obsolete-consoleloggeroptions-properties.md)]

***

[!INCLUDE [hardware-instrinsics-issupported-checks](../../../includes/core-changes/corefx/5.0/hardware-instrinsics-issupported-checks.md)]

***

[!INCLUDE [reference-assembly-parameter-names](../../../includes/core-changes/corefx/5.0/reference-assembly-parameter-names.md)]

***

[!INCLUDE [non-ascii-chars-in-uri-parsed-correctly](../../../includes/core-changes/corefx/5.0/non-ascii-chars-in-uri-parsed-correctly.md)]

***

[!INCLUDE [unc-path-recognition-unix](../../../includes/core-changes/corefx/5.0/unc-path-recognition-unix.md)]

***

[!INCLUDE [environment-osversion-returns-correct-version](../../../includes/core-changes/corefx/5.0/environment-osversion-returns-correct-version.md)]

***

[!INCLUDE [orderby-firstordefault-complexity-increase](../../../includes/core-changes/corefx/5.0/orderby-firstordefault-complexity-increase.md)]

***

[!INCLUDE [intptr-uintptr-implement-iformattable](../../../includes/core-changes/corefx/5.0/intptr-uintptr-implement-iformattable.md)]

***

[!INCLUDE [principalpermissionattribute-obsolete](../../../includes/core-changes/corefx/5.0/principalpermissionattribute-obsolete.md)]

***

[!INCLUDE [binaryformatter-serialization-obsolete](../../../includes/core-changes/corefx/5.0/binaryformatter-serialization-obsolete.md)]

***

[!INCLUDE [utf-7-code-paths-obsolete](../../../includes/core-changes/corefx/5.0/utf-7-code-paths-obsolete.md)]

***

[!INCLUDE [vectort-throws-notsupportedexception](../../../includes/core-changes/corefx/5.0/vectort-throws-notsupportedexception.md)]

***

[!INCLUDE [default-activityidformat-changed](../../../includes/core-changes/corefx/5.0/default-activityidformat-changed.md)]

***

[!INCLUDE [vector-lerp-behavior-change](../../../includes/core-changes/corefx/5.0/vector-lerp-behavior-change.md)]

***

[!INCLUDE [sse-comparegreaterthan-intrinsics](../../../includes/core-changes/corefx/5.0/sse-comparegreaterthan-intrinsics.md)]

***

[!INCLUDE [createcountersetinstance-throws-invalidoperation](../../../includes/core-changes/corefx/5.0/createcountersetinstance-throws-invalidoperation.md)]

***

[!INCLUDE [platformabstractions-package-removed](../../../includes/core-changes/corefx/5.0/platformabstractions-package-removed.md)]

***

## <a name="net-core-30"></a><span data-ttu-id="f4548-187">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="f4548-187">.NET Core 3.0</span></span>

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

***

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

***

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

***

## <a name="net-core-21"></a><span data-ttu-id="f4548-188">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="f4548-188">.NET Core 2.1</span></span>

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

***

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

***

## <a name="net-core-10"></a><span data-ttu-id="f4548-189">.NET Core 1.0</span><span class="sxs-lookup"><span data-stu-id="f4548-189">.NET Core 1.0</span></span>

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

***

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

***

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

***
