---
title: 將 NetTcpBinding 應用程式轉換為對等通道應用程式
ms.date: 03/30/2017
ms.assetid: d4137292-a923-4b8f-8594-42276f2d3ce2
ms.openlocfilehash: 42266d8c7c04e2d8f3f1e4734d9a05181c3f1ea3
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595553"
---
# <a name="converting-a-nettcpbinding-application-to-a-peer-channel-application"></a>將 NetTcpBinding 應用程式轉換為對等通道應用程式
您可以使用描述連接參數的系結，在使用 WinFX 的用戶端之間建立連接。 轉換 .NET Framework 應用程式以使用對等連接時，需要在進行用戶端連線時支援這項技術的系結。 對等通道會提供名稱為 <xref:System.ServiceModel.NetPeerTcpBinding> 的繫結，其使用方法類似於使用 <xref:System.ServiceModel.NetTcpBinding>。 之間的主要差異則包括指定解析程式服務和定義安全性設定。  
  
 如果應用程式使用預設解析程式和安全性設定，轉換正常用戶端/伺服器型應用程式以使用對等通道則牽涉到在應用程式的組態檔中將繫結的名稱從 "NetTcpBinding" 變更為 "NetPeerTcpBinding"，而您並不需要變更應用程式的程式碼基礎。  
  
## <a name="see-also"></a>請參閱

- [建置對等通道應用程式](building-a-peer-channel-application.md)
- [系統提供的繫結](../system-provided-bindings.md)
