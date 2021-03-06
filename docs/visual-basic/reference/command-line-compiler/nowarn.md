---
title: -nowarn
ms.date: 07/20/2015
helpviewer_keywords:
- nowarn compiler option [Visual Basic]
- /nowarn compiler option [Visual Basic]
- -nowarn compiler option [Visual Basic]
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
ms.openlocfilehash: cde96fff975a65d6303ee62e6a811bfd83d5ff97
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91097679"
---
# <a name="-nowarn"></a>-nowarn

抑制編譯器產生警告的功能。  
  
## <a name="syntax"></a>語法  
  
```console  
-nowarn[:numberList]  
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|定義|  
|---|---|  
|`numberList`|選擇性。 編譯器應該隱藏的警告識別碼編號清單（以逗號分隔）。 如果未指定警告識別碼，則會隱藏所有警告。|  
  
## <a name="remarks"></a>備註  

 `-nowarn`選項會導致編譯器不會產生警告。 若要隱藏個別警告，請將警告識別碼提供給 `-nowarn` 冒號後面的選項。 以逗號分隔多個警告編號。  
  
 您只需要指定警告識別碼的數值部分。 例如，如果您想要隱藏 BC42024 （未使用之區域變數的警告），請指定 `-nowarn:42024` 。  
  
 如需有關警告識別碼的詳細資訊，請參閱設定 [Visual Basic 中的警告](/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
|在 Visual Studio 整合式開發環境中設定-nowarn|  
|---|  
|1. 在 **方案總管**中選取專案。 按一下 [專案] 功能表上的 [屬性]。 <br />2. 按一下 [ **編譯** ] 索引標籤。<br />3. 選取 [ **停用所有警告** ] 核取方塊，以停用所有警告。<br />     - 或 -<br />     若要停用特定警告，請在警告旁的下拉式清單中按一下 [ **無** ]。|  
  
## <a name="example"></a>範例  

 下列程式碼 `T2.vb` 會進行編譯，而且不會顯示任何警告。  
  
```console
vbc -nowarn t2.vb  
```  
  
## <a name="example"></a>範例  

 下列 `T2.vb` 程式碼會進行編譯，而且不會顯示 (42024) 中未使用之區域變數的警告。  
  
```console
vbc -nowarn:42024 t2.vb  
```  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)
- [編譯命令列的範例](sample-compilation-command-lines.md)
- [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)
