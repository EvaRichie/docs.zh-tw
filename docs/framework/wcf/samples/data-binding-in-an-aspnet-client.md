---
title: ASP.NET 用戶端中的資料繫結
ms.date: 03/30/2017
ms.assetid: 68b49fa6-94e7-4d4c-a34e-902a2b3770b6
ms.openlocfilehash: 3e30bcb9852b34eeb919339d57d701e4dda8a644
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266866"
---
# <a name="data-binding-in-an-aspnet-client"></a><span data-ttu-id="88cbc-102">ASP.NET 用戶端中的資料繫結</span><span class="sxs-lookup"><span data-stu-id="88cbc-102">Data Binding in an ASP.NET Client</span></span>

<span data-ttu-id="88cbc-103">這個範例示範如何在 Web Form 應用程式中，將一般 Windows Communication Foundation (WCF) 服務所傳回的資料系結。</span><span class="sxs-lookup"><span data-stu-id="88cbc-103">This sample demonstrates how to bind data returned by a typical Windows Communication Foundation (WCF) service in a Web Forms application.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="88cbc-104">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="88cbc-104">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="88cbc-105">這個範例會示範實作可定義要求-回覆通訊模式之合約的服務。</span><span class="sxs-lookup"><span data-stu-id="88cbc-105">This sample demonstrates a service that implements a contract that defines a request-reply communication pattern.</span></span> <span data-ttu-id="88cbc-106">此範例包含可從瀏覽器存取的用戶端 Web Form 應用程式，以及由 Internet Information Services (IIS) 所裝載的 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="88cbc-106">The sample consists of a client Web Forms application accessible from a browser and a WCF service hosted by Internet Information Services (IIS).</span></span>  
  
 <span data-ttu-id="88cbc-107">服務會實作定義要求-回覆通訊模式的合約。</span><span class="sxs-lookup"><span data-stu-id="88cbc-107">The service implements a contract that defines a request-reply communication pattern.</span></span> <span data-ttu-id="88cbc-108">合約是由 `IWeatherService` 介面所定義，而該介面會公開 (Expose) 名為 `GetWeatherData` 的作業。</span><span class="sxs-lookup"><span data-stu-id="88cbc-108">The contract is defined by the `IWeatherService` interface, which exposes an operation named `GetWeatherData`.</span></span> <span data-ttu-id="88cbc-109">這項作業會接受城市陣列並傳回 `WeatherData` 物件的陣列，而這些物件表示某個城市的最高和最低預測溫度。</span><span class="sxs-lookup"><span data-stu-id="88cbc-109">This operation accepts an array of cities and returns an array of `WeatherData` objects that represent the high and low forecasted temperature for a city.</span></span>  
  
 <span data-ttu-id="88cbc-110">在 ASP.NET 用戶端 .aspx 頁面上，會定義 DataGrid Web 控制項，其中包含服務所傳回之資料的圖形表示。</span><span class="sxs-lookup"><span data-stu-id="88cbc-110">On the ASP.NET client .aspx page, a DataGrid Web control is defined, which contains the graphical representation of the data returned by the service.</span></span> <span data-ttu-id="88cbc-111">.Aspx 頁面上的程式碼會呼叫氣象資料的 WCF 服務，並將資料傳回物件的陣列 `WeatherData` 。</span><span class="sxs-lookup"><span data-stu-id="88cbc-111">Code on the .aspx page calls the WCF service for weather data and returns the data to an array of `WeatherData` objects.</span></span> <span data-ttu-id="88cbc-112">DataGrid 指定從何處取得其資料的方式，是將 `DataSource` 屬性設定為該陣列。</span><span class="sxs-lookup"><span data-stu-id="88cbc-112">The DataGrid specifies where to get its data from by setting its `DataSource` property to that array.</span></span> <span data-ttu-id="88cbc-113">呼叫 DataGrid 的 `DataBind` 方法時便會發生資料繫結。</span><span class="sxs-lookup"><span data-stu-id="88cbc-113">The data binding occurs with a call to the DataGrid's `DataBind` method.</span></span> <span data-ttu-id="88cbc-114">這所有程式碼都包含在中。`aspx`</span><span class="sxs-lookup"><span data-stu-id="88cbc-114">All of this code is contained inside the .`aspx`</span></span> <span data-ttu-id="88cbc-115">頁面的 `Page_Load` 方法，因此每次使用者重新整理瀏覽器頁面時，資料會在 DataGrid 中更新。</span><span class="sxs-lookup"><span data-stu-id="88cbc-115">page's `Page_Load` method, so every time the user refreshes the browser page, the data is updated in the DataGrid.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="88cbc-116">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="88cbc-116">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="88cbc-117">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="88cbc-117">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="88cbc-118">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="88cbc-118">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="88cbc-119">這個範例的用戶端是在程式開發 Web 伺服器中執行的網站。</span><span class="sxs-lookup"><span data-stu-id="88cbc-119">This sample's client is a Web site that runs under a development Web server.</span></span> <span data-ttu-id="88cbc-120">若要啟動開發 Web 服務器，請在命令提示字元中輸入下列命令： `%SystemDrive%\Program Files\Common Files\Microsoft Shared\DevServer\9.0\WebDev.WebServer.EXE" /port:8000 /path:<WebFormsSamplePath>\CS\client /vpath:/client` 。</span><span class="sxs-lookup"><span data-stu-id="88cbc-120">To launch the development Web server, type the following at the command prompt: `%SystemDrive%\Program Files\Common Files\Microsoft Shared\DevServer\9.0\WebDev.WebServer.EXE" /port:8000 /path:<WebFormsSamplePath>\CS\client /vpath:/client`.</span></span> <span data-ttu-id="88cbc-121">然後流覽至 `http://localhost:8000/client` 。</span><span class="sxs-lookup"><span data-stu-id="88cbc-121">Then browse to `http://localhost:8000/client`.</span></span> <span data-ttu-id="88cbc-122">如果要在多部電腦上執行這個範例，請使用伺服器的電腦名稱來取代用戶端的 Web.config 檔案中的 的所有參照。</span><span class="sxs-lookup"><span data-stu-id="88cbc-122">To run this sample across computers, replace all references to `localhost` in the client's Web.config file with the computer name of the server.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="88cbc-123">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="88cbc-123">The samples may already be installed on your machine.</span></span> <span data-ttu-id="88cbc-124">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="88cbc-124">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="88cbc-125">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="88cbc-125">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="88cbc-126">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="88cbc-126">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WebForms`
