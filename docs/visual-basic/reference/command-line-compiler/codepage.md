---
title: -codepage
ms.date: 03/09/2018
helpviewer_keywords:
- -codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
ms.openlocfilehash: 34dbf36cc79a8c4715cf6a07c57d559e14f40030
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363626"
---
# <a name="-codepage-visual-basic"></a>-字碼頁（Visual Basic）
指定編譯過程中所有原始程式碼檔使用的字碼頁。  
  
## <a name="syntax"></a>語法  
  
```console  
-codepage:id  
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|定義|  
|---|---|  
|`id`|必要。 編譯器會使用所指定的字碼頁 `id` 來解讀來源檔案的編碼方式。|  
  
## <a name="remarks"></a>備註  
 若要編譯以特定編碼方式儲存的原始程式碼，您可以使用 `-codepage` 來指定應該使用的字碼頁。 此 `-codepage` 選項適用于編譯中的所有原始程式碼檔。 如需詳細資訊，請參閱[.NET Framework 中的字元編碼](../../../standard/base-types/character-encoding.md)。  
  
 `-codepage`如果原始程式碼檔案是使用目前的 ANSI 字碼頁、Unicode 或 utf-8 （含簽章）儲存，則不需要選項。 Visual Studio 預設會儲存目前 ANSI 字碼頁的所有原始程式碼檔，除非使用者在 [**編碼**] 對話方塊中指定另一種編碼方式。 Visual Studio 使用 [**編碼**] 對話方塊來開啟以不同字碼頁儲存的原始程式碼檔案。  
  
> [!NOTE]
> 此 `-codepage` 選項無法從 Visual Studio 開發環境中使用; 只有在從命令列進行編譯時，才能使用此選項。  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)
