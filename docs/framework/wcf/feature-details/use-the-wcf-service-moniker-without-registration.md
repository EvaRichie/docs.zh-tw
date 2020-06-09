---
title: HOW TO：使用 Windows Communication Foundation 服務 Moniker 且不註冊
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], service monikers without registration
ms.assetid: ee3cf5c0-24f0-4ae7-81da-73a60de4a1a8
ms.openlocfilehash: f69314948a0e0a69e49ec148f94572f17d0b8e3c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595046"
---
# <a name="how-to-use-the-windows-communication-foundation-service-moniker-without-registration"></a><span data-ttu-id="0e4a4-102">HOW TO：使用 Windows Communication Foundation 服務 Moniker 且不註冊</span><span class="sxs-lookup"><span data-stu-id="0e4a4-102">How to: Use the Windows Communication Foundation Service Moniker without Registration</span></span>
<span data-ttu-id="0e4a4-103">若要連接到 Windows Communication Foundation （WCF）服務並與之通訊，WCF 用戶端應用程式必須具有服務位址、系結設定和服務合約的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-103">To connect to and communicate with a Windows Communication Foundation (WCF) service, a WCF client application must have the details of the service address, the binding configuration, and the service contract.</span></span>  
  
 <span data-ttu-id="0e4a4-104">WCF 服務名字標記通常會透過先前註冊的必要屬性類型來取得所需的合約，但可能會發生這種情況不可行的情況。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-104">The WCF service moniker typically obtains the required contract through prior registration of the required attribute types, but there might be cases where this is not feasible.</span></span> <span data-ttu-id="0e4a4-105">如果沒有註冊，Moniker 可使用 `wsdl` 參數、中繼資料交換和使用 `mexAddress` 參數，即可用 Web 服務定義語言 (WSDL) 文件格式來取得合約的定義。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-105">In place of registration, the moniker can obtain the definition of the contract in the form of a Web Services Definition Language (WSDL) document, through the use of the `wsdl` parameter or through Metadata Exchange, through the use of the `mexAddress` parameter.</span></span>  
  
 <span data-ttu-id="0e4a4-106">所適用的案例包括散發 Excel 試算表，在試算表中有些儲存格的值會透過 Web 服務互動計算而來。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-106">This enables scenarios such as the distribution of an Excel spreadsheet where some of the cell values are calculated through Web service interactions.</span></span> <span data-ttu-id="0e4a4-107">在此案例中，可能無法在開啟文件的所有用戶端上註冊服務合約組件。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-107">In this scenario, it might not be feasible to register the service contract assembly on all clients that might open the document.</span></span> <span data-ttu-id="0e4a4-108">`wsdl` 參數或 `mexAddress` 參數將會啟用獨立的 (Self-Contained) 解決方案。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-108">The `wsdl` parameter or the `mexAddress` parameter enables a self-contained solution.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0e4a4-109">您必須使用相互驗證以保護要求和回應不會被竄改或詐騙。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-109">Mutual authentication must be used to protect against request and response tampering or spoofing.</span></span> <span data-ttu-id="0e4a4-110">特別重要的是，用戶端必須確定發出回應的中繼資料交換端點為預期的信任的一方。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-110">Specifically, it is important for clients to be assured that the Metadata Exchange endpoint that is responding is the intended trusted party.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0e4a4-111">範例</span><span class="sxs-lookup"><span data-stu-id="0e4a4-111">Example</span></span>  
 <span data-ttu-id="0e4a4-112">這個範例會顯示搭配使用服務 Moniker 和 MEX 合約。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-112">This example shows the use of the service moniker with a MEX contract.</span></span> <span data-ttu-id="0e4a4-113">將使用 wsHttpBinding 公開具有下列合約的服務。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-113">A service with the following contract is exposed with a wsHttpBinding.</span></span>  
  
```csharp
using System.ServiceModel;  
  
// ...
  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Demo")]  
public interface IAffiliate  
{  
    [OperationContract]  
    bool NewAffiliate(string ID, string company, string fullname, string accountsCode);  
    [OperationContract]  
    bool RemoveAffiliate(string ID);  
    [OperationContract]  
    double RevenueCheckMonthly(ref string ID);  
    [OperationContract]  
    double RevenueCheckTotal(ref string ID);  
}  
```  
  
 <span data-ttu-id="0e4a4-114">若要為遠端服務建立 WCF 用戶端，可以使用下列範例標記字串。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-114">To construct a WCF client for the remote service the following example moniker string can be used.</span></span>  
  
```
service4:mexAddress="http://servername/Affiliates/service.svc/mex",  
address="http://servername/Affiliates/service.svc",  
contract=IAffiliate, contractNamespace=http://Microsoft.ServiceModel.Demo,  
binding=WSHttpBinding_IAffiliate, bindingNamespace=http://tempuri.org/  
```  
  
 <span data-ttu-id="0e4a4-115">在執行用戶端應用程式期間，用戶端會使用提供的 `WS-MetadataExchange` 來執行 `mexAddress`。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-115">During the execution of the client application, the client performs a `WS-MetadataExchange` with the provided `mexAddress`.</span></span> <span data-ttu-id="0e4a4-116">這樣做可能會對一些服務傳回位址、繫結和合約詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-116">This might return the address, binding and contract details for a number of services.</span></span> <span data-ttu-id="0e4a4-117">您可以使用 `address`, `contract`, `contractNamespace`, `binding` 和 `bindingNamespace` 參數來識別要用的服務。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-117">The `address`, `contract`, `contractNamespace`, `binding` and `bindingNamespace` parameters are used to identify the intended service.</span></span> <span data-ttu-id="0e4a4-118">一旦符合這些參數之後，名字標記就會以適當的合約定義來建立 WCF 用戶端，然後使用 WCF 用戶端來呼叫，如同具型別合約。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-118">Once those parameters have been matched, the moniker constructs a WCF client with the appropriate contract definition and calls can then be made using the WCF client, as with the typed contract.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0e4a4-119">如果 Moniker 的格式錯誤或服務無法使用，則呼叫 `GetObject` 時將會傳回「無效的語法」錯誤。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-119">If the moniker is malformed or if the service is unavailable, the call to `GetObject` returns an error saying "Invalid Syntax".</span></span> <span data-ttu-id="0e4a4-120">如果您收到這個錯誤，請確定您所使用的 Moniker 正確無誤，而且此服務為可用狀態。</span><span class="sxs-lookup"><span data-stu-id="0e4a4-120">If you receive this error, make sure the moniker you are using is correct and the service is available.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0e4a4-121">請參閱</span><span class="sxs-lookup"><span data-stu-id="0e4a4-121">See also</span></span>

- [<span data-ttu-id="0e4a4-122">如何：註冊和設定服務 Moniker</span><span class="sxs-lookup"><span data-stu-id="0e4a4-122">How to: Register and Configure a Service Moniker</span></span>](how-to-register-and-configure-a-service-moniker.md)
