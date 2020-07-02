---
title: 封送處理字串
description: 請參閱如何封送處理字串。 請參閱依值或參考封送處理字串的選項，如此一來，在結構或類別中的值或參考，還有更多。
ms.date: 03/30/2017
helpviewer_keywords:
- marshaling, samples
- platform invoke, marshaling data
- data marshaling, strings
- data marshaling, samples
- data marshaling, platform invoke
- marshaling. strings
- marshaling, platform invoke
- sample applications [.NET Framework], marshaling strings
ms.assetid: e21b078b-70fb-4905-be26-c097ab2433ff
ms.openlocfilehash: 0be5a5817bd92c5be6b701200a74650ef9de1955
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621479"
---
# <a name="marshaling-strings"></a>封送處理字串
平台叫用會複製字串參數，並視需要從 .NET Framework 格式 (Unicode) 轉換成 Unmanaged 格式 (ANSI)。 傳回函式時，因為 Managed 字串不可變，所以平台叫用不會將 Managed 字串從 Unmanaged 記憶體複製回 Managed 記憶體。  
  
 下表列出字串的封送處理選項，並描述其用法，以及提供對應 .NET Framework 範例的連結。  
  
|String|描述|範例|  
|------------|-----------------|------------|  
|傳值。|將字串傳遞為 In 參數。|[MsgBox](msgbox-sample.md)|  
|作為結果。|從 Unmanaged 程式碼傳回字串。|[字串](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e765dyyy(v=vs.100))|  
|傳址。|使用 <xref:System.Text.StringBuilder> 將字串傳遞為 In/Out 參數。|[緩衝區](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/x3txb6xc(v=vs.100))|  
|在傳值結構中。|透過本身為 In 參數的結構傳遞字串。|[結構](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/eadtsekz(v=vs.100))|  
|在結構中以傳址方式 **（char \* ）**。|透過本身為 In/Out 參數的結構傳遞字串。 Unmanaged 函式需要字元緩衝區的指標，而且緩衝區大小是結構的成員。|[字串](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e765dyyy(v=vs.100))|  
|在傳址結構中 **(char[])**。|透過本身為 In/Out 參數的結構傳遞字串。 Unmanaged 函式需要內嵌的字元緩衝區。|[OSInfo](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/795sy883(v=vs.100))|  
|在類別中，依值 **（char \* ）**。|在類別中傳遞字串 (類別是 In/Out 參數)。 Unmanaged 函式需要字元緩衝區的指標。|[OpenFileDlg](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w5tyztk9(v=vs.100))|  
|在傳值類別中 **(char[])**。|在類別中傳遞字串 (類別是 In/Out 參數)。 Unmanaged 函式需要內嵌的字元緩衝區。|[OSInfo](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/795sy883(v=vs.100))|  
|作為傳值字串陣列。|建立以傳值方式傳遞的字串陣列。|[陣列](marshaling-different-types-of-arrays.md)|  
|作為包含傳值字串的結構陣列。|建立包含字串的結構陣列，並以傳值方式傳遞該陣列。|[陣列](marshaling-different-types-of-arrays.md)|  
  
## <a name="see-also"></a>另請參閱

- [字串的預設封送處理](default-marshaling-for-strings.md)
- [使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)
- [封送處理類別、結構和等位](marshaling-classes-structures-and-unions.md)
- [封送處理不同類型的陣列](marshaling-different-types-of-arrays.md)
- [其他封送處理範例](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ss9sb93t(v=vs.100))
