---
title: Web 和通訊端權限
description: 瞭解 WebPermission 和 SocketPermission 類別如何提供使用 .NET Framework 中的 System.Net 命名空間的網際網路安全性。
ms.date: 03/30/2017
helpviewer_keywords:
- Networking
- positions [.NET Framework], accepting
- sockets, permissions
- network, permissions
- Internet, permissions
- Network Resources
- SocketPermission class, about SocketPermission class
- positions [.NET Framework], connecting
- WebPermission class, about WebPermission class
- permissions [.NET Framework], sockets
- security [.NET Framework], Internet
- positions [.NET Framework], granting
ms.assetid: d51ad8cb-03ae-4a51-bfcd-cfcf6b98afa9
ms.openlocfilehash: b940e6deb98686051847728da6fa5e20debc0f11
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276603"
---
# <a name="web-and-socket-permissions"></a>Web 和通訊端權限

使用 <xref:System.Net> 命名空間之應用程式的網際網路安全性是透過 <xref:System.Net.WebPermission> 和 <xref:System.Net.SocketPermission> 類別提供。 **WebPermission** 類別可控制應用程式向 URI 要求資料，或提供 URI 給網際網路的權限。 **SocketPermission** 類別則可控制應用程式根據通訊端的主機、連接埠編號和傳輸通訊協定，使用 <xref:System.Net.Sockets.Socket> 在本機連接埠上接受資料，或使用另一個位址上的傳輸通訊協定連絡遠端裝置的權限。  
  
 使用的權限類別取決於您的應用程式類型。 使用 <xref:System.Net.WebRequest> 和其子系的應用程式應使用 **WebPermission** 類別來管理權限。 使用通訊端層級存取的應用程式應使用 **SocketPermission** 類別來管理權限。  
  
 **WebPermission** 和 **SocketPermission** 定義兩個權限：接受和連線。 接受可授與應用程式回應來自另一方之連入連線的權限。 連線可授與應用程式起始與另一方之連線的權限。  
  
 若是 **SocketPermission** 執行個體，接受表示應用程式可以在本機傳輸位址上接受連入連線；連線表示應用程式可以連線到某個遠端 (或本機) 傳輸位址。  
  
 若是 **WebPermission** 執行個體，接受表示應用程式可以將 **WebPermission** 所控制的 URI 匯出到全世界；連線表示應用程式可以存取該 URI (不論它是遠端或本機)。  
  
## <a name="see-also"></a>另請參閱

- [安全性](../../standard/security/index.md)
- [網路程式設計的安全性](security-in-network-programming.md)
