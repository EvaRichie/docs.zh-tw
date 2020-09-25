---
title: 作法：使用 EdmGen.exe 驗證模型和對應檔
ms.date: 03/30/2017
ms.assetid: 2641906a-971a-4d0b-8aee-13fabc02a1cc
ms.openlocfilehash: 62a3bde9d2431b9e9e86e2a8d8896520f3456590
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198115"
---
# <a name="how-to-use-edmgenexe-to-validate-model-and-mapping-files"></a>作法：使用 EdmGen.exe 驗證模型和對應檔

本主題說明如何使用 EDM 產生器 [ ( # A0) ](edm-generator-edmgen-exe.md) 工具來驗證模型和對應檔。 如需詳細資訊，請參閱 [實體資料模型](../entity-data-model.md)。  
  
### <a name="to-validate-the-school-model-using-edmgenexe"></a>使用 EdmGen.exe 驗證 School 模型  
  
1. 建立 School 資料庫。 如需詳細資訊，請參閱 [建立 School 範例資料庫](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100))。  
  
2. 產生 School 模型。 如需詳細資訊，請參閱 [如何：使用 EdmGen.exe 產生模型和對應](how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)檔。  
  
3. 在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```console
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:ValidateArtifacts /inssdl:.\School.ssdl /inmsl:.\School.msl /incsdl:.\School.csdl  
    ```  
  
## <a name="see-also"></a>另請參閱

- [如何：手動設定 Entity Framework 專案](/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))
- [ADO.NET 實體資料模型工具](/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [如何：預先產生檢視以改善查詢效能](/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))
- [作法：使用 EdmGen.exe 產生物件層程式碼](how-to-use-edmgen-exe-to-generate-object-layer-code.md)
