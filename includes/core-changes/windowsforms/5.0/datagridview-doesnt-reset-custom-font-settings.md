---
ms.openlocfilehash: 9c84c9f844a2a7efb9633c11634b069ef6b6033b
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91804852"
---
### <a name="datagridview-no-longer-resets-fonts-for-customized-cell-styles"></a><span data-ttu-id="7a9df-101">DataGridView 不再重置自定义单元格样式的字体</span><span class="sxs-lookup"><span data-stu-id="7a9df-101">DataGridView no longer resets fonts for customized cell styles</span></span>

<span data-ttu-id="7a9df-102">当环境字体更改时，如果已自定义单元格样式字体，则 <xref:System.Windows.Forms.DataGridViewElement.DataGridView> 不再重置默认单元格样式字体，以让其与环境字体一致。</span><span class="sxs-lookup"><span data-stu-id="7a9df-102">When the ambient font changes, <xref:System.Windows.Forms.DataGridViewElement.DataGridView> no longer resets default cell style fonts to match the ambient font if the cell style font has been customized.</span></span>

#### <a name="change-description"></a><span data-ttu-id="7a9df-103">更改描述</span><span class="sxs-lookup"><span data-stu-id="7a9df-103">Change description</span></span>

<span data-ttu-id="7a9df-104">在以前的 .NET 版本中，如果环境字体发生更改，<xref:System.Windows.Forms.DataGridViewElement.DataGridView> 将重置并覆盖 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>、<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> 和 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> 属性中的用户定义的字体。</span><span class="sxs-lookup"><span data-stu-id="7a9df-104">In previous .NET versions, if the ambient font changes, <xref:System.Windows.Forms.DataGridViewElement.DataGridView> resets and overrides user-defined fonts in the <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle>, and <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> properties.</span></span>

<span data-ttu-id="7a9df-105">从 .NET 5.0 开始，如果在 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>、<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> 或 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> 属性中配置了字体设置，即使环境字体发生更改，也会保留这些设置。</span><span class="sxs-lookup"><span data-stu-id="7a9df-105">Starting in .NET 5.0, if you configure font settings in the <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle>, or <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> properties, those settings are retained even when the ambient font changes.</span></span> <span data-ttu-id="7a9df-106">对于任何未自定义字体的属性，字体都将被更改为与环境字体设置一致。</span><span class="sxs-lookup"><span data-stu-id="7a9df-106">For any of these properties that you don't customize the font, the font will change to match the ambient font settings.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="7a9df-107">更改原因</span><span class="sxs-lookup"><span data-stu-id="7a9df-107">Reason for change</span></span>

<span data-ttu-id="7a9df-108">[.NET Core 3.0](../../../../docs/core/compatibility/winforms.md#default-control-font-changed-to-segoe-ui-9-pt) 中的默认字体更改时，各单元格样式的默认字体设置也会更改。</span><span class="sxs-lookup"><span data-stu-id="7a9df-108">With the [change of the default font in .NET Core 3.0](../../../../docs/core/compatibility/winforms.md#default-control-font-changed-to-segoe-ui-9-pt), the default font settings for the various cell styles also changed.</span></span> <span data-ttu-id="7a9df-109">如果应用程序依赖其 <xref:System.Windows.Forms.DataGridViewElement.DataGridView> 控件中的自定义样式，妨碍这些应用从 .NET Framework 迁移至 .NET 5.0，则不需要这种行为。</span><span class="sxs-lookup"><span data-stu-id="7a9df-109">This behavior is undesirable for apps that rely on custom styling in their <xref:System.Windows.Forms.DataGridViewElement.DataGridView> controls, and impeded the migration of these apps from .NET Framework to .NET 5.0.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="7a9df-110">引入的版本</span><span class="sxs-lookup"><span data-stu-id="7a9df-110">Version introduced</span></span>

<span data-ttu-id="7a9df-111">.NET 5.0 RC2</span><span class="sxs-lookup"><span data-stu-id="7a9df-111">.NET 5.0 RC2</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="7a9df-112">建议的操作</span><span class="sxs-lookup"><span data-stu-id="7a9df-112">Recommended action</span></span>

<span data-ttu-id="7a9df-113">你无需执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="7a9df-113">No action is required on your part.</span></span> <span data-ttu-id="7a9df-114">但如果已自定义 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>、<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> 或 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> 属性中的字体，并希望字体与环境字体一致，请将每个属性的 <xref:System.Windows.Forms.DataGridViewCellStyle.Font?displayProperty=nameWithType> 设置为 `null`。</span><span class="sxs-lookup"><span data-stu-id="7a9df-114">However, if you've customized the font in the <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle>, or <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> properties and want the font to match the ambient font, set <xref:System.Windows.Forms.DataGridViewCellStyle.Font?displayProperty=nameWithType> to `null` for each property.</span></span>

#### <a name="category"></a><span data-ttu-id="7a9df-115">类别</span><span class="sxs-lookup"><span data-stu-id="7a9df-115">Category</span></span>

- <span data-ttu-id="7a9df-116">Windows 窗体</span><span class="sxs-lookup"><span data-stu-id="7a9df-116">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="7a9df-117">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="7a9df-117">Affected APIs</span></span>

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Windows.Forms.DataGridView.DefaultCellStyle`
- `P:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle`
- `P:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle`

-->
