---
title: 使用 My 進行開發
ms.date: 07/20/2015
f1_keywords:
- My.MyWpfExtension.Windows
helpviewer_keywords:
- My object
- My namespace
- My feature
- Visual Basic, programming in
ms.assetid: f1d04509-5e46-4551-9f9f-94334a121fca
ms.openlocfilehash: 3befac591de8fbc7250777a8b87247ee395abf25
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411702"
---
# <a name="development-with-my-visual-basic"></a>使用 My 進行開發 (Visual Basic)

Visual Basic 提供可進行快速應用程式開發的新功能來提高產能且易於使用，同時還能提供電源。 這其中一個功能稱為 `My`，可提供對與應用程式及其執行階段環境相關資訊和預設物件執行個體的存取。 此資訊的組織方式是以可透過 IntelliSense 進行探索且邏輯上根據使用方式分隔的格式來進行。  
  
 `My` 的最上層成員會公開為物件。 每個物件的運作方式類似具有 `Shared` 成員的命名空間或類別，而它會公開一組相關的成員。  
  
 此表格顯示最上層 `My` 物件及其彼此間的關聯性。  
  
 ![圖表顯示 My 的物件模型。](./media/index/my-object-model-relationships.gif)  
  
## <a name="in-this-section"></a>本節內容  

 [使用 My.Application、My.Computer 及 My.User 執行工作](performing-tasks-with-my-application-my-computer-and-my-user.md)  
 描述三種中央 `My` 物件 (`My.Application`、`My.Computer` 和 `My.User`)，它們提供對資訊和功能的存取。  
  
 [My.Forms 及 My.WebServices 提供的預設物件執行個體](default-object-instances-provided-by-my-forms-and-my-webservices.md)  
 描述 `My.Forms` 和 `My.WebServices` 物件，它們提供對您應用程式所使用的表單、資料來源和 XML Web 服務的存取。  
  
 [使用 My.Resources 及 my.settings 加快開發應用程式的速度](rapid-application-development-with-my-resources-and-my-settings.md)  
 描述 `My.Resources` 和 `My.Settings` 物件，它們提供對應用程式資源和設定的存取。  
  
 [Visual Basic 應用程式模型概觀](overview-of-the-visual-basic-application-model.md)  
 描述 Visual Basic 應用程式啟動/關閉模型。  
  
 [My 與專案類型的相依關係](how-my-depends-on-project-type.md)  
 提供有關 `My` 功能可在不同專案型別中使用的詳細資料。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [My.Forms 物件](../../language-reference/objects/my-forms-object.md)
- [My.WebServices 物件](../../language-reference/objects/my-webservices-object.md)
- [My 與專案類型的相依關係](how-my-depends-on-project-type.md)
