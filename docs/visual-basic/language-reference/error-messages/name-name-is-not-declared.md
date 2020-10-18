---
title: 名称“<name>”未声明
ms.date: 10/10/2018
f1_keywords:
- bc30451
- vbc30451
helpviewer_keywords:
- BC30451
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
ms.openlocfilehash: 0a2c2a90b99017fcd9bb594acc6f2dbcf29d9536
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160192"
---
# <a name="bc30451-name-name-is-not-declared"></a><span data-ttu-id="ad867-102">BC30451：名称 " \<name> " 未声明</span><span class="sxs-lookup"><span data-stu-id="ad867-102">BC30451: Name '\<name>' is not declared</span></span>

<span data-ttu-id="ad867-103">语句引用编程元素，但编译器找不到具有该确切名称的元素。</span><span class="sxs-lookup"><span data-stu-id="ad867-103">A statement refers to a programming element, but the compiler cannot find an element with that exact name.</span></span>

 <span data-ttu-id="ad867-104">**错误 ID：** BC30451</span><span class="sxs-lookup"><span data-stu-id="ad867-104">**Error ID:** BC30451</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="ad867-105">更正此错误</span><span class="sxs-lookup"><span data-stu-id="ad867-105">To correct this error</span></span>

1. <span data-ttu-id="ad867-106">检查引用语句中名称的拼写。</span><span class="sxs-lookup"><span data-stu-id="ad867-106">Check the spelling of the name in the referring statement.</span></span> <span data-ttu-id="ad867-107">Visual Basic 不区分大小写，但拼写中的任何其他变体被视为完全不同的名称。</span><span class="sxs-lookup"><span data-stu-id="ad867-107">Visual Basic is case-insensitive, but any other variation in the spelling is regarded as a completely different name.</span></span> <span data-ttu-id="ad867-108">请注意，下划线 (`_`) 是名称的一部分，因此也是拼写的一部分。</span><span class="sxs-lookup"><span data-stu-id="ad867-108">Note that the underscore (`_`) is part of the name and therefore part of the spelling.</span></span>

2. <span data-ttu-id="ad867-109">检查是否有成员访问运算符在 `.` 对象及其成员之间 () 。</span><span class="sxs-lookup"><span data-stu-id="ad867-109">Check that you have the member access operator (`.`) between an object and its member.</span></span> <span data-ttu-id="ad867-110">例如，如果你拥有名为 <xref:System.Windows.Forms.TextBox> 的 `TextBox1`控件，则要键入 <xref:System.Windows.Forms.TextBoxBase.Text%2A> 才可访问其 `TextBox1.Text`。</span><span class="sxs-lookup"><span data-stu-id="ad867-110">For example, if you have a <xref:System.Windows.Forms.TextBox> control named `TextBox1`, to access its <xref:System.Windows.Forms.TextBoxBase.Text%2A> property you should type `TextBox1.Text`.</span></span> <span data-ttu-id="ad867-111">如果你转而键入 `TextBox1Text`，则会创建不同的名称。</span><span class="sxs-lookup"><span data-stu-id="ad867-111">If instead you type `TextBox1Text`, you have created a different name.</span></span>

3. <span data-ttu-id="ad867-112">如果拼写正确并且任何对象成员访问的语法正确，请验证元素是否已声明。</span><span class="sxs-lookup"><span data-stu-id="ad867-112">If the spelling is correct and the syntax of any object member access is correct, verify that the element has been declared.</span></span> <span data-ttu-id="ad867-113">有关详细信息，请参阅已 [声明元素](../../programming-guide/language-features/declared-elements/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ad867-113">For more information, see [Declared Elements](../../programming-guide/language-features/declared-elements/index.md).</span></span>

4. <span data-ttu-id="ad867-114">如果已声明编程元素，请检查它是否在范围内。</span><span class="sxs-lookup"><span data-stu-id="ad867-114">If the programming element has been declared, check that it is in scope.</span></span> <span data-ttu-id="ad867-115">如果引用语句位于声明编程元素的区域外，则可能需要限定元素名称。</span><span class="sxs-lookup"><span data-stu-id="ad867-115">If the referring statement is outside the region declaring the programming element, you might need to qualify the element name.</span></span> <span data-ttu-id="ad867-116">有关详细信息，请参阅 [Scope in Visual Basic](../../programming-guide/language-features/declared-elements/scope.md)。</span><span class="sxs-lookup"><span data-stu-id="ad867-116">For more information, see [Scope in Visual Basic](../../programming-guide/language-features/declared-elements/scope.md).</span></span>

5. <span data-ttu-id="ad867-117">如果未使用完全限定的类型或类型和成员名称 (例如，你的代码将属性视为 `MethodInfo.Name` 而不是 `System.Reflection.MethodInfo.Name`) ，请添加 [Imports 语句](../statements/imports-statement-net-namespace-and-type.md)。</span><span class="sxs-lookup"><span data-stu-id="ad867-117">If you are not using a fully qualified type or type and member name (for example, your code refers to a property as `MethodInfo.Name` instead of `System.Reflection.MethodInfo.Name`), add an [Imports statement](../statements/imports-statement-net-namespace-and-type.md).</span></span>

6. <span data-ttu-id="ad867-118">如果尝试使用 .vbproj 文件（以行) 开头的文件）编译 SDK 样式 (项目， \* `<Project Sdk="Microsoft.NET.Sdk">` 并且错误消息引用 Microsoft.VisualBasic.dll 程序集中的类型或成员，则将应用程序配置为使用对 Visual Basic 运行库的引用进行编译。</span><span class="sxs-lookup"><span data-stu-id="ad867-118">If you are attempting to compile an SDK-style project (a project with a \*.vbproj file that begins with the line `<Project Sdk="Microsoft.NET.Sdk">`), and the error message refers to a type or member in the Microsoft.VisualBasic.dll assembly, configure your application to compile with a reference to the Visual Basic Runtime Library.</span></span> <span data-ttu-id="ad867-119">默认情况下，库的一个子集嵌入 SDK 样式项目中的程序集。</span><span class="sxs-lookup"><span data-stu-id="ad867-119">By default, a subset of the library is embedded in your assembly in an SDK-style project.</span></span>

   <span data-ttu-id="ad867-120">例如，下面的示例无法编译，因为 <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ChangeType%2A?displayProperty=fullName> 找不到该方法。</span><span class="sxs-lookup"><span data-stu-id="ad867-120">For example, the following example fails to compile because the <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ChangeType%2A?displayProperty=fullName> method cannot be found.</span></span> <span data-ttu-id="ad867-121">它不会嵌入到应用程序附带的 Visual Basic 运行时的子集中。</span><span class="sxs-lookup"><span data-stu-id="ad867-121">It is not embedded in the subset of the Visual Basic Runtime included with your application.</span></span>

   [!code-vb[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/program1.vb?highlight=7)]

   <span data-ttu-id="ad867-122">若要解决此错误，请将 `<VBRuntime>Default</VBRuntime>` 元素添加到 "项目" `<PropertyGroup>` 部分，如以下 Visual Basic 项目文件所示。</span><span class="sxs-lookup"><span data-stu-id="ad867-122">To address this error, add the `<VBRuntime>Default</VBRuntime>` element to the projects `<PropertyGroup>` section, as the following Visual Basic project file shows.</span></span>

   [!code-xml[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/vbruntime.vbproj?highlight=6)]

## <a name="see-also"></a><span data-ttu-id="ad867-123">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ad867-123">See also</span></span>

- [<span data-ttu-id="ad867-124">声明和常量摘要</span><span class="sxs-lookup"><span data-stu-id="ad867-124">Declarations and Constants Summary</span></span>](../keywords/declarations-and-constants-summary.md)
- [<span data-ttu-id="ad867-125">Visual Basic 命名约定</span><span class="sxs-lookup"><span data-stu-id="ad867-125">Visual Basic Naming Conventions</span></span>](../../programming-guide/program-structure/naming-conventions.md)
- [<span data-ttu-id="ad867-126">Declared Element Names</span><span class="sxs-lookup"><span data-stu-id="ad867-126">Declared Element Names</span></span>](../../programming-guide/language-features/declared-elements/declared-element-names.md)
- [<span data-ttu-id="ad867-127">References to Declared Elements</span><span class="sxs-lookup"><span data-stu-id="ad867-127">References to Declared Elements</span></span>](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
