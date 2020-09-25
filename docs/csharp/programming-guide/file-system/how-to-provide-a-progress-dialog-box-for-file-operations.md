---
title: '如何提供檔案作業的進度對話方塊-c # 程式設計指南'
description: 瞭解如何使用 CopyFile (String、String、UIOption) 方法提供檔案作業的進度對話方塊。
ms.date: 07/20/2015
helpviewer_keywords:
- progress dialog [C#]
ms.assetid: 01b71fe7-8178-4dc8-aeb1-12053be7b51c
ms.openlocfilehash: 5d16aeb3a5394ca250e4a5e26074db797c54216d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185882"
---
# <a name="how-to-provide-a-progress-dialog-box-for-file-operations-c-programming-guide"></a>如何提供檔案作業的進度對話方塊 (c # 程式設計指南) 

如果您在 <xref:Microsoft.VisualBasic?displayProperty=nameWithType> 命名空間中使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%28System.String%2CSystem.String%2CMicrosoft.VisualBasic.FileIO.UIOption%29> 方法，則可以提供標準對話方塊，以在 Windows 中顯示檔案作業進度。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-reference-in-visual-studio"></a>在 Visual Studio 中加入參考  
  
1. 在功能表列上，選擇 **[專案]**、**[加入參考]**。  
  
     [參考管理員]**** 對話方塊隨即顯示。  
  
2. 在 [組件]**** 區域中，選擇 [Framework]**** (如果尚未選擇)。  
  
3. 在名稱清單中，選取 **[Microsoft.VisualBasic]** 核取方塊，然後選擇 **[確定]** 按鈕以關閉對話方塊。  
  
## <a name="example"></a>範例  

 下列程式碼會將 `sourcePath` 指定的目錄複製到 `destinationPath` 指定的目錄。 此程式碼也會提供標準對話方塊，來顯示作業完成前的預估剩餘時間量。  
  
 [!code-csharp[csFilesandFolders#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#11)]  
  
## <a name="see-also"></a>另請參閱

- [檔案系統和登錄 (C# 程式設計手冊)](./index.md)
