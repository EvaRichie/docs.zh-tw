---
title: 作法：呼叫 Windows API
ms.date: 07/20/2015
helpviewer_keywords:
- API calls [Visual Basic]
- Windows API, calling
- API calls [Visual Basic], platform invoke
- calls [Visual Basic], stored procedures
ms.assetid: 27d75f0a-54ab-4ee1-b91d-43513a19b12d
ms.openlocfilehash: 2c3bb599b79575180eb2b0ec89453f01901f94c0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396839"
---
# <a name="how-to-call-windows-apis-visual-basic"></a>如何：呼叫 Windows API (Visual Basic)
這個範例會定義並呼叫 `MessageBox` user32 中的函式，然後將字串傳遞給它。  
  
## <a name="example"></a>範例  
 [!code-vb[VbVbalrInterop#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#1)]  
  
## <a name="compile-the-code"></a>編譯程式碼  
 這個範例需要：  
  
- <xref:System> 命名空間的參考。  
  
## <a name="robust-programming"></a>穩固程式設計  
 以下條件可能會造成例外狀況：  
  
- 方法不是靜態、是抽象，或先前已定義過。 父類型是介面，或*名稱*或*dllName*的長度為零。 (<xref:System.ArgumentException>)  
  
- *名稱*或*dllName*為 `Nothing` 。 (<xref:System.ArgumentNullException>)  
  
- 之前已使用 `CreateType` 建立包含類型。 (<xref:System.InvalidOperationException>)  
  
## <a name="see-also"></a>另請參閱

- [進一步了解平台叫用](../../../framework/interop/consuming-unmanaged-dll-functions.md#a-closer-look-at-platform-invoke)
- [平台叫用範例](../../../framework/interop/platform-invoke-examples.md)
- [使用 Unmanaged DLL 函式](../../../framework/interop/consuming-unmanaged-dll-functions.md)
- [使用反映發出定義方法](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w63y4d4f(v=vs.100))
- [逐步解說：呼叫 Windows API](walkthrough-calling-windows-apis.md)
- [COM Interop](index.md)
