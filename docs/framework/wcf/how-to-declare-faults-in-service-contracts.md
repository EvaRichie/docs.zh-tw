---
title: 作法：在服務合約中宣告錯誤
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e8da98e7-d22f-4f60-ac82-3fb0928a353f
ms.openlocfilehash: 06262d5f698f8898e162e92dad272a7188897af0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96240052"
---
# <a name="how-to-declare-faults-in-service-contracts"></a>作法：在服務合約中宣告錯誤

在 Managed 程式碼中，發生錯誤狀況時會擲回例外狀況。 不過，在 Windows Communication Foundation (WCF) 應用程式中，服務合約會在服務合約中宣告 SOAP 錯誤，以指定傳回給用戶端的錯誤資訊。 如需例外狀況和錯誤之間關聯性的總覽，請參閱 [指定和處理合約和服務中的錯誤](specifying-and-handling-faults-in-contracts-and-services.md)。

## <a name="create-a-service-contract-that-specifies-a-soap-fault"></a>建立會指定 SOAP 錯誤的服務合約

1. 建立其中至少包含一個作業的服務合約。 如需範例，請參閱 [如何：定義服務合約](how-to-define-a-wcf-service-contract.md)。

2. 選取作業，這個作業會指定用戶端預期會收到通知的錯誤狀況。 若要決定哪些錯誤狀況證明將 SOAP 錯誤傳回給用戶端，請參閱 [在合約和服務中指定和處理錯誤](specifying-and-handling-faults-in-contracts-and-services.md)。

3. 將 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> 套用至選取的作業，並將可序列化的錯誤類型傳遞至建構函式。 如需建立和使用可序列化類型的詳細資訊，請參閱 [指定服務合約中的資料傳輸](./feature-details/specifying-data-transfer-in-service-contracts.md)。 下列範例將示範如何指定會在 `SampleMethod` 中產生 `GreetingFault` 作業。

     [!code-csharp[FaultContractAttribute#4](~/samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#4)]
     [!code-vb[FaultContractAttribute#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#4)]

4. 對合約中會與用戶端溝通錯誤狀況的所有作業，重複步驟 2 和 3。

## <a name="implementing-an-operation-to-return-a-specified-soap-fault"></a>實作作業以傳回指定的 SOAP 錯誤

 一旦作業已指定可傳回特定 SOAP 錯誤 (如之前的程序所示)，以與呼叫應用程式溝通錯誤狀況，則下一個步驟就是實作該指定項目。

### <a name="throw-the-specified-soap-fault-in-the-operation"></a>在作業中擲回指定的 SOAP 錯誤

1. 在作業中發生 <xref:System.ServiceModel.FaultContractAttribute> 特定的錯誤狀況時，會擲回新的 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>，其中指定的 SOAP 錯誤為型別參數。 下列範例會示範如何在之前程序中顯示的 `GreetingFault` 中擲回 `SampleMethod`，以及如何在下列「程式碼」區段中擲回。

     [!code-csharp[FaultContractAttribute#5](~/samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#5)]
     [!code-vb[FaultContractAttribute#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#5)]

## <a name="example"></a>範例

下列程式碼範例會顯示對 `GreetingFault` 作業指定 `SampleMethod` 的單一作業實作。

[!code-csharp[FaultContractAttribute#1](~/samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#1)]
[!code-vb[FaultContractAttribute#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#1)]

## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
