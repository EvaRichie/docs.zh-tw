---
title: 限定 COM 互通的 .NET 型別
description: 本文提供的指導方針可協助您將 .NET 元件中的類型公開給 com interop 的 COM 應用程式。
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET components to COM
- COM interop, qualifying .NET types
- qualifying .NET types for interoperation
- interoperation with unmanaged code, qualifying .NET types
- interoperation with unmanaged code, exposing .NET components
- COM interop, exposing COM components
ms.assetid: 4b8afb52-fb8d-4e65-b47c-fd82956a3cdd
ms.openlocfilehash: 3fa9f0d5d8dd4d532fc510a1d946eddf32016748
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2020
ms.locfileid: "93187758"
---
# <a name="qualifying-net-types-for-com-interoperation"></a>限定 COM 互通的 .NET 型別
如果您想要向 COM 應用程式公開組件中的類型，請考慮設計階段的 COM Interop 需求。 當您遵守下列方針時，Managed 類型 (類別、介面、結構和列舉) 會與 COM 類型緊密整合：  
  
- 類別應該明確地實作介面。  
  
     雖然 COM Interop 提供機制來自動產生包含類別之所有成員和其基底類別成員的介面，最好是目前提供明確的介面。但是最好是提供明確介面。 自動產生的介面稱為類別介面。 如需指導方針，請參閱 [類別介面簡介](com-callable-wrapper.md#introducing-the-class-interface)。  
  
     您可以使用 Visual Basic、C# 和 C++ 在程式碼中併入介面定義，而不需使用介面定義語言 (IDL) 或其對等項目。 如需語法詳細資訊，請參閱您的語言文件。  
  
- Managed 類型必須是公用的。  
  
     只有組件中的公用類型才會註冊並匯出至型別程式庫。 因此，只有 COM 才能看到公用類型。  
  
     Managed 類型會向可能未向 COM 公開的其他 Managed 程式碼公開功能。 例如，不會向 COM 用戶端公開參數化建構函式、靜態方法和常數欄位。 此外，執行階段將資料封送處理至類型或從中封送處理資料時，可能會複製或轉換資料。  
  
- 方法、屬性、欄位和事件必須是公用的。  
  
     如果要讓 COM 看到公用類型的成員，則它們也必須是公用的。 您可以套用 <xref:System.Runtime.InteropServices.ComVisibleAttribute>，以限制組件、公用類型或公用類型的公用成員的可見性。 根據預設，會顯示所有公用類型和成員。  
  
- 型別必須具有要從 COM 啟用的公用無參數建構函式。  
  
     COM 可以看到 Managed 公用類型。 不過，若沒有公用無參數建構函式 (沒有引數的建構函式)，COM 用戶端就無法建立該型別。 如果該類型是透過一些其他方式啟用，則 COM 用戶端仍然可以使用它。  
  
- 類型不能是抽象的。  
  
     COM 用戶端和 .NET 用戶端都無法建立抽象類型。  
  
 匯出至 COM 時，會壓平合併 Managed 類型的繼承階層。 Managed 與 Unmanaged 環境之間的版本設定不同。 向 COM 公開之類型與其他 Managed 類型的版本設定特性不同。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.ComVisibleAttribute>
- [將 .NET Framework 元件公開給 COM](../../framework/interop/exposing-dotnet-components-to-com.md)
- [類別介面簡介](com-callable-wrapper.md#introducing-the-class-interface)
- [套用 Interop 屬性](apply-interop-attributes.md)
- [封裝 COM 的 .NET Framework 組件](../../framework/interop/packaging-an-assembly-for-com.md)
