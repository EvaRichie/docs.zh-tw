---
title: 安全性和產生作業中的程式碼
description: 代表以較高信任度執行的較低信任程式碼產生程式碼是一項安全性考慮，特別是當呼叫者可能會影響程式碼產生時。
ms.date: 07/15/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- code security, on-the-fly code generation
- on-the-fly code generation
- security [.NET], on-the-fly code generation
- secure coding, on-the-fly code generation
ms.assetid: 6d221724-bb21-4d76-90c3-0ee2a2e69be2
ms.openlocfilehash: a3fc51c346feffa85537d95ccdbd23d943827edf
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555691"
---
# <a name="security-and-on-the-fly-code-generation"></a>安全性和產生作業中的程式碼

某些程式庫的運作方式為產生程式碼，然後執行這個程式碼以進行呼叫端的特定作業。 這種方法的基本問題在於程式庫可能會代表較不受信任的程式碼來產生程式碼，然後以較高的信任層級來執行這個程式碼。 當呼叫端可能影響程式碼產生時，這個問題會更嚴重，因此您必須確保產生的程式碼只會是您認為安全的程式碼。  
  
您必須隨時掌握所產生的實際程式碼內容。 這表示您必須嚴格控制從使用者取得的任何值，這些值可以是以引號括住的字串 (必須逸出以避免包含未預期的程式碼項目)、識別項 (必須檢查以驗證是否為有效的識別項)，或其他任何值。 識別項可能具有危險性，因為編譯過的組件可能會被修改，讓它的識別項包含一些可能會破壞組件的特殊字元 (雖然這通常不是安全性弱點)。  
  
建議您使用反映發出來產生程式碼，這通常可協助您避免許多問題。  
  
當您編譯程式碼時，請考慮惡意程式是否有可能修改程式碼。 在編譯器讀取原始程式碼之前，或在您的程式碼載入 .dll 檔案之前，是不是有空檔時間可以讓惡意程式碼變更磁碟上的原始程式碼？ 如果是，您必須視需要使用檔案系統中的存取控制清單，來保護含有這些檔案的目錄。  
  
## <a name="see-also"></a>另請參閱

- [安全程式碼撰寫方針](secure-coding-guidelines.md)
- [ASP.NET Core 安全性](/aspnet/core/security/)
