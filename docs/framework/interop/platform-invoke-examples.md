---
title: 平台叫用範例
description: 請參閱平台叫用範例，其中示範如何在 User32.dll 中定義和呼叫 MessageBox 函式。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [.NET Framework], platform invoke
- unmanaged functions
- COM interop, platform invoke
- platform invoke, examples
- interoperation with unmanaged code, platform invoke
- DLL functions
ms.assetid: 15926806-f0b7-487e-93a6-4e9367ec689f
ms.openlocfilehash: 97b0720b8954bc24a4058e6a03c32d32bd9e3180
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620803"
---
# <a name="platform-invoke-examples"></a>平台叫用範例
下列範例示範如何在 User32.dll 中定義和呼叫 **MessageBox** 函式，並將簡單字串傳遞為引數。 在這些範例中，<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位會設定為 **Auto**，讓目標平台決定字元寬度和字串封送處理。  
  
 [!code-cpp[Conceptual.Interop.PInvoke#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.Interop.PInvoke/cpp/Example.cpp#1)]
 [!code-csharp[Conceptual.Interop.PInvoke#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.Interop.PInvoke/cs/Example1.cs#1)]
 [!code-vb[Conceptual.Interop.PInvoke#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.Interop.PInvoke/vb/Example1.vb#1)]  
  
 如需其他範例，請參閱[使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [在 Managed 程式碼中建立原型](creating-prototypes-in-managed-code.md)
- [指定字元集](specifying-a-character-set.md)
