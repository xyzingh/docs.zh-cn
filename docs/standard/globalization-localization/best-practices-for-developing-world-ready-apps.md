---
title: 开发全球通用应用程序的最佳做法
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- global applications, best practices
- world-ready applications, best practices
- globalization [.NET], best practices
- international applications [.NET], best practices
ms.assetid: f08169c7-aad8-4ec3-9a21-9ebd3b89986c
ms.openlocfilehash: 5b6fd468c40e42d25986cb79ca6402afca2d7a7d
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064010"
---
# <a name="best-practices-for-developing-world-ready-applications"></a><span data-ttu-id="b52b6-102">开发全球通用应用程序的最佳做法</span><span class="sxs-lookup"><span data-stu-id="b52b6-102">Best practices for developing world-ready applications</span></span>

<span data-ttu-id="b52b6-103">本节描述在开发全球通用的应用程序时应遵循的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="b52b6-103">This section describes the best practices to follow when developing world-ready applications.</span></span>

## <a name="globalization-best-practices"></a><span data-ttu-id="b52b6-104">全球化最佳做法</span><span class="sxs-lookup"><span data-stu-id="b52b6-104">Globalization best practices</span></span>

1. <span data-ttu-id="b52b6-105">在内部使应用程序代码成为 Unicode。</span><span class="sxs-lookup"><span data-stu-id="b52b6-105">Make your application Unicode internally.</span></span>

2. <span data-ttu-id="b52b6-106">使用 <xref:System.Globalization> 命名空间提供的区域性识别类来操作和格式化数据。</span><span class="sxs-lookup"><span data-stu-id="b52b6-106">Use the culture-aware classes provided by the <xref:System.Globalization> namespace to manipulate and format data.</span></span>

    - <span data-ttu-id="b52b6-107">对于排序，使用 <xref:System.Globalization.SortKey> 类和 <xref:System.Globalization.CompareInfo> 类。</span><span class="sxs-lookup"><span data-stu-id="b52b6-107">For sorting, use the <xref:System.Globalization.SortKey> class and the <xref:System.Globalization.CompareInfo> class.</span></span>

    - <span data-ttu-id="b52b6-108">对于字符串比较，使用 <xref:System.Globalization.CompareInfo> 类。</span><span class="sxs-lookup"><span data-stu-id="b52b6-108">For string comparisons, use the <xref:System.Globalization.CompareInfo> class.</span></span>

    - <span data-ttu-id="b52b6-109">对于日期和时间格式化，使用 <xref:System.Globalization.DateTimeFormatInfo> 类。</span><span class="sxs-lookup"><span data-stu-id="b52b6-109">For date and time formatting, use the <xref:System.Globalization.DateTimeFormatInfo> class.</span></span>

    - <span data-ttu-id="b52b6-110">对于数字格式化，使用 <xref:System.Globalization.NumberFormatInfo> 类。</span><span class="sxs-lookup"><span data-stu-id="b52b6-110">For numeric formatting, use the <xref:System.Globalization.NumberFormatInfo> class.</span></span>

    - <span data-ttu-id="b52b6-111">对于公历和非公历，使用 <xref:System.Globalization.Calendar> 类或特定的日历实现之一。</span><span class="sxs-lookup"><span data-stu-id="b52b6-111">For Gregorian and non-Gregorian calendars, use the <xref:System.Globalization.Calendar> class or one of the specific calendar implementations.</span></span>

3. <span data-ttu-id="b52b6-112">在适当的情况下，使用 <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> 类提供的区域性属性设置。</span><span class="sxs-lookup"><span data-stu-id="b52b6-112">Use the culture property settings provided by the <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> class in the appropriate situations.</span></span> <span data-ttu-id="b52b6-113">使用 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 属性来执行格式化任务，如日期和时间或数字的格式化。</span><span class="sxs-lookup"><span data-stu-id="b52b6-113">Use the <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> property for formatting tasks, such as date and time or numeric formatting.</span></span> <span data-ttu-id="b52b6-114">使用 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 属性来检索资源。</span><span class="sxs-lookup"><span data-stu-id="b52b6-114">Use the <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> property to retrieve resources.</span></span> <span data-ttu-id="b52b6-115">请注意，`CurrentCulture` 和 `CurrentUICulture` 属性可以通过线程进行设置。</span><span class="sxs-lookup"><span data-stu-id="b52b6-115">Note that the `CurrentCulture` and `CurrentUICulture` properties can be set per thread.</span></span>

4. <span data-ttu-id="b52b6-116">通过使用 <xref:System.Text> 命名空间中的编码类，使应用程序能够与各种编码相互进行数据读写。</span><span class="sxs-lookup"><span data-stu-id="b52b6-116">Enable your application to read and write data to and from a variety of encodings by using the encoding classes in the <xref:System.Text> namespace.</span></span> <span data-ttu-id="b52b6-117">不要采用 ASCII 数据。</span><span class="sxs-lookup"><span data-stu-id="b52b6-117">Do not assume ASCII data.</span></span> <span data-ttu-id="b52b6-118">假定在用户可以输入文本的任何位置都将提供国际字符。</span><span class="sxs-lookup"><span data-stu-id="b52b6-118">Assume that international characters will be supplied anywhere a user can enter text.</span></span> <span data-ttu-id="b52b6-119">例如，应用程序应接受服务器名、目录、文件名、用户名和 URL 中的国际字符。</span><span class="sxs-lookup"><span data-stu-id="b52b6-119">For example, the application should accept international characters in server names, directories, file names, user names, and URLs.</span></span>

5. <span data-ttu-id="b52b6-120">使用 <xref:System.Text.UTF8Encoding> 类时，出于安全原因，应使用此类提供的错误检测功能。</span><span class="sxs-lookup"><span data-stu-id="b52b6-120">When using the <xref:System.Text.UTF8Encoding> class, for security reasons, use the error detection feature offered by this class.</span></span> <span data-ttu-id="b52b6-121">为了打开错误检测功能，请使用具有一个 `throwOnInvalidBytes` 参数的构造函数来创建该类的一个实例，并将该参数的值设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="b52b6-121">To turn on the error detection feature, create an instance of the class using the constructor that takes a `throwOnInvalidBytes` parameter and set the value of this parameter to `true`.</span></span>

6. <span data-ttu-id="b52b6-122">尽可能将字符串按整个字符串处理，而不是按一系列个别字符处理。</span><span class="sxs-lookup"><span data-stu-id="b52b6-122">Whenever possible, handle strings as entire strings instead of as a series of individual characters.</span></span> <span data-ttu-id="b52b6-123">这在排序或搜索子字符串时尤为重要。</span><span class="sxs-lookup"><span data-stu-id="b52b6-123">This is especially important when sorting or searching for substrings.</span></span> <span data-ttu-id="b52b6-124">这可以防止与分析组合字符有关的问题。</span><span class="sxs-lookup"><span data-stu-id="b52b6-124">This will prevent problems associated with parsing combined characters.</span></span> <span data-ttu-id="b52b6-125">还可以通过 <xref:System.Globalization.StringInfo?displayProperty=nameWithType> 类使用文本单元而不是单个字符。</span><span class="sxs-lookup"><span data-stu-id="b52b6-125">You can also work with units of text rather than single characters by using the <xref:System.Globalization.StringInfo?displayProperty=nameWithType> class.</span></span>

7. <span data-ttu-id="b52b6-126">使用 <xref:System.Drawing> 命名空间提供的类来显示文本。</span><span class="sxs-lookup"><span data-stu-id="b52b6-126">Display text using the classes provided by the <xref:System.Drawing> namespace.</span></span>

8. <span data-ttu-id="b52b6-127">为保持操作系统间的一致性，不要允许用户设置重写 <xref:System.Globalization.CultureInfo>。</span><span class="sxs-lookup"><span data-stu-id="b52b6-127">For consistency across operating systems, do not allow user settings to override <xref:System.Globalization.CultureInfo>.</span></span> <span data-ttu-id="b52b6-128">使用接受 `CultureInfo` 参数的 `useUserOverride` 构造函数并将此参数设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="b52b6-128">Use the `CultureInfo` constructor that accepts a `useUserOverride` parameter and set it to `false`.</span></span>

9. <span data-ttu-id="b52b6-129">在国际操作系统版本上使用国际数据来测试应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="b52b6-129">Test your application functionality on international operating system versions, using international data.</span></span>

10. <span data-ttu-id="b52b6-130">如果安全决策基于字符串比较或大小写更改操作的结果，请使用不区分区域性的字符串操作。</span><span class="sxs-lookup"><span data-stu-id="b52b6-130">If a security decision is based on the result of a string comparison or case change operation, use a culture-insensitive string operation.</span></span> <span data-ttu-id="b52b6-131">这种做法可确保结果不会受 `CultureInfo.CurrentCulture` 值的影响。</span><span class="sxs-lookup"><span data-stu-id="b52b6-131">This practice ensures that the result is not affected by the value of `CultureInfo.CurrentCulture`.</span></span> <span data-ttu-id="b52b6-132">有关展示了区分区域性字符串比较如何产生不一致结果的示例，请参阅[字符串使用最佳做法](../base-types/best-practices-strings.md)的[“使用当前区域性的字符串比较”](../base-types/best-practices-strings.md#string-comparisons-that-use-the-current-culture)部分。</span><span class="sxs-lookup"><span data-stu-id="b52b6-132">See the ["String Comparisons that Use the Current Culture"](../base-types/best-practices-strings.md#string-comparisons-that-use-the-current-culture) section of [Best Practices for Using Strings](../base-types/best-practices-strings.md) for an example that demonstrates how culture-sensitive string comparisons can produce inconsistent results.</span></span>

## <a name="localization-best-practices"></a><span data-ttu-id="b52b6-133">本地化最佳做法</span><span class="sxs-lookup"><span data-stu-id="b52b6-133">Localization best practices</span></span>

1. <span data-ttu-id="b52b6-134">将所有可本地化的资源移动到单独的纯资源 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="b52b6-134">Move all localizable resources to separate resource-only DLLs.</span></span> <span data-ttu-id="b52b6-135">可本地化的资源包括用户界面元素，如字符串、错误消息、对话框、菜单以及嵌入的对象资源。</span><span class="sxs-lookup"><span data-stu-id="b52b6-135">Localizable resources include user interface elements, such as strings, error messages, dialog boxes, menus, and embedded object resources.</span></span>

2. <span data-ttu-id="b52b6-136">不要对字符串或用户界面资源进行硬编码。</span><span class="sxs-lookup"><span data-stu-id="b52b6-136">Do not hardcode strings or user interface resources.</span></span>

3. <span data-ttu-id="b52b6-137">不要将不可本地化的资源放在纯资源 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="b52b6-137">Do not put nonlocalizable resources into the resource-only DLLs.</span></span> <span data-ttu-id="b52b6-138">否则会使翻译人员产生困惑。</span><span class="sxs-lookup"><span data-stu-id="b52b6-138">This causes confusion for translators.</span></span>

4. <span data-ttu-id="b52b6-139">不要使用在运行时从串联词组生成的复合字符串。</span><span class="sxs-lookup"><span data-stu-id="b52b6-139">Do not use composite strings that are built at run time from concatenated phrases.</span></span> <span data-ttu-id="b52b6-140">复合字符串难以本地化，因为它们往往采用英语语法顺序，而此顺序并不适用于所有语言。</span><span class="sxs-lookup"><span data-stu-id="b52b6-140">Composite strings are difficult to localize because they often assume an English grammatical order that does not apply to all languages.</span></span>

5. <span data-ttu-id="b52b6-141">避免不明确的结构，如“Empty Folder”，因为根据字符串组成部分的语法规则，这些字符串可能产生不同的翻译。</span><span class="sxs-lookup"><span data-stu-id="b52b6-141">Avoid ambiguous constructs such as "Empty Folder" where the strings can be translated differently depending on the grammatical roles of the string components.</span></span> <span data-ttu-id="b52b6-142">例如，“empty”既可以是一个动词，也可以是一个形容词，因此在诸如意大利语或法语等语言中就可能导致不同的翻译。</span><span class="sxs-lookup"><span data-stu-id="b52b6-142">For example, "empty" can be either a verb or an adjective, which can lead to different translations in languages such as Italian or French.</span></span>

6. <span data-ttu-id="b52b6-143">避免在应用程序中使用包含文本的图像和图标。</span><span class="sxs-lookup"><span data-stu-id="b52b6-143">Avoid using images and icons that contain text in your application.</span></span> <span data-ttu-id="b52b6-144">本地化这些图像和图标的成本是很大的。</span><span class="sxs-lookup"><span data-stu-id="b52b6-144">They are expensive to localize.</span></span>

7. <span data-ttu-id="b52b6-145">允许在用户界面中为字符串长度的扩展保留足够的空间。</span><span class="sxs-lookup"><span data-stu-id="b52b6-145">Allow plenty of room for the length of strings to expand in the user interface.</span></span> <span data-ttu-id="b52b6-146">在某些语言中，词组所需的空间可能比在其他语言中多 50-75%。</span><span class="sxs-lookup"><span data-stu-id="b52b6-146">In some languages, phrases can require 50-75 percent more space than they need in other languages.</span></span>

8. <span data-ttu-id="b52b6-147">使用 <xref:System.Resources.ResourceManager?displayProperty=nameWithType> 类来根据区域性检索资源。</span><span class="sxs-lookup"><span data-stu-id="b52b6-147">Use the <xref:System.Resources.ResourceManager?displayProperty=nameWithType> class to retrieve resources based on culture.</span></span>

9. <span data-ttu-id="b52b6-148">使用 [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) 创建 Windows 窗体对话框，以便可以使用 [Windows 窗体资源编辑器 (Winres.exe)](../../framework/tools/winres-exe-windows-forms-resource-editor.md) 对它们进行本地化。</span><span class="sxs-lookup"><span data-stu-id="b52b6-148">Use [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) to create Windows Forms dialog boxes so they can be localized using the [Windows Forms Resource Editor (Winres.exe)](../../framework/tools/winres-exe-windows-forms-resource-editor.md).</span></span> <span data-ttu-id="b52b6-149">不要对 Windows 窗体对话框进行手动编码。</span><span class="sxs-lookup"><span data-stu-id="b52b6-149">Do not code Windows Forms dialog boxes by hand.</span></span>

10. <span data-ttu-id="b52b6-150">安排进行专业本地化工作（翻译）。</span><span class="sxs-lookup"><span data-stu-id="b52b6-150">Arrange for professional localization (translation).</span></span>

11. <span data-ttu-id="b52b6-151">有关创建并本地化资源的完整说明，请参阅[应用中的资源](../../framework/resources/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b52b6-151">For a complete description of creating and localizing resources, see [Resources in Applications](../../framework/resources/index.md).</span></span>

## <a name="globalization-best-practices-for-aspnet-applications"></a><span data-ttu-id="b52b6-152">ASP.NET 应用程序的全球化最佳做法</span><span class="sxs-lookup"><span data-stu-id="b52b6-152">Globalization best practices for ASP.NET applications</span></span>

1. <span data-ttu-id="b52b6-153">在应用程序中显式设置 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> 和 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> 属性。</span><span class="sxs-lookup"><span data-stu-id="b52b6-153">Explicitly set the <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> and <xref:System.Globalization.CultureInfo.CurrentCulture%2A> properties in your application.</span></span> <span data-ttu-id="b52b6-154">不要依赖于默认设置。</span><span class="sxs-lookup"><span data-stu-id="b52b6-154">Do not rely on defaults.</span></span>

2. <span data-ttu-id="b52b6-155">请注意，ASP.NET 应用程序是托管应用程序，因此可以使用与其他托管应用程序相同的类，以根据区域性检索、显示和操作信息。</span><span class="sxs-lookup"><span data-stu-id="b52b6-155">Note that ASP.NET applications are managed applications and therefore can use the same classes as other managed applications for retrieving, displaying, and manipulating information based on culture.</span></span>

3. <span data-ttu-id="b52b6-156">注意在 ASP.NET 中可以指定以下三种编码类型：</span><span class="sxs-lookup"><span data-stu-id="b52b6-156">Be aware that you can specify the following three types of encodings in ASP.NET:</span></span>

    - <span data-ttu-id="b52b6-157">requestEncoding 指定从客户端浏览器接收的编码。</span><span class="sxs-lookup"><span data-stu-id="b52b6-157">requestEncoding specifies the encoding received from the client's browser.</span></span>

    - <span data-ttu-id="b52b6-158">responseEncoding 指定要发送到客户端浏览器的编码。</span><span class="sxs-lookup"><span data-stu-id="b52b6-158">responseEncoding specifies the encoding to send to the client browser.</span></span> <span data-ttu-id="b52b6-159">在大多数情形下，此编码应该与为 requestEncoding 指定的编码相同。</span><span class="sxs-lookup"><span data-stu-id="b52b6-159">In most situations, this encoding should be the same as that specified for requestEncoding.</span></span>

    - <span data-ttu-id="b52b6-160">fileEncoding 指定用于 .aspx、.asmx 和 .asax 文件分析的默认编码。</span><span class="sxs-lookup"><span data-stu-id="b52b6-160">fileEncoding specifies the default encoding for .aspx, .asmx, and .asax file parsing.</span></span>

4. <span data-ttu-id="b52b6-161">在 ASP.NET 应用程序中的以下三个位置指定 requestEncoding、responseEncoding、fileEncoding、culture 和 uiCulture 特性的值：</span><span class="sxs-lookup"><span data-stu-id="b52b6-161">Specify the values for the requestEncoding, responseEncoding, fileEncoding, culture, and uiCulture attributes in the following three places in an ASP.NET application:</span></span>

    - <span data-ttu-id="b52b6-162">在 Web.config 文件的全球化一节中。</span><span class="sxs-lookup"><span data-stu-id="b52b6-162">In the globalization section of a Web.config file.</span></span> <span data-ttu-id="b52b6-163">此文件是 ASP.NET 应用程序的外部文件。</span><span class="sxs-lookup"><span data-stu-id="b52b6-163">This file is external to the ASP.NET application.</span></span> <span data-ttu-id="b52b6-164">有关详细信息，请参阅 [\<globalization> 元素](/previous-versions/dotnet/netframework-4.0/hy4kkhe0(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="b52b6-164">For more information, see [\<globalization> Element](/previous-versions/dotnet/netframework-4.0/hy4kkhe0(v=vs.100)).</span></span>

    - <span data-ttu-id="b52b6-165">在页面指令中。</span><span class="sxs-lookup"><span data-stu-id="b52b6-165">In a page directive.</span></span> <span data-ttu-id="b52b6-166">请注意，当应用程序在页面中时，文件已经被读取。</span><span class="sxs-lookup"><span data-stu-id="b52b6-166">Note that, when an application is in a page, the file has already been read.</span></span> <span data-ttu-id="b52b6-167">因此，指定 fileEncoding 和 requestEncoding 为时已晚。</span><span class="sxs-lookup"><span data-stu-id="b52b6-167">Therefore, it is too late to specify fileEncoding and requestEncoding.</span></span> <span data-ttu-id="b52b6-168">只有 uiCulture、Culture 和 responseEncoding 可以在页面指令中指定。</span><span class="sxs-lookup"><span data-stu-id="b52b6-168">Only uiCulture, Culture, and responseEncoding can be specified in a page directive.</span></span>

    - <span data-ttu-id="b52b6-169">在应用程序代码中以编程方式指定。</span><span class="sxs-lookup"><span data-stu-id="b52b6-169">Programmatically in application code.</span></span> <span data-ttu-id="b52b6-170">该设置可能随请求的不同而不同。</span><span class="sxs-lookup"><span data-stu-id="b52b6-170">This setting can vary per request.</span></span> <span data-ttu-id="b52b6-171">同页面指令一样，到打开应用程序代码时，指定 fileEncoding 和 requestEncoding 为时已晚。</span><span class="sxs-lookup"><span data-stu-id="b52b6-171">As with a page directive, by the time the application's code is reached it is too late to specify fileEncoding and requestEncoding.</span></span> <span data-ttu-id="b52b6-172">只有 uiCulture、Culture 和 responseEncoding 可以在应用程序代码中指定。</span><span class="sxs-lookup"><span data-stu-id="b52b6-172">Only uiCulture, Culture, and responseEncoding can be specified in application code.</span></span>

5. <span data-ttu-id="b52b6-173">请注意，uiCulture 值可以设置为浏览器接受的语言。</span><span class="sxs-lookup"><span data-stu-id="b52b6-173">Note that the uiCulture value can be set to the browser accept language.</span></span>

## <a name="see-also"></a><span data-ttu-id="b52b6-174">请参阅</span><span class="sxs-lookup"><span data-stu-id="b52b6-174">See also</span></span>

- [<span data-ttu-id="b52b6-175">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="b52b6-175">Globalization and Localization</span></span>](index.md)
- [<span data-ttu-id="b52b6-176">桌面应用中的资源</span><span class="sxs-lookup"><span data-stu-id="b52b6-176">Resources in Desktop Apps</span></span>](../../framework/resources/index.md)
