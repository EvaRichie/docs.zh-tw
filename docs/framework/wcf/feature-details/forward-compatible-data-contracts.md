---
title: 向前相容資料合約
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], forward compatibility
ms.assetid: 413c9044-26f8-4ecb-968c-18495ea52cd9
ms.openlocfilehash: 34bde56b78ec0148cf6b924f8edd29343b97faa4
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597380"
---
# <a name="forward-compatible-data-contracts"></a>向前相容資料合約
Windows Communication Foundation （WCF）資料合約系統的一項功能，就是合約可以在一段時間內以不中斷的方式進化。 也就是說，有舊版資料合約的用戶端可以與有新版相同資料合約的服務通訊，或是有新版資料合約的用戶端可以與有舊版相同資料合約通訊。 如需詳細資訊，請參閱[最佳做法：資料合約版本控制](../best-practices-data-contract-versioning.md)。  
  
 建立新版的現有資料合約時，您可以根據需要套用大部分的版本控制功能。 不過，必須在第一版的型別內建一個版本設定*功能，才能*正常運作。  
  
## <a name="round-tripping"></a>往返  
 當資料從新版本傳遞到舊版本，然後回到新版本的資料合約時，即代表發生往返。 使用往返時，任何資料保證都不會遺失。 如果啟用往返，就會使類型向前相容於資料合約版本控制模型所支援的任何未來變更。  
  
 若要啟用特定類型的往返，類型必須實作 <xref:System.Runtime.Serialization.IExtensibleDataObject> 介面， 這個介面則包含屬性 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> (傳回 <xref:System.Runtime.Serialization.ExtensionDataObject> 型別)。 該屬性會儲存來自目前版本未知的資料合約未來版本的任何資料。  
  
### <a name="example"></a>範例  
 下列資料合約未向前相容於未來變更。  
  
 [!code-csharp[C_DataContract#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#7)]
 [!code-vb[C_DataContract#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#7)]  
  
 若要使類型向前相容於未來變更 (例如新增名為 "phoneNumber" 的新資料成員)，請實作 <xref:System.Runtime.Serialization.IExtensibleDataObject> 介面。  
  
 [!code-csharp[C_DataContract#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#8)]
 [!code-vb[C_DataContract#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#8)]  
  
 當 WCF 基礎結構遇到不屬於原始資料合約的資料時，資料會儲存在屬性中並加以保留。 這個資料只會以暫時儲存的方式處理。 如果物件傳回到其產生位置，原始 (未知的) 資料也會傳回。 因此，這代表資料往返於原始端點之間，而且沒有遺失。 不過請注意，如果產生物件的端點要求處理資料，上述情況便不成立，端點也就必須偵測與配合變更。  
  
 <xref:System.Runtime.Serialization.ExtensionDataObject> 型別不包含公用方法或屬性， 因此無法直接存取儲存在 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 屬性中的資料。  
  
 在 `ignoreExtensionDataObject` 建構函式中將 `true` 設定為 <xref:System.Runtime.Serialization.DataContractSerializer> 或針對 <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> 將 `true` 屬性設定為 <xref:System.ServiceModel.ServiceBehaviorAttribute>，即可關閉往返功能。 此功能關閉時，還原序列化程式將不會填入 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 屬性，而且序列化程式將不會發出屬性內容。  
  
## <a name="see-also"></a>請參閱

- <xref:System.Runtime.Serialization.IExtensibleDataObject>
- <xref:System.Runtime.Serialization.ExtensionDataObject>
- [資料合約版本控制](data-contract-versioning.md)
- [最佳做法：資料合約版本控制](../best-practices-data-contract-versioning.md)
