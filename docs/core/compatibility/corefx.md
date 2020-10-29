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
# <a name="core-net-libraries-breaking-changes"></a>核心 .NET 库重大更改

核心 .NET 库提供了 .NET Core 使用的基元和其他常规类型。

本页记录了以下中断性变更：

| 重大更改 | 引入的版本 |
| - | :-: |
| [全局程序集缓存 API 已过时](#global-assembly-cache-apis-are-obsolete) | 5.0 |
| [远程处理 API 已过时](#remoting-apis-are-obsolete) | 5.0 |
| [大多数代码访问安全 API 已过时](#most-code-access-security-apis-are-obsolete) | 5.0 |
| [API 已过时并带有非默认诊断 ID](#api-obsoletions-with-non-default-diagnostic-ids) | 5.0 |
| [FrameworkDescription 的值是 .NET 而不是 .NET Core](#frameworkdescriptions-value-is-net-instead-of-net-core) | 5.0 |
| [针对单个文件发布格式的与程序集相关的 API 行为更改](#assembly-related-api-behavior-changes-for-single-file-publishing-format) | 5.0 |
| [ 中的标记顺序是相反的](#order-of-tags-in-activitytags-is-reversed) | 5.0 |
| [RC1 中的参数名称已更改](#parameter-names-changed-in-rc1) | 5.0 |
| [已重命名或已删除 OSPlatform 属性](#osplatform-attributes-renamed-or-removed) | 5.0 |
| [Thread.Abort 已过时](#threadabort-is-obsolete) | 5.0 |
| [ConsoleLoggerOptions 上已过时的属性](#obsolete-properties-on-consoleloggeroptions) | 5.0 |
| [嵌套类型的硬件内部 IsSupported 检查可能有所不同](#hardware-intrinsic-issupported-checks-may-differ-for-nested-types) | 5.0 |
| [引用程序集中的参数名称已更改](#parameter-names-changed-in-reference-assemblies) | 5.0 |
| [在 Unix 上正确分析包含非 ASCII 字符的 URI 路径](#uri-paths-with-non-ascii-characters-parse-correctly-on-unix) | 5.0 |
| [Unix 上 UNC 路径的 URI 识别](#uri-recognition-of-unc-paths-on-unix) | 5.0 |
| [Environment.OSVersion 返回正确的操作系统版本](#environmentosversion-returns-the-correct-operating-system-version) | 5.0 |
| [增加了 LINQ OrderBy.First{OrDefault} 的复杂度](#complexity-of-linq-orderbyfirstordefault-increased) | 5.0 |
| [IntPtr 和 UIntPtr 实现 IFormattable](#intptr-and-uintptr-implement-iformattable) | 5.0 |
| [PrincipalPermissionAttribute 已过时，报告为错误](#principalpermissionattribute-is-obsolete-as-error) | 5.0 |
| [BinaryFormatter 序列化方法已过时，并且已在 ASP.NET 应用中禁用](#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps) | 5.0 |
| [UTF-7 代码路径已过时](#utf-7-code-paths-are-obsolete) | 5.0 |
| [对于不支持的类型，Vector\<T> 始终引发 NotSupportedException](#vectort-always-throws-notsupportedexception-for-unsupported-types) | 5.0 |
| [默认 ActivityIdFormat 为 W3C](#default-activityidformat-is-w3c) | 5.0 |
| [Vector2.Lerp 和 Vector4.Lerp 的行为变更](#behavior-change-for-vector2lerp-and-vector4lerp) | 5.0 |
| [SSE 和 SSE2 CompareGreaterThan 方法正确处理 NaN 输入](#sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs) | 5.0 |
| [如果实例已存在，CounterSet.CreateCounterSetInstance 现在将引发 InvalidOperationException](#countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists) | 5.0 |
| [Microsoft.DotNet.PlatformAbstractions 包已删除](#microsoftdotnetplatformabstractions-package-removed) | 5.0 |
| [报告版本的 API 现在报告产品版本而不是文件版本](#apis-that-report-version-now-report-product-and-not-file-version) | 3.0 |
| [自定义 EncoderFallbackBuffer 实例无法递归回退](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | 3.0 |
| [浮点格式设置和分析行为变更](#floating-point-formatting-and-parsing-behavior-changed) | 3.0 |
| [浮点分析操作不再失败或引发 OverflowException](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | 3.0 |
| [InvalidAsynchronousStateException 已移到另一个程序集](#invalidasynchronousstateexception-moved-to-another-assembly) | 3.0 |
| [替换格式错误的 UTF-8 字节序列将遵循 Unicode 准则](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | 3.0 |
| [TypeDescriptionProviderAttribute 已移到另一个程序集](#typedescriptionproviderattribute-moved-to-another-assembly) | 3.0 |
| [ZipArchiveEntry 不再处理条目大小不一致的存档](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | 3.0 |
| [FieldInfo.SetValue 将对静态、仅初始化字段引发异常](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | 3.0 |
| [添加到内置结构类型的私有字段](#private-fields-added-to-built-in-struct-types) | 2.1 |
| [UseShellExecute 默认值更改](#change-in-default-value-of-useshellexecute) | 2.1 |
| [macOS 上的 OpenSSL 版本](#openssl-versions-on-macos) | 2.1 |
| [FileSystemInfo.Attributes 引发的 UnauthorizedAccessException](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | 1.0 |
| [不支持处理损坏的进程状态异常](#handling-corrupted-state-exceptions-is-not-supported) | 1.0 |
| [UriBuilder 属性不再预置前导字符](#uribuilder-properties-no-longer-prepend-leading-characters) | 1.0 |
| [Process.StartInfo 对未启动的进程引发 InvalidOperationException](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | 1.0 |

## <a name="net-50"></a>.NET 5.0

[!INCLUDE [remoting-apis-obsolete](../../../includes/core-changes/corefx/5.0/remoting-apis-obsolete.md)]

***

[!INCLUDE [globalassemblycache-property-obsolete](../../../includes/core-changes/corefx/5.0/global-assembly-cache-apis-obsolete.md)]

**_

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

## <a name="net-core-30"></a>.NET Core 3.0

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

## <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

_*_

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

_*_

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

_*_

## <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

_*_

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

_*_

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

_*_

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

_**
