---
title: XML Schema Definition Tool (Xsd.exe)
description: XML 序列化程序生成器为特定程序集中的类型创建 XML 序列化程序集，从而提高 XmlSerializer 的启动性能。
ms.date: 03/30/2017
ms.assetid: a6e6e65c-347f-4494-9457-653bf29baac2
ms.openlocfilehash: c8ae3e05f2d775cbc4c44ce27e7474d1fcfc06a3
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93281748"
---
# <a name="xml-schema-definition-tool-xsdexe"></a><span data-ttu-id="a9ce3-103">XML Schema Definition Tool (Xsd.exe)</span><span class="sxs-lookup"><span data-stu-id="a9ce3-103">XML Schema Definition Tool (Xsd.exe)</span></span>

<span data-ttu-id="a9ce3-104">XML 架构定义 (Xsd.exe) 工具从 XDR、XML 和 XSD 文件或者从运行时程序集中的类生成 XML 架构或公共语言运行时类。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-104">The XML Schema Definition (Xsd.exe) tool generates XML schema or common language runtime classes from XDR, XML, and XSD files, or from classes in a runtime assembly.</span></span>

<span data-ttu-id="a9ce3-105">XML 架构定义工具 (Xsd.exe) 通常可在以下路径中找到：</span><span class="sxs-lookup"><span data-stu-id="a9ce3-105">The XML Schema Definition tool (Xsd.exe) usually can be found in the following path:</span></span>\
<span data-ttu-id="a9ce3-106">C:\\Program Files (x86)\\Microsoft SDKs\\Windows\\{版本}\\bin\\NETFX {版本} Tools\\</span><span class="sxs-lookup"><span data-stu-id="a9ce3-106">_C:\\Program Files (x86)\\Microsoft SDKs\\Windows\\{version}\\bin\\NETFX {version} Tools\\_</span></span>

## <a name="syntax"></a><span data-ttu-id="a9ce3-107">语法</span><span class="sxs-lookup"><span data-stu-id="a9ce3-107">Syntax</span></span>

<span data-ttu-id="a9ce3-108">从命令行运行该工具。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-108">Run the tool from the command line.</span></span>

```console
xsd file.xdr [-outputdir:directory][/parameters:file.xml]
xsd file.xml [-outputdir:directory] [/parameters:file.xml]
xsd file.xsd {/classes | /dataset} [/element:element]
             [/enableLinqDataSet] [/language:language]
                          [/namespace:namespace] [-outputdir:directory] [URI:uri]
                          [/parameters:file.xml]
xsd {file.dll | file.exe} [-outputdir:directory] [/type:typename [...]][/parameters:file.xml]
```
  
> [!TIP]
> <span data-ttu-id="a9ce3-109">要使 .NET Framework 工具正常发挥作用，必须正确设置 `Path`、`Include` 和 `Lib` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-109">For .NET Framework tools to function properly, you must set your `Path`, `Include`, and `Lib` environment variables correctly.</span></span> <span data-ttu-id="a9ce3-110">可以通过运行 SDKVars.bat（位于 \<SDK>\\\<version>\Bin 目录中）来设置这些环境变量。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-110">Set these environment variables by running SDKVars.bat, which is located in the \<SDK>\\\<version>\Bin directory.</span></span> <span data-ttu-id="a9ce3-111">必须在每个命令 shell 程序中执行 SDKVars.bat。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-111">SDKVars.bat must be executed in every command shell.</span></span>

## <a name="argument"></a><span data-ttu-id="a9ce3-112">参数</span><span class="sxs-lookup"><span data-stu-id="a9ce3-112">Argument</span></span>

|<span data-ttu-id="a9ce3-113">参数</span><span class="sxs-lookup"><span data-stu-id="a9ce3-113">Argument</span></span>|<span data-ttu-id="a9ce3-114">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-114">Description</span></span>|
|--------------|-----------------|
|<span data-ttu-id="a9ce3-115">file.extension</span><span class="sxs-lookup"><span data-stu-id="a9ce3-115">*file.extension*</span></span>|<span data-ttu-id="a9ce3-116">指定要转换的输入文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-116">Specifies the input file to convert.</span></span> <span data-ttu-id="a9ce3-117">必须将扩展名指定为下列之一：.xdr、.xml、.xsd、.dll 或 .exe。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-117">You must specify the extension as one of the following: .xdr, .xml, .xsd, .dll, or .exe.</span></span><br /><br /> <span data-ttu-id="a9ce3-118">如果指定一个 XDR 架构文件（.xdr 扩展名），则 Xsd.exe 将 XDR 架构转换为 XSD 架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-118">If you specify an XDR schema file (.xdr extension), Xsd.exe converts the XDR schema to an XSD schema.</span></span> <span data-ttu-id="a9ce3-119">输出文件与 XDR 架构同名，但扩展名为 .xsd。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-119">The output file has the same name as the XDR schema, but with the .xsd extension.</span></span><br /><br /> <span data-ttu-id="a9ce3-120">如果指定一个 XML 文件（.xml 扩展名），则 Xsd.exe 从文件中的数据推导出架构并产生一个 XSD 架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-120">If you specify an XML file (.xml extension), Xsd.exe infers a schema from the data in the file and produces an XSD schema.</span></span> <span data-ttu-id="a9ce3-121">输出文件与 XML 文件同名，但扩展名为 .xsd。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-121">The output file has the same name as the XML file, but with the .xsd extension.</span></span><br /><br /> <span data-ttu-id="a9ce3-122">如果指定一个 XML 架构文件（.xsd 扩展名），则 Xsd.exe 将为对应于 XML 架构的运行时对象生成源代码。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-122">If you specify an XML schema file (.xsd extension), Xsd.exe generates source code for runtime objects that correspond to the XML schema.</span></span><br /><br /> <span data-ttu-id="a9ce3-123">如果指定一个运行时程序集文件（.exe 或 .dll 扩展名），则 Xsd.exe 为该程序集中的一个或多个类型生成架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-123">If you specify a runtime assembly file (.exe or .dll extension), Xsd.exe generates schemas for one or more types in that assembly.</span></span> <span data-ttu-id="a9ce3-124">可以使用 `/type` 选项来指定为其生成架构的类型。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-124">You can use the `/type` option to specify the types for which to generate schemas.</span></span> <span data-ttu-id="a9ce3-125">输出架构被命名为 schema0.xsd、schema1.xsd，依此类推。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-125">The output schemas are named schema0.xsd, schema1.xsd, and so on.</span></span> <span data-ttu-id="a9ce3-126">仅当给定类型使用 `XMLRoot` 自定义特性指定命名空间时，Xsd.exe 才生成多个架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-126">Xsd.exe produces multiple schemas only if the given types specify a namespace using the `XMLRoot` custom attribute.</span></span>|

## <a name="general-options"></a><span data-ttu-id="a9ce3-127">常规选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-127">General Options</span></span>

|<span data-ttu-id="a9ce3-128">选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-128">Option</span></span>|<span data-ttu-id="a9ce3-129">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-129">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="a9ce3-130">/h\[elp\]</span><span class="sxs-lookup"><span data-stu-id="a9ce3-130">**/h\[elp\]**</span></span>|<span data-ttu-id="a9ce3-131">显示该工具的命令语法和选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-131">Displays command syntax and options for the tool.</span></span>|
|<span data-ttu-id="a9ce3-132">/o\[utputdir\]:directory</span><span class="sxs-lookup"><span data-stu-id="a9ce3-132">**/o\[utputdir\]:**_directory_</span></span>|<span data-ttu-id="a9ce3-133">指定输出文件的目录。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-133">Specifies the directory for output files.</span></span> <span data-ttu-id="a9ce3-134">此参数只能出现一次。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-134">This argument can appear only once.</span></span> <span data-ttu-id="a9ce3-135">默认为当前目录。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-135">The default is the current directory.</span></span>|
|<span data-ttu-id="a9ce3-136">**/?**</span><span class="sxs-lookup"><span data-stu-id="a9ce3-136">**/?**</span></span>|<span data-ttu-id="a9ce3-137">显示该工具的命令语法和选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-137">Displays command syntax and options for the tool.</span></span>|
|<span data-ttu-id="a9ce3-138">/p\[arameters\]:file.xml</span><span class="sxs-lookup"><span data-stu-id="a9ce3-138">**/p\[arameters\]:**_file.xml_</span></span>|<span data-ttu-id="a9ce3-139">从指定的 .xml 文件读取各种操作模式的选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-139">Read options for various operation modes from the specified .xml file.</span></span> <span data-ttu-id="a9ce3-140">缩写形式为 `/p:`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-140">The short form is `/p:`.</span></span> <span data-ttu-id="a9ce3-141">有关详细信息，请参阅[备注](#remarks)部分。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-141">For more information, see the [Remarks](#remarks) section.</span></span>|

## <a name="xsd-file-options"></a><span data-ttu-id="a9ce3-142">XSD 文件选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-142">XSD File Options</span></span>
 <span data-ttu-id="a9ce3-143">必须为 xsd 文件仅指定下列选项中的一个。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-143">You must specify only one of the following options for .xsd files.</span></span>

|<span data-ttu-id="a9ce3-144">选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-144">Option</span></span>|<span data-ttu-id="a9ce3-145">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-145">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="a9ce3-146">/c\[lasses\]</span><span class="sxs-lookup"><span data-stu-id="a9ce3-146">**/c\[lasses\]**</span></span>|<span data-ttu-id="a9ce3-147">生成与指定架构相对应的类。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-147">Generates classes that correspond to the specified schema.</span></span> <span data-ttu-id="a9ce3-148">若要将 XML 数据读入对象中，请使用 <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-148">To read XML data into the object, use the <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A?displayProperty=nameWithType> method.</span></span>|
|<span data-ttu-id="a9ce3-149">/d\[ataset\]</span><span class="sxs-lookup"><span data-stu-id="a9ce3-149">**/d\[ataset\]**</span></span>|<span data-ttu-id="a9ce3-150">生成一个从 <xref:System.Data.DataSet> 派生的类，该类与指定的架构相对应。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-150">Generates a class derived from <xref:System.Data.DataSet> that corresponds to the specified schema.</span></span> <span data-ttu-id="a9ce3-151">若要将 XML 数据读入派生类中，请使用 <xref:System.Data.DataSet.ReadXml%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-151">To read XML data into the derived class, use the <xref:System.Data.DataSet.ReadXml%2A?displayProperty=nameWithType> method.</span></span>|

 <span data-ttu-id="a9ce3-152">还可以为 .xsd 文件指定下列任何选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-152">You can also specify any of the following options for .xsd files.</span></span>

|<span data-ttu-id="a9ce3-153">选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-153">Option</span></span>|<span data-ttu-id="a9ce3-154">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-154">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="a9ce3-155">/e\[lement\]:element</span><span class="sxs-lookup"><span data-stu-id="a9ce3-155">**/e\[lement\]:**_element_</span></span>|<span data-ttu-id="a9ce3-156">指定架构中要为其生成代码的元素。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-156">Specifies the element in the schema to generate code for.</span></span> <span data-ttu-id="a9ce3-157">默认情况下，键入所有元素。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-157">By default all elements are typed.</span></span> <span data-ttu-id="a9ce3-158">可以多次指定该参数。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-158">You can specify this argument more than once.</span></span>|
|<span data-ttu-id="a9ce3-159">**/enableDataBinding**</span><span class="sxs-lookup"><span data-stu-id="a9ce3-159">**/enableDataBinding**</span></span>|<span data-ttu-id="a9ce3-160">在所有生成的类型上实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口以启用数据绑定。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-160">Implements the <xref:System.ComponentModel.INotifyPropertyChanged> interface on all generated types to enable data binding.</span></span> <span data-ttu-id="a9ce3-161">缩写形式为 `/edb`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-161">The short form is `/edb`.</span></span>|
|<span data-ttu-id="a9ce3-162">**/enableLinqDataSet**</span><span class="sxs-lookup"><span data-stu-id="a9ce3-162">**/enableLinqDataSet**</span></span>|<span data-ttu-id="a9ce3-163">（缩写形式：`/eld`。）指定可使用 LINQ to DataSet 查询的生成的数据集。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-163">(Short form: `/eld`.) Specifies that the generated DataSet can be queried against using LINQ to DataSet.</span></span> <span data-ttu-id="a9ce3-164">此选项在同时指定 /dataset 选项的情况下使用。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-164">This option is used when the /dataset option is also specified.</span></span> <span data-ttu-id="a9ce3-165">有关详细信息，请参阅 [LINQ to DataSet 概述](../../framework/data/adonet/linq-to-dataset-overview.md)和[查询类型化数据集](../../framework/data/adonet/querying-typed-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-165">For more information, see [LINQ to DataSet Overview](../../framework/data/adonet/linq-to-dataset-overview.md) and [Querying Typed DataSets](../../framework/data/adonet/querying-typed-datasets.md).</span></span> <span data-ttu-id="a9ce3-166">有关使用 LINQ 的常规信息，请参阅[语言集成查询 (LINQ) - C#](../../csharp/programming-guide/concepts/linq/index.md) 或[语言集成查询 (LINQ) - Visual Basic](../../visual-basic/programming-guide/concepts/linq/index.md)。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-166">For general information about using LINQ, see [Language-Integrated Query (LINQ) - C#](../../csharp/programming-guide/concepts/linq/index.md) or [Language-Integrated Query (LINQ) - Visual Basic](../../visual-basic/programming-guide/concepts/linq/index.md).</span></span>|
|<span data-ttu-id="a9ce3-167">/f\[ields\]</span><span class="sxs-lookup"><span data-stu-id="a9ce3-167">**/f\[ields\]**</span></span>|<span data-ttu-id="a9ce3-168">生成字段，而不是生成属性。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-168">Generates fields instead of properties.</span></span> <span data-ttu-id="a9ce3-169">默认情况下生成属性。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-169">By default, properties are generated.</span></span>|
|<span data-ttu-id="a9ce3-170">/l\[anguage\]:language</span><span class="sxs-lookup"><span data-stu-id="a9ce3-170">**/l\[anguage\]:**_language_</span></span>|<span data-ttu-id="a9ce3-171">指定要使用的编程语言。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-171">Specifies the programming language to use.</span></span> <span data-ttu-id="a9ce3-172">从 `CS`（默认情况下为 C#）、`VB` (Visual Basic)、`JS` (JScript) 或 `VJS` (Visual J#) 中进行选择。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-172">Choose from `CS` (C#, which is the default), `VB` (Visual Basic), `JS` (JScript), or `VJS` (Visual J#).</span></span> <span data-ttu-id="a9ce3-173">也可指定实现 <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> 的类的完全限定名</span><span class="sxs-lookup"><span data-stu-id="a9ce3-173">You can also specify a fully qualified name for a class implementing <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType></span></span>|
|<span data-ttu-id="a9ce3-174">/n\[amespace\]:namespace</span><span class="sxs-lookup"><span data-stu-id="a9ce3-174">**/n\[amespace\]:**_namespace_</span></span>|<span data-ttu-id="a9ce3-175">为生成的类型指定运行时命名空间。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-175">Specifies the runtime namespace for the generated types.</span></span> <span data-ttu-id="a9ce3-176">默认命名空间为 `Schemas`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-176">The default namespace is `Schemas`.</span></span>|
|<span data-ttu-id="a9ce3-177">**/nologo**</span><span class="sxs-lookup"><span data-stu-id="a9ce3-177">**/nologo**</span></span>|<span data-ttu-id="a9ce3-178">取消显示版权标志。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-178">Suppresses the banner.</span></span>|
|<span data-ttu-id="a9ce3-179">**/order**</span><span class="sxs-lookup"><span data-stu-id="a9ce3-179">**/order**</span></span>|<span data-ttu-id="a9ce3-180">在所有粒子成员上生成显式顺序标识符。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-180">Generates explicit order identifiers on all particle members.</span></span>|
|<span data-ttu-id="a9ce3-181">/o\[ut\]:directoryName</span><span class="sxs-lookup"><span data-stu-id="a9ce3-181">**/o\[ut\]:**_directoryName_</span></span>|<span data-ttu-id="a9ce3-182">指定用来放置文件的输出目录。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-182">Specifies the output directory to place the files in.</span></span> <span data-ttu-id="a9ce3-183">默认为当前目录。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-183">The default is the current directory.</span></span>|
|<span data-ttu-id="a9ce3-184">/u\[ri\]:uri</span><span class="sxs-lookup"><span data-stu-id="a9ce3-184">**/u\[ri\]:**_uri_</span></span>|<span data-ttu-id="a9ce3-185">为架构中要为其生成代码的元素指定 URI。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-185">Specifies the URI for the elements in the schema to generate code for.</span></span> <span data-ttu-id="a9ce3-186">该 URI（如果存在）应用于使用 `/element` 选项指定的所有元素。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-186">This URI, if present, applies to all elements specified with the `/element` option.</span></span>|

## <a name="dll-and-exe-file-options"></a><span data-ttu-id="a9ce3-187">DLL 和 EXE 文件选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-187">DLL and EXE File Options</span></span>

|<span data-ttu-id="a9ce3-188">选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-188">Option</span></span>|<span data-ttu-id="a9ce3-189">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-189">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="a9ce3-190">/t\[ype\]:typename</span><span class="sxs-lookup"><span data-stu-id="a9ce3-190">**/t\[ype\]:**_typename_</span></span>|<span data-ttu-id="a9ce3-191">指定要为其创建架构的类型的名称。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-191">Specifies the name of the type to create a schema for.</span></span> <span data-ttu-id="a9ce3-192">可以指定多个类型参数。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-192">You can specify multiple type arguments.</span></span> <span data-ttu-id="a9ce3-193">如果 typename 不指定一个命名空间，则 Xsd.exe 将程序集中的所有类型与指定类型相匹配。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-193">If *typename* does not specify a namespace, Xsd.exe matches all types in the assembly with the specified type.</span></span> <span data-ttu-id="a9ce3-194">如果 typename 指定一个命名空间，则仅匹配那个类型。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-194">If *typename* specifies a namespace, only that type is matched.</span></span> <span data-ttu-id="a9ce3-195">如果 typename 以星号字符 (\*) 结尾，则此工具匹配所有以 \* 前的字符串开头的类型。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-195">If *typename* ends with an asterisk character (\*), the tool matches all types that start with the string preceding the \*.</span></span> <span data-ttu-id="a9ce3-196">如果省略 `/type` 选项，则 Xsd.exe 为程序集中的所有类型生成架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-196">If you omit the `/type` option, Xsd.exe generates schemas for all types in the assembly.</span></span>|

## <a name="remarks"></a><span data-ttu-id="a9ce3-197">备注</span><span class="sxs-lookup"><span data-stu-id="a9ce3-197">Remarks</span></span>

<span data-ttu-id="a9ce3-198">下表显示了 Xsd.exe 执行的操作。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-198">The following table shows the operations that Xsd.exe performs.</span></span>

| | |
|------------|-----------------|
|<span data-ttu-id="a9ce3-199">XDR 到 XSD</span><span class="sxs-lookup"><span data-stu-id="a9ce3-199">XDR to XSD</span></span>|<span data-ttu-id="a9ce3-200">使用精简 XML 数据架构文件生成 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-200">Generates an XML schema from an XML-Data-Reduced schema file.</span></span> <span data-ttu-id="a9ce3-201">XDR 为早期基于 XML 的架构格式。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-201">XDR is an early XML-based schema format.</span></span>|
|<span data-ttu-id="a9ce3-202">XML 到 XSD</span><span class="sxs-lookup"><span data-stu-id="a9ce3-202">XML to XSD</span></span>|<span data-ttu-id="a9ce3-203">使用 XML 文件生成 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-203">Generates an XML schema from an XML file.</span></span>|
|<span data-ttu-id="a9ce3-204">XSD 到 DataSet</span><span class="sxs-lookup"><span data-stu-id="a9ce3-204">XSD to DataSet</span></span>|<span data-ttu-id="a9ce3-205">使用 XSD 架构文件生成公共语言运行时 <xref:System.Data.DataSet> 类。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-205">Generates common language runtime <xref:System.Data.DataSet> classes from an XSD schema file.</span></span> <span data-ttu-id="a9ce3-206">生成的类为规则 XML 数据提供复杂对象模型。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-206">The generated classes provide a rich object model for regular XML data.</span></span>|
|<span data-ttu-id="a9ce3-207">XSD 到类</span><span class="sxs-lookup"><span data-stu-id="a9ce3-207">XSD to Classes</span></span>|<span data-ttu-id="a9ce3-208">使用 XSD 架构文件生成运行时类。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-208">Generates runtime classes from an XSD schema file.</span></span> <span data-ttu-id="a9ce3-209">生成的类可以与 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 一起使用，来读写遵循该架构的 XML 代码。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-209">The generated classes can be used in conjunction with <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> to read and write XML code that follows the schema.</span></span>|
|<span data-ttu-id="a9ce3-210">类到 XSD</span><span class="sxs-lookup"><span data-stu-id="a9ce3-210">Classes to XSD</span></span>| <span data-ttu-id="a9ce3-211">使用运行时程序集文件中的一个或多个类型生成 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-211">Generates an XML schema from a type or types in a runtime assembly file.</span></span> <span data-ttu-id="a9ce3-212">生成的架构定义了 <xref:System.Xml.Serialization.XmlSerializer> 使用的 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-212">The generated schema defines the XML format used by the <xref:System.Xml.Serialization.XmlSerializer>.</span></span>|

 <span data-ttu-id="a9ce3-213">Xsd.exe 只允许操作遵循由万维网联合会 (W3C) 提议的 XML 架构定义 (XSD) 语言的 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-213">Xsd.exe only allows you to manipulate XML schemas that follow the XML Schema Definition (XSD) language proposed by the World Wide Web Consortium (W3C).</span></span> <span data-ttu-id="a9ce3-214">有关 XML 架构定义提议或 XML 标准的详细信息，请参阅 <https://w3.org>。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-214">For more information on the XML Schema Definition proposal or the XML standard, see <https://w3.org>.</span></span>

## <a name="setting-options-with-an-xml-file"></a><span data-ttu-id="a9ce3-215">通过 XML 文件设置选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-215">Setting Options with an XML File</span></span>

<span data-ttu-id="a9ce3-216">通过使用 `/parameters` 开关，可指定设置各种选项的单个 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-216">By using the `/parameters` switch, you can specify a single XML file that sets various options.</span></span> <span data-ttu-id="a9ce3-217">可设置的选项取决于您如何使用 XSD.exe 工具。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-217">The options you can set depend on how you are using the XSD.exe tool.</span></span> <span data-ttu-id="a9ce3-218">选择包括生成架构、生成代码文件，或生成包含 `DataSet` 功能的代码文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-218">Choices include generating schemas, generating code files, or generating code files that include `DataSet` features.</span></span> <span data-ttu-id="a9ce3-219">例如，生成架构时可将 `<assembly>` 元素设置为可执行文件 (.exe) 或类库文件 (.dll) 的名称，但生成代码文件时则不能。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-219">For example, you can set the `<assembly>` element to the name of an executable (.exe) or type library (.dll) file when generating a schema, but not when generating a code file.</span></span> <span data-ttu-id="a9ce3-220">下面的 XML 演示如何将 `<generateSchemas>` 元素用于指定的可执行文件：</span><span class="sxs-lookup"><span data-stu-id="a9ce3-220">The following XML shows how to use the `<generateSchemas>` element with a specified executable:</span></span>

```xml
<!-- This is in a file named GenerateSchemas.xml. -->
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateSchemas>
   <assembly>ConsoleApplication1.exe</assembly>
</generateSchemas>
</xsd>
```

<span data-ttu-id="a9ce3-221">如果前面的 XML 包含在名为 GenerateSchemas.xml 的文件中，则通过在命令提示处键入下面的内容并按 Enter 来使用 `/parameters` 开关：</span><span class="sxs-lookup"><span data-stu-id="a9ce3-221">If the preceding XML is contained in a file named GenerateSchemas.xml, then use the `/parameters` switch by typing the following at a command prompt and pressing **Enter** :</span></span>

```console
 xsd /p:GenerateSchemas.xml
```

<span data-ttu-id="a9ce3-222">另外，如果为程序集中的单个类型生成架构，则可以使用下面的 XML：</span><span class="sxs-lookup"><span data-stu-id="a9ce3-222">On the other hand, if you are generating a schema for a single type found in the assembly, you can use the following XML:</span></span>

```xml
<!-- This is in a file named GenerateSchemaFromType.xml. -->
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateSchemas>
   <type>IDItems</type>
</generateSchemas>
</xsd>
```

<span data-ttu-id="a9ce3-223">但是若要使用上面的代码，您还必须在命令提示处提供程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-223">But to use preceding code, you must also supply the name of the assembly at the command prompt.</span></span> <span data-ttu-id="a9ce3-224">在命令提示处输入下面的内容（假设 XML 文件名为 GenerateSchemaFromType.xml）：</span><span class="sxs-lookup"><span data-stu-id="a9ce3-224">Enter the following at a command prompt (presuming the XML file is named GenerateSchemaFromType.xml):</span></span>

```console
xsd /p:GenerateSchemaFromType.xml ConsoleApplication1.exe
```

<span data-ttu-id="a9ce3-225">必须为 `<generateSchemas>` 元素仅指定以下选项中的一个。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-225">You must specify only one of the following options for the `<generateSchemas>` element.</span></span>

|<span data-ttu-id="a9ce3-226">元素</span><span class="sxs-lookup"><span data-stu-id="a9ce3-226">Element</span></span>|<span data-ttu-id="a9ce3-227">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-227">Description</span></span>|
|-------------|-----------------|
|\<assembly>|<span data-ttu-id="a9ce3-228">指定将从中生成架构的程序集。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-228">Specifies an assembly to generate the schema from.</span></span>|
|\<type>|<span data-ttu-id="a9ce3-229">指定程序集中找到的要为其生成架构的类型。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-229">Specifies a type found in an assembly to generate a schema for.</span></span>|
|\<xml>|<span data-ttu-id="a9ce3-230">指定要为其生成架构的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-230">Specifies an XML file to generate a schema for.</span></span>|
|\<xdr>|<span data-ttu-id="a9ce3-231">指定要为其生成架构的 XDR 文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-231">Specifies an XDR file to generate a schema for.</span></span>|

<span data-ttu-id="a9ce3-232">若要生成代码文件，请使用 `<generateClasses>` 元素。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-232">To generate a code file, use the `<generateClasses>` element.</span></span> <span data-ttu-id="a9ce3-233">下面的示例生成一个代码文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-233">The following example generates a code file.</span></span> <span data-ttu-id="a9ce3-234">请注意，另外还显示了两个特性，它们允许您为生成的文件设置编程语言和命名空间。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-234">Note that two attributes are also shown that allow you to set the programming language and namespace of the generated file.</span></span>

```xml
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateClasses language='VB' namespace='Microsoft.Serialization.Examples'/>
</xsd>
<!-- You must supply an .xsd file when typing in the command line.-->
<!-- For example: xsd /p:genClasses mySchema.xsd -->
```

 <span data-ttu-id="a9ce3-235">可为 `<generateClasses>` 元素设置以下选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-235">Options you can set for the `<generateClasses>` element include the following.</span></span>

|<span data-ttu-id="a9ce3-236">元素</span><span class="sxs-lookup"><span data-stu-id="a9ce3-236">Element</span></span>|<span data-ttu-id="a9ce3-237">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-237">Description</span></span>|
|-------------|-----------------|
|\<element>|<span data-ttu-id="a9ce3-238">指定 .xsd 文件中要为其生成代码的元素。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-238">Specifies an element in the .xsd file to generate code for.</span></span>|
|\<schemaImporterExtensions>|<span data-ttu-id="a9ce3-239">指定派生自 <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> 类的类型。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-239">Specifies a type derived from the <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> class.</span></span>|
|\<schema>|<span data-ttu-id="a9ce3-240">指定要为其生成代码的 XML 架构文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-240">Specifies a XML Schema file to generate code for.</span></span> <span data-ttu-id="a9ce3-241">可使用多个 \<schema> 元素指定多个 XML 架构文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-241">Multiple XML Schema files can be specified using multiple \<schema> elements.</span></span>|

<span data-ttu-id="a9ce3-242">下表显示也可用于 `<generateClasses>` 元素的特性。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-242">The following table shows the attributes that can also be used with the `<generateClasses>` element.</span></span>

|<span data-ttu-id="a9ce3-243">特性</span><span class="sxs-lookup"><span data-stu-id="a9ce3-243">Attribute</span></span>|<span data-ttu-id="a9ce3-244">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-244">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="a9ce3-245">语言</span><span class="sxs-lookup"><span data-stu-id="a9ce3-245">language</span></span>|<span data-ttu-id="a9ce3-246">指定要使用的编程语言。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-246">Specifies the programming language to use.</span></span> <span data-ttu-id="a9ce3-247">从 `CS`（默认情况下为 C#）、`VB` (Visual Basic)、`JS` (JScript) 或 `VJS` (Visual J#) 中进行选择。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-247">Choose from `CS` (C#, the default), `VB` (Visual Basic), `JS` (JScript), or `VJS` (Visual J#).</span></span> <span data-ttu-id="a9ce3-248">也可指定实现 <xref:System.CodeDom.Compiler.CodeDomProvider> 的类的完全限定名。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-248">You can also specify a fully qualified name for a class that implements <xref:System.CodeDom.Compiler.CodeDomProvider>.</span></span>|
|<span data-ttu-id="a9ce3-249">namespace</span><span class="sxs-lookup"><span data-stu-id="a9ce3-249">namespace</span></span>|<span data-ttu-id="a9ce3-250">为生成的代码指定命名空间。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-250">Specifies the namespace for the generated code.</span></span> <span data-ttu-id="a9ce3-251">命名空间必须符合 CLR 标准（例如，没有空格或反斜杠字符）。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-251">The namespace must conform to CLR standards (for example, no spaces or backslash characters).</span></span>|
|<span data-ttu-id="a9ce3-252">选项</span><span class="sxs-lookup"><span data-stu-id="a9ce3-252">options</span></span>|<span data-ttu-id="a9ce3-253">以下值之一：`none`、`properties`（生成属性而不是公共字段）、`order` 或 `enableDataBinding`（请参见前面“XSD 文件选项”一节的 `/order` 和 `/enableDataBinding` 开关）。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-253">One of the following values: `none`, `properties` (generates properties instead of public fields), `order`, or `enableDataBinding` (see the `/order` and `/enableDataBinding` switches in the preceding XSD File Options section.</span></span>|

 <span data-ttu-id="a9ce3-254">使用 `DataSet` 元素还可以控制如何生成 `<generateDataSet>` 代码。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-254">You can also control how `DataSet` code is generated by using the `<generateDataSet>` element.</span></span> <span data-ttu-id="a9ce3-255">下面的 XML 指定生成的代码使用 `DataSet` 结构（如 <xref:System.Data.DataTable> 类）为指定元素创建 Visual Basic 代码。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-255">The following XML specifies that the generated code uses `DataSet` structures (such as the <xref:System.Data.DataTable> class) to create Visual Basic code for a specified element.</span></span> <span data-ttu-id="a9ce3-256">生成的数据集结构将支持 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-256">The generated DataSet structures will support LINQ queries.</span></span>

 ```xml
 <xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
     <generateDataSet language='VB' namespace='Microsoft.Serialization.Examples' enableLinqDataSet='true'>
     </generateDataSet>
 </xsd>
```

<span data-ttu-id="a9ce3-257">可为 `<generateDataSet>` 元素设置以下选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-257">Options you can set for the `<generateDataSet>` element include the following.</span></span>

|<span data-ttu-id="a9ce3-258">元素</span><span class="sxs-lookup"><span data-stu-id="a9ce3-258">Element</span></span>|<span data-ttu-id="a9ce3-259">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-259">Description</span></span>|
|-------------|-----------------|
|\<schema>|<span data-ttu-id="a9ce3-260">指定要为其生成代码的 XML 架构文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-260">Specifies an XML Schema file to generate code for.</span></span> <span data-ttu-id="a9ce3-261">可使用多个 \<schema> 元素指定多个 XML 架构文件。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-261">Multiple XML Schema files can be specified using multiple \<schema> elements.</span></span>|

 <span data-ttu-id="a9ce3-262">下表显示可与 `<generateDataSet>` 元素一起使用的特性。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-262">The following table shows the attributes that can be used with the `<generateDataSet>` element.</span></span>

|<span data-ttu-id="a9ce3-263">特性</span><span class="sxs-lookup"><span data-stu-id="a9ce3-263">Attribute</span></span>|<span data-ttu-id="a9ce3-264">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-264">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="a9ce3-265">enableLinqDataSet</span><span class="sxs-lookup"><span data-stu-id="a9ce3-265">enableLinqDataSet</span></span>|<span data-ttu-id="a9ce3-266">指定可使用 LINQ to DataSet 查询的生成的数据集。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-266">Specifies that the generated DataSet can be queried against using LINQ to DataSet.</span></span> <span data-ttu-id="a9ce3-267">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-267">The default value is false.</span></span>|
|<span data-ttu-id="a9ce3-268">语言</span><span class="sxs-lookup"><span data-stu-id="a9ce3-268">language</span></span>|<span data-ttu-id="a9ce3-269">指定要使用的编程语言。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-269">Specifies the programming language to use.</span></span> <span data-ttu-id="a9ce3-270">从 `CS`（默认情况下为 C#）、`VB` (Visual Basic)、`JS` (JScript) 或 `VJS` (Visual J#) 中进行选择。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-270">Choose from `CS` (C#, the default), `VB` (Visual Basic), `JS` (JScript), or `VJS` (Visual J#).</span></span> <span data-ttu-id="a9ce3-271">也可指定实现 <xref:System.CodeDom.Compiler.CodeDomProvider> 的类的完全限定名。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-271">You can also specify a fully qualified name for a class that implements <xref:System.CodeDom.Compiler.CodeDomProvider>.</span></span>|
|<span data-ttu-id="a9ce3-272">namespace</span><span class="sxs-lookup"><span data-stu-id="a9ce3-272">namespace</span></span>|<span data-ttu-id="a9ce3-273">为生成的代码指定命名空间。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-273">Specifies the namespace for the generated code.</span></span> <span data-ttu-id="a9ce3-274">命名空间必须符合 CLR 标准（例如，没有空格或反斜杠字符）。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-274">The namespace must conform to CLR standards (for example, no spaces or backslash characters).</span></span>|

 <span data-ttu-id="a9ce3-275">有些特性可在顶级 `<xsd>` 元素上设置。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-275">There are attributes that you can set on the top level `<xsd>` element.</span></span> <span data-ttu-id="a9ce3-276">这些选项可用于任何子元素（`<generateSchemas>`、`<generateClasses>` 或 `<generateDataSet>`）。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-276">These options can be used with any of the child elements (`<generateSchemas>`, `<generateClasses>` or `<generateDataSet>`).</span></span> <span data-ttu-id="a9ce3-277">下面的 XML 代码在名为“MyOutputDirectory”的输出目录中为名为“IDItems”的元素生成代码。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-277">The following XML code generates code for an element named "IDItems" in the output directory named "MyOutputDirectory".</span></span>

```xml
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/' output='MyOutputDirectory'>
<generateClasses>
    <element>IDItems</element>
</generateClasses>
</xsd>
```

<span data-ttu-id="a9ce3-278">下表显示也可用于 `<xsd>` 元素的特性。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-278">The following table shows the attributes that can also be used with the `<xsd>` element.</span></span>

|<span data-ttu-id="a9ce3-279">特性</span><span class="sxs-lookup"><span data-stu-id="a9ce3-279">Attribute</span></span>|<span data-ttu-id="a9ce3-280">描述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-280">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="a9ce3-281">输出</span><span class="sxs-lookup"><span data-stu-id="a9ce3-281">output</span></span>|<span data-ttu-id="a9ce3-282">将放置生成的架构或代码文件的目录的名称。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-282">The name of a directory where the generated schema or code file will be placed.</span></span>|
|<span data-ttu-id="a9ce3-283">nologo</span><span class="sxs-lookup"><span data-stu-id="a9ce3-283">nologo</span></span>|<span data-ttu-id="a9ce3-284">取消显示版权标志。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-284">Suppresses the banner.</span></span> <span data-ttu-id="a9ce3-285">设置为 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-285">Set to `true` or `false`.</span></span>|
|<span data-ttu-id="a9ce3-286">帮助</span><span class="sxs-lookup"><span data-stu-id="a9ce3-286">help</span></span>|<span data-ttu-id="a9ce3-287">显示该工具的命令语法和选项。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-287">Displays command syntax and options for the tool.</span></span> <span data-ttu-id="a9ce3-288">设置为 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-288">Set to `true` or `false`.</span></span>|

## <a name="examples"></a><span data-ttu-id="a9ce3-289">示例</span><span class="sxs-lookup"><span data-stu-id="a9ce3-289">Examples</span></span>
 <span data-ttu-id="a9ce3-290">下面的命令从 `myFile.xdr` 生成一个 XML 架构并将它保存到当前目录中。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-290">The following command generates an XML schema from `myFile.xdr` and saves it to the current directory.</span></span>

```console
xsd myFile.xdr
```

<span data-ttu-id="a9ce3-291">下面的命令从 `myFile.xml` 生成一个 XML 架构并将它保存到指定目录中。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-291">The following command generates an XML schema from `myFile.xml` and saves it to the specified directory.</span></span>

```console
xsd myFile.xml /outputdir:myOutputDir
```

<span data-ttu-id="a9ce3-292">下面的命令生成一个与 C# 语言中的指定架构相对应的数据集，并在当前目录中将其保存为 `XSDSchemaFile.cs`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-292">The following command generates a data set that corresponds to the specified schema in the C# language and saves it as `XSDSchemaFile.cs` in the current directory.</span></span>

```console
xsd /dataset /language:CS XSDSchemaFile.xsd
```

<span data-ttu-id="a9ce3-293">下面的命令为程序集 `myAssembly.dll` 中的所有类型生成 XML 架构，并在当前目录中将它们保存为 `schema0.xsd`。</span><span class="sxs-lookup"><span data-stu-id="a9ce3-293">The following command generates XML schemas for all types in the assembly `myAssembly.dll` and saves them as `schema0.xsd` in the current directory.</span></span>

```console
xsd myAssembly.dll
```

## <a name="see-also"></a><span data-ttu-id="a9ce3-294">请参阅</span><span class="sxs-lookup"><span data-stu-id="a9ce3-294">See also</span></span>

- <xref:System.Data.DataSet>
- <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
- [<span data-ttu-id="a9ce3-295">工具</span><span class="sxs-lookup"><span data-stu-id="a9ce3-295">Tools</span></span>](../../framework/tools/index.md)
- [<span data-ttu-id="a9ce3-296">命令提示</span><span class="sxs-lookup"><span data-stu-id="a9ce3-296">Command Prompts</span></span>](../../framework/tools/developer-command-prompt-for-vs.md)
- [<span data-ttu-id="a9ce3-297">LINQ to DataSet 概述</span><span class="sxs-lookup"><span data-stu-id="a9ce3-297">LINQ to DataSet Overview</span></span>](../../framework/data/adonet/linq-to-dataset-overview.md)
- [<span data-ttu-id="a9ce3-298">查询类型化数据集</span><span class="sxs-lookup"><span data-stu-id="a9ce3-298">Querying Typed DataSets</span></span>](../../framework/data/adonet/querying-typed-datasets.md)
- [<span data-ttu-id="a9ce3-299">LINQ（语言集成查询）(C#)</span><span class="sxs-lookup"><span data-stu-id="a9ce3-299">LINQ (Language-Integrated Query) (C#)</span></span>](../../csharp/programming-guide/concepts/linq/index.md)
- [<span data-ttu-id="a9ce3-300">LINQ（语言集成查询）(Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="a9ce3-300">LINQ (Language-Integrated Query) (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/linq/index.md)
