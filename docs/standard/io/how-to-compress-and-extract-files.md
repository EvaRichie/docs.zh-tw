---
title: 操作說明：壓縮與解壓縮檔案
description: 使用 System.object 壓縮 & 解壓縮檔案。 請參閱使用 ZipFile、ZipArchive、Ziparchiveentry 中、DeflateStream、& GZipStream 的範例。
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET Framework], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
ms.openlocfilehash: c13f464432aa6f67136d3a844bdeda256e7ab9b6
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769232"
---
# <a name="how-to-compress-and-extract-files"></a>操作說明：壓縮與解壓縮檔案

<xref:System.IO.Compression> 命名空間包含壓縮及解壓縮檔案和資料流的下列類型。 您也可以使用這些類型讀取和修改壓縮檔案的內容。

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

下列範例示範您可以搭配壓縮檔案執行的部分作業。 這些範例需要將下列 NuGet 套件新增至您的專案：

- [System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)
- [System.IO.Compression.ZipFile](https://www.nuget.org/packages/System.IO.Compression.ZipFile)

如果您使用 .NET Framework，請將這兩個程式庫的參考新增至您的專案：

- `System.IO.Compression`
- `System.IO.Compression.FileSystem`

## <a name="example-1-create-and-extract-a-zip-file"></a>範例1：建立和解壓縮 .zip 檔案

下列範例示範如何使用 <xref:System.IO.Compression.ZipFile> 類別，建立和解壓縮 *.zip* 檔案。 此範例會將資料夾的內容壓縮至新的 *.zip* 檔案，然後將該 zip 解壓縮至新的資料夾。

若要執行樣本，請在程式資料夾中建立*啟動*資料夾，並在其中填入要壓縮的檔案。

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a>範例2：解壓縮特定的副檔名

下一個範例會逐一查看現有 *.zip* 檔案的內容，並將副檔名為 *.txt* 的檔案解壓縮。 它會使用 <xref:System.IO.Compression.ZipArchive> 類別來存取 zip，以及使用 <xref:System.IO.Compression.ZipArchiveEntry> 類別來檢查個別項目。 <xref:System.IO.Compression.ZipArchiveEntry> 物件的擴充方法 <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> 可在 <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType> 類別中使用。

若要執行樣本，請將名為 *result.zip* 的 *.zip* 檔案置於您的程式資料夾中。 出現提示時，提供要擷取至的資料夾名稱。

> [!IMPORTANT]
> 當您在解壓縮檔案時，必須尋找惡意的檔案路徑，以免它逸出您解壓縮的目的目錄。 這是所謂的路徑周遊攻擊。 以下範例示範如何檢查惡意的檔案路徑，並提供安全的方式來解壓縮。

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a>範例3：將檔案新增至現有的 zip

下列範例使用 <xref:System.IO.Compression.ZipArchive> 類別存取現有的 *.zip* 檔案，並將檔案新增至其中。 將新檔案新增至現有的 .zip 時，即會壓縮該檔案。

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a>範例4：壓縮和解壓縮 gz 檔案

您也可以使用 <xref:System.IO.Compression.GZipStream> 和 <xref:System.IO.Compression.DeflateStream> 類別壓縮和解壓縮資料。 它們會使用相同的壓縮演算法。 您可以使用許多常用工具，將寫入至 *.gz* 檔案的 <xref:System.IO.Compression.GZipStream> 物件解壓縮。 以下範例示範如何使用 <xref:System.IO.Compression.GZipStream> 類別壓縮和解壓縮檔案目錄：

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a>另請參閱

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [檔案和資料流 I/O](index.md)
