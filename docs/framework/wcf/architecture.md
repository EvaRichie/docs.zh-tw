---
title: Windows Communication Foundation 架構
description: 瞭解 Windows Communication Foundation 架構的主要層級，包括合約、服務執行時間、訊息和啟用 & 裝載。
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], architecture
- WCF [WCF], architecture
- architecture [WCF]
ms.assetid: a3bcb0a1-56ea-4ba6-9736-d260d90dade5
ms.openlocfilehash: 7cb03ddd7207fbea23577ff18e984e90779333bc
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294881"
---
# <a name="windows-communication-foundation-architecture"></a>Windows Communication Foundation 架構

下圖說明 Windows Communication Foundation (WCF) 架構的主要層級。  
  
## <a name="wcf-architecture"></a>WCF 架構  

 ![WCF 架構](./media/wcf-architecture.gif "WCF_Architecture")  
  
### <a name="contracts-and-descriptions"></a>合約和描述  

 合約會定義訊息系統的各方面。 資料合約會描述服務所能建立或使用之每個訊息在構成時所使用的每個參數。 這些訊息參數是由 XML 結構描述定義語言 (XSD) 文件所定義，因此可使任何瞭解 XML 的系統都能處理這些文件。 訊息合約會使用 SOAP 通訊協定來定義特定訊息部分，並允許在互通性 (Interoperability) 要求時對訊息的部分進行更精細的控制。 服務合約會指定服務的實際方法簽章，而且會透過一種支援的程式語言 (例如 Visual Basic 或 Visual C#) 來散發為介面。  
  
 原則和繫結會規定與服務進行通訊時的必要條件。  例如，繫結必須 (至少需要) 指定使用的傳輸 (例如，HTTP 或 TCP)，以及編碼方式。 原則包含在與服務通訊時必須符合的安全性需求和其他條件。  
  
### <a name="service-runtime"></a>服務執行階段  

 服務執行階段層包含只會在服務之實際作業期間發生的行為，也就是服務的執行階段行為。 節流設定會控制要處理多少訊息，而隨著對服務的要求擴大到預設限制，這個數量可能會有所不同。 錯誤行為會指定在服務發生內部錯誤時所要發生的動作，例如，控制有哪些資訊要傳送到用戶端   (的資訊太多，可能會讓惡意使用者有機會發動攻擊。 ) 中繼資料行為會控制外部的中繼資料是否可供外界使用。 執行個體 (Instance) 行為會指定可以執行服務之執行個體的數目 (例如，「單一」就是指定僅能使用一個執行個體來處理所有訊息)。 異動行為可使異動的作業在發生失敗時進行復原。 分派行為是由 WCF 基礎結構處理訊息的方式控制。  
  
 擴充性可使執行階段處理序進行自訂。 例如，訊息檢查是檢查訊息之部分的功能，而啟用參數篩選功能時，便會根據作用於訊息標頭的篩選來發生預設動作。  
  
### <a name="messaging"></a>訊息傳送  

 訊息層是由 *通道* 所組成。 通道是指能以某種方式 (例如，藉由驗證訊息) 處理訊息的元件。 一組通道也稱為 *通道堆疊*。 通道會在訊息和訊息標頭上運作。 這點不同於服務執行階段層，其主要著重於關於處理訊息本文的執行。  
  
 通道類型有兩種：傳輸通道和通訊協定通道。  
  
 傳輸通道會從網路讀取和寫入訊息 (或是與外界連接的一些其他通訊點)。 有些傳輸會使用編碼器在訊息 (表示為 XML Infoset) 和網路所使用的位元組資料流表示之間來回轉換。 這類傳輸的範例包括 HTTP、具名管道 (Named Pipe)、TCP 及 MSMQ。 這類編碼的範例包括 XML 和最佳化的二進位編碼。  
  
 通訊協定通道會實作訊息處理通訊協定，而此通常是藉由讀取或寫入訊息的額外標頭來完成。 這類通訊協定的範例包括 WS-Security 和 WS-Reliability。  
  
 訊息層說明資料的可能格式與交換模式。 WS-Security 是 WS-Security 規格的實作 (Implementation)，此規格會啟用訊息層的安全性。 WS-Reliable 訊息通道可保證訊息的傳遞。 編碼器會提供可以用來滿足訊息需要的各種編碼方式。 HTTP 通道會指定對訊息傳遞使用超文字傳輸協定 (Hypertext Transfer Protocol，HTTP)。 同樣地，TCP 通道會指定 TCP 通訊協定。 交易流程通道會管理交易的訊息模式。 具名管道通道會啟用處理序間通訊。 MSMQ 通道會啟用與 MSMQ 應用程式的互通。  
  
### <a name="hosting-and-activation"></a>裝載和啟動  

 服務的最終形式就是程式。 就像其他的程式，服務必須在可執行檔中執行。 這就是所謂的 *自我* 裝載服務。  
  
 服務也可以裝載在外部代理程式所管理的可執行檔 *中，或執行，例如* IIS 或 Windows 啟用服務 () 。 WAS 可讓 WCF 應用程式在部署于執行 WAS 的電腦時自動啟動。 服務也可以透過手動方式來當做可執行檔 (.exe 檔) 執行。 服務也可以自動當做 Windows 服務執行。 COM + 元件也可以主控為 WCF 服務。  
  
## <a name="see-also"></a>另請參閱

- [何謂 Windows Communication Foundation](whats-wcf.md)
- [Windows Communication Foundation 的主要概念](fundamental-concepts.md)
