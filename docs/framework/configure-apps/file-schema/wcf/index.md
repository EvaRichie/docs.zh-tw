---
title: WCF 組態結構描述
ms.date: 03/30/2017
ms.assetid: c282aeb5-91f0-4522-8e2f-704c1ef3651f
ms.openlocfilehash: ab64b41e6e79c934ac0145dd7eec0a943f5dc473
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91165126"
---
# <a name="wcf-configuration-schema"></a>WCF 組態結構描述

Windows Communication Foundation (WCF) 設定元素可讓您設定 WCF 服務和用戶端應用程式。 您可使用[組態編輯器工具 (SvcConfigEditor.exe)](../../../wcf/configuration-editor-tool-svcconfigeditor-exe.md) 來建立並修改用戶端與服務的組態檔。 由於組態檔採用 XML 格式，因此，如果要使用文字編輯器手動編輯這些檔案，則必須熟悉 XML。 否則，您可能會碰到 XML 項目標記或屬性找不到等問題， 因為 XML 項目標記與屬性有區分大小寫。  
  
 WCF 設定系統是以 <xref:System.Configuration> 命名空間為基礎。 因此，您可以使用 <xref:System.Configuration> 命名空間提供的所有標準功能，例如組態鎖定、加密與合併，以提升應用程式及其組態的安全性。 如需這些概念的詳細資訊，請參閱下列主題。  
  
 [加密組態資訊](/previous-versions/aspnet/53tyfkaw(v=vs.100))  
  
 [鎖定組態設定](/previous-versions/aspnet/55th21y4(v=vs.100))  
  
 本節說明每個組態項目的所有可能值，以及項目如何與其他 WCF 組態項目互動。 下圖說明 WCF 設定架構：  
  
 ![顯示 WCF 設定架構的圖表。](./media/index/windows-communication-foundation-configuration-schema.gif)  
  
> [!CAUTION]
> 您應該在應用程式佈建檔中使用適當的存取控制)  (清單來保護應用程式佈建檔中的 WCF 設定區段 ( # A0) ，以防止任何潛在的安全性威脅。  例如，您要確定只有適當人員才能存取或修改應用程式繫結上的安全性設定，或是服務組態檔的服務模型區段。  
  
## <a name="in-this-section"></a>本節內容  

 [\<system.serviceModel>](system-servicemodel.md)  
 說明 `ServiceModel` 項目。  
  
 [\<system.serviceModel.activation>](system-servicemodel-activation.md)  
 設定 SMSvcHost.exe 工具。  
  
 [\<system.runtime.serialization>](system-runtime-serialization.md)  
 使用 <xref:System.Runtime.Serialization.DataContractSerializer> 等序列化程式時，設定選項的最上層項目。  
  
## <a name="related-sections"></a>相關章節  

 [Configuring Windows Communication Foundation Applications](../../../wcf/configuring-services.md)  
 說明如何設定 WCF 服務與用戶端。
