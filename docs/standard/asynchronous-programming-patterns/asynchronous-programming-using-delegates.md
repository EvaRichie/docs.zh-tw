---
title: 使用委派非同步設計程式
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- BeginInvoke method
- asynchronous programming, delegates
- asynchronous delegates
- calling synchronous methods in asynchronous manner
- EndInvoke method
- calling asynchronous methods
- delegates [.NET Framework], asynchronous
- synchronous calling in asynchronous manner
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
ms.openlocfilehash: 82e0a57c3d8e180456aed48886e38ca466db16c8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289963"
---
# <a name="asynchronous-programming-using-delegates"></a>使用委派非同步設計程式
委派可讓您以非同步方式呼叫同步方法。 當您同步呼叫委派時，`Invoke` 方法會在目前的執行緒上直接呼叫目標方法。 如果呼叫 `BeginInvoke` 方法，通用語言執行平台 (CLR) 會將要求排入佇列，並立即返回呼叫端。 在執行緒集區中的執行緒上會非同步呼叫目標方法。 送出要求的原始執行緒不被佔用，可以繼續與目標方法平行執行。 如果已在 `BeginInvoke` 方法呼叫中指定回撥方法，目標方法結束時會呼叫回撥方法。 在回撥方法中，`EndInvoke` 方法會取得傳回值和任何輸入/輸出或僅輸出參數。 如果呼叫 `BeginInvoke` 時未指定回撥方法，則可以從呼叫 `BeginInvoke` 的執行緒呼叫 `EndInvoke`。  
  
> [!IMPORTANT]
> 編譯器應該利用由使用者指定的委派簽章，使用 `Invoke`、`BeginInvoke` 和 `EndInvoke` 方法發出委派類別。 `BeginInvoke` 和 `EndInvoke` 方法應該裝飾為原生。 因為這些方法標示為原生，CLR 會在類別載入時自動提供實作。 載入器可確保不覆寫它們。  
  
## <a name="in-this-section"></a>本節內容  
 [以非同步的方式呼叫同步方法](calling-synchronous-methods-asynchronously.md) \(部分機器翻譯\)  
 討論使用委派對一般方法進行非同步呼叫，並提供簡單的程式碼範例，示範等待非同步呼叫返回的四種方式。  
  
## <a name="related-sections"></a>相關章節  
 [事件架構非同步模式 (EAP)](event-based-asynchronous-pattern-eap.md)  
 描述使用 .NET Framework 進行非同步程式設計。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Delegate>
