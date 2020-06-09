---
title: HOW TO：在 IIS 中裝載 WCF 服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b044b1c9-c1e5-4c9f-84d8-0f02f4537f8b
ms.openlocfilehash: 326a270c4af38738c910828acd483070ab02ecd1
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593083"
---
# <a name="how-to-host-a-wcf-service-in-iis"></a>HOW TO：在 IIS 中裝載 WCF 服務
本主題概述建立裝載于 Internet Information Services （IIS）中的 Windows Communication Foundation （WCF）服務所需的基本步驟。 本主題假設您熟悉 IIS，而且了解如何使用 IIS 管理工具建立與管理 IIS 應用程式。 如需 IIS 的詳細資訊，請參閱[Internet Information Services](https://www.iis.net/)。 在 IIS 環境中執行的 WCF 服務會充分利用 IIS 的功能，例如進程回收、閒置關機、進程健康狀態監控，以及訊息型啟用。 這個裝載選項要求必須正確設定 IIS，但不要求您將任何裝載程式碼撰寫為應用程式的一部分。 IIS 裝載只能和 HTTP 傳輸一起使用。  
  
 如需 WCF 和 ASP.NET 如何互動的詳細資訊，請參閱[Wcf 服務和 ASP.NET](wcf-services-and-aspnet.md)。 如需設定安全性的詳細資訊，請參閱[安全性](security.md)。  
  
 如需此範例的來源複本，請參閱[使用內嵌程式碼的 IIS 裝載](../samples/iis-hosting-using-inline-code.md)。  
  
### <a name="to-create-a-service-hosted-by-iis"></a>若要建立 IIS 裝載的服務  
  
1. 確認您的電腦上已安裝 IIS 且正在執行中。 如需安裝和設定 IIS 的詳細資訊，請參閱[安裝和設定 iis 7.0](https://docs.microsoft.com/iis/install/installing-iis-7/installing-necessary-iis-components-on-windows-vista)  
  
2. 為您的應用程式檔建立名為 "IISHostedCalcService" 的新資料夾，確認 ASP.NET 可存取資料夾的內容，並使用 IIS 管理工具來建立實際位於此應用程式目錄中的新 IIS 應用程式。 建立應用程式目錄的別名時，請使用 "IISHostedCalc"。  
  
3. 在應用程式目錄中建立名為 "service.svc" 的新檔案。 新增下列專案以編輯此檔案 @ServiceHost 。  
  
   ```
   <%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService"%>
   ```  
  
4. 在應用程式目錄中建立 App_Code 子目錄。  
  
5. 在 App_Code 子目錄中建立名為 Service.cs 的程式碼檔案。  
  
6. 使用陳述式將以下加入至 Service.cs 檔案的最上方。  
  
    ```csharp  
    using System;  
    using System.ServiceModel;  
    ```  
  
7. 使用陳述式之後，加入下列命名空間宣告。  
  
    ```csharp  
    namespace Microsoft.ServiceModel.Samples  
    {  
    }  
    ```  
  
8. 在命名空間宣告內定義服務合約，如下列程式碼所示。  
  
     [!code-csharp[c_HowTo_HostInIIS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#11)]
     [!code-vb[c_HowTo_HostInIIS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#11)]  
  
9. 在符合合約定義之後實作服務合約，如下列程式碼所示。  
  
     [!code-csharp[c_HowTo_HostInIIS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#12)]
     [!code-vb[c_HowTo_HostInIIS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#12)]  
  
10. 在應用程式目錄中建立名為 "Web.config" 的檔案，並將下列組態程式碼加入至該檔案中。 在執行時間，WCF 基礎結構會使用此資訊來建立用戶端應用程式可以與之通訊的端點。  
  
     [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]
  
     此範例會在組態檔中明確地指定端點。 如果您沒有將任何端點加入至服務中，執行階段會為您加入預設端點。 如需預設端點、系結和行為的詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定和[WCF 服務的簡化](../samples/simplified-configuration-for-wcf-services.md)設定。  
  
11. 若要確認服務裝載正確，請開啟 Internet Explorer 的執行個體，然後瀏覽到服務的 URL：`http://localhost/IISHostedCalc/Service.svc`  
  
## <a name="example"></a>範例  
 以下是裝載於 IIS 之計算機服務的完整程式碼清單。  
  
 [!code-csharp[C_HowTo_HostInIIS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#1)]
 [!code-vb[C_HowTo_HostInIIS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#1)]
 [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]  
  
## <a name="see-also"></a>請參閱

- [在網際網路資訊服務中裝載](hosting-in-internet-information-services.md)
- [裝載服務](../hosting-services.md)
- [WCF 服務與 ASP.NET](wcf-services-and-aspnet.md)
- [安全性](security.md)
- [Windows Server AppFabric 裝載功能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))
