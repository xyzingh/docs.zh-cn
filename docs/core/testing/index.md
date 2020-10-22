---
title: 在 .NET 中测试
description: 本文简要概述了在 .NET 中测试的测试概念、术语和工具。
author: IEvangelist
ms.author: dapine
ms.date: 10/19/2020
ms.openlocfilehash: 36e88cc059447a98931593e0535c70cbc92a2cf4
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223481"
---
# <a name="testing-in-net"></a><span data-ttu-id="603e3-103">在 .NET 中测试</span><span class="sxs-lookup"><span data-stu-id="603e3-103">Testing in .NET</span></span>

<span data-ttu-id="603e3-104">本文介绍了测试概念，并说明了如何使用不同类型的测试来验证代码。</span><span class="sxs-lookup"><span data-stu-id="603e3-104">This article introduces the concept of testing, and illustrates how different kinds of tests can be used to validate code.</span></span> <span data-ttu-id="603e3-105">有多种工具可用于测试 .NET 应用程序，如 [.NET CLI](#net-cli) 或[集成开发环境 (IDE)](#ide)。</span><span class="sxs-lookup"><span data-stu-id="603e3-105">There are various tools available for testing .NET applications, such as the [.NET CLI](#net-cli) or [Integrated Development Environments (IDEs)](#ide).</span></span>

## <a name="test-types"></a><span data-ttu-id="603e3-106">测试类型</span><span class="sxs-lookup"><span data-stu-id="603e3-106">Test types</span></span>

<span data-ttu-id="603e3-107">使用自动测试是确保应用程序代码按作者期望执行操作的一种绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="603e3-107">Having automated tests is a great way to ensure that application code does what its authors intend it to do.</span></span> <span data-ttu-id="603e3-108">本文介绍了单元测试、集成测试和负载测试。</span><span class="sxs-lookup"><span data-stu-id="603e3-108">This article covers unit tests, integration tests, and load tests.</span></span>

### <a name="unit-tests"></a><span data-ttu-id="603e3-109">单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-109">Unit tests</span></span>

<span data-ttu-id="603e3-110">单元测试是一种试验单个软件组件或方法（也称为“工作单元”）的测试。</span><span class="sxs-lookup"><span data-stu-id="603e3-110">A *unit test* is a test that exercises individual software components or methods, also known as "unit of work".</span></span> <span data-ttu-id="603e3-111">单元测试仅应测试开发人员控件内的代码。</span><span class="sxs-lookup"><span data-stu-id="603e3-111">Unit tests should only test code within the developer's control.</span></span> <span data-ttu-id="603e3-112">它们不测试基础结构问题。</span><span class="sxs-lookup"><span data-stu-id="603e3-112">They do not test infrastructure concerns.</span></span> <span data-ttu-id="603e3-113">基础结构问题包括与数据库、文件系统和网络资源的交互。</span><span class="sxs-lookup"><span data-stu-id="603e3-113">Infrastructure concerns include interacting with databases, file systems, and network resources.</span></span>

<span data-ttu-id="603e3-114">有关创建单元测试的详细信息，请参阅[测试工具](#testing-tools)。</span><span class="sxs-lookup"><span data-stu-id="603e3-114">For more information on creating unit tests, see [Testing tools](#testing-tools).</span></span>

### <a name="integration-tests"></a><span data-ttu-id="603e3-115">集成测试</span><span class="sxs-lookup"><span data-stu-id="603e3-115">Integration tests</span></span>

<span data-ttu-id="603e3-116">*集成测试*与单元测试的不同之处在于，它试验两个或更多软件组件一同工作（也称为其“集成”）的能力。</span><span class="sxs-lookup"><span data-stu-id="603e3-116">An *integration test* differs from a unit test in that it exercises two or more software components' ability to function together, also known as their "integration."</span></span> <span data-ttu-id="603e3-117">这些测试在更广泛范围的受测系统上运行，而单元测试则侧重于单个组件。</span><span class="sxs-lookup"><span data-stu-id="603e3-117">These tests operate on a broader spectrum of the system under test, whereas unit tests focus on individual components.</span></span> <span data-ttu-id="603e3-118">通常，集成测试会包括对基础结构问题的测试。</span><span class="sxs-lookup"><span data-stu-id="603e3-118">Often, integration tests do include infrastructure concerns.</span></span>

### <a name="load-tests"></a><span data-ttu-id="603e3-119">负载测试</span><span class="sxs-lookup"><span data-stu-id="603e3-119">Load tests</span></span>

<span data-ttu-id="603e3-120">负载测试旨在确定系统是否可以处理指定的负载，例如，使用应用程序的并发用户数和应用程序响应性处理交互的能力。</span><span class="sxs-lookup"><span data-stu-id="603e3-120">A *load test* aims to determine whether or not a system can handle a specified load, for example, the number of concurrent users using an application and the app's ability to handle interactions responsively.</span></span> <span data-ttu-id="603e3-121">有关 Web 应用程序负载测试的详细信息，请参阅 [ASP.NET Core 负载/压力测试](/aspnet/core/test/load-tests)。</span><span class="sxs-lookup"><span data-stu-id="603e3-121">For more information on load testing of web applications, see [ASP.NET Core load/stress testing](/aspnet/core/test/load-tests).</span></span>

## <a name="test-considerations"></a><span data-ttu-id="603e3-122">测试注意事项</span><span class="sxs-lookup"><span data-stu-id="603e3-122">Test considerations</span></span>

<span data-ttu-id="603e3-123">请记住，可以使用编写测试的[最佳做法](unit-testing-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="603e3-123">Keep in mind there are [best practices](unit-testing-best-practices.md) for writing tests.</span></span> <span data-ttu-id="603e3-124">例如，[测试驱动开发 (TDD)](https://deviq.com/test-driven-development) 是指先编写单元测试，再编写该单元测试要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="603e3-124">For example, [Test Driven Development (TDD)](https://deviq.com/test-driven-development) is when a unit test is written before the code it's meant to check.</span></span> <span data-ttu-id="603e3-125">TDD 就像先编写书籍大纲，再编写该书籍。</span><span class="sxs-lookup"><span data-stu-id="603e3-125">TDD is like creating an outline for a book before you write it.</span></span> <span data-ttu-id="603e3-126">它旨在帮助开发人员编写更简单、更具可读性的高效代码。</span><span class="sxs-lookup"><span data-stu-id="603e3-126">It is meant to help developers write simpler, more readable, and efficient code.</span></span>

## <a name="testing-tools"></a><span data-ttu-id="603e3-127">测试工具</span><span class="sxs-lookup"><span data-stu-id="603e3-127">Testing tools</span></span>

<span data-ttu-id="603e3-128">.NET 是一个多语言开发平台，可以为 [C#](../../csharp/index.yml)、[F#](../../fsharp/index.yml) 和 [Visual Basic](../../visual-basic/index.yml) 编写各种测试类型。</span><span class="sxs-lookup"><span data-stu-id="603e3-128">.NET is a multi-language development platform, and you can write various test types for [C#](../../csharp/index.yml), [F#](../../fsharp/index.yml), and [Visual Basic](../../visual-basic/index.yml).</span></span> <span data-ttu-id="603e3-129">对于每种语言，可以在几个测试框架中进行选择。</span><span class="sxs-lookup"><span data-stu-id="603e3-129">For each of these languages, you can choose between several test frameworks.</span></span>

### <a name="xunit"></a><span data-ttu-id="603e3-130">xUnit</span><span class="sxs-lookup"><span data-stu-id="603e3-130">xUnit</span></span>

<span data-ttu-id="603e3-131">[xUnit](https://xunit.net) 是一个适用于 .NET 的免费、开源、面向社区的单元测试工具。</span><span class="sxs-lookup"><span data-stu-id="603e3-131">[xUnit](https://xunit.net) is a free, open source, community-focused unit testing tool for .NET.</span></span> <span data-ttu-id="603e3-132">xUnit.net 由 NUnit v2 的原发明者编写，是针对单元测试 .NET 应用的最新技术。</span><span class="sxs-lookup"><span data-stu-id="603e3-132">Written by the original inventor of NUnit v2, xUnit.net is the latest technology for unit testing .NET apps.</span></span> <span data-ttu-id="603e3-133">xUnit.net 适用于 ReSharper、CodeRush、TestDriven.NET 和 [Xamarin](/apps/xamarin)。</span><span class="sxs-lookup"><span data-stu-id="603e3-133">xUnit.net works with ReSharper, CodeRush, TestDriven.NET, and [Xamarin](/apps/xamarin).</span></span> <span data-ttu-id="603e3-134">它是 [.NET Foundation](https://dotnetfoundation.org) 的项目，并在其行为准则下运行。</span><span class="sxs-lookup"><span data-stu-id="603e3-134">It is a project of the [.NET Foundation](https://dotnetfoundation.org) and operates under their code of conduct.</span></span>

<span data-ttu-id="603e3-135">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="603e3-135">For more information, see the following resources:</span></span>

- [<span data-ttu-id="603e3-136">使用 C# 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-136">Unit testing with C#</span></span>](unit-testing-with-dotnet-test.md)
- [<span data-ttu-id="603e3-137">使用 F# 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-137">Unit testing with F#</span></span>](unit-testing-fsharp-with-dotnet-test.md)
- [<span data-ttu-id="603e3-138">使用 Visual Basic 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-138">Unit testing with Visual Basic</span></span>](unit-testing-visual-basic-with-dotnet-test.md)

### <a name="nunit"></a><span data-ttu-id="603e3-139">NUnit</span><span class="sxs-lookup"><span data-stu-id="603e3-139">NUnit</span></span>

<span data-ttu-id="603e3-140">[NUnit](https://nunit.org) 是适用于所有 .NET 语言的单元测试框架。</span><span class="sxs-lookup"><span data-stu-id="603e3-140">[NUnit](https://nunit.org) is a unit-testing framework for all .NET languages.</span></span> <span data-ttu-id="603e3-141">最初从 JUnit 移植而来，当前生产版本已被重写，添加了许多新功能和对各种 .NET 平台的支持。</span><span class="sxs-lookup"><span data-stu-id="603e3-141">Initially ported from JUnit, the current production release has been rewritten with many new features and support for a wide range of .NET platforms.</span></span> <span data-ttu-id="603e3-142">它是 [.NET Foundation](https://dotnetfoundation.org) 的项目。</span><span class="sxs-lookup"><span data-stu-id="603e3-142">It is a project of the [.NET Foundation](https://dotnetfoundation.org).</span></span>

<span data-ttu-id="603e3-143">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="603e3-143">For more information, see the following resources:</span></span>

- [<span data-ttu-id="603e3-144">使用 C# 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-144">Unit testing with C#</span></span>](unit-testing-with-nunit.md)
- [<span data-ttu-id="603e3-145">使用 F# 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-145">Unit testing with F#</span></span>](unit-testing-fsharp-with-nunit.md)
- [<span data-ttu-id="603e3-146">使用 Visual Basic 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-146">Unit testing with Visual Basic</span></span>](unit-testing-visual-basic-with-nunit.md)

### <a name="mstest"></a><span data-ttu-id="603e3-147">MSTest</span><span class="sxs-lookup"><span data-stu-id="603e3-147">MSTest</span></span>

<span data-ttu-id="603e3-148">[MSTest](https://github.com/Microsoft/testfx-docs) 是适用于所有 .NET 语言的 Microsoft 测试框架。</span><span class="sxs-lookup"><span data-stu-id="603e3-148">[MSTest](https://github.com/Microsoft/testfx-docs) is the Microsoft test framework for all .NET languages.</span></span> <span data-ttu-id="603e3-149">它可以扩展，并且适用于 .NET CLI 和 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="603e3-149">It's extensible and works with both .NET CLI and Visual Studio.</span></span> <span data-ttu-id="603e3-150">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="603e3-150">For more information, see the following resources:</span></span>

- [<span data-ttu-id="603e3-151">使用 C# 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-151">Unit testing with C#</span></span>](unit-testing-with-mstest.md)
- [<span data-ttu-id="603e3-152">使用 F# 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-152">Unit testing with F#</span></span>](unit-testing-fsharp-with-mstest.md)
- [<span data-ttu-id="603e3-153">使用 Visual Basic 执行单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-153">Unit testing with Visual Basic</span></span>](unit-testing-visual-basic-with-mstest.md)

### <a name="net-cli"></a><span data-ttu-id="603e3-154">.NET CLI</span><span class="sxs-lookup"><span data-stu-id="603e3-154">.NET CLI</span></span>

<span data-ttu-id="603e3-155">你可以使用 [dotnet test](../tools/dotnet-test.md) 命令，从 [.NET CLI](../tools/index.md) 运行解决方案单元测试。</span><span class="sxs-lookup"><span data-stu-id="603e3-155">You can run a solutions unit tests from the [.NET CLI](../tools/index.md), with the [dotnet test](../tools/dotnet-test.md) command.</span></span> <span data-ttu-id="603e3-156">.NET CLI 公开了 [集成开发环境 (IDE)](#ide) 通过用户界面提供的大部分功能。</span><span class="sxs-lookup"><span data-stu-id="603e3-156">The .NET CLI exposes a majority of the functionality that [Integrated Development Environments (IDEs)](#ide) make available through user interfaces.</span></span> <span data-ttu-id="603e3-157">.NET CLI 是跨平台的，可作为持续集成和交付管道的一部分使用。</span><span class="sxs-lookup"><span data-stu-id="603e3-157">The .NET CLI is cross-platform and available to use as part of continuous integration and delivery pipelines.</span></span> <span data-ttu-id="603e3-158">.NET CLI 用于脚本化进程，以自动执行常见任务。</span><span class="sxs-lookup"><span data-stu-id="603e3-158">The .NET CLI is used with scripted processes to automate common tasks.</span></span>

### <a name="ide"></a><span data-ttu-id="603e3-159">IDE</span><span class="sxs-lookup"><span data-stu-id="603e3-159">IDE</span></span>

<span data-ttu-id="603e3-160">无论使用的是 Visual Studio、Visual Studio for Mac 还是 Visual Studio Code，都有用于测试功能的图形用户界面。</span><span class="sxs-lookup"><span data-stu-id="603e3-160">Whether you're using Visual Studio, Visual Studio for Mac, or Visual Studio Code, there are graphical user interfaces for testing functionality.</span></span> <span data-ttu-id="603e3-161">IDE 提供了比 CLI 更多的功能，例如 [Live Unit Testing](/visualstudio/test/live-unit-testing)。</span><span class="sxs-lookup"><span data-stu-id="603e3-161">There are more features available to IDEs than the CLI, for example [Live Unit Testing](/visualstudio/test/live-unit-testing).</span></span> <span data-ttu-id="603e3-162">有关详细信息，请参阅 [Visual Studio 中的包含与排除测试](/visualstudio/test/live-unit-testing#include-and-exclude-test-projects-and-test-methods)。</span><span class="sxs-lookup"><span data-stu-id="603e3-162">For more information, see [Including and excluding tests with Visual Studio](/visualstudio/test/live-unit-testing#include-and-exclude-test-projects-and-test-methods).</span></span>

## <a name="see-also"></a><span data-ttu-id="603e3-163">另请参阅</span><span class="sxs-lookup"><span data-stu-id="603e3-163">See also</span></span>

<span data-ttu-id="603e3-164">有关详细信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="603e3-164">For more information, see the following articles:</span></span>

- [<span data-ttu-id="603e3-165">使用 .NET 执行单元测试的最佳实践</span><span class="sxs-lookup"><span data-stu-id="603e3-165">Unit testing best practices with .NET</span></span>](unit-testing-best-practices.md)
- <span data-ttu-id="603e3-166">ASP.NET Core 中的集成测试  </span><span class="sxs-lookup"><span data-stu-id="603e3-166">[Integration tests in ASP.NET Core](/aspnet/core/test/integration-tests#test-app-prerequisites)</span></span>
- [<span data-ttu-id="603e3-167">运行选择性单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-167">Running selective unit tests</span></span>](selective-unit-tests.md)
- [<span data-ttu-id="603e3-168">将代码覆盖率用于单元测试</span><span class="sxs-lookup"><span data-stu-id="603e3-168">Use code coverage for unit testing</span></span>](unit-testing-code-coverage.md)
