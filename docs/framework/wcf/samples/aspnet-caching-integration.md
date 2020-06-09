---
title: ASP.NET 快取整合
ms.date: 03/30/2017
ms.assetid: f581923a-8a72-42fc-bd6a-46de2aaeecc1
ms.openlocfilehash: c541f3caad8a500b9fdb33d00b58706bac876e37
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594747"
---
# <a name="aspnet-caching-integration"></a>ASP.NET 快取整合

這個範例示範如何使用 ASP.NET 輸出快取搭配 WCF WEB HTTP 程式設計模型。 本主題著重在 ASP.NET 輸出快取整合功能。

## <a name="demonstrates"></a>示範

與 ASP.NET 輸出快取整合

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\AspNetCachingIntegration`

## <a name="discussion"></a>討論區

此範例會使用 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 來利用 ASP.NET 輸出快取搭配 Windows Communication Foundation （WCF）服務。 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 會套用至服務作業，並提供應套用至所指作業之回應的組態檔中快取設定檔的名稱。

在範例服務專案的 Service.cs 檔案中， `GetCustomer` 和 `GetCustomers` 作業都以標示 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> ，這會提供快取設定檔名稱 "CacheFor60Seconds"。 在服務專案的 web.config 檔案中，快取設定檔 "CacheFor60Seconds" 是在 `caching` < > 的 < > 元素底下提供 `system.web` 。 此快取設定檔的 `duration` 屬性值為 "60"，因此與此設定檔相關聯的回應會在 ASP.NET 輸出快取中快取60秒。 此外，此快取設定檔的 `varmByParam` 屬性設定為 "format"，因此查詢字串參數具有不同值的要求 `format` 會分別快取其回應。 最後，快取設定檔的 `varyByHeader` 屬性會設定為「接受」，因此具有不同 Accept 標頭值的要求會分別快取其回應。

用戶端專案中的 Program.cs 會示範如何使用 <xref:System.Net.HttpWebRequest> 編寫這種用戶端。 請注意，這只是存取 WCF 服務的其中一種方式。 您也可以使用其他 .NET Framework 類別（例如 WCF 通道處理站和）來存取服務 <xref:System.Net.WebClient> 。 SDK 中的其他範例（例如[基本 HTTP 服務](basic-http-service.md)範例）說明如何使用這些類別與 WCF 服務進行通訊。

## <a name="to-run-the-sample"></a>執行範例

此範例包含三個專案：

- **服務**：包含裝載于 ASP.NET 之 WCF HTTP 服務的 Web 應用程式專案。

- **用戶端**：會呼叫服務的主控台應用程式專案。

- **通用**：包含用戶端和服務所使用之客戶類型的共用程式庫。

當用戶端主控台應用程式執行時，用戶端會對服務發出要求，然後將相關的資訊從回應寫入至主控台視窗。

#### <a name="to-run-the-sample"></a>執行範例

1. 開啟「ASP.NET 快取整合範例」的方案。

2. 按 CTRL+SHIFT+B 建置解決方案。

3. 如果 [**方案總管**] 視窗尚未開啟，請按 CTRL + W + S。

4. 從 [**方案總管**] 視窗中，以滑鼠右鍵按一下**服務**專案，然後選取 [**開始新實例**]。 這樣會啟動裝載服務的 ASP.NET 程式開發伺服器。

5. 從 [**方案總管**] 視窗中，以滑鼠右鍵按一下**用戶端**專案，然後選取 [**開始新實例**]。

6. 用戶端主控台視窗隨即出現，並提供執行中服務的 URI，以及執行中服務之 HTML 說明頁的 URI。 您可以隨時在瀏覽器中輸入說明頁的 URI 來檢視 HTML 說明頁。

7. 當範例執行時，用戶端會寫入目前活動的狀態。

8. 按下任何按鍵可終止用戶端主控台應用程式。

9. 按 SHIFT+F5 停止對服務偵錯。

10. 在 Windows 通知區域中，以滑鼠右鍵按一下 ASP.NET 開發伺服器圖示，然後選取 [**停止**]。
