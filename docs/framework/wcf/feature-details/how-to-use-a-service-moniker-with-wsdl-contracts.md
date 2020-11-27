---
title: 作法：使用服務 Moniker 搭配 WSDL 合約
ms.date: 03/30/2017
ms.assetid: a88d9650-bb50-4f48-8c85-12f5ce98a83a
ms.openlocfilehash: 6b1a6c905008b0232a098f253b9007e5147d71a2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96280880"
---
# <a name="how-to-use-a-service-moniker-with-wsdl-contracts"></a><span data-ttu-id="974e0-102">作法：使用服務 Moniker 搭配 WSDL 合約</span><span class="sxs-lookup"><span data-stu-id="974e0-102">How to: Use a Service Moniker with WSDL Contracts</span></span>

<span data-ttu-id="974e0-103">在某些情況中，您可能會想要有完全獨立的 COM Interop 用戶端。</span><span class="sxs-lookup"><span data-stu-id="974e0-103">There are situations when you may want to have a completely self-contained COM Interop client.</span></span> <span data-ttu-id="974e0-104">您要呼叫的服務可能不會公開 MEX 端點，而且系統可能也不會註冊 COM Interop 的 WCF 用戶端 DLL。</span><span class="sxs-lookup"><span data-stu-id="974e0-104">The service you want to call may not expose a MEX endpoint, and the WCF client DLL may not be registered for COM interop.</span></span> <span data-ttu-id="974e0-105">在這些情況中，您可以建立 WSDL 檔案，使其描述服務並傳遞至 WCF 服務 Moniker 中。</span><span class="sxs-lookup"><span data-stu-id="974e0-105">In these cases, you can create a WSDL file that describes the service and pass it into the WCF service moniker.</span></span> <span data-ttu-id="974e0-106">本主題說明如何使用 WCF WSDL Moniker 來呼叫使用者入門 WCF 範例。</span><span class="sxs-lookup"><span data-stu-id="974e0-106">This topic describes how to call the Getting Started WCF sample using a WCF WSDL moniker.</span></span>  
  
### <a name="using-the-wsdl-service-moniker"></a><span data-ttu-id="974e0-107">使用 WSDL 服務 Moniker</span><span class="sxs-lookup"><span data-stu-id="974e0-107">Using the WSDL service moniker</span></span>  
  
1. <span data-ttu-id="974e0-108">開啟和建置 GettingStarted 範例方案。</span><span class="sxs-lookup"><span data-stu-id="974e0-108">Open and build the GettingStarted sample solution.</span></span>  
  
2. <span data-ttu-id="974e0-109">開啟 Internet Explorer 並流覽至， `http://localhost/ServiceModelSamples/Service.svc` 以確定服務可正常運作。</span><span class="sxs-lookup"><span data-stu-id="974e0-109">Open Internet Explorer and browse to `http://localhost/ServiceModelSamples/Service.svc` to make sure that the service is working.</span></span>  
  
3. <span data-ttu-id="974e0-110">在 Service.cs 檔案中新增 CalculatorService 類別的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="974e0-110">In the Service.cs file, add the following attribute on the CalculatorService class:</span></span>  
  
     [!code-csharp[S_WSDL_Client#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wsdl_client/cs/service.cs#0)]  
  
4. <span data-ttu-id="974e0-111">新增繫結命名空間至服務 App.config：</span><span class="sxs-lookup"><span data-stu-id="974e0-111">Add a binding namespace to the service App.config:</span></span>  

5. <span data-ttu-id="974e0-112">建立讓應用程式讀取的 WSDL 檔案。</span><span class="sxs-lookup"><span data-stu-id="974e0-112">Create a WSDL file for the application to read.</span></span> <span data-ttu-id="974e0-113">因為命名空間是在步驟3和4中新增的，所以您可以藉由流覽至，使用 IE 來查詢服務的整個 WSDL 描述 `http://localhost/ServiceModelSamples/Service.svc?wsdl` 。</span><span class="sxs-lookup"><span data-stu-id="974e0-113">Because the namespaces were added in steps 3 and 4, you can use IE to query for the entire WSDL description of the service by browsing to `http://localhost/ServiceModelSamples/Service.svc?wsdl`.</span></span> <span data-ttu-id="974e0-114">然後，您可以從 Internet Explorer 將檔案另存為 serviceWSDL.xml。</span><span class="sxs-lookup"><span data-stu-id="974e0-114">You can then save the file from Internet Explorer as serviceWSDL.xml.</span></span> <span data-ttu-id="974e0-115">如果您在步驟 3 和 4 中沒有指定命名空間，藉由查詢上述 URL 而傳回的 WSDL 文件將不會是完整的 WSDL。</span><span class="sxs-lookup"><span data-stu-id="974e0-115">If you do not specify the namespaces in steps 3 and 4, the WSDL document returned from querying the above URL will not be the complete WSDL.</span></span> <span data-ttu-id="974e0-116">傳回的 WSDL 文件將包含數個匯入其他 WSDL 文件的匯入陳述式。</span><span class="sxs-lookup"><span data-stu-id="974e0-116">The WSDL document returned will include several import statements that import other WSDL documents.</span></span> <span data-ttu-id="974e0-117">您必須瀏覽每個匯入陳述式並建置完整的 WSDL 文件，結合從服務傳回的 WSDL 和匯入 WSDL。</span><span class="sxs-lookup"><span data-stu-id="974e0-117">You will have to go through each import statement and build the complete WSDL document, combining the WSDL returned from the service with the WSDL imported.</span></span>  
  
6. <span data-ttu-id="974e0-118">開啟 Visual Basic 6.0，並建立新的標準 .exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="974e0-118">Open Visual Basic 6.0 and create a new Standard .exe file.</span></span> <span data-ttu-id="974e0-119">將按鈕加入至表單中，然後按兩下這個按鈕，將下列程式碼加入至 Click 處理常式：</span><span class="sxs-lookup"><span data-stu-id="974e0-119">Add a button to the form and double-click the button to add the following code to the Click handler:</span></span>  
  
    ```vb
    ' Open the WSDL contract file and read it all into the wsdlContract string.  
    Const ForReading = 1  
    Set objFSO = CreateObject("Scripting.FileSystemObject")  
    Set objFile = objFSO.OpenTextFile("c:\serviceWsdl.xml", ForReading)  
    wsdlContract = objFile.ReadAll  
    objFile.Close  
  
    ' Create a string for the service moniker including the content of the WSDL contract file.  
    wsdlMonikerString = "service4:address='http://localhost/ServiceModelSamples/service.svc'"  
    wsdlMonikerString = wsdlMonikerString + ", wsdl='" & wsdlContract & "'"  
    wsdlMonikerString = wsdlMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
    wsdlMonikerString = wsdlMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
    ' Create the service moniker object.  
    Set wsdlServiceMoniker = GetObject(wsdlMonikerString)  
  
    ' Call the service operations using the moniker object.  
    MsgBox "WSDL service moniker: 145 - 76.54 = " & wsdlServiceMoniker.Subtract(145, 76.54)  
    ```  
  
    > [!NOTE]
    > 如果 Moniker 格式錯誤或服務無法使用，則呼叫 `GetObject` 時將會傳回「無效的語法」錯誤。  <span data-ttu-id="974e0-121">如果您收到這個錯誤，請確定您所使用的 Moniker 正確無誤，而且此服務為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="974e0-121">If you receive this error, make sure the moniker you are using is correct and the service is available.</span></span>  
  
7. <span data-ttu-id="974e0-122">執行 Visual Basic 應用程式。</span><span class="sxs-lookup"><span data-stu-id="974e0-122">Run the Visual Basic application.</span></span> <span data-ttu-id="974e0-123">訊息方塊會和呼叫 Subtract(145, 76.54) 的結果一起顯示。</span><span class="sxs-lookup"><span data-stu-id="974e0-123">A message box will be displayed with the results of calling Subtract(145, 76.54).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="974e0-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="974e0-124">See also</span></span>

- [<span data-ttu-id="974e0-125">快速入門</span><span class="sxs-lookup"><span data-stu-id="974e0-125">Getting Started</span></span>](../samples/getting-started-sample.md)
- [<span data-ttu-id="974e0-126">整合 COM 應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="974e0-126">Integrating with COM Applications Overview</span></span>](integrating-with-com-applications-overview.md)
