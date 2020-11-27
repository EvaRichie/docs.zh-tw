---
title: 作法：建立自訂宣告
description: 瞭解如何在 WCF 中建立自訂宣告。 WCF 支援各種內建宣告，有些應用程式可能需要自訂宣告。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d619976b-eda3-475e-ac23-c7988a2dceb0
ms.openlocfilehash: ea3bc7384ca10538ca5ab1d3bb05da6a2757fb67
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256010"
---
# <a name="how-to-create-a-custom-claim"></a>作法：建立自訂宣告

Windows Communication Foundation (WCF) 中的身分識別模型基礎結構會提供一組內建的宣告類型和許可權，其中包含協助程式函式，可用來建立 <xref:System.IdentityModel.Claims.Claim> 具有這些類型和許可權的實例。 這些內建宣告是設計用來建立 WCF 支援的用戶端認證類型中所找到的資訊模型。 在許多情況下，內建宣告就已足夠；不過有些應用程式可能需要自訂宣告。 宣告中包含了宣告類型、宣告適用的資源，以及擁有該資源所需的權限。 這個主題會描述如何建立自訂宣告。  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-primitive-data-type"></a>依據基本資料型別建立自訂宣告  
  
1. 將宣告類型、資源值和權限傳遞至 <xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> 建構函式，即可建立自訂宣告。  
  
    1. 決定用於宣告類型的唯一值。  
  
         宣告類型為唯一的字串識別碼。 自訂宣告設計者的責任在於確保用於宣告類型的字串識別碼為獨一無二的。 如需 WCF 所定義之宣告類型的清單，請參閱 <xref:System.IdentityModel.Claims.ClaimTypes> 類別。  
  
    2. 選擇基本資料型別和資源的值。  
  
         資源就是物件。 資源的 CLR 類型可以為基本，例如 <xref:System.String> 或 <xref:System.Int32>，或任何可序列化的類型。 資源的 CLR 型別必須是可序列化的，因為宣告是在 WCF 的不同點進行序列化。 基本類型為可序列化。  
  
    3. 選擇由 WCF 定義的許可權，或自訂許可權的唯一值。  
  
         權限為唯一字串識別碼。 由 WCF 定義的許可權定義于 <xref:System.IdentityModel.Claims.Rights> 類別中。  
  
         自訂宣告設計者的責任在於確保用於權限的字串識別碼為獨一無二的。  
  
         下列程式碼範例會使用 `http://example.org/claims/simplecustomclaim` 宣告類型，對名稱為 `Driver's License` 的資源建立自訂宣告，也會使用 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 權限建立自訂宣告。  
  
     [!code-csharp[c_CustomClaim#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#4)]
     [!code-vb[c_CustomClaim#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#4)]  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-non-primitive-data-type"></a>依據非基本資料型別建立自訂宣告  
  
1. 將宣告類型、資源值和權限傳遞至 <xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> 建構函式，即可建立自訂宣告。  
  
    1. 決定用於宣告類型的唯一值。  
  
         宣告類型為唯一的字串識別碼。 自訂宣告設計者的責任在於確保用於宣告類型的字串識別碼為獨一無二的。 如需 WCF 所定義之宣告類型的清單，請參閱 <xref:System.IdentityModel.Claims.ClaimTypes> 類別。  
  
    2. 選擇或定義資源的可序列化非基本類型。  
  
         資源就是物件。 資源的 CLR 型別必須是可序列化的，因為宣告是在 WCF 的不同點進行序列化。 基本類型已為可序列化。  
  
         定義新類型時，請將 <xref:System.Runtime.Serialization.DataContractAttribute> 套用至類別。 也將 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性套用至需要序列化以做為宣告一部分之新類型的所有成員。  
  
         下列程式碼範例會定義名稱為 `MyResourceType` 的自訂資源類型。  
  
         [!code-csharp[c_CustomClaim#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#2)]
         [!code-vb[c_CustomClaim#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#2)]
  
    3. 選擇由 WCF 定義的許可權，或自訂許可權的唯一值。  
  
         權限為唯一字串識別碼。 由 WCF 定義的許可權定義于 <xref:System.IdentityModel.Claims.Rights> 類別中。  
  
         自訂宣告設計者的責任在於確保用於權限的字串識別碼為獨一無二的。  
  
         下列程式碼範例會使用 `http://example.org/claims/complexcustomclaim` 的宣告類型、`MyResourceType` 的自訂資源類型和 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 權限，建立自訂宣告。  
  
         [!code-csharp[c_CustomClaim#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#5)]
         [!code-vb[c_CustomClaim#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#5)]
  
## <a name="example"></a>範例  

 下列程式碼範例會示範如何使用基本資源類型和非基本資源類型建立自訂宣告。  
  
 [!code-csharp[c_CustomClaim#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#0)]
 [!code-vb[c_CustomClaim#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#0)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.Rights>
- <xref:System.IdentityModel.Claims.ClaimTypes>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [使用身分識別模型來管理宣告與授權](../feature-details/managing-claims-and-authorization-with-the-identity-model.md)
