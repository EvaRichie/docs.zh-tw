---
title: 作法：使用通道處理站以非同步方式呼叫作業
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cc17dd47-b9ad-451c-a362-e36e0aac7ba0
ms.openlocfilehash: c288df6059cfe1cd1f4ff35cebffafd3fddb38d1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96257531"
---
# <a name="how-to-call-operations-asynchronously-using-a-channel-factory"></a>作法：使用通道處理站以非同步方式呼叫作業

本主題涵蓋用戶端如何能夠在使用 <xref:System.ServiceModel.ChannelFactory%601> 架構的用戶端應用程式時，非同步地存取服務作業  (當使用 <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType> 物件來叫用服務時，您可以使用事件驅動的非同步呼叫模型。 如需詳細資訊，請參閱 [如何：以非同步方式呼叫服務作業](how-to-call-wcf-service-operations-asynchronously.md)。 如需事件架構非同步呼叫模型的詳細資訊，請參閱以 [事件為基礎的非同步模式 (EAP) ](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)。 )   
  
 本主題中的服務會實作 `ICalculator` 介面。 用戶端可透過非同步的方式來呼叫在此介面上的作業，這表示類似 `Add` 的作業會分割為兩個方法，`BeginAdd` 和 `EndAdd`，其中前者會啟始呼叫，後者則會在作業完成時擷取結果。 如需示範如何在服務中以非同步方式執行作業的範例，請參閱 [如何：執行非同步服務](../how-to-implement-an-asynchronous-service-operation.md)作業。 如需同步和非同步作業的詳細資訊，請參閱 [同步和非同步作業](../synchronous-and-asynchronous-operations.md)。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-call-wcf-service-operations-asynchronously"></a>若要以非同步方式呼叫 WCF 服務作業  
  
1. 使用如下列命令所示的選項， [ ( # A0) 工具來執行 [System.servicemodel 中繼資料公用程式] 工具 ](../servicemodel-metadata-utility-tool-svcutil-exe.md) `/async` 。  
  
    ```console
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a  
    ```  
  
     這會針對作業的服務合約產生非同步用戶端版本。  
  
2. 建立要在非同步作業完成時呼叫的回呼函式 (Callback Function)，如下列範例程式碼所示。  
  
     [!code-csharp[C_How_To_CF_Async#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#2)]
     [!code-vb[C_How_To_CF_Async#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#2)]  
  
3. 若要以非同步方式來存取服務作業，請建立用戶端和呼叫 `Begin[Operation]` (例如，`BeginAdd`)，並指定回呼函式，如下列範例程式碼所示。  
  
     [!code-csharp[C_How_To_CF_Async#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#3)]
     [!code-vb[C_How_To_CF_Async#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#3)]  
  
     當此回呼函式執行時，用戶端便會呼叫 `End<operation>` (例如，`EndAdd`) 以擷取結果。  
  
## <a name="example"></a>範例  

 在用於上述程序中之用戶端程式碼所使用的服務會實作 `ICalculator` 介面，如下列程式碼所示。 在服務端，合約的 `Add` 和 `Subtract` 作業會由 WINDOWS COMMUNICATION FOUNDATION (WCF) 執行時間同步叫用，即使先前的用戶端步驟是在用戶端上非同步叫用也一樣。 在服務端，會使用 `Multiply` 和 `Divide` 作業來非同步叫用服務，即使用戶端會同步叫用這些服務也是一樣。 這個範例會將 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> 屬性設定為 `true`。 此屬性設定結合了 .NET Framework 非同步模式的執行，可告知執行時間以非同步方式叫用作業。  
  
 [!code-csharp[C_How_To_CF_Async#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/service.cs#4)]
 [!code-vb[C_How_To_CF_Async#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/service.vb#4)]  
