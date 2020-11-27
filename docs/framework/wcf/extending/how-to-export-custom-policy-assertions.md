---
title: 作法：匯出自訂原則判斷提示
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 99030386-43b0-4f7b-866d-17ea307f5cbd
ms.openlocfilehash: 8bdc9948d6846631fde1d428c113682f40d15ec3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249211"
---
# <a name="how-to-export-custom-policy-assertions"></a>作法：匯出自訂原則判斷提示

原則判斷提示描述服務端點的功能與需求。 服務應用程式可使用服務中繼資料中的自訂原則判斷提示，與用戶端應用程式進行端點、繫結或合約自訂資訊的通訊。 您可以根據所要通訊的功能或需求，使用 Windows Communication Foundation (WCF) ，將 WSDL 系結中附加于 WSDL 系結的原則運算式匯出判斷提示。  
  
 匯出自訂原則判斷提示的方法，是實作 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> 上的 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> 介面，然後直接將繫結項目插入服務端點的繫結或將繫結項目登錄於應用程式組態檔。 您的原則匯出實作應將您的自訂原則判斷提示當成 <xref:System.Xml.XmlElement?displayProperty=nameWithType> 執行個體新增至位於傳入 <xref:System.ServiceModel.Description.PolicyAssertionCollection?displayProperty=nameWithType> 方法的 <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=nameWithType> 上之合適 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A>。  
  
 除此之外，您還必須檢查 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 類別的 <xref:System.ServiceModel.Description.WsdlExporter> 屬性 (Property)，並且根據指定的原則版本，以正確命名空間匯出巢狀原則運算式及原則架構屬性 (Attribute)。  
  
 若要匯入自訂原則判斷提示，請參閱 <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> 和 how [to：匯入自訂原則判斷](how-to-import-custom-policy-assertions.md)提示。  
  
### <a name="to-export-custom-policy-assertions"></a>若要匯出自訂原則判斷提示  
  
1. 實作 上的  介面。 下列程式碼範例顯示繫結層級之自訂原則判斷提示的實作。  
  
     [!code-csharp[CustomPolicySample#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyexporter.cs#14)]
     [!code-vb[CustomPolicySample#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyexporter.vb#14)]  
  
2. 以程式設計的方式或使用應用程式組態檔將繫結項目插入端點繫結。 請參閱下列程序。  
  
### <a name="to-insert-a-binding-element-using-an-application-configuration-file"></a>若要使用應用程式組態檔插入繫結項目  
  
1. 針對您的自訂原則判斷提示繫結項目實作 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=nameWithType>。  
  
2. 使用專案，將繫結項目延伸加入至設定檔 [\<bindingElementExtensions>](../../configure-apps/file-schema/wcf/bindingelementextensions.md) 。  
  
3. 使用 建置自訂繫結。  
  
### <a name="to-insert-a-binding-element-programmatically"></a>以程式設計的方式插入繫結項目  
  
1. 建立新的 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> 並將它新增至 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>。  
  
2. 將步驟 1 中的自訂繫結加入。 至新服務端點，並呼叫 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> 方法，以將新服務端點加入至 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>。  
  
3. 開啟 <xref:System.ServiceModel.ServiceHost>。 下列程式碼範例顯示自訂繫結的建立，以及使用程式設計方式插入繫結項目。  
  
     [!code-csharp[s_imperative#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_imperative/cs/service.cs#1)]
     [!code-vb[s_imperative#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_imperative/vb/service.vb#1)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Description.IPolicyImportExtension>
- <xref:System.ServiceModel.Description.IPolicyExportExtension>
- [作法：匯入自訂原則判斷提示](how-to-import-custom-policy-assertions.md)
