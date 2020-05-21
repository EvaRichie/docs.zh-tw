---
ms.openlocfilehash: 8c8e87c885c99d28aa9a7a5d5a2b48c80d40d7db
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721146"
---
### <a name="ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes"></a>Ziparchiveentry 中不再處理具有不一致專案大小的封存

Zip 封存會列出中央目錄和本機標頭中的壓縮大小和未壓縮大小。  專案資料本身也會指出其大小。  在 .NET Core 2.2 和更早版本中，永遠不會檢查這些值是否一致。 從 .NET Core 3.0 開始，它們現在是。

#### <a name="change-description"></a>變更描述

在 .NET Core 2.2 和更早版本中， <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType> 即使本機標頭不同意的是 zip 檔案的中央標頭，也會成功。 資料會解壓縮到已達到壓縮資料流程的結尾，即使其長度超過中央目錄/本機標頭中列出的未壓縮檔案大小也一樣。

從 .NET Core 3.0 開始， <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType> 方法會檢查本機標頭和中央標頭是否同意專案的壓縮和未壓縮大小。  如果沒有，則 <xref:System.IO.InvalidDataException> 如果封存的本機標頭和/或資料描述項清單大小與 zip 檔案的中央目錄不一致，方法就會擲回。 當讀取專案時，解壓縮的資料會被截斷為標頭中所列的未壓縮檔案大小。

這項變更是為了確保 <xref:System.IO.Compression.ZipArchiveEntry> 正確地代表其資料的大小，而且只會讀取該資料量。

#### <a name="version-introduced"></a>引進的版本

3.0

#### <a name="recommended-action"></a>建議的動作

重新封裝任何展示這些問題的 zip 封存。

#### <a name="category"></a>類別

CoreFx

#### <a name="affected-apis"></a>受影響的 API

- <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFileExtensions.ExtractToDirectory%2A?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFile.ExtractToDirectory%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

`M:System.IO.Compression.ZipArchiveEntry.Open`
`Overload:System.IO.Compression.ZipFileExtensions.ExtractToDirectory%2A`
`Overload:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A`
`Overload:System.IO.Compression.ZipFile.ExtractToDirectory%2A`

-->
