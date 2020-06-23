---
title: 使用平台叫用封送處理資料
description: 在 .NET 中使用平台叫用封送處理資料。 查看 Windows Api 和 C 樣式函式中使用的資料類型清單，並尋找其 .NET managed 類型對等專案。
ms.date: 03/20/2019
dev_langs:
- cpp
helpviewer_keywords:
- platform invoke, marshaling data
- data marshaling, platform invoke
- marshaling, platform invoke
ms.assetid: dc5c76cf-7b12-406f-b79c-d1a023ec245d
ms.openlocfilehash: 27045790780c1eef9537bdf7e52deb579e2b467c
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904100"
---
# <a name="marshaling-data-with-platform-invoke"></a>使用平台叫用封送處理資料

若要呼叫從 Unmanaged 程式庫匯出的函式，.NET Framework 應用程式需要代表此 Unmanaged 函式之 Managed 程式碼中的函式原型。 若要建立使平台叫用正確地封送處理資料的原型，您必須執行下列動作：

- 將 <xref:System.Runtime.InteropServices.DllImportAttribute> 屬性套用至使用 Managed 程式碼的靜態函式或方法。

- 將 Unmanaged 資料類型替代為 Managed 資料類型。

您可以使用 Unmanaged 函式所提供的文件，以選擇性欄位套用屬性，並且將 Unmanaged 資料類型替代為 Managed 資料類型，來建構對等的 Managed 原型。 如需如何套用 <xref:System.Runtime.InteropServices.DllImportAttribute> 的指示，請參閱[使用 Unmanaged DLL 函式](consuming-unmanaged-dll-functions.md)。

本節提供範例，示範如何建立 Managed 函式原型，供傳遞引數至函式和接收 Unmanaged 程式庫所匯出函式的傳回值。 此範例也會示範使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 屬性和 <xref:System.Runtime.InteropServices.Marshal> 類別來明確封送處理資料的時機。

## <a name="platform-invoke-data-types"></a>平台叫用資料類型

下表列出 Windows API 和 C 樣式函式中所使用的資料類型。 許多 Unmanaged 程式庫包含傳遞資料類型做為參數和傳回值的函式。 第三個行列出對應的 .NET Framework 內建實值類型或您在 Managed 程式碼中使用的類別。 在某些情況下，您可將本表格中所列的類型取代為相同大小的類型。

|Windows API 中的 Unmanaged 類型|Unmanaged C 語言類型|Managed 類型|描述|
|--------------------------------|-------------------------------|------------------------|-----------------|
|`VOID`|`void`|<xref:System.Void?displayProperty=nameWithType>|套用至未傳回值的函式。|
|`HANDLE`|`void *`|<xref:System.IntPtr?displayProperty=nameWithType> 或 <xref:System.UIntPtr?displayProperty=nameWithType>|在 32 位元 Windows 作業系統上為 32 位元，在 64 位元 Windows 作業系統上為 64 位元。|
|`BYTE`|`unsigned char`|<xref:System.Byte?displayProperty=nameWithType>|8 位元|
|`SHORT`|`short`|<xref:System.Int16?displayProperty=nameWithType>|16 位元|
|`WORD`|`unsigned short`|<xref:System.UInt16?displayProperty=nameWithType>|16 位元|
|`INT`|`int`|<xref:System.Int32?displayProperty=nameWithType>|32 位元|
|`UINT`|`unsigned int`|<xref:System.UInt32?displayProperty=nameWithType>|32 位元|
|`LONG`|`long`|<xref:System.Int32?displayProperty=nameWithType>|32 位元|
|`BOOL`|`long`|<xref:System.Boolean?displayProperty=nameWithType> 或 <xref:System.Int32?displayProperty=nameWithType>|32 位元|
|`DWORD`|`unsigned long`|<xref:System.UInt32?displayProperty=nameWithType>|32 位元|
|`ULONG`|`unsigned long`|<xref:System.UInt32?displayProperty=nameWithType>|32 位元|
|`CHAR`|`char`|<xref:System.Char?displayProperty=nameWithType>|使用 ANSI 裝飾。|
|`WCHAR`|`wchar_t`|<xref:System.Char?displayProperty=nameWithType>|使用 Unicode 裝飾。|
|`LPSTR`|`char *`|<xref:System.String?displayProperty=nameWithType> 或 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|使用 ANSI 裝飾。|
|`LPCSTR`|`const char *`|<xref:System.String?displayProperty=nameWithType> 或 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|使用 ANSI 裝飾。|
|`LPWSTR`|`wchar_t *`|<xref:System.String?displayProperty=nameWithType> 或 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|使用 Unicode 裝飾。|
|`LPCWSTR`|`const wchar_t *`|<xref:System.String?displayProperty=nameWithType> 或 <xref:System.Text.StringBuilder?displayProperty=nameWithType>|使用 Unicode 裝飾。|
|`FLOAT`|`float`|<xref:System.Single?displayProperty=nameWithType>|32 位元|
|`DOUBLE`|`double`|<xref:System.Double?displayProperty=nameWithType>|64 位元|

如需 Visual Basic、C# 和 C++ 中的對應類型，請參閱 [.NET Framework 類別庫簡介](../../standard/class-library-overview.md#system-namespace)。

## <a name="pinvokelibdll"></a>PinvokeLib.dll

下列程式碼定義 Pinvoke.dll 所提供的程式庫函式。 本節所描述的許多範例會呼叫此程式庫。

### <a name="example"></a>範例

[!code-cpp[PInvokeLib#1](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.cpp#1)]

[!code-cpp[PInvokeLib#2](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.h#2)]
