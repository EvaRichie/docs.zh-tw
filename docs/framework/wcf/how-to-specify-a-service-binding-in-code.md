---
title: 作法：在程式碼中指定服務繫結
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 67ab5dd8-79c1-4e62-aa75-828ea918a53a
ms.openlocfilehash: 7cf54754661182dca1e91c75b158d9b0a34a1f5e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236477"
---
# <a name="how-to-specify-a-service-binding-in-code"></a>作法：在程式碼中指定服務繫結

在此範例中，已為計算機服務定義了 `ICalculator` 合約、在 `CalculatorService` 類別中實作了服務，並於程式碼中定義其端點，同時指定服務必須使用 <xref:System.ServiceModel.BasicHttpBinding> 類別。  
  
 通常最佳作法是在組態中以宣告方式指定繫結和位址資訊，而不是在程式碼中強制指定。 在程式碼中定義端點通常不太實用，因為部署之服務的繫結和位址通常與開發服務時所使用的繫結和位址不同。 比較一般性的作法是將繫結和位址資訊留在程式碼外面，如此一來，不需要重新編譯或重新部署應用程式，就可以變更繫結和位址資訊。  
  
 如需如何使用設定元素而非程式碼來設定此服務的說明，請參閱 [如何：在設定中指定服務](how-to-specify-a-service-binding-in-configuration.md)系結。  
  
### <a name="to-specify-in-code-to-use-the-basichttpbinding-for-the-service"></a>若要在程式碼中指定使用服務的 BasicHttpBinding  
  
1. 定義服務類型的服務合約。  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2. 在服務類別中實作服務合約。  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3. 在裝載的應用程式中，建立服務起始位址以及要與服務一起搭配使用的繫結。  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4. 建立服務的主機、新增端點，然後開啟主機。  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#4)]
     [!code-vb[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#4)]  
  
### <a name="to-modify-the-default-values-of-the-binding-properties"></a>若要修改繫結屬性的預設值  
  
1. 若要修改 <xref:System.ServiceModel.BasicHttpBinding> 類別的一個預設屬性值，請在建立主機之前，先將繫結上的屬性值設為新值。 例如，若要將預設的開啟與關閉逾時值由 1 分鐘改為 2 分鐘，請使用下列值。  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#5)]
     [!code-vb[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#5)]  
  
## <a name="see-also"></a>另請參閱

- [使用繫結來設定服務和用戶端](using-bindings-to-configure-services-and-clients.md)
- [指定端點位址](specifying-an-endpoint-address.md)
