---
description: -pdb (C# 編譯器選項)
title: -pdb (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /pdb
helpviewer_keywords:
- -pdb compiler option [C#]
- pdb compiler option [C#]
- /pdb compiler option [C#]
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
ms.openlocfilehash: ced1ee1f4f079830a032a628da96a389ba27da90
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193851"
---
# <a name="-pdb-c-compiler-options"></a>-pdb (C# 編譯器選項)

**-pdb** 編譯器選項指定偵錯符號檔的名稱和位置。  
  
## <a name="syntax"></a>語法  
  
```console  
-pdb:filename  
```  
  
## <a name="arguments"></a>引數  

 `filename`  
 偵錯符號檔案的名稱和位置。  
  
## <a name="remarks"></a>備註  

 當您指定 [-debug (C# 編譯器選項)](./debug-compiler-option.md) 時，編譯器會在相同的目錄中建立 .pdb 檔案，而編譯器會在此目錄中建立檔案名稱與輸出檔案名稱相同的輸出檔案 (.exe 或 .dll)。  
  
 **-pdb** 可讓您指定 .pdb 檔案的非預設檔案名稱和位置。  
  
 無法在 Visual Studio 開發環境中設定此編譯器選項，也無法以程式設計方式進行變更。  
  
## <a name="example"></a>範例  

 編譯 `t.cs` 並建立稱為 tt.pdb 的 .pdb 檔案：  
  
```console  
csc -debug -pdb:tt t.cs  
```  
  
## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](./index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
