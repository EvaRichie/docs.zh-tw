---
title: 如何在 C# 中定義常數
description: '瞭解如何在 c # 中定義常數，也就是值在編譯時期設定的欄位。 使用常數為特殊值提供有意義的名稱。'
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, constants
- constants [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
ms.openlocfilehash: 972deaa4616c15c00e83e26891c4473eae7bfcf8
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513051"
---
# <a name="how-to-define-constants-in-c"></a>如何在 C 中定義常數\#

常數是欄位，其值於編譯時期設定且絕對不會變更。 使用常數提供有意義的名稱，而不是特殊值的數值常值 (「神奇號碼」)。  
  
> [!NOTE]
> 在 C# 中，[#define](../../language-reference/preprocessor-directives/preprocessor-define.md) 前置處理器指示詞不能以 C 和 C++ 一般使用的方式來定義常數。  
  
 若要定義整數型別的常數值 (`int`、`byte` 等等)，請使用列舉類型。 如需詳細資訊，請參閱 [enum](../../language-reference/builtin-types/enum.md)。  
  
 若要定義非整數常數，其中一個方法是將它們分組在名為 `Constants` 的單一靜態類別中。 如下列範例所示，這需要常數的所有參考都以類別名稱開頭。  
  
## <a name="example"></a>範例  

 [!code-csharp[csProgGuideObjects#89](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#89)]  
  
 使用類別名稱限定詞，可協助確保您和其他常數使用者了解它是無法修改的常數。  
  
## <a name="see-also"></a>請參閱

- [類別和結構](./index.md)
