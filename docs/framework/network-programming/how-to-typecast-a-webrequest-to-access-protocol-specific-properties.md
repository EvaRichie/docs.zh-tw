---
title: 作法：轉換 WebRequest 類型以存取通訊協定特定屬性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d9a8eae2-7454-46f9-b43b-c98477c5bcde
ms.openlocfilehash: 09bd551dad77358b1503871c6ee100a869adf75b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253423"
---
# <a name="how-to-typecast-a-webrequest-to-access-protocol-specific-properties"></a>作法：轉換 WebRequest 類型以存取通訊協定特定屬性

這個範例示範如何轉換 WebRequest 類型以存取通訊協定特定屬性。  
  
## <a name="example"></a>範例  
  
```csharp  
HttpWebRequest httpreq =
   (HttpWebRequest) WebRequest.Create("http://www.contoso.com/");  
```  
  
```vb  
Dim httpreq As HttpWebRequest = _  
   CType(WebRequest.Create("http://www.contoso.com/"), HttpWebRequest)  
```  
  
## <a name="see-also"></a>另請參閱

- [可插式通訊協定程式設計](programming-pluggable-protocols.md)
