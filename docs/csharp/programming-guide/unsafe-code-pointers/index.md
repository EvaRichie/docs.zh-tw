---
title: 不安全的程式碼與指標 - C# 程式設計手冊
Description: "瞭解 unsafe 程式碼和指標。 C # 不支援指標，但是您可以定義不安全的內容，其中的指標可與 ' unsafe ' 關鍵字搭配使用。"
ms.date: 07/20/2015
helpviewer_keywords:
- security [C#], type safety
- C# language, unsafe code
- type safety [C#]
- unsafe keyword [C#]
- unsafe code [C#]
- C# language, pointers
- pointers [C#], about pointers
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
ms.openlocfilehash: 5684a97ed6f7b6632d8fe3d52747d9187c4b8cbc
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381771"
---
# <a name="unsafe-code-and-pointers-c-programming-guide"></a>不安全的程式碼和指標 (C# 程式設計手冊)

為了維護型別安全和安全性，C# 預設不支援指標算術。 不過，藉由使用 [unsafe](../../language-reference/keywords/unsafe.md) 關鍵字，即可定義能在其中使用指標的不安全內容。 如需指標的詳細資訊，請參閱[指標類型](pointer-types.md)。  
  
> [!NOTE]
> 在 Common Language Runtime (CLR) 中，不安全的程式碼是指無法驗證的程式碼。 C# 中不安全的程式碼不一定具有危險性，這不過是其安全性無法由 CLR 驗證的程式碼。 因此，CLR 只會執行完全受信任之組件中不安全的程式碼。 如果您使用不安全的程式碼，則有責任確保程式碼不會帶來安全性風險或造成指標錯誤。  
  
## <a name="unsafe-code-overview"></a>不安全的程式碼概觀

不安全的程式碼具有下列屬性：

- 方法、類型和程式碼區塊可以定義為不安全。

- 在某些情況下，不安全的程式碼可能會藉由移除陣列界限檢查，來提升應用程式的效能。

- 當您呼叫需要指標的原生函式時，需要不安全的程式碼。

- 使用不安全的程式碼會帶來安全性和穩定性風險。

- 包含不安全之區塊的程式碼必須使用 [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) 編譯器選項編譯。
  
## <a name="related-sections"></a>相關章節

如需詳細資訊，請參閱

- [指標類型](pointer-types.md)

- [固定大小的緩衝區](fixed-size-buffers.md)

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)中的[不安全的程式碼](~/_csharplang/spec/unsafe-code.md)主題。
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [不安全](../../language-reference/keywords/unsafe.md)
