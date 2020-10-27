---
title: 重大更改和 .NET 库
description: 有关在创建 .NET 库时浏览重大更改的最佳做法建议。
ms.date: 10/02/2018
ms.openlocfilehash: 2cbd9e0a818b52aede6c9b1f60fdf52dcbd7b96f
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223326"
---
# <a name="breaking-changes"></a><span data-ttu-id="3d8fa-103">中断性变更</span><span class="sxs-lookup"><span data-stu-id="3d8fa-103">Breaking changes</span></span>

<span data-ttu-id="3d8fa-104">对于 .NET 库而言，在现有用户的稳定性与未来的创新之间找到平衡点非常重要。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-104">It's important for a .NET library to find a balance between stability for existing users and innovation for the future.</span></span> <span data-ttu-id="3d8fa-105">库创建者倾向于重构和重新考虑代码，直到达到完美，但是使现有用户中断会造成负面影响，尤其是对于低级库。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-105">Library authors lean towards refactoring and rethinking code until it's perfect, but breaking your existing users has a negative impact, especially for low-level libraries.</span></span>

## <a name="project-types-and-breaking-changes"></a><span data-ttu-id="3d8fa-106">项目类型和重大更改</span><span class="sxs-lookup"><span data-stu-id="3d8fa-106">Project types and breaking changes</span></span>

<span data-ttu-id="3d8fa-107">.NET 社区使用库的方式改变了重大更改对最终用户开发人员的影响。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-107">How a library is used by the .NET community changes the effect of breaking changes on end-user developers.</span></span>

- <span data-ttu-id="3d8fa-108">低级和中级库  （如序列化程序、HTML 分析器、数据库对象关系映射程序或 Web 框架）受重大更改的影响最大。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-108">**Low and middle-level libraries** like a serializer, HTML parser, database object-relational mapper, or web framework are the most affected by breaking changes.</span></span>

  <span data-ttu-id="3d8fa-109">构建基块包由最终用户开发人员用于构建应用程序，并由其他库用作 NuGet 依赖项。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-109">Building block packages are used by end-user developers to build applications, and by other libraries as NuGet dependencies.</span></span> <span data-ttu-id="3d8fa-110">例如，你在构建应用程序并使用开放源代码客户端调用 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-110">For example, you're building an application and are using an open-source client to call a web service.</span></span> <span data-ttu-id="3d8fa-111">对客户端使用的依赖项的重大更新不是你可以解决的问题。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-111">A breaking update to a dependency the client uses isn't something you can fix.</span></span> <span data-ttu-id="3d8fa-112">开放源代码客户端需要进行更改，你无法控制它。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-112">It's the open-source client that needs to be changed and you have no control over it.</span></span> <span data-ttu-id="3d8fa-113">你必须找到库的兼容版本或提交客户端库的修复程序并等待新版本。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-113">You have to find compatible versions of the libraries or submit a fix to the client library and wait for a new version.</span></span> <span data-ttu-id="3d8fa-114">最糟糕的情况是如果你要使用两个库，但它们依赖于第三个库的互相不兼容版本。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-114">The worst-case situation is if you want to use two libraries that depend on mutually incompatible versions of a third library.</span></span>

- <span data-ttu-id="3d8fa-115">高级库  （如一套 UI 控件）对于重大更改不太敏感。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-115">**High-level libraries** like a suite of UI controls are less sensitive to breaking changes.</span></span>

  <span data-ttu-id="3d8fa-116">高级库在最终用户应用程序中直接引用。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-116">High-level libraries are directly referenced in an end-user application.</span></span> <span data-ttu-id="3d8fa-117">如果发生重大更改，则开发人员可以选择更新到最新版本，或者可以修改其应用程序以应对重大更改。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-117">If breaking changes occur, the developer can choose to update to the latest version, or can modify their application to work with the breaking change.</span></span>

<span data-ttu-id="3d8fa-118">✔️ 请考虑将如何使用库。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-118">✔️ DO think about how your library will be used.</span></span> <span data-ttu-id="3d8fa-119">重大更改会对使用它的应用程序和库有何影响？</span><span class="sxs-lookup"><span data-stu-id="3d8fa-119">What effect will breaking changes have on applications and libraries that use it?</span></span>

<span data-ttu-id="3d8fa-120">✔️ 请在开发低级 .NET 库时尽量减少重大更改。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-120">✔️ DO minimize breaking changes when developing a low-level .NET library.</span></span>

<span data-ttu-id="3d8fa-121">✔️ 请考虑将库的重大重写作为新 NuGet 包进行发布。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-121">✔️ CONSIDER publishing a major rewrite of a library as a new NuGet package.</span></span>

## <a name="types-of-breaking-changes"></a><span data-ttu-id="3d8fa-122">重大更改的类型</span><span class="sxs-lookup"><span data-stu-id="3d8fa-122">Types of breaking changes</span></span>

<span data-ttu-id="3d8fa-123">重大更改划分为不同类别，其影响并不相同。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-123">Breaking changes fall into different categories and aren't equally impactful.</span></span>

### <a name="source-breaking-change"></a><span data-ttu-id="3d8fa-124">源代码重大更改</span><span class="sxs-lookup"><span data-stu-id="3d8fa-124">Source breaking change</span></span>

<span data-ttu-id="3d8fa-125">源代码重大更改不影响程序执行，但是会在下次重新编译应用程序时导致编译错误。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-125">A source breaking change doesn't affect program execution but will cause compilation errors the next time the application is recompiled.</span></span> <span data-ttu-id="3d8fa-126">例如，新重载可能会在以前明确的方法调用中形成多义性，或是重命名的参数会中断使用命名参数的调用方。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-126">For example, a new overload can create an ambiguity in method calls that were unambiguous previously, or a renamed parameter will break callers that use named parameters.</span></span>

```csharp
public class Task
{
    // Adding a type called Task could conflict with System.Threading.Tasks.Task at compilation
}
```

<span data-ttu-id="3d8fa-127">因为源代码重大更改仅在开发人员重新编译其应用程序时有害，所以它是破坏性最小的重大更改。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-127">Because a source breaking change is only harmful when developers recompile their applications, it's the least disruptive breaking change.</span></span> <span data-ttu-id="3d8fa-128">开发人员可以轻松地修复自己的中断源代码。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-128">Developers can fix their own broken source code easily.</span></span>

### <a name="behavior-breaking-change"></a><span data-ttu-id="3d8fa-129">行为重大更改</span><span class="sxs-lookup"><span data-stu-id="3d8fa-129">Behavior breaking change</span></span>

<span data-ttu-id="3d8fa-130">行为更改是最常见的重大更改类型：行为中的几乎任何更改都可能会造成中断。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-130">Behavior changes are the most common type of breaking change: almost any change in behavior could break someone.</span></span> <span data-ttu-id="3d8fa-131">库的更改（如方法签名、引发的异常或是输入或输出数据格式）都可能会对库使用者产生负面影响。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-131">Changes to your library, such as method signatures, exceptions thrown or input or output data formats, could all negatively impact your library consumers.</span></span> <span data-ttu-id="3d8fa-132">如果用户依赖于以前中断的行为，则甚至 bug 修复都可以作为重大更改。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-132">Even a bug fix can qualify as a breaking change if users relied on the previously broken behavior.</span></span>

<span data-ttu-id="3d8fa-133">添加功能和改进不良行为是件好事，但如果不谨慎，则可能会使现有用户非常难以升级。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-133">Adding features and improving bad behaviors is a good thing, but without care it can make it very hard for existing users to upgrade.</span></span> <span data-ttu-id="3d8fa-134">帮助开发人员处理行为重大更改的一种方法是将更改隐藏在设置后面。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-134">One approach to helping developers deal with behavior breaking changes is to hide them behind settings.</span></span> <span data-ttu-id="3d8fa-135">设置使开发人员可以更新到库的最新版本，同时可选择加入或退出重大更改。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-135">Settings let developers update to the latest version of your library while at the same time choosing to opt in or opt out of breaking changes.</span></span> <span data-ttu-id="3d8fa-136">此策略使开发人员可以保持更新，同时使其使用代码随时间推移而进行适应。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-136">This strategy lets developers stay up to date while letting their consuming code adapt over time.</span></span>

<span data-ttu-id="3d8fa-137">例如，ASP.NET Core MVC 提出了[兼容性版本](/aspnet/core/mvc/compatibility-version)这一概念，可在 `MvcOptions` 中修改启用和禁用的功能。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-137">For example, ASP.NET Core MVC has the concept of a [compatibility version](/aspnet/core/mvc/compatibility-version) that modifies the features enabled and disabled on `MvcOptions`.</span></span>

<span data-ttu-id="3d8fa-138">✔️ 请考虑在默认情况下关闭新功能（如果它们会影响现有用户），通过设置让开发人员可以选择加入功能。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-138">✔️ CONSIDER leaving new features off by default, if they affect existing users, and let developers opt in to the feature with a setting.</span></span>

### <a name="binary-breaking-change"></a><span data-ttu-id="3d8fa-139">二进制重大更改</span><span class="sxs-lookup"><span data-stu-id="3d8fa-139">Binary breaking change</span></span>

<span data-ttu-id="3d8fa-140">二进制重大更改在更改库的公共 API 时发生，因此针对库的较旧版本编译的程序集将不再能够调用 API。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-140">A binary breaking change happens when you change the public API of your library, so assemblies compiled against older versions of your library are no longer able to call the API.</span></span> <span data-ttu-id="3d8fa-141">例如，通过添加新参数来更改方法签名会导致针对库的较旧版本编译的程序集引发 <xref:System.MissingMethodException>。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-141">For example, changing a method's signature by adding a new parameter will cause assemblies compiled against the older version of the library to throw a <xref:System.MissingMethodException>.</span></span>

<span data-ttu-id="3d8fa-142">二进制重大更改还可能会中断整个程序集  。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-142">A binary breaking change can also break an **entire assembly** .</span></span> <span data-ttu-id="3d8fa-143">使用 `AssemblyName` 重命名程序集会更改程序集的标识，如同添加、删除或更改程序集的强命名密钥一样。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-143">Renaming an assembly with `AssemblyName` will change the assembly's identity, as will adding, removing, or changing the assembly's strong naming key.</span></span> <span data-ttu-id="3d8fa-144">程序集标识的更改会中断所有使用它的已编译代码。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-144">A change of an assembly's identity will break all compiled code that uses it.</span></span>

<span data-ttu-id="3d8fa-145">❌ 请勿更改程序集名称。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-145">❌ DO NOT change an assembly name.</span></span>

<span data-ttu-id="3d8fa-146">❌ 请勿添加、删除或更改强命名密钥。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-146">❌ DO NOT add, remove, or change the strong naming key.</span></span>

<span data-ttu-id="3d8fa-147">✔️ 请考虑使用抽象基类而不是接口。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-147">✔️ CONSIDER using abstract base classes instead of interfaces.</span></span>

> <span data-ttu-id="3d8fa-148">向接口添加任何内容都会导致实现它的现有类型失败。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-148">Adding anything to an interface will cause existing types that implement it to fail.</span></span> <span data-ttu-id="3d8fa-149">抽象基类允许添加默认虚拟实现。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-149">An abstract base class allows you to add a default virtual implementation.</span></span>

<span data-ttu-id="3d8fa-150">✔️ 请考虑在打算删除的类型和成员上放置 <xref:System.ObsoleteAttribute>。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-150">✔️ CONSIDER placing the <xref:System.ObsoleteAttribute> on types and members that you intend to remove.</span></span> <span data-ttu-id="3d8fa-151">该属性应具有有关更新代码以不再使用已过时 API 的说明。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-151">The attribute should have instructions for updating code to no longer use the obsolete API.</span></span>

> <span data-ttu-id="3d8fa-152">调用具有 <xref:System.ObsoleteAttribute> 的类型和方法的代码会生成一个生成警告，其中包含向该属性提供的消息。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-152">Code that calls types and methods with the <xref:System.ObsoleteAttribute> will generate a build warning with the message supplied to the attribute.</span></span> <span data-ttu-id="3d8fa-153">警告向使用已过时 API 的人员提供了进行迁移的缓冲时间，以便在删除已过时 API 时，大多数人都不再使用它。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-153">The warnings give people who use the obsolete API surface time to migrate so that when the obsolete API is removed, most are no longer using it.</span></span>

```csharp
public class Document
{
    [Obsolete("LoadDocument(string) is obsolete. Use LoadDocument(Uri) instead.")]
    public static Document LoadDocument(string uri)
    {
        return LoadDocument(new Uri(uri));
    }

    public static Document LoadDocument(Uri uri)
    {
        // Load the document
    }
}
```

<span data-ttu-id="3d8fa-154">✔️ 请考虑在低级和中级库中无限期地保留具有 <xref:System.ObsoleteAttribute> 的类型和方法。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-154">✔️ CONSIDER keeping types and methods with the <xref:System.ObsoleteAttribute> indefinitely in low and middle-level libraries.</span></span>

> <span data-ttu-id="3d8fa-155">删除 API 是一种二进制重大更改。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-155">Removing APIs is a binary breaking change.</span></span> <span data-ttu-id="3d8fa-156">如果维护成本较低，并且不会向库增添大量技术债务，请考虑保留已过时类型和方法。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-156">Considering keeping obsolete types and methods if maintaining them is low cost and doesn't add lot of technical debt to your library.</span></span> <span data-ttu-id="3d8fa-157">不删除类型和方法可以帮助避免上述最糟糕情况。</span><span class="sxs-lookup"><span data-stu-id="3d8fa-157">Not removing types and methods can help avoid the worst-case scenarios mentioned above.</span></span>

## <a name="see-also"></a><span data-ttu-id="3d8fa-158">另请参阅</span><span class="sxs-lookup"><span data-stu-id="3d8fa-158">See also</span></span>

- [<span data-ttu-id="3d8fa-159">面向 C# 开发人员的版本和更新注意事项</span><span class="sxs-lookup"><span data-stu-id="3d8fa-159">Version and update considerations for C# developers</span></span>](../../csharp/whats-new/version-update-considerations.md)
- [<span data-ttu-id="3d8fa-160">.NET 中的 API 重大更改的权威指南</span><span class="sxs-lookup"><span data-stu-id="3d8fa-160">A definitive guide to API-breaking changes in .NET</span></span>](https://stackoverflow.com/questions/1456785/a-definitive-guide-to-api-breaking-changes-in-net)
- [<span data-ttu-id="3d8fa-161">.NET 重大更改规则</span><span class="sxs-lookup"><span data-stu-id="3d8fa-161">.NET breaking change rules</span></span>](https://github.com/dotnet/runtime/blob/master/docs/coding-guidelines/breaking-change-rules.md)

>[!div class="step-by-step"]
>[<span data-ttu-id="3d8fa-162">上一页</span><span class="sxs-lookup"><span data-stu-id="3d8fa-162">Previous</span></span>](versioning.md)
