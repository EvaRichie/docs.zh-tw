---
description: '##pragma warning - C# 參考'
title: '##pragma warning - C# 參考'
ms.date: 07/20/2015
f1_keywords:
- '#pragma warning'
helpviewer_keywords:
- '#pragma warning [C#]'
ms.assetid: 723493d5-9753-4cec-babb-54e2b8eb36b6
ms.openlocfilehash: 5b67d384e37a5e509ce8ebcc5ddeb16a4437ea2b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168526"
---
# <a name="pragma-warning-c-reference"></a>#pragma warning (C# 參考)

`#pragma warning` 可以啟用或停用特定警告。  
  
## <a name="syntax"></a>語法  
  
```csharp
#pragma warning disable warning-list  
#pragma warning restore warning-list  
```  
  
## <a name="parameters"></a>參數  

 `warning-list`  
 警告編號的逗點分隔清單。 "CS" 前置詞是選擇性的。  
  
 未指定警告編號時，`disable` 會停用所有警告，而 `restore` 會啟用所有警告。  
  
> [!NOTE]
> 若要尋找 Visual Studio 中的警告編號，請建立專案，然後在 [輸出]**** 視窗中尋找警告編號。  
  
## <a name="example"></a>範例  
  
```csharp
// pragma_warning.cs  
using System;  
  
#pragma warning disable 414, CS3021  
[CLSCompliant(false)]  
public class C  
{  
    int i = 1;  
    static void Main()  
    {  
    }  
}  
#pragma warning restore CS3021  
[CLSCompliant(false)]  // CS3021  
public class D  
{  
    int i = 1;  
    public static void F()  
    {  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 預處理器指示詞](./index.md)
- [C # 編譯器錯誤](../compiler-messages/index.md)
