---
title: 作法：使用服務 Moniker 搭配中繼資料交換合約
ms.date: 03/30/2017
ms.assetid: c41a07e5-cb9d-45d6-9ea4-34511e227faf
ms.openlocfilehash: 194caf6a48e64a4358a77ecd514dda456cc35e0b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265956"
---
# <a name="how-to-use-a-service-moniker-with-metadata-exchange-contracts"></a><span data-ttu-id="28644-102">作法：使用服務 Moniker 搭配中繼資料交換合約</span><span class="sxs-lookup"><span data-stu-id="28644-102">How to: Use a Service Moniker with Metadata Exchange Contracts</span></span>

<span data-ttu-id="28644-103">在開發新的 WCF 服務之後，您可能會決定要能夠從腳本或 Visual Basic 6.0 應用程式呼叫這些服務。</span><span class="sxs-lookup"><span data-stu-id="28644-103">After developing some new WCF services, you may decide that you want to be able to call these services from a script or a Visual Basic 6.0 application.</span></span> <span data-ttu-id="28644-104">其中一個方法是產生 WCF 用戶端元件、向 COM 註冊元件、將元件安裝在 GAC 中，然後從您的 Visual Basic 程式碼中參考 COM 類型。</span><span class="sxs-lookup"><span data-stu-id="28644-104">One method would be to generate a WCF client assembly, register the assembly with COM, install the assembly in the GAC, and then reference the COM types from your Visual Basic code.</span></span> <span data-ttu-id="28644-105">當您散發應用程式時，您也必須散發 WCF 用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="28644-105">When you distribute the application, you will have to distribute the WCF Client assembly as well.</span></span> <span data-ttu-id="28644-106">然後使用者必須向 COM 註冊 WCF 用戶端組件，並將它放在 GAC 中。</span><span class="sxs-lookup"><span data-stu-id="28644-106">The user will then have to register the WCF client assembly with COM and place it in the GAC.</span></span> <span data-ttu-id="28644-107">WCF COM Interop 也可讓您進行相同的服務呼叫，而不需要依賴 WCF 用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="28644-107">WCF COM Interop also allows you to make the same service calls without relying on a WCF client assembly.</span></span> <span data-ttu-id="28644-108">WCF 標記可讓您從任何 COM 相容的語言呼叫任何 WCF 服務 (Visual Basic、VBScript、Visual Basic for Applications (VBA) 等) ，方法是指定中繼資料交換 (端點 URI，讓服務的標記用來解壓縮服務的類型資訊。</span><span class="sxs-lookup"><span data-stu-id="28644-108">The WCF moniker allows you to call any WCF service from any COM-compatible language (Visual Basic, VBScript, Visual Basic for Applications (VBA), and so on) by specifying a metadata exchange (Mex) endpoint URI that the service moniker uses to extract type information about the service.</span></span> <span data-ttu-id="28644-109">本主題說明如何使用指定 Mex 端點的 WCF 標記來呼叫消費者入門 WCF 範例。</span><span class="sxs-lookup"><span data-stu-id="28644-109">This topic describes how to call the Getting Started WCF sample using a WCF moniker that specifies a Mex endpoint.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="28644-110">WCF 用戶端元件所定義的類型絕不會真正具現化。</span><span class="sxs-lookup"><span data-stu-id="28644-110">The types defined by the WCF client assembly are never actually instantiated.</span></span> <span data-ttu-id="28644-111">此組件僅用於中繼資料。</span><span class="sxs-lookup"><span data-stu-id="28644-111">The assembly is used only for metadata.</span></span>  
  
### <a name="using-the-service-moniker-with-a-mex-address"></a><span data-ttu-id="28644-112">使用含有 Mex 位址的服務 Moniker</span><span class="sxs-lookup"><span data-stu-id="28644-112">Using the service moniker with a Mex address</span></span>  
  
1. <span data-ttu-id="28644-113">建立消費者入門範例，並使用 Internet Explorer 流覽至 () 的 URL， `http://localhost/ServiceModelSamples/Service.svc` 以確保服務正常運作。</span><span class="sxs-lookup"><span data-stu-id="28644-113">Build the Getting Started sample and use Internet Explorer to browse to its URL (`http://localhost/ServiceModelSamples/Service.svc`) to ensure that the service is working.</span></span>  
  
2. <span data-ttu-id="28644-114">建立 Visual Basic 指令碼或含有下列程式碼的 Visual Basic 應用程式：</span><span class="sxs-lookup"><span data-stu-id="28644-114">Create a Visual Basic script or Visual Basic application that contains the following code:</span></span>  
  
    ```vb
    monString = "service:mexaddress=http://localhost/ServiceModelSamples/Service.svc/MEX"  
    monString = monString + ", address=http://localhost/ServiceModelSamples/Service.svc"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set calc = GetObject(monString)  
    MsgBox calc.Add(3, 4)  
    ```  
  
3. <span data-ttu-id="28644-115">執行 Visual Basic 應用程式或指令碼。</span><span class="sxs-lookup"><span data-stu-id="28644-115">Run the Visual Basic application or script.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="28644-116">您正在呼叫的服務必須公開 Mex 端點，Moniker 才能從服務讀取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="28644-116">The service you are calling must expose a Mex endpoint for the moniker to be able to read the metadata from the service.</span></span> <span data-ttu-id="28644-117">如需詳細資訊，請參閱 [如何：使用設定檔發行服務的中繼資料](how-to-publish-metadata-for-a-service-using-a-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="28644-117">For more information, see [How to: Publish Metadata for a Service Using a Configuration File](how-to-publish-metadata-for-a-service-using-a-configuration-file.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="28644-118">如果 Moniker 的格式錯誤或服務無法使用，則呼叫 `GetObject` 時將會傳回「無效的語法」錯誤。</span><span class="sxs-lookup"><span data-stu-id="28644-118">If the moniker is malformed or if the service is unavailable, the call to `GetObject` will return an error saying "Invalid Syntax."</span></span>  <span data-ttu-id="28644-119">如果您收到這個錯誤，請確定您所使用的 Moniker 正確無誤，而且此服務為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="28644-119">If you receive this error, make sure the moniker you are using is correct and the service is available.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="28644-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="28644-120">See also</span></span>

- [<span data-ttu-id="28644-121">作法：使用 Windows Communication Foundation 服務 Moniker 且不註冊</span><span class="sxs-lookup"><span data-stu-id="28644-121">How to: Use the Windows Communication Foundation Service Moniker without Registration</span></span>](use-the-wcf-service-moniker-without-registration.md)
- [<span data-ttu-id="28644-122">作法：使用服務 Moniker 搭配 WSDL 合約</span><span class="sxs-lookup"><span data-stu-id="28644-122">How to: Use a Service Moniker with WSDL Contracts</span></span>](how-to-use-a-service-moniker-with-wsdl-contracts.md)
