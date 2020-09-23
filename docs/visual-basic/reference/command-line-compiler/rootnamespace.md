---
title: -rootnamespace
ms.date: 03/13/2018
f1_keywords:
- /rootnamespace
- rootnamespace
helpviewer_keywords:
- /rootnamespace compiler option [Visual Basic]
- -rootnamespace compiler option [Visual Basic]
- rootnamespace compiler option [Visual Basic]
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
ms.openlocfilehash: d9388ace03f654458eb955e989673b7441e72f23
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91085135"
---
# <a name="-rootnamespace"></a>-rootnamespace

指定所有類型宣告的命名空間。  
  
## <a name="syntax"></a>語法  
  
```console  
-rootnamespace:namespace  
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|定義|  
|---|---|  
|`namespace`|命名空間的名稱，用來括住目前專案的所有類型宣告。|  
  
## <a name="remarks"></a>備註  

 如果您使用 Visual Studio 可執行檔 ( # A0) 來編譯在 Visual Studio 整合式開發環境中建立的專案，請使用 `-rootnamespace` 來指定屬性的值 <xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A> 。 如需詳細資訊，請參閱 [Devenv 命令列參數](/visualstudio/ide/reference/devenv-command-line-switches) 。  
  
 使用 common language runtime MSIL 解譯器 (`Ildasm.exe`) 來查看輸出檔中的命名空間名稱。  
  
|在 Visual Studio 整合式開發環境中設定-rootnamespace|  
|---|  
|1. 在 **方案總管**中選取專案。 按一下 [專案] 功能表上的 [屬性]。 <br />2. 按一下 [ **應用程式** ] 索引標籤。<br />3. 修改 [ **根命名空間** ] 方塊中的值。|  
  
## <a name="example"></a>範例  

 下列程式碼會編譯 `In.vb` 並將所有型別宣告封裝在命名空間中 `mynamespace` 。  
  
```console
vbc -rootnamespace:mynamespace in.vb  
```  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)
- [Ildasm.exe (IL 解譯器) ](../../../framework/tools/ildasm-exe-il-disassembler.md)
- [編譯命令列的範例](sample-compilation-command-lines.md)
