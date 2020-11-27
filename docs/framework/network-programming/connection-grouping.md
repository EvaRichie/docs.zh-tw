---
title: 連接群組
ms.date: 03/30/2017
helpviewer_keywords:
- Internet, connections
- connections [.NET Framework], grouping
- WebRequest class, connection grouping
- network resources, connections
- connection pooling
ms.assetid: 2ec502e8-4ba0-4c22-9410-f28eaf4eee63
ms.openlocfilehash: 8bd4412a4c13dd490fce3118f59b5bb1f0d3ea85
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250563"
---
# <a name="connection-grouping"></a>連接群組

連線群組會建立與單一應用程式內所定義連接集區之特定要求的關聯。 連線至代表使用者的後端伺服器並使用支援委派的驗證通訊協定 (例如 Kerberos) 的中介層應用程式，或者提供其專屬認證的中介層應用程式，可能需要這項作業，如下列範例所示。 例如，假設使用者 Joe 瀏覽內部網站，以顯示其薪資資訊。 驗證 Joe 之後，中介層應用程式伺服器會使用 Joe 的認證來連線至後端伺服器，以擷取其薪資資訊。 接下來，Susan 會瀏覽網站，並要求其薪資資訊。 因為中介層應用程式已經使用 Joe 的認證進行連線，所以後端伺服器會回應 Joe 的資訊。 不過，如果應用程式將傳送至後端伺服器的每個要求指派給使用者名稱所組成的連線群組，則每位使用者都屬於不同的連接集區，因此不會意外與其他使用者共用驗證資訊。  
  
 若要將要求指派給特定連線群組，您必須先將名稱指派給 <xref:System.Net.WebRequest> 的 <xref:System.Net.WebRequest.ConnectionGroupName%2A> 屬性，再提出要求。  
  
## <a name="see-also"></a>另請參閱

- [管理連接](managing-connections.md)
- [作法：將使用者資訊指派給群組連線](how-to-assign-user-information-to-group-connections.md)
