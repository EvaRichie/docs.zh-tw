---
title: 定義並指定錯誤
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling faults [WCF], specifying
- handling faults [WCF], defining
ms.assetid: c00c84f1-962d-46a7-b07f-ebc4f80fbfc1
ms.openlocfilehash: 67096c4531d13bc66f584c09c458c0a5a2a41c6b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96260899"
---
# <a name="defining-and-specifying-faults"></a>定義並指定錯誤

SOAP 錯誤會將錯誤狀況資訊從服務傳送到用戶端，而在雙工案例中，則是以互通的方式從用戶端傳送到服務。 本主題討論何時及如何定義自訂錯誤內容，並指定可以傳回它們的作業。 如需有關服務或雙工用戶端如何傳送這些錯誤，以及用戶端或服務應用程式如何處理這些錯誤的詳細資訊，請參閱傳送 [和接收錯誤](sending-and-receiving-faults.md)。 如需 Windows Communication Foundation (WCF) 應用程式中的錯誤處理總覽，請參閱 [指定和處理合約和服務中](specifying-and-handling-faults-in-contracts-and-services.md)的錯誤。  
  
## <a name="overview"></a>概觀  

 已宣告的 SOAP 錯誤是其中作業具有指定自訂 SOAP 錯誤類型之 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>的 SOAP 錯誤。 未宣告的 SOAP 錯誤則是在作業的合約中未指定的 SOAP 錯誤。 本主題將協助您識別這些錯誤狀況，並為您的服務建立錯誤合約，讓用戶端在收到自訂 SOAP 錯誤的通知時，可以用於正確處理這些錯誤狀況。 基本的工作依序為：  
  
1. 定義您服務的用戶端應該知道的錯誤狀況。  
  
2. 定義這些錯誤狀況的 SOAP 錯誤的自訂內容。  
  
3. 標示您的作業，讓其擲回的特定 SOAP 錯誤以 WSDL 格式對用戶端公開。  
  
### <a name="defining-error-conditions-that-clients-should-know-about"></a>定義用戶端應知道的錯誤狀況  

 SOAP 錯誤是公開描述的訊息，具有特定作業的錯誤資訊。 由於它們是和其他作業訊息一起以 WSDL 描述的，因此用戶端知道並預期在叫用作業時處理這類錯誤。 但因為 WCF 服務是以 managed 程式碼撰寫，所以決定要將 managed 程式碼中的哪些錯誤狀況轉換為錯誤，並傳回給用戶端，讓您有機會在您的服務中，將錯誤狀況和 bug 與用戶端的正式錯誤交談分開。  
  
 例如，下列程式碼範例顯示採用兩個整數並傳回另一個整數的作業。 此處可擲回數個例外狀況，因此當設計錯誤合約時，您必須決定哪些錯誤狀況對您的用戶端是重要的。 在此案例中，服務應會偵測到 <xref:System.DivideByZeroException?displayProperty=nameWithType> 例外狀況。  
  
```csharp  
[ServiceContract]  
public class CalculatorService  
{  
    [OperationContract]
    int Divide(int a, int b)  
    {  
      if (b==0) throw new Exception("Division by zero!");  
      return a/b;  
    }  
}  
```  
  
```vb
<ServiceContract> _
Public Class CalculatorService
    <OperationContract> _
    Public Function Divide(a As Integer, b As Integer) As Integer
        If b = 0 Then Throw New DivideByZeroException("Division by zero!")
        Return a / b
    End Function
End Class
```
  
 在前例中，作業可以傳回除以零特定的自訂 SOAP 錯誤、數學作業特定但包含除以零特定的資訊的自訂錯誤、數個不同錯誤情況的多重錯誤或完全沒有 SOAP 錯誤。  
  
### <a name="define-the-content-of-error-conditions"></a>定義錯誤狀況的內容  

 在錯誤狀況被識別為可用於傳回自訂 SOAP 錯誤之後，下一個步驟就是定義該錯誤的內容，並確保可以序列化內容結構。 上節的程式碼範例顯示 `Divide` 作業特定的錯誤，但如果 `Calculator` 服務上有其他的作業，則單一自訂 SOAP 錯誤可以通知用戶端所有的計算機錯誤狀況，包括 `Divide`。 下列程式碼範例顯示自訂 SOAP 錯誤 `MathFault` 的建立，它可以報告使用所有數學作業所造成的錯誤，包括 `Divide`。 雖然此類別可以指定作業 (`Operation` 屬性) 和描述問題的值 (`ProblemType` 屬性)，但是此類別和這些屬性必須是可序列化的，才能傳輸到自訂 SOAP 錯誤中的用戶端。 因此，<xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> 和 <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> 屬性是用於讓類型和其屬性變成可序列化的，並盡量互通。  
  
 [!code-csharp[Faults#2](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#2)]
 [!code-vb[Faults#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#2)]  
  
 如需如何確保資料可序列化的詳細資訊，請參閱 [指定服務合約中的資料傳輸](./feature-details/specifying-data-transfer-in-service-contracts.md)。 如需提供之序列化支援的清單 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> ，請參閱 [資料合約序列化程式支援的類型](./feature-details/types-supported-by-the-data-contract-serializer.md)。  
  
### <a name="mark-operations-to-establish-the-fault-contract"></a>標示作業以建立錯誤合約  

 在定義傳回做為自訂 SOAP 錯誤一部分的可序列化資料之後，最後一個步驟就是將您的作業合約標示為擲回該類型的 SOAP 錯誤。 如果要執行這項操作，請使用 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> 屬性，並傳遞您所建構之自訂資料型別的型別。 下列程式碼範例將示範如何使用 <xref:System.ServiceModel.FaultContractAttribute> 屬性來指定 `Divide` 作業可以傳回型別 `MathFault` 的 SOAP 錯誤。 其他以數學為基礎的作業現在也可以指定它們可以傳回 `MathFault`。  
  
 [!code-csharp[Faults#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#1)]
 [!code-vb[Faults#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#1)]  
  
 作業可以使用一個以上的 <xref:System.ServiceModel.FaultContractAttribute> 屬性來標示該作業，以指定傳回一個以上的自訂錯誤。  
  
 下一步是在您的作業實施中執行錯誤合約，將在傳送 [和接收錯誤](sending-and-receiving-faults.md)的主題中說明。  
  
#### <a name="soap-wsdl-and-interoperability-considerations"></a>SOAP、WSDL 和互通性考量  

 在某些情況中，特別是在與其他平台互通時，控制錯誤在 SOAP 訊息中出現的方式或在 WSDL 中繼資料中描述的方式可能會很重要。  
  
 <xref:System.ServiceModel.FaultContractAttribute> 屬性具有 <xref:System.ServiceModel.FaultContractAttribute.Name%2A> 屬性，可控制為該錯誤在中繼資料中產生的 WSDL 錯誤項目名稱。  
  
 根據 SOAP 標準，錯誤可以有 `Action`、`Code` 和 `Reason`。 `Action` 是由 <xref:System.ServiceModel.FaultContractAttribute.Action%2A> 屬性控制的。 <xref:System.ServiceModel.FaultException.Code%2A> 屬性和 <xref:System.ServiceModel.FaultException.Reason%2A> 屬性都是 <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> 類別的屬性，而該類別是一般 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> 的父類別。 `Code` 屬性包括 <xref:System.ServiceModel.FaultCode.SubCode%2A> 成員。  
  
 當存取產生錯誤的非服務時，會有特定限制。 WCF 僅支援架構所描述且與資料合約相容的詳細類型錯誤。 例如，如先前所述，WCF 不支援在詳細資料類型中使用 XML 屬性的錯誤，或是在詳細資料區段中有一個以上最上層元素的錯誤。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [指定與處理合約和服務中的錯誤](specifying-and-handling-faults-in-contracts-and-services.md)
- [傳送和接收錯誤](sending-and-receiving-faults.md)
- [作法：在服務合約中宣告錯誤](how-to-declare-faults-in-service-contracts.md)
- [了解保護層級](understanding-protection-level.md)
- [作法：設定 ProtectionLevel 屬性](how-to-set-the-protectionlevel-property.md)
- [指定服務合約中的資料傳輸](./feature-details/specifying-data-transfer-in-service-contracts.md)
