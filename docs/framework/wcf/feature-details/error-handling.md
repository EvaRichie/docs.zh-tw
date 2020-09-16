---
title: 錯誤處理
ms.date: 03/30/2017
ms.assetid: c948841a-7db9-40ae-9b78-587d216cbcaf
ms.openlocfilehash: 9c7d6814a6bf1189fd85de5eb440ec4a6840447e
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90539979"
---
# <a name="error-handling-in-windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF) 中的錯誤處理

當服務發生未預期的例外狀況或錯誤時，有幾種方式可設計例外狀況處理方案。 雖然沒有單一「正確」或「最佳做法」錯誤處理解決方案，但有多個有效的路徑可供考慮。 一般來說，建議您根據 WCF 的複雜度、例外狀況的類型和頻率、處理的和未處理的例外狀況本質，以及任何相關的追蹤、記錄或原則需求，來實行混合式解決方案，以結合下列清單中的多種方法。

這些方案在本節的其他部分會做更深入的說明。

## <a name="the-microsoft-enterprise-library"></a>Microsoft 企業程式庫

Microsoft 企業程式庫例外狀況處理應用程式區塊協助實作常見的設計模式，並建立一致策略以處理企業應用程式的所有架構圖層中發生的例外狀況。 其設計目的為支援包含在應用程式元件之 catch 陳述式的典型程式碼。 並非在同一應用程式的相同 catch 區塊重複此程式碼 (例如記錄例外狀況資訊的程式碼)，例外狀況處理應用程式區塊可讓開發人員封裝這個邏輯，做為可重複使用的例外狀況處理常式。

這個程式庫包含隨附的錯誤合約例外狀況處理常式。 這個例外狀況處理常式的設計目的是要在 WCF 服務界限使用，並從例外狀況產生新的錯誤合約。

應用程式區塊的目標是納入常用的最佳做法，並在您的應用程式中提供處理例外狀況的常見方法。 另一方面，自訂錯誤處理常式和自行開發錯誤合約也非常有用。 例如，自訂錯誤處理常式提供一個好機會，可自動升級所有 FaultExceptions 的例外狀況，同時將記錄功能加入至您的應用程式。

如需詳細資訊，請參閱 [Microsoft Enterprise Library](/previous-versions/msp-n-p/ff632023(v=pandp.10))。

## <a name="dealing-with-expected-exceptions"></a>處理預期的例外狀況

適當的動作就是在每個作業或相關的擴充點中攔截預期的例外狀況，決定是否可以從復原，並在 FaultException 中傳回適當的自訂錯誤 \<T> 。
  
## <a name="dealing-with-unexpected-exceptions-using-an-ierrorhandler"></a>使用 IErrorHandler 處理未預期的例外狀況

若要處理未預期的例外狀況，建議的作法是將 IErrorHandler 「掛上」。 錯誤處理常式只會攔截 WCF 執行時間層級的例外狀況 (「服務模型」層) ，而不是在通道層。 在通道層級攔截 IErrorHandler 的唯一方式是建立自訂通道，在大部分的情況下不建議使用。

「未預期的例外狀況」通常不是無法復原的例外狀況，也不是處理例外狀況;它會改為非預期的使用者例外狀況。 無法復原的例外狀況 (例如記憶體不足的例外狀況) –通常由 [服務模型例外狀況處理常式](xref:System.ServiceModel.Dispatcher.ExceptionHandler) 所處理的例外狀況，通常無法正常處理，也不能正常處理這類例外狀況的唯一原因可能是要進行額外的記錄，或將標準例外狀況傳回給用戶端。 處理中的例外狀況發生於訊息的處理過程中 - 例如序列化、編碼器或格式器層級 - 通常無法在 IErrorHandler 處理，因為對錯誤處理常式而言，這些例外狀況發生的時間通常太早或太晚，使其無法介入。 同樣地，也無法在 IErrorHandler 處理傳輸例外狀況。

當例外狀況擲回時，您可使用 IErrorHandler 明確控制應用程式的行為。 您可以：  

1. 決定是否要將錯誤傳送給用戶端。

2. 將例外狀況取代為錯誤。

3. 將錯誤取代為另一個錯誤。

4. 執行記錄或追蹤。

5. 執行其他自訂活動。

針對您的服務將錯誤處理常式加入通道發送器的 ErrorHandlers 屬性，即可安裝自訂錯誤處理常式。  錯誤處理常式可能不只一個，會依照它們加入集合的順序呼叫它們。

IErrorHandler.ProvideFault 可控制傳送至用戶端的錯誤訊息。 不論服務中的作業擲回何種例外狀況類型，都會呼叫這個方法。 如果未在此執行任何作業，WCF 會假設其預設行為，並如同沒有任何自訂錯誤處理常式一樣繼續進行。

您可能使用此方法的情況如下，當您想在例外狀況傳送給用戶端前，建立一個集中位置以將例外狀況轉換為錯誤時 (確保不會處理執行個體，且不會將通道移至錯誤狀態)。

IErrorHandler. HandleError 方法通常用來執行錯誤相關行為，例如錯誤記錄、系統通知、關閉應用程式等。IErrorHandler 可在服務內的多個位置呼叫，而視擲回錯誤的位置而定，HandleError 方法可能會或可能不會被與作業相同的執行緒呼叫;這一點不會有任何保證。

## <a name="dealing-with-exceptions-outside-wcf"></a>處理 WCF 以外的例外狀況

通常，組態例外狀況、資料庫連接字串例外狀況以及其他類似的例外狀況，都可能發生在 WCF 應用程式的內容中，但其本身並不是由服務模型或 Web 服務自己所造成的例外狀況。 這些例外狀況是 web 服務外部的「一般」例外狀況，而且應如同環境中的其他外部例外狀況處理一樣處理。

## <a name="tracing-exceptions"></a>追蹤例外狀況

追蹤是唯一可能會看到所有例外狀況的「全部攔截」位置。 如需追蹤和記錄例外狀況的詳細資訊，請參閱追蹤和記錄。

## <a name="uri-template-errors-when-using-webgetattribute-and-webinvokeattribute"></a>使用 WebGetAttribute 和 WebInvokeAttribute 時，URI 範本發生錯誤。

WebGet 和 WebInvoke 屬性允許您指定 URI 範本，此範本可將要求位址的元件對應至作業參數。 例如，URI 範本 "weather/{state}/{city}" 將要求位址對應到常值語彙基元、參數具名國家/地區和參數具名城市。 接著這些參數可能依名稱繫結至一些作業的型式參數。

當類型合約的型式參數可能為非字串類型時，範本參數在 URI 中會以字串形式出現。 因此需要在作業可叫用之前進行轉換。 [轉換格式的資料表](wcf-web-http-programming-model-overview.md)可供使用。

不過，如果轉換失敗，則無法讓作業知道錯誤已發生。 類型轉換改以分派失敗的形式呈現。

如同許多其他類型的分派失敗一般，透過安裝錯誤處理常式也可以檢查類型轉換分派失敗。 呼叫 IErrorHandler 擴充點，以處理服務層級例外狀況。 從此處，也可以選擇要送回呼叫端的回應 - 同時也執行任何自訂的工作和報告。

## <a name="see-also"></a>另請參閱

- [基本 WCF 程式設計](../basic-wcf-programming.md)
