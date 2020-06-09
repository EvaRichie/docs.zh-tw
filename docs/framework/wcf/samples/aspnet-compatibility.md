---
title: ASP.NET 相容性
ms.date: 03/30/2017
ms.assetid: c8b51f1e-c096-4c42-ad99-0519887bbbc5
ms.openlocfilehash: 23930e0756d3fbefc28a8f650b5a056106145a50
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594708"
---
# <a name="aspnet-compatibility"></a><span data-ttu-id="0f383-102">ASP.NET 相容性</span><span class="sxs-lookup"><span data-stu-id="0f383-102">ASP.NET Compatibility</span></span>

<span data-ttu-id="0f383-103">這個範例會示範如何在 Windows Communication Foundation （WCF）中啟用 ASP.NET 相容性模式。</span><span class="sxs-lookup"><span data-stu-id="0f383-103">This sample demonstrates how to enable ASP.NET Compatibility mode in Windows Communication Foundation (WCF).</span></span> <span data-ttu-id="0f383-104">在 ASP.NET 相容性模式中執行的服務會完全參與 ASP.NET 應用程式管線，並可利用檔案/URL 授權、會話狀態和類別等 ASP.NET 功能 <xref:System.Web.HttpContext> 。</span><span class="sxs-lookup"><span data-stu-id="0f383-104">Services running in ASP.NET Compatibility mode participate fully in the ASP.NET application pipeline and can make use of ASP.NET features such as file/URL authorization, session state, and the <xref:System.Web.HttpContext> class.</span></span> <span data-ttu-id="0f383-105"><xref:System.Web.HttpContext>類別可讓您存取 cookie、會話和其他 ASP.NET 功能。</span><span class="sxs-lookup"><span data-stu-id="0f383-105">The <xref:System.Web.HttpContext> class allows access to cookies, sessions, and other ASP.NET features.</span></span> <span data-ttu-id="0f383-106">這個模式會要求這些繫結使用 HTTP 傳輸，而且服務本身必須以 IIS 裝載。</span><span class="sxs-lookup"><span data-stu-id="0f383-106">This mode requires that the bindings use the HTTP transport and the service itself must be hosted in IIS.</span></span>

<span data-ttu-id="0f383-107">在這個範例中，用戶端是主控台應用程式 (可執行檔)，而服務則是由網際網路資訊服務 (IIS) 裝載。</span><span class="sxs-lookup"><span data-stu-id="0f383-107">In this sample, the client is a console application (an executable) and the service is hosted in Internet Information Services (IIS).</span></span>

> [!NOTE]
> <span data-ttu-id="0f383-108">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="0f383-108">The set-up procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="0f383-109">此範例需要 .NET Framework 4 應用程式集區，才能執行。</span><span class="sxs-lookup"><span data-stu-id="0f383-109">This sample requires a .NET Framework 4 application pool in order to run.</span></span> <span data-ttu-id="0f383-110">若要建立應用程式集區，或是修改預設的應用程式集區，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="0f383-110">To create a new application pool, or to modify the default application pool, follow these steps.</span></span>

1. <span data-ttu-id="0f383-111">開啟 [ **控制台**]。</span><span class="sxs-lookup"><span data-stu-id="0f383-111">Open **Control Panel**.</span></span>  <span data-ttu-id="0f383-112">開啟 [**系統及安全性**] 標題下的 [系統**管理工具**] 小程式。</span><span class="sxs-lookup"><span data-stu-id="0f383-112">Open the **Administrative Tools** applet under the **System and Security** heading.</span></span> <span data-ttu-id="0f383-113">開啟 [ **Internet Information Services （IIS）管理員**] 小程式。</span><span class="sxs-lookup"><span data-stu-id="0f383-113">Open the **Internet Information Services (IIS) Manager** applet.</span></span>

2. <span data-ttu-id="0f383-114">展開 [**連接**] 窗格中的 treeview。</span><span class="sxs-lookup"><span data-stu-id="0f383-114">Expand the treeview in the **Connections** pane.</span></span> <span data-ttu-id="0f383-115">選取 [**應用程式**集區] 節點。</span><span class="sxs-lookup"><span data-stu-id="0f383-115">Select the **Application Pools** node.</span></span>

3. <span data-ttu-id="0f383-116">若要將預設應用程式集區設定為使用 .NET Framework 4 （這可能會造成與現有網站不相容的問題），請以滑鼠右鍵按一下**DefaultAppPool**清單專案，然後選取 [**基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="0f383-116">To set the default application pool to use .NET Framework 4 (which may cause incompatibility problems with existing sites), right-click the **DefaultAppPool** list item and select **Basic Settings…**.</span></span> <span data-ttu-id="0f383-117">將 [ **.Net Framework 版本**] 下拉設定為 [ **.net framework v v4.0.30128]** （或更新版本）]。</span><span class="sxs-lookup"><span data-stu-id="0f383-117">Set the **.Net Framework Version** pull-down to **.Net Framework v4.0.30128** (or later).</span></span>

4. <span data-ttu-id="0f383-118">若要建立使用 .NET Framework 4 的新應用程式集區（以保留其他應用程式的相容性），請以滑鼠右鍵按一下 [**應用程式**集區] 節點，然後選取 [**新增應用程式集**區 ...]。</span><span class="sxs-lookup"><span data-stu-id="0f383-118">To create a new application pool that uses .NET Framework 4 (to preserve compatibility for other applications), right-click the **Application Pools** node and select **Add Application Pool…**.</span></span> <span data-ttu-id="0f383-119">將新的應用程式集區命名為，然後將 **.Net Framework 版本**向下提取至 **.net framework v v4.0.30128]** （或更新版本）。</span><span class="sxs-lookup"><span data-stu-id="0f383-119">Name the new application pool, and set the **.Net Framework Version** pull-down to **.Net Framework v4.0.30128** (or later).</span></span> <span data-ttu-id="0f383-120">執行下列設定步驟之後，以滑鼠右鍵按一下**ServiceModelSamples**應用程式，然後選取 [**管理應用程式**]、[**高級設定**]。</span><span class="sxs-lookup"><span data-stu-id="0f383-120">After running the setup steps below, right-click the **ServiceModelSamples** application and select **Manage Application**, **Advanced Settings…**.</span></span> <span data-ttu-id="0f383-121">將**應用程式**集區設定為新的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="0f383-121">Set the **Application Pool** to the new application pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f383-122">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0f383-122">The samples may already be installed on your computer.</span></span> <span data-ttu-id="0f383-123">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="0f383-123">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="0f383-124">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="0f383-124">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="0f383-125">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="0f383-125">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\ASPNetCompatibility`

<span data-ttu-id="0f383-126">這個範例是以執行計算機服務的[消費者入門](getting-started-sample.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="0f383-126">This sample is based on the [Getting Started](getting-started-sample.md), which implements a calculator service.</span></span> <span data-ttu-id="0f383-127">`ICalculator` 合約已修改成允許執行一組作業的 `ICalculatorSession` 合約，並同時保留執行結果。</span><span class="sxs-lookup"><span data-stu-id="0f383-127">The `ICalculator` contract has been modified as the `ICalculatorSession` contract to allow a set of operations to be performed, while keeping a running result.</span></span>

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculatorSession
{
    [OperationContract]
    void Clear();
    [OperationContract]
    void AddTo(double n);
    [OperationContract]
    void SubtractFrom(double n);
    [OperationContract]
    void MultiplyBy(double n);
    [OperationContract]
    void DivideBy(double n);
    [OperationContract]
    double Result();
}
```

<span data-ttu-id="0f383-128">此服務會維護用戶端的狀態 (方法是使用該功能)，因為在進行計算時已呼叫了多個服務作業。</span><span class="sxs-lookup"><span data-stu-id="0f383-128">The service maintains state, using the feature, for each client as multiple service operations are called to perform a calculation.</span></span> <span data-ttu-id="0f383-129">用戶端會呼叫 `Result` 以擷取目前的結果，並且能夠呼叫 `Clear` 將結果清除為零。</span><span class="sxs-lookup"><span data-stu-id="0f383-129">The client can retrieve the current result by calling `Result` and can clear the result to zero by calling `Clear`.</span></span>

<span data-ttu-id="0f383-130">服務會使用 ASP.NET 會話來儲存每個用戶端會話的結果。</span><span class="sxs-lookup"><span data-stu-id="0f383-130">The service uses the ASP.NET session to store the result for each client session.</span></span> <span data-ttu-id="0f383-131">這樣服務便可在跨多個服務呼叫時維護每個工作階段的執行結果。</span><span class="sxs-lookup"><span data-stu-id="0f383-131">This allows the service to maintain the running result for each client across multiple calls to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="0f383-132">ASP.NET 會話狀態和 WCF 會話是非常不同的事。</span><span class="sxs-lookup"><span data-stu-id="0f383-132">ASP.NET session state and WCF sessions are very different things.</span></span> <span data-ttu-id="0f383-133">如需 WCF 會話的詳細資訊，請參閱[會話](session.md)。</span><span class="sxs-lookup"><span data-stu-id="0f383-133">See [Session](session.md) for details on WCF sessions.</span></span>

<span data-ttu-id="0f383-134">服務具有 ASP.NET 會話狀態的相關資訊，而且需要 ASP.NET 相容性模式才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="0f383-134">The service has an intimate dependency on ASP.NET session state and requires ASP.NET compatibility mode to function correctly.</span></span> <span data-ttu-id="0f383-135">這些需求會在套用 `AspNetCompatibilityRequirements` 屬性時以宣告方式表達。</span><span class="sxs-lookup"><span data-stu-id="0f383-135">These requirements are expressed declaratively by applying the `AspNetCompatibilityRequirements` attribute.</span></span>

```csharp
[AspNetCompatibilityRequirements(RequirementsMode =
                       AspNetCompatibilityRequirementsMode.Required)]
public class CalculatorService : ICalculatorSession
{
    double Result
    {  // store result in AspNet Session
       get {
          if (HttpContext.Current.Session["Result"] != null)
             return (double)HttpContext.Current.Session["Result"];
          return 0.0D;
       }
       set
       {
          HttpContext.Current.Session["Result"] = value;
       }
    }
    public void Clear()
    {
        Result = 0.0D;
    }
    public void AddTo(double n)
    {
        Result += n;
    }
    public void SubtractFrom(double n)
    {
        Result -= n;
    }
    public void MultiplyBy(double n)
    {
        Result *= n;
    }
    public void DivideBy(double n)
    {
        Result /= n;
    }
    public double Result()
    {
        return Result;
    }
}
```

<span data-ttu-id="0f383-136">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="0f383-136">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="0f383-137">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="0f383-137">Press ENTER in the client window to shut down the client.</span></span>

```console
0, + 100, - 50, * 17.65, / 2 = 441.25
Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="0f383-138">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="0f383-138">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="0f383-139">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="0f383-139">Be sure you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="0f383-140">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="0f383-140">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="0f383-141">建立解決方案之後，請執行 Setup .bat 來設定 IIS 7.0 中的 ServiceModelSamples 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f383-141">After the solution has been built, run Setup.bat to set up the ServiceModelSamples Application in IIS 7.0.</span></span> <span data-ttu-id="0f383-142">ServiceModelSamples 目錄現在應該會顯示為 IIS 7.0 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f383-142">The ServiceModelSamples directory should now appear as an IIS 7.0 Application.</span></span>

4. <span data-ttu-id="0f383-143">若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="0f383-143">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0f383-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0f383-144">See also</span></span>

- <span data-ttu-id="0f383-145">[AppFabric 主控與持續性範例](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="0f383-145">[AppFabric Hosting and Persistence Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))</span></span>
