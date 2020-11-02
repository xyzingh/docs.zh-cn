---
title: 如何：使用支持基于事件的异步模式的组件
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET], asynchronous features
- components [.NET], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
ms.openlocfilehash: 51394a49f12e8611ac6dba7eb93a6c9a9fae0cd0
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888797"
---
# <a name="how-to-use-components-that-support-the-event-based-asynchronous-pattern"></a><span data-ttu-id="08d62-102">如何：使用支持基于事件的异步模式的组件</span><span class="sxs-lookup"><span data-stu-id="08d62-102">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>
<span data-ttu-id="08d62-103">许多组件都支持异步执行工作。</span><span class="sxs-lookup"><span data-stu-id="08d62-103">Many components provide you with the option of performing their work asynchronously.</span></span> <span data-ttu-id="08d62-104">例如，通过 <xref:System.Media.SoundPlayer> 和 <xref:System.Windows.Forms.PictureBox> 组件，可以“在后台”加载音频和图像，同时主线程继续运行而不中断。</span><span class="sxs-lookup"><span data-stu-id="08d62-104">The <xref:System.Media.SoundPlayer> and <xref:System.Windows.Forms.PictureBox> components, for example, enable you to load sounds and images "in the background" while your main thread continues running without interruption.</span></span>  
  
 <span data-ttu-id="08d62-105">对支持 [基于事件的异步模式概述](event-based-asynchronous-pattern-overview.md)的类使用异步方法，这与将事件处理程序附加到组件的 _MethodName_**Completed** 事件一样简单，就像处理其他任何事件一样。</span><span class="sxs-lookup"><span data-stu-id="08d62-105">Using asynchronous methods on a class that supports the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md) can be as simple as attaching an event handler to the component's _MethodName_**Completed** event, just as you would for any other event.</span></span> <span data-ttu-id="08d62-106">调用 _MethodName_**Async** 方法后，应用程序会继续运行而不中断，除非 _MethodName_**Completed** 事件抛出。</span><span class="sxs-lookup"><span data-stu-id="08d62-106">When you call the _MethodName_**Async** method, your application will continue running without interruption until the _MethodName_**Completed** event is raised.</span></span> <span data-ttu-id="08d62-107">在事件处理程序中，可以检查 <xref:System.ComponentModel.AsyncCompletedEventArgs> 参数，以确定异步操作是已成功完成，还是已取消。</span><span class="sxs-lookup"><span data-stu-id="08d62-107">In your event handler, you can examine the <xref:System.ComponentModel.AsyncCompletedEventArgs> parameter to determine if the asynchronous operation successfully completed or if it was canceled.</span></span>  
  
 <span data-ttu-id="08d62-108">若要详细了解如何使用事件处理程序，请参阅[事件处理程序概述](/dotnet/desktop/winforms/event-handlers-overview-windows-forms)。</span><span class="sxs-lookup"><span data-stu-id="08d62-108">For more information about using event handlers, see [Event Handlers Overview](/dotnet/desktop/winforms/event-handlers-overview-windows-forms).</span></span>  
  
 <span data-ttu-id="08d62-109">下面的过程展示了如何使用 <xref:System.Windows.Forms.PictureBox> 控件的异步图像加载功能。</span><span class="sxs-lookup"><span data-stu-id="08d62-109">The following procedure shows how to use the asynchronous image-loading capability of a <xref:System.Windows.Forms.PictureBox> control.</span></span>  
  
### <a name="to-enable-a-picturebox-control-to-asynchronously-load-an-image"></a><span data-ttu-id="08d62-110">启用 PictureBox 控件以异步加载图像的具体步骤</span><span class="sxs-lookup"><span data-stu-id="08d62-110">To enable a PictureBox control to asynchronously load an image</span></span>  
  
1. <span data-ttu-id="08d62-111">在窗体中，创建 <xref:System.Windows.Forms.PictureBox> 组件的实例。</span><span class="sxs-lookup"><span data-stu-id="08d62-111">Create an instance of the <xref:System.Windows.Forms.PictureBox> component in your form.</span></span>  
  
2. <span data-ttu-id="08d62-112">将事件处理程序分配给 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 事件。</span><span class="sxs-lookup"><span data-stu-id="08d62-112">Assign an event handler to the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event.</span></span>  
  
     <span data-ttu-id="08d62-113">检查是否有异步下载期间可能会发生的任何错误。</span><span class="sxs-lookup"><span data-stu-id="08d62-113">Check for any errors that may have occurred during the asynchronous download here.</span></span> <span data-ttu-id="08d62-114">此时，还检查是否有取消事件。</span><span class="sxs-lookup"><span data-stu-id="08d62-114">This is also where you check for cancellation.</span></span>  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#5)]  
  
3. <span data-ttu-id="08d62-115">将两个按钮 `loadButton` 和 `cancelLoadButton` 添加到窗体。</span><span class="sxs-lookup"><span data-stu-id="08d62-115">Add two buttons, called `loadButton` and `cancelLoadButton`, to your form.</span></span> <span data-ttu-id="08d62-116">添加 <xref:System.Windows.Forms.Control.Click> 事件处理程序，以启动和取消下载。</span><span class="sxs-lookup"><span data-stu-id="08d62-116">Add <xref:System.Windows.Forms.Control.Click> event handlers to start and cancel the download.</span></span>  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/Form1.vb#4)]  
  
4. <span data-ttu-id="08d62-117">运行您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="08d62-117">Run your application.</span></span>  
  
     <span data-ttu-id="08d62-118">随着图像继续下载，可以随意移动窗体，也能最小化和最大化窗体。</span><span class="sxs-lookup"><span data-stu-id="08d62-118">As the image download proceeds, you can move the form freely, minimize it, and maximize it.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="08d62-119">另请参阅</span><span class="sxs-lookup"><span data-stu-id="08d62-119">See also</span></span>

- [<span data-ttu-id="08d62-120">如何：在后台运行操作</span><span class="sxs-lookup"><span data-stu-id="08d62-120">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="08d62-121">基于事件的异步模式概述</span><span class="sxs-lookup"><span data-stu-id="08d62-121">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
