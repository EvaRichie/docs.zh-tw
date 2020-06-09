---
title: UriTemplate 表發送器範例
ms.date: 03/30/2017
ms.assetid: 3b32975d-ba90-4c5c-83bc-2fbb48f11c0c
ms.openlocfilehash: 97e916aaf9d137eb7931470f9565797b03620d28
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591068"
---
# <a name="uritemplate-table-dispatcher-sample"></a>UriTemplate 表發送器範例
<xref:System.UriTemplateTable> 類別會提供可用來處理 <xref:System.UriTemplate> 執行個體集合的字典式關聯表結構。 這個範例示範使用 `UriTemplateTable` 建置的基本分派引擎，這是 `UriTemplateTable` 類別的常用案例。  
  
 這個範例會示範 `UriTemplateTable` 類別的下列主要概念：  
  
- 在 `UriTemplates` 中將委派與 `UriTemplateTable` 加以關聯。  
  
- 使用 <xref:System.UriTemplateTable.MatchSingle%2A> 取得特定 URI 的正確處理常式委派。  
  
- 叫用處理常式委派以處理要求。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
2. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\UriTemplateDispatcher`  
  
## <a name="see-also"></a>另請參閱

- [UriTemplate 資料表](uritemplate-table-sample.md)
- [UriTemplate](uritemplate-sample.md)
