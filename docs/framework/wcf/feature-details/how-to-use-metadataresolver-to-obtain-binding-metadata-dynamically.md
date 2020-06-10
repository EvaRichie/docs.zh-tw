---
title: HOW TO：使用 MetadataResolver 來動態取得繫結中繼資料
ms.date: 03/30/2017
ms.assetid: 56ffcb99-fff0-4479-aca0-e3909009f605
ms.openlocfilehash: 98fe4977f270b008c51039af19261ca86b8d6642
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601123"
---
# <a name="how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically"></a>HOW TO：使用 MetadataResolver 來動態取得繫結中繼資料
本主題示範如何使用 <xref:System.ServiceModel.Description.MetadataResolver> 類別來動態取得繫結中繼資料。  
  
### <a name="to-dynamically-obtain-binding-metadata"></a>若要動態取得繫結中繼資料  
  
1. 建立具有中繼資料端點位址的 <xref:System.ServiceModel.EndpointAddress> 物件。  
  
    ```csharp
    EndpointAddress metaAddress  
      = new EndpointAddress(new Uri("http://localhost:8080/SampleService/mex"));  
    ```  
  
2. 呼叫 <xref:System.ServiceModel.Description.MetadataResolver.Resolve%28System.Type%2CSystem.ServiceModel.EndpointAddress%29>，它會傳入服務類型和中繼資料端點位址。 這麼做會傳回實作指定之合約的端點集合。 只有繫結資訊會從中繼資料匯出，不會匯出合約資訊。 並改用所提供的合約。  
  
    ```csharp  
    ServiceEndpointCollection endpoints = MetadataResolver.Resolve(typeof(SampleServiceClient),metaAddress);  
    ```  
  
3. 您接著便可以逐一查看服務端點的集合，以擷取所需的繫結資訊。 下列程式碼會逐一查看端點、建立服務用戶端物件 (此物件會傳入與目前端點關聯的繫結和位址)，然後再呼叫服務上的方法。  
  
    ```csharp  
    foreach (ServiceEndpoint point in endpoints)  
    {  
       if (point != null)  
       {  
          // Create a new wcfClient using retrieved endpoints.  
          using (wcfClient = new SampleServiceClient(point.Binding, point.Address))  
          {  
             Console.WriteLine(  
               wcfClient.SampleMethod("Client used the "  
               + point.Address.ToString() + " address."));  
          }  
      }  
    }  
    ```  
  
## <a name="see-also"></a>請參閱

- [中繼資料](metadata.md)
