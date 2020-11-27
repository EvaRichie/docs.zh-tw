---
title: 從 XAML 載入
ms.date: 03/30/2017
ms.assetid: 1f103ef6-7bed-4f16-ae52-9e665c5a43d7
ms.openlocfilehash: ebf6ebe1001773768d8da318a0d6b68d50c7848c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283558"
---
# <a name="load-from-xaml"></a><span data-ttu-id="fb023-102">從 XAML 載入</span><span class="sxs-lookup"><span data-stu-id="fb023-102">Load From XAML</span></span>

<span data-ttu-id="fb023-103">這個範例示範如何動態載入 XAML 工作流程，而不必執行 XamlBuildTask 工具。</span><span class="sxs-lookup"><span data-stu-id="fb023-103">This sample demonstrates how to dynamically load a XAML workflow without having to run the XamlBuildTask tool.</span></span> <span data-ttu-id="fb023-104">這個範例會改為呼叫 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="fb023-104">Instead, the sample calls the <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> method.</span></span> <span data-ttu-id="fb023-105">此範例是 Windows Presentation Foundation (WPF) 用戶端應用程式，它會使用類別載入 XAML 工作流程 <xref:System.Activities.XamlIntegration.ActivityXamlServices> ，並執行這些工作流程。</span><span class="sxs-lookup"><span data-stu-id="fb023-105">The sample is a Windows Presentation Foundation (WPF) client application that loads XAML workflows using the <xref:System.Activities.XamlIntegration.ActivityXamlServices> class and executes them.</span></span> <span data-ttu-id="fb023-106">使用 <xref:System.Activities.XamlIntegration.ActivityXamlServices> 類別載入工作流程之後，就會傳回可以執行的 <xref:System.Activities.DynamicActivity%601>。</span><span class="sxs-lookup"><span data-stu-id="fb023-106">After they have been loaded using the <xref:System.Activities.XamlIntegration.ActivityXamlServices> class, a <xref:System.Activities.DynamicActivity%601> is returned that can be executed.</span></span>

#### <a name="to-use-this-sample"></a><span data-ttu-id="fb023-107">若要使用這個範例</span><span class="sxs-lookup"><span data-stu-id="fb023-107">To use this sample</span></span>

1. <span data-ttu-id="fb023-108">使用 Visual Studio 2010，開啟 LoadFromXAML .sln 方案檔。</span><span class="sxs-lookup"><span data-stu-id="fb023-108">Using Visual Studio 2010, open the LoadFromXAML.sln solution file.</span></span>

2. <span data-ttu-id="fb023-109">若要建置此方案，請按 CTRL+SHIFT+B。</span><span class="sxs-lookup"><span data-stu-id="fb023-109">To build the solution, press CTRL+SHIFT+B.</span></span>

3. <span data-ttu-id="fb023-110">若要執行此方案，請按下 CTRL+F5。</span><span class="sxs-lookup"><span data-stu-id="fb023-110">To run the solution, press CTRL+F5.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb023-111">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="fb023-111">The samples may already be installed on your machine.</span></span> <span data-ttu-id="fb023-112">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="fb023-112">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="fb023-113">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="fb023-113">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="fb023-114">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="fb023-114">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Built-InActivities\DynamicActivity\LoadFromXAML`
