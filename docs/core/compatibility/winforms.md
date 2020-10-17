---
title: Windows 窗体重大更改
description: 列出适用于 .NET Core 和 .NET 5 的 Windows 窗体中的中断性变更。
ms.date: 09/08/2020
ms.openlocfilehash: 2311faab026bf1dfde348e231937eff73ec46172
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91804851"
---
# <a name="breaking-changes-in-windows-forms"></a><span data-ttu-id="e2541-103">Windows 窗体中的中断性变更</span><span class="sxs-lookup"><span data-stu-id="e2541-103">Breaking changes in Windows Forms</span></span>

<span data-ttu-id="e2541-104">已在 .NET Core 的版本 3.0 中添加 Windows 窗体支持。</span><span class="sxs-lookup"><span data-stu-id="e2541-104">Windows Forms support was added to .NET Core in version 3.0.</span></span> <span data-ttu-id="e2541-105">本文按引入了中断性变更的 .NET 版本列出了 Windows 窗体的中断性变更。</span><span class="sxs-lookup"><span data-stu-id="e2541-105">This article lists breaking changes for Windows Forms by the .NET version in which they were introduced.</span></span> <span data-ttu-id="e2541-106">如果要从 .NET Framework 或 .NET Core 的早期版本（3.0 或更高版本）升级 Windows 窗体应用，本文能为你提供帮助。</span><span class="sxs-lookup"><span data-stu-id="e2541-106">If you're upgrading a Windows Forms app from .NET Framework or from a previous version of .NET Core (3.0 or later), this article applies to you.</span></span>

<span data-ttu-id="e2541-107">本页记录了以下中断性变更：</span><span class="sxs-lookup"><span data-stu-id="e2541-107">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="e2541-108">重大更改</span><span class="sxs-lookup"><span data-stu-id="e2541-108">Breaking change</span></span> | <span data-ttu-id="e2541-109">引入的版本</span><span class="sxs-lookup"><span data-stu-id="e2541-109">Version introduced</span></span> |
| - | :-: |
| [<span data-ttu-id="e2541-110">DataGridView 不再重置自定义单元格样式的字体</span><span class="sxs-lookup"><span data-stu-id="e2541-110">DataGridView no longer resets fonts for customized cell styles</span></span>](#datagridview-no-longer-resets-fonts-for-customized-cell-styles) | <span data-ttu-id="e2541-111">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-111">5.0</span></span> |
| [<span data-ttu-id="e2541-112">对于 WPF 和 WinForms 应用，OutputType 设置为 WinExe</span><span class="sxs-lookup"><span data-stu-id="e2541-112">OutputType set to WinExe for WPF and WinForms apps</span></span>](#outputtype-set-to-winexe-for-wpf-and-winforms-apps) | <span data-ttu-id="e2541-113">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-113">5.0</span></span> |
| [<span data-ttu-id="e2541-114">与 DataGridView 相关的 API 现在引发 InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="e2541-114">DataGridView-related APIs now throw InvalidOperationException</span></span>](#datagridview-related-apis-now-throw-invalidoperationexception) | <span data-ttu-id="e2541-115">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-115">5.0</span></span> |
| [<span data-ttu-id="e2541-116">WinForms 和 WPF 应用使用 Microsoft.NET.Sdk</span><span class="sxs-lookup"><span data-stu-id="e2541-116">WinForms and WPF apps use Microsoft.NET.Sdk</span></span>](#winforms-and-wpf-apps-use-microsoftnetsdk) | <span data-ttu-id="e2541-117">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-117">5.0</span></span> |
| [<span data-ttu-id="e2541-118">已删除的状态栏控件</span><span class="sxs-lookup"><span data-stu-id="e2541-118">Removed status bar controls</span></span>](#removed-status-bar-controls) | <span data-ttu-id="e2541-119">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-119">5.0</span></span> |
| [<span data-ttu-id="e2541-120">WinForms 方法现在会引发 ArgumentException</span><span class="sxs-lookup"><span data-stu-id="e2541-120">WinForms methods now throw ArgumentException</span></span>](#winforms-methods-now-throw-argumentexception) | <span data-ttu-id="e2541-121">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-121">5.0</span></span> |
| [<span data-ttu-id="e2541-122">WinForms 方法现在会引发 ArgumentNullException</span><span class="sxs-lookup"><span data-stu-id="e2541-122">WinForms methods now throw ArgumentNullException</span></span>](#winforms-methods-now-throw-argumentnullexception) | <span data-ttu-id="e2541-123">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-123">5.0</span></span> |
| [<span data-ttu-id="e2541-124">WinForms 属性现在引发 ArgumentOutOfRangeException</span><span class="sxs-lookup"><span data-stu-id="e2541-124">WinForms properties now throw ArgumentOutOfRangeException</span></span>](#winforms-properties-now-throw-argumentoutofrangeexception) | <span data-ttu-id="e2541-125">5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-125">5.0</span></span> |
| [<span data-ttu-id="e2541-126">已删除的控件</span><span class="sxs-lookup"><span data-stu-id="e2541-126">Removed controls</span></span>](#removed-controls) | <span data-ttu-id="e2541-127">3.1</span><span class="sxs-lookup"><span data-stu-id="e2541-127">3.1</span></span> |
| [<span data-ttu-id="e2541-128">如果显示工具提示，则不引发 CellFormatting 事件</span><span class="sxs-lookup"><span data-stu-id="e2541-128">CellFormatting event not raised if tooltip is shown</span></span>](#cellformatting-event-not-raised-if-tooltip-is-shown) | <span data-ttu-id="e2541-129">3.1</span><span class="sxs-lookup"><span data-stu-id="e2541-129">3.1</span></span> |
| [<span data-ttu-id="e2541-130">Control.DefaultFont 已更改为 Segoe UI 9 pt</span><span class="sxs-lookup"><span data-stu-id="e2541-130">Control.DefaultFont changed to Segoe UI 9 pt</span></span>](#default-control-font-changed-to-segoe-ui-9-pt) | <span data-ttu-id="e2541-131">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-131">3.0</span></span> |
| [<span data-ttu-id="e2541-132">FolderBrowserDialog 的现代化</span><span class="sxs-lookup"><span data-stu-id="e2541-132">Modernization of the FolderBrowserDialog</span></span>](#modernization-of-the-folderbrowserdialog) | <span data-ttu-id="e2541-133">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-133">3.0</span></span> |
| [<span data-ttu-id="e2541-134">已从一些 Windows 窗体类型中删除 SerializableAttribute</span><span class="sxs-lookup"><span data-stu-id="e2541-134">SerializableAttribute removed from some Windows Forms types</span></span>](#serializableattribute-removed-from-some-windows-forms-types) | <span data-ttu-id="e2541-135">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-135">3.0</span></span> |
| [<span data-ttu-id="e2541-136">不支持 AllowUpdateChildControlIndexForTabControls 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-136">AllowUpdateChildControlIndexForTabControls compatibility switch not supported</span></span>](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported) | <span data-ttu-id="e2541-137">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-137">3.0</span></span> |
| [<span data-ttu-id="e2541-138">不支持 DomainUpDown.UseLegacyScrolling 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-138">DomainUpDown.UseLegacyScrolling compatibility switch not supported</span></span>](#domainupdownuselegacyscrolling-compatibility-switch-not-supported) | <span data-ttu-id="e2541-139">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-139">3.0</span></span> |
| [<span data-ttu-id="e2541-140">不支持 DoNotLoadLatestRichEditControl 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-140">DoNotLoadLatestRichEditControl compatibility switch not supported</span></span>](#donotloadlatestricheditcontrol-compatibility-switch-not-supported) | <span data-ttu-id="e2541-141">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-141">3.0</span></span> |
| [<span data-ttu-id="e2541-142">不支持 DoNotSupportSelectAllShortcutInMultilineTextBox 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-142">DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported</span></span>](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported) | <span data-ttu-id="e2541-143">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-143">3.0</span></span> |
| [<span data-ttu-id="e2541-144">不支持 DontSupportReentrantFilterMessage 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-144">DontSupportReentrantFilterMessage compatibility switch not supported</span></span>](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported) | <span data-ttu-id="e2541-145">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-145">3.0</span></span> |
| [<span data-ttu-id="e2541-146">不支持 EnableVisualStyleValidation 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-146">EnableVisualStyleValidation compatibility switch not supported</span></span>](#enablevisualstylevalidation-compatibility-switch-not-supported) | <span data-ttu-id="e2541-147">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-147">3.0</span></span> |
| [<span data-ttu-id="e2541-148">不支持 UseLegacyContextMenuStripSourceControlValue 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-148">UseLegacyContextMenuStripSourceControlValue compatibility switch not supported</span></span>](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported) | <span data-ttu-id="e2541-149">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-149">3.0</span></span> |
| [<span data-ttu-id="e2541-150">不支持 UseLegacyImages 兼容性开关</span><span class="sxs-lookup"><span data-stu-id="e2541-150">UseLegacyImages compatibility switch not supported</span></span>](#uselegacyimages-compatibility-switch-not-supported) | <span data-ttu-id="e2541-151">3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-151">3.0</span></span> |

## <a name="net-50"></a><span data-ttu-id="e2541-152">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="e2541-152">.NET 5.0</span></span>

[!INCLUDE [datagridview-doesnt-reset-custom-font-settings](../../../includes/core-changes/windowsforms/5.0/datagridview-doesnt-reset-custom-font-settings.md)]

***

[!INCLUDE [automatically-infer-winexe-output-type](../../../includes/core-changes/windowsforms/5.0/automatically-infer-winexe-output-type.md)]

***

[!INCLUDE [null-owner-causes-invalidoperationexception](../../../includes/core-changes/windowsforms/5.0/null-owner-causes-invalidoperationexception.md)]

***

[!INCLUDE [sdk-and-target-framework-change](../../../includes/core-changes/windowsforms/5.0/sdk-and-target-framework-change.md)]

***

[!INCLUDE [winforms-deprecated-controls](../../../includes/core-changes/windowsforms/5.0/winforms-deprecated-controls.md)]

***

[!INCLUDE [invalid-args-cause-argumentexception](../../../includes/core-changes/windowsforms/5.0/invalid-args-cause-argumentexception.md)]

***

[!INCLUDE [null-args-cause-argumentnullexception](../../../includes/core-changes/windowsforms/5.0/null-args-cause-argumentnullexception.md)]

***

[!INCLUDE [invalid-args-cause-argumentoutofrangeexception](../../../includes/core-changes/windowsforms/5.0/invalid-args-cause-argumentoutofrangeexception.md)]

***

## <a name="net-core-31"></a><span data-ttu-id="e2541-153">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="e2541-153">.NET Core 3.1</span></span>

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

***

## <a name="net-core-30"></a><span data-ttu-id="e2541-154">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="e2541-154">.NET Core 3.0</span></span>

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

***

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

***

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

***

## <a name="see-also"></a><span data-ttu-id="e2541-155">请参阅</span><span class="sxs-lookup"><span data-stu-id="e2541-155">See also</span></span>

- [<span data-ttu-id="e2541-156">将 Windows 窗体应用移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="e2541-156">Port a Windows Forms app to .NET Core</span></span>](../porting/winforms.md)
