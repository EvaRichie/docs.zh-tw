---
title: 識別 DLL 中的函式
description: 識別 DLL 中的函式。 DLL 函式的身分識別是由函式名稱或序數，以及可以在其中找到執行的 DLL 檔案名所組成。
ms.date: 03/30/2017
helpviewer_keywords:
- platform invoke, identifying functions
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- identifying DLL functions
- DLL functions
ms.assetid: 3e3f6780-6d90-4413-bad7-ba641220364d
ms.openlocfilehash: 054d1351a9ee6adab17117c9f423aa26d0d9ed59
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622727"
---
# <a name="identifying-functions-in-dlls"></a>識別 DLL 中的函式
DLL 函式的身分識別是由下列項目所組成：  
  
- 函式名稱或序數  
  
- 可在其中找到實作之 DLL 檔案的名稱  
  
 例如，在 User32.dll 中指定 **MessageBox** 函式可識別此函式 (**MessageBox**) 及其位置 (User32.dll、User32 或 user32)。 Microsoft Windows 應用程式開發介面 (Windows API) 可針對處理字元和字串的每一個函式，各包含兩個版本：一個是單位元組字元的 ANSI 版本，另一個是雙位元組字元的 Unicode 版本。 未指定時，由 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> 欄位所代表的字元集預設為 ANSI。 某些函式可以有兩個以上的版本。  
  
 **MessageBoxA** 是 **MessageBox** 函式的 ANSI 進入點；**MessageBoxW** 則是 Unicode 版本。 您可以藉由執行各種不同的命令列工具，列出特定 DLL 的函式名稱，例如 user32.dll 。 例如，您可以使用 `dumpbin /exports user32.dll` 或 `link /dump /exports user32.dll` 來取得函式名稱。  
  
 只要將新名稱對應至 DLL 中原始的進入點，您就可以在程式碼內將 Unmanaged 函式重新命名為您喜歡的任何名稱。 如需在 Managed 原始程式碼中重新命名 Unmanaged DLL 函式中的指示，請參閱[指定進入點](specifying-an-entry-point.md)。  
  
 平台叫用可讓您藉由呼叫 Windows API 和其他 DLL 中的函式，控制作業系統的重要部分。 除了 Windows API 以外，還有許多其他 API 和 DLL 可透過平台叫用供您使用。  
  
 下表描述 Windows API 中常用的數個 DLL。  
  
|DLL|內容的描述|  
|---------|-----------------------------|  
|GDI32.dll|用於裝置輸出的圖形裝置介面 (GDI) 函式，例如用於繪圖和字型管理的函式。|  
|Kernel32.dll|用於記憶體管理和資源處理的低階作業系統函式。|  
|User32.dll|用於訊息處理、計時器、功能表和通訊的 Windows 管理函式。|  
  
 如需 Windows API 的完整文件，請參閱 Platform SDK。 如需示範如何建構要與平台叫用搭配使用之 .NET 型宣告的範例，請參閱[使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)。  
  
## <a name="see-also"></a>另請參閱

- [使用 Unmanaged DLL 函式](consuming-unmanaged-dll-functions.md)
- [指定進入點](specifying-an-entry-point.md)
- [建立類別以包裝 DLL 函式](creating-a-class-to-hold-dll-functions.md)
- [在 Managed 程式碼中建立原型](creating-prototypes-in-managed-code.md)
- [呼叫 DLL 函式](calling-a-dll-function.md)
