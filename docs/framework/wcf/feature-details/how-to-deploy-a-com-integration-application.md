---
title: HOW TO：部署 COM+ 整合應用程式
ms.date: 03/30/2017
ms.assetid: 2e5a0510-db3c-4988-a09c-696285836650
ms.openlocfilehash: b4ae7f730296d54debc1cf2971b61e5700503430
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595423"
---
# <a name="how-to-deploy-a-com-integration-application"></a>HOW TO：部署 COM+ 整合應用程式
撰寫好 COM+ 整合應用程式後，您可能會想要將它部署在其他機器上。 此主題描述如何將 COM+ 整合應用程式從一部機器移到另一部機器。  
  
### <a name="moving-a-com-hosted-integration-app"></a>移動 COM+ 主控的整合應用程式  
  
1. 確定兩部電腦上都已安裝 WCF。  
  
2. 從機器 A 匯出應用程式。  
  
3. 將應用程式匯入機器 B。  
  
4. 設定應用程式根目錄。 根據慣例，根目錄是 %PROGRAMFILES%/ComPlus Applications/{AppGUID}。  
  
5. 從機器 A 的應用程式根目錄，將 Application.config 和 Application.manifest 檔案複製到機器 B 的應用程式根目錄。  
  
6. 在機器 B 的 Application.config 檔案中編輯服務端點位址，以識別適當的機器。 例如，將 `http://machineA/MyService` 變更為 `http://machineB/MyService`。  
  
### <a name="moving-a-web-hosted-integration-application"></a>移動 Web 主控的整合應用程式  
  
1. 確定兩部電腦上都已安裝 WCF。  
  
2. 從機器 A 匯出應用程式。  
  
3. 將應用程式匯入機器 B。  
  
4. 在機器 B 上建立 IIS VRoot。  
  
5. 從機器 A 的 VRoot，將 .svc 檔 (componentName.svc) 和 Web.config 檔複製到機器 B 上新建立的 VRoot。  
  
## <a name="see-also"></a>請參閱

- [整合 COM+ 應用程式概觀](integrating-with-com-plus-applications-overview.md)
- [HOW TO：設定 COM+ 服務設定](how-to-configure-com-service-settings.md)
- [如何：使用 COM+ 服務模型組態工具](how-to-use-the-com-service-model-configuration-tool.md)
