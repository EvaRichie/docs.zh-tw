---
title: 作法：使用 EdmGen.exe 產生模型和對應檔
ms.date: 03/30/2017
ms.assetid: 40db462d-2fd2-4cc1-ad86-d280403e63fa
ms.openlocfilehash: 8837afd05eec0eaf8ef3e909d46b280e8ae05da7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198180"
---
# <a name="how-to-use-edmgenexe-to-generate-the-model-and-mapping-files"></a>作法：使用 EdmGen.exe 產生模型和對應檔

本主題示範如何使用 EDM 產生器 (EdmGen.exe) 工具依據 School 資料庫產生下列檔案：  
  
- 概念模型 (.csdl 檔)。  
  
- 儲存體模型 (.ssdl 檔)。  
  
- 概念模型和儲存模型之間的對應 (.msl 檔)。  
  
- Visual Basic 或 C# 中的物件層程式碼。  
  
- 檢視檔案。  
  
 EdmGen.exe 工具使用 /mode:FullGeneration 產生以上所列檔案。 如需 EdmGen.exe 命令的詳細資訊，請參閱 EDM 產生器 [ ( # A1) ](edm-generator-edmgen-exe.md)。  
  
 如果您使用 EdmGen.exe 來產生模型和對應檔，您仍然需要將 Visual Studio 專案設定為使用 Entity Framework。 如需詳細資訊，請參閱 [如何：手動設定 Entity Framework 專案](/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))。  
  
> [!NOTE]
> EdmGen.exe 所產生的概念模型會包括資料庫中的所有物件。 如果您想要產生僅包含特定物件的概念模型，請使用 Entity Data Model 精靈。 如需詳細資訊，請參閱 [如何：使用實體資料模型 Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))。  
  
### <a name="to-generate-the-school-model-for-a-visual-basic-project-using-edmgenexe"></a>若要使用 EdmGen.exe 來產生 Visual Basic 專案的 School 模型  
  
1. 建立 School 資料庫。 如需詳細資訊，請參閱 [建立 School 範例資料庫](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100))。  
  
2. 在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```console  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:fullgeneration
    /c:"Data Source=%datasourceserver%; Initial Catalog=School; Integrated Security=SSPI"
    /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:VB  
    ```  
  
### <a name="to-generate-the-school-model-for-a-c-project-using-edmgenexe"></a>若要使用 EdmGen.exe 來產生 C# 專案的 School 模型  
  
1. 建立 School 資料庫。 如需詳細資訊，請參閱 [建立 School 範例資料庫](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100))。  
  
2. 在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```console  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:fullgeneration
    /c:"Data Source=%datasourceserver%; Initial Catalog=School; Integrated Security=SSPI"
    /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:CSharp  
    ```  
  
## <a name="see-also"></a>另請參閱

- [建立模型和對應](modeling-and-mapping.md)
- [如何：手動設定 Entity Framework 專案](/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))
- [如何：預先產生檢視以改善查詢效能](/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))
- [ADO.NET 實體資料模型工具](/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [作法：使用 EdmGen.exe 驗證模型和對應檔](how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)
