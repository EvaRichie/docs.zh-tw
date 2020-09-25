---
title: 微服務中的復原和高可用性
description: 微服務必須設計為能夠承受暫時性的網路和相依性失敗，他們必須能夠復原才能達到高可用性。
ms.date: 09/20/2018
ms.openlocfilehash: 601255c1e6941b2de9fdb34098dea7edf6d8b987
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172446"
---
# <a name="resiliency-and-high-availability-in-microservices"></a>微服務中的復原和高可用性

處理非預期的失敗是最難解決的問題之一，特別是在分散式系統中。 開發人員撰寫的許多程式碼都是關於處理例外狀況，這也是測試時花費最多時間的部分。 問題比撰寫程式碼來處理失敗更複雜。 當執行微服務的電腦故障時，該怎麼辦？ 您不僅需要偵測此微服務失敗 (本身就是棘手的問題)，還需要設法重新啟動微服務。

微服務通常需要在有可用性的另一部電腦上復原失敗以及重新啟動。 此復原也會回復曾以微服務名義儲存的狀態，即微服務可以復原此狀態的來源，以及微服務是否可以成功重新啟動。 換句話說，計算能力需要有復原功能 (程序可以隨時重新啟動)，以及狀態或資料需有復原性 (無資料遺失且資料維持一致)。

發生其他狀況時，復原功能的問題是複合性的，例如應用程式在升級期間發生錯誤。 配合部署系統工作的微服務，需判斷要繼續前進到較新版本，還是改復原回到前一版本，以維護一致的狀態。 需要考慮一些問題，例如，是否有足夠的電腦可繼續升級，以及如何復原舊版的微服務。 這需要微服務發出健康狀態資訊，以便全體應用程式及協調器做出決定。

此外，復原功能與雲端式系統的必要行為方式有關。 如前所述，雲端式系統必須不怕失敗，也必須嘗試自動從失敗中復原。 例如，如果網路或容器發生錯誤，用戶端應用程式或用戶端服務必須有重試傳送訊息或重試要求的策略，因為在許多情況下，雲端的失敗僅為部分。 本指南的[實作復原應用程式](../implement-resilient-applications/index.md)一節會說明如何處理部分失敗。 它描述使用類似 [Polly](https://github.com/App-vNext/Polly) 的程式庫，以 .NET Core 的指數型輪詢或斷路器模式重試等技術，提供各種處理此主體的原則。

## <a name="health-management-and-diagnostics-in-microservices"></a>微服務的健康狀態管理與診斷

微服務必須報告其健康狀態及診斷，這似乎很明顯，卻常被忽略。 否則，作業層面的見解就會很少。 所面臨的挑戰是讓一組獨立服務的診斷事件相互關聯，並修正電腦時間差異以了解事件順序。 如同您透過協定之通訊協定及資料格式與微服務互動的方式，也必須設立健康狀態和診斷事件的記錄方式標準，這些事件最後都會儲存到事件存放區供查詢和檢視。 在微服務方法中，讓不同團隊在單一記錄格式上取得同意是一件非常重要的事。 檢視應用程式的診斷事件需有一致的方法。

### <a name="health-checks"></a>健康狀態檢查

狀況與診斷不同。 健全狀況是指微服務報告其目前狀態，以便採取適當的行動。 使用升級和部署機制來維護可用性是一個很好例子。 雖然服務目前可能因為處理序當機或電腦重新開機而處於不良狀態，但服務也許還能運作。 您不應該執行升級而讓情況惡化。 最好是先進行調查，或讓微服務有時間復原。 微服務的健全狀況事件可協助我們做出明智的決策，實際上有助於建立自我修復的服務。

在本指南的 [Implementing health checks in ASP.NET Core services](../implement-resilient-applications/monitor-app-health.md#implement-health-checks-in-aspnet-core-services) (實作 ASP.NET Core 服務中的健康狀態檢查) 一節中，我們會說明如何使用您微服務中的新 ASP.NET HealthChecks 程式庫，讓它們向監視服務報告其狀態，以採取適當的動作。

您也可以選擇使用名為 Beat Pulse 的優異開放原始碼程式庫，可在 [GitHub](https://github.com/Xabaril/BeatPulse) 上取得，並為 [NuGet 套件](https://www.nuget.org/packages/BeatPulse/)的形式。 此程式庫也會執行健康狀態檢查，但它會處理兩種檢查：

- **活動**：檢查微服務是否為作用中，也就是是否可以接受要求和回應。
- **就緒**：檢查微服務的相依性 (資料庫、佇列服務等 ) 是否已備妥，因此微服務可以執行它應該執行的動作。

### <a name="using-diagnostics-and-logs-event-streams"></a>使用診斷和記錄檔事件資料流

記錄檔會提供應用程式或服務如何執行的資訊，包括例外狀況、警告和簡單參考訊息。 通常，每個記錄檔都是一行一事件的文字格式，雖然例外狀況通常也會跨多行顯示堆疊追蹤。

在整合型伺服器應用程式中，您可以只將記錄寫入磁碟的檔案 (記錄檔)，再使用任何工具予以分析。 因為應用程式執行僅限於固定的伺服器或 VM，所以分析事件流程一般不會太複雜。 不過，在多項服務跨許多協調器叢集節點執行的分散式應用程式中，能夠讓分散式事件相互關聯是一項挑戰。

微服務型應用程式不應該嘗試自行儲存事件或記錄檔的輸出資料流，甚至不應該嘗試管理事件路由至中央位置。 它應該是透明的，意即每個處理序都應該只將自己的事件資料流寫入標準輸出，隨後由其執行所在之執行環境基礎結構收集。 這些事件資料流路由器的範例之一是 [Microsoft.Diagnostic.EventFlow](https://github.com/Azure/diagnostics-eventflow)，它會收集多個來源的事件資料流，並將它發佈至輸出系統。 這些包括開發環境或雲端系統的簡單標準輸出，例如 [Azure 監視器](https://azure.microsoft.com/services/monitor//)和 [Azure 診斷](/azure/azure-monitor/platform/diagnostics-extension-overview)。 也有良好的協力廠商記錄分析平台和工具，可以搜尋、警示、報告以及監視記錄，甚至是即時的，例如 [Splunk](https://www.splunk.com/goto/Splunk_Log_Management?ac=ga_usa_log_analysis_phrase_Mar17&_kk=logs%20analysis&gclid=CNzkzIrex9MCFYGHfgodW5YOtA)。

### <a name="orchestrators-managing-health-and-diagnostics-information"></a>協調器管理健康狀態和診斷資訊

當您建立微服務型應用程式時，您需要處理複雜性。 當然，單一的微服務很好處理，但是數十或數百種和成千上萬的微服務執行個體就是很複雜的問題。 這不僅是建置您的微服務架構而已，如果您想要擁有穩定且一致的系統，您還需要高可用性、可定址性、復原力、健康狀態及診斷。

![提供微服務支援平臺的群集圖表。](./media/resilient-high-availability-microservices/microservice-platform.png)

**圖 4-22**。 微服務平台是應用程式健康狀態管理的基礎

圖 4-22 顯示的複雜問題，您很難自行解決。 開發小組應該專注於解決商務問題以及使用微服務型方法建置自訂的應用程式。 他們不應該專注於解決複雜的基礎結構問題，如果他們專注於此，則所有微服務型應用程式的成本就會很龐大。 因此有稱為協調器或微服務叢集的微服務導向平台，會嘗試解決建置與執行服務以及有效率使用基礎結構資源的難題。 這會減少使用微服務方法來建置應用程式的複雜性。

不同的協調器可能看似雷同，但它們提供的診斷和健康狀態檢查在功能和到期日各不相同，有時會隨作業系統平台而異，如下節所述。

## <a name="additional-resources"></a>其他資源

- **十二因數的 App.config。記錄檔：將記錄視為事件資料流程** \
  <https://12factor.net/logs>

- **Microsoft 診斷 EventFlow 程式庫** GitHub 存放庫 \
  <https://github.com/Azure/diagnostics-eventflow>

- **什麼是 Azure 診斷** \
  <https://docs.microsoft.com/azure/azure-diagnostics>

- **將 Windows 電腦連線到 Azure 監視器服務** \
  <https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows>

- **記錄您的意義：使用語義記錄應用程式區塊** \
  <https://docs.microsoft.com/previous-versions/msp-n-p/dn440729(v=pandp.60)>

- **Splunk** 官方網站。 \
  <https://www.splunk.com/>

- Windows 事件追蹤 (ETW) **EventSource Class** API
  [https://docs.microsoft.com/dotnet/api/system.diagnostics.tracing.eventsource](xref:System.Diagnostics.Tracing.EventSource)

>[!div class="step-by-step"]
>[上一個](microservice-based-composite-ui-shape-layout.md) 
>[下一步](scalable-available-multi-container-microservice-applications.md)
